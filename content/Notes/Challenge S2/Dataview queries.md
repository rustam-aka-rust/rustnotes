---
author:
book:
aliases:
---
## Dataview queries

> [!NOTE]+ Notes on the topic
> 
> ```dataview
> TABLE without ID
> 	file.link AS Title,
> 	Author AS "author",
> 	aliases AS "Aliases",
> 	file.ctime AS "Date Created"
> FROM "Гаражик"
> WHERE contains(author, "Авдеева")
> SORT file.ctime DESC
> ```

***

> [!NOTE] Онтология
> ID: 202411280511
> Source::
> Child::
> Next::

**Список источников:**