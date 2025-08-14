---
Author: Рустам Агамалиев
Book:
ID: 202508110721
discourse:
notebook: p. [№4]
date: 2025-08-11
title:
aliases:
---
## Python Script for parsing books data from the YandexBooks

```python
import asyncio, csv, re, random, json
from pathlib import Path
from typing import Dict, List, Optional, Tuple, Set
from playwright.async_api import async_playwright

# ========= CONFIG =========
ENTRY_POINTS = [
    # Add shelves/searches you want:
    "https://books.yandex.ru/books/t-samorazvitie-ru/all",
]
OUTPUT_CSV = "yandex_nonfiction.csv"

# Browser
USE_SYSTEM_CHROME = False          # set True if Chromium has issues; then run: python -m playwright install chrome
USE_PERSISTENT_PROFILE = True      # keeps cookies (log in once)
USER_DATA_DIR = "ydx_profile"

# Loader
SCROLL_MAX_STEPS = 420
STOP_AFTER = 300
STAGNATION_LIMIT = 8

# Enrichment
ENRICH_CONCURRENCY = 3
# ==========================

BOOK_LINK_SELECTOR = "a[href^='/books/']"

# Heuristics on cards (we overwrite later from book page)
READERS_PAT = re.compile(r"(читал[аи]?|читает|readers?)\D*([0-9\u00A0\u202F\s.,]+)", re.I)
QUOTES_PAT  = re.compile(r"(цитат[аы]?|quotes?)\D*([0-9\u00A0\u202F\s.,]+)", re.I)

# Robust patterns for book tabs
BOOK_READERS_PAT = re.compile(r"(читали|читают|читает|прочитал[аи]?|readers?)\s*[:\s]*([0-9\u00A0\u202F\s.,]+(?:\s*(?:тыс\.?|млн|k|к))?)", re.I)
BOOK_QUOTES_PAT  = re.compile(r"(цитат[аы]?|quotes?)\s*[:\s]*([0-9\u00A0\u202F\s.,]+(?:\s*(?:тыс\.?|млн|k|к))?)", re.I)

BOOK_HREF_RE = re.compile(r'\/books\/[A-Za-z0-9_-]+')

def normalize_count_phrase(raw: str) -> int:
    """
    Handles '848', '3,9 тыс.', '4.3K', '1 499', '1,2 млн', etc.
    """
    t = raw.replace("\u00A0", " ").replace("\u202F", " ").strip()
    m = re.search(r"(\d+(?:[.,]\d+)?)", t)
    if not m:
        return 0
    val = float(m.group(1).replace(",", "."))
    s = t.lower()
    if "млрд" in s or " billion" in s:
        val *= 1_000_000_000
    elif "млн" in s or " million" in s:
        val *= 1_000_000
    elif "тыс" in s or "тысяч" in s or "k" in s or "к" in s:
        val *= 1_000
    return int(val)

async def safe_text(locator) -> str:
    try:
        return (await locator.inner_text()) or ""
    except:
        return ""

# ---------- Loader: virtualized list + show-more ----------
async def load_all_cards(page, max_steps=SCROLL_MAX_STEPS, target_count=STOP_AFTER, stagnation_limit=STAGNATION_LIMIT):
    stagnation = 0
    prev_count = -1
    for _ in range(max_steps):
        count = await page.locator(BOOK_LINK_SELECTOR).count()

        if count >= target_count:
            break

        stagnation = stagnation + 1 if count == prev_count else 0
        prev_count = count

        if stagnation >= stagnation_limit:
            # last nudge
            try:
                last = page.locator(BOOK_LINK_SELECTOR).last
                if await last.count():
                    await last.scroll_into_view_if_needed()
                    await page.wait_for_timeout(800)
                    try:
                        await page.wait_for_load_state("networkidle", timeout=3000)
                    except:
                        pass
            except:
                pass
            again = await page.locator(BOOK_LINK_SELECTOR).count()
            if again <= count:
                break
            stagnation = 0
            prev_count = again
            continue

        # click "show more"
        try:
            more = page.locator(
                "button:has-text('Показать ещё'), button:has-text('Ещё'), "
                "a:has-text('Показать ещё'), a:has-text('Ещё'), "
                "button:has-text('Show more'), a:has-text('Show more')"
            )
            if await more.count():
                await more.first.click(timeout=800)
                await page.wait_for_timeout(900)
        except:
            pass

        # scroll containers + window + last card
        await page.evaluate("""
        () => {
          const els = [document.scrollingElement, ...Array.from(document.querySelectorAll('*'))];
          for (const el of els) {
            if (!el) continue;
            if (el.scrollHeight - el.clientHeight > 50) el.scrollTop = el.scrollHeight;
          }
          window.scrollTo(0, document.body.scrollHeight);
        }""")
        try:
            last = page.locator(BOOK_LINK_SELECTOR).last
            if await last.count():
                await last.scroll_into_view_if_needed()
        except:
            pass

        await page.wait_for_timeout(500 + int(random.uniform(150, 450)))
        try:
            await page.wait_for_load_state("networkidle", timeout=3000)
        except:
            pass

# ---------- XHR sniffer ----------
def looks_like_json(resp) -> bool:
    try:
        ct = resp.headers.get("content-type", "")
        return "application/json" in ct or resp.url.endswith(".json")
    except:
        return False

def attach_sniffer(page, bucket: Set[str]):
    async def handle_resp(resp):
        try:
            if resp.request.resource_type in ("xhr", "fetch") and looks_like_json(resp):
                txt = await resp.text()
                for m in BOOK_HREF_RE.findall(txt):
                    bucket.add("https://books.yandex.ru" + m)
                # Optionally parse JSON structures here if you map them.
        except:
            pass
    page.on("response", lambda resp: asyncio.create_task(handle_resp(resp)))

# ---------- Card parsing on listing ----------
async def extract_card_data(card) -> Optional[Dict]:
    a = card.locator(BOOK_LINK_SELECTOR)
    if not await a.count():
        return None
    href = await a.first.get_attribute("href")
    title = (await a.first.inner_text() or "").strip()
    if not (href and title):
        return None

    authors = ""
    for sel in ["[class*='author']", "[data-testid*='author']", "a[href^='/authors/']", "a[href*='/persons/']"]:
        loc = card.locator(sel)
        if await loc.count():
            names = []
            for i in range(min(await loc.count(), 6)):
                nm = (await loc.nth(i).inner_text() or "").strip()
                if nm and nm.lower() != title.lower():
                    names.append(nm)
            if names:
                authors = "; ".join(dict.fromkeys(names))
                break
    if not authors:
        blob = (await card.inner_text() or "")
        lines = [ln.strip() for ln in blob.splitlines() if ln.strip()]
        if title in lines:
            i = lines.index(title)
            if i + 1 < len(lines):
                authors = lines[i + 1]
        elif len(lines) >= 2:
            authors = lines[1]

    readers = quotes = 0
    chips_blob = await safe_text(card)
    m = READERS_PAT.search(chips_blob);  readers = normalize_count_phrase(m.group(0)) if m else 0
    m = QUOTES_PAT.search(chips_blob);   quotes  = normalize_count_phrase(m.group(0)) if m else 0

    low = title.lower()
    if any(k in low for k in ["роман", "novel"]) and "non" not in low:
        return None

    return {
        "url": "https://books.yandex.ru" + href,
        "title": title,
        "authors": authors or "",
        "readers": readers,
        "quotes": quotes,
    }

async def scrape_listing(page) -> List[Dict]:
    results: List[Dict] = []
    seen = set()
    cards = await page.locator("article, div").all()
    for card in cards:
        try:
            data = await extract_card_data(card)
            if not data:
                continue
            key = (data["title"].strip().lower(), data["authors"].strip().lower())
            if key in seen:
                continue
            seen.add(key)
            results.append(data)
        except:
            continue
    return results

# ---------- Robust tab counter (returns value + raw) ----------
async def read_counter_from_tab(page, suffix: str) -> Tuple[int, str]:
    a = page.locator(f"a[href$='/{suffix}']").first
    if not await a.count():
        return 0, ""
    parts = []

    # keep split spans and plain text
    try:
        html = await a.evaluate("el => el.innerHTML")
        if html:
            parts.append(html)
    except:
        pass
    try:
        txt = await a.evaluate("el => el.textContent")
        if txt:
            parts.append(txt)
    except:
        pass
    for attr in ("aria-label", "title"):
        try:
            v = await a.get_attribute(attr)
            if v:
                parts.append(v)
        except:
            pass

    blob = " ".join(p.strip() for p in parts if p and p.strip())
    raw = blob

    # Strict label-anchored match first
    if suffix == "readers":
        m = BOOK_READERS_PAT.search(blob)
    else:
        m = BOOK_QUOTES_PAT.search(blob)
    if m:
        return normalize_count_phrase(m.group(0)), raw

    # Fallback: first clean number (with optional suffix)
    m = re.search(r"([0-9\u00A0\u202F\s.,]+(?:\s*(?:тыс\.?|млн|k|к))?)", blob, re.I)
    if m:
        return normalize_count_phrase(m.group(1)), raw

    return 0, raw

async def ensure_title_authors(page, b: Dict):
    if b.get("title") and b.get("authors"):
        return
    tloc = page.locator("h1, [data-testid*='title']")
    if await tloc.count():
        t = (await tloc.first.inner_text() or "").strip()
        if t:
            b["title"] = t
    aloc = page.locator("a[href^='/authors/'], a[href*='/persons/'], [data-testid*='author']")
    if await aloc.count():
        names = []
        for i in range(min(await aloc.count(), 6)):
            nm = (await aloc.nth(i).inner_text() or "").strip()
            if nm:
                names.append(nm)
        if names:
            b["authors"] = "; ".join(dict.fromkeys(names))

async def parse_counts_from_book(ctx, b: Dict) -> Tuple[int, int, str, str]:
    p = await ctx.new_page()
    try:
        await p.goto(b["url"], wait_until="domcontentloaded")
        await p.wait_for_timeout(800)

        await ensure_title_authors(p, b)

        readers, raw_r = await read_counter_from_tab(p, "readers")
        quotes,  raw_q = await read_counter_from_tab(p, "quotes")

        if readers == 0:
            await p.goto(b["url"].rstrip("/") + "/readers", wait_until="domcontentloaded")
            await p.wait_for_timeout(800)
            r2, rr2 = await read_counter_from_tab(p, "readers")
            if r2 > readers:
                readers, raw_r = r2, rr2

        if quotes == 0:
            await p.goto(b["url"].rstrip("/") + "/quotes", wait_until="domcontentloaded")
            await p.wait_for_timeout(800)
            q2, rq2 = await read_counter_from_tab(p, "quotes")
            if q2 > quotes:
                quotes, raw_q = q2, rq2

        return readers or 0, quotes or 0, raw_r, raw_q
    finally:
        await p.close()

# ---------- Main ----------
async def main():
    out = Path(OUTPUT_CSV)
    rows: List[Dict] = []
    seen_urls: Set[str] = set()
    seen_from_api: Set[str] = set()

    async with async_playwright() as pw:
        launch_args = ["--disable-blink-features=AutomationControlled"]
        if USE_PERSISTENT_PROFILE:
            if USE_SYSTEM_CHROME:
                ctx = await pw.chromium.launch_persistent_context(
                    user_data_dir=USER_DATA_DIR, channel="chrome",
                    headless=False, args=launch_args
                )
            else:
                ctx = await pw.chromium.launch_persistent_context(
                    user_data_dir=USER_DATA_DIR, headless=False, args=launch_args
                )
            page = await ctx.new_page()
        else:
            if USE_SYSTEM_CHROME:
                browser = await pw.chromium.launch(channel="chrome", headless=False, args=launch_args)
            else:
                browser = await pw.chromium.launch(headless=False, args=launch_args)
            ctx = await browser.new_context()
            page = await ctx.new_page()

        # open home (captcha?)
        await page.goto("https://books.yandex.ru", wait_until="domcontentloaded")
        if "showcaptcha" in page.url:
            print("⚠️ Captcha detected. Solve it in the browser, then press ENTER here...")
            input()

        attach_sniffer(page, seen_from_api)

        for url in ENTRY_POINTS:
            print(f"▶️ Visiting: {url}")
            await page.goto(url, wait_until="domcontentloaded")
            if "showcaptcha" in page.url:
                print("⚠️ Captcha detected again. Solve it, then press ENTER...")
                input()

            await load_all_cards(page)
            scraped = await scrape_listing(page)
            for b in scraped:
                if b["url"] in seen_urls:
                    continue
                seen_urls.add(b["url"])
                rows.append(b)
                print(f" + {b['title']} — {b['authors']} (R:{b['readers']} Q:{b['quotes']})")

        # merge URLs from XHR sniffer
        added = 0
        for url in list(seen_from_api):
            if url not in seen_urls:
                rows.append({"url": url, "title": "", "authors": "", "readers": 0, "quotes": 0})
                seen_urls.add(url); added += 1
        if added:
            print(f"📦 Added {added} book URLs from API sniffing.")

        # Enrich: accurate counts + fill metadata; also keep raw strings
        print("⏳ Fetching accurate readers/quotes from book pages...")
        sem = asyncio.Semaphore(ENRICH_CONCURRENCY)

        async def enrich(b):
            async with sem:
                try:
                    r, q, raw_r, raw_q = await parse_counts_from_book(ctx, b)
                    if r: b["readers"] = max(b.get("readers", 0), r)
                    if q: b["quotes"]  = max(b.get("quotes", 0),  q)
                    b["readers_raw"] = raw_r
                    b["quotes_raw"]  = raw_q
                    print(f"   ↳ counts: {b['title'] or '[no title]'} (R:{b['readers']} Q:{b['quotes']})")
                except Exception as e:
                    print(f"   ! enrich failed: {b.get('title','[no title]')} — {e}")

        await asyncio.gather(*(enrich(b) for b in rows))

        # Save CSV (with raw columns for auditing)
        with out.open("w", newline="", encoding="utf-8") as f:
            w = csv.DictWriter(f, fieldnames=["title","authors","readers","quotes","url","readers_raw","quotes_raw"])
            w.writeheader()
            for r in rows:
                w.writerow(r)

        print(f"✅ Saved {len(rows)} records to {out.resolve()}")

        # close
        if USE_PERSISTENT_PROFILE:
            await ctx.close()
        else:
            await ctx.browser.close()

if __name__ == "__main__":
    asyncio.run(main())
```

***
## BIO
> [!map]+ 🧠 theBrain mapping
> ==ID: 202508110721==
> Source::
> Friend::
> Child::
> Next::

**Keywords**:

**Reference**: 