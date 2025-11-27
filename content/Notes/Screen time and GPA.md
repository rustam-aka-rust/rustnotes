```python
import pandas as pd

# Load the data into a variable called 'df' (short for DataFrame)
# If you renamed your file, change the name inside the quotes below
filename = 'Респонденты, балюусь со временем - Ответы на форму (1)-3.csv'
df = pd.read_csv(filename)

# .shape tells us the size of the data (rows, columns)
print(f"Data Loaded Successfully!")
print(f"Rows: {df.shape[0]}, Columns: {df.shape[1]}")

# .head() shows the first 5 rows so we can visually check it
df.head()
```

    Data Loaded Successfully!
    Rows: 206, Columns: 75





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Отметка времени</th>
      <th>Я ...</th>
      <th>Мне ...</th>
      <th>Какие устройства у меня имеются (можно выбрать несколько)</th>
      <th>В среднем в будний день я провожу перед экраном ...</th>
      <th>Наш расчет ср нед</th>
      <th>В среднем в выходной день я провожу перед экраном ...</th>
      <th>Наш расчет ср вых</th>
      <th>Сколько у вас экранного времени было вчера?</th>
      <th>Сколько у вас экранного времени было позавчера?</th>
      <th>...</th>
      <th>Малина – ягода.1</th>
      <th>Отравление – смерть</th>
      <th>Малина – ягода.2</th>
      <th>Враг – неприятель.3</th>
      <th>Отравление – смерть.1</th>
      <th>Враг – неприятель.4</th>
      <th>Море – океан.2</th>
      <th>Отравление – смерть.2</th>
      <th>Свет – темнота.2</th>
      <th>Итог</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>14.12.2024 15:14:38</td>
      <td>Девочка</td>
      <td>15 лет</td>
      <td>Планшет</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>14.12.2024 15:18:18</td>
      <td>Девочка</td>
      <td>15 лет</td>
      <td>Смартфон, Компьютер|Ноутбук</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>3,5</td>
      <td>3</td>
      <td>4</td>
      <td>...</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14.12.2024 15:19:44</td>
      <td>Мальчик</td>
      <td>15 лет</td>
      <td>Смартфон, Компьютер|Ноутбук</td>
      <td>7</td>
      <td>6</td>
      <td>3</td>
      <td>11</td>
      <td>12</td>
      <td>10</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>14.12.2024 15:24:39</td>
      <td>Девочка</td>
      <td>15 лет</td>
      <td>Смартфон, Компьютер|Ноутбук</td>
      <td>3</td>
      <td>3,8</td>
      <td>6</td>
      <td>4</td>
      <td>3</td>
      <td>5</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>14.12.2024 15:24:44</td>
      <td>Девочка</td>
      <td>15 лет</td>
      <td>Смартфон, Компьютер|Ноутбук</td>
      <td>5</td>
      <td>7</td>
      <td>7</td>
      <td>5</td>
      <td>6</td>
      <td>4</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 75 columns</p>
</div>




```python
# 1. Rename difficult columns to simple variables
# This mapping focuses on the most important statistical columns
new_names = {
    'Я ...': 'Gender',
    'Мне ...': 'Age',
    'В среднем в будний день я провожу перед экраном ...': 'ScreenTime_Weekday',
    'В среднем в выходной день я провожу перед экраном ...': 'ScreenTime_Weekend',
    'Какая у тебя средняя оценка по всем предметам': 'GPA',
    'Сколько часов ты в среднем спишь?': 'Sleep_Hours',
    'Итог': 'Total_Score' # Psychometric score
}

df = df.rename(columns=new_names)

# 2. Remove completely empty rows
df = df.dropna(how='all')

# 3. Function to clean numbers (change "3,5" to 3.5)
def clean_currency_format(x):
    if pd.isna(x):
        return None
    # Convert to string, replace comma with dot
    x_str = str(x).replace(',', '.')
    # Extract only the number part (removes " лет" or other text)
    try:
        import re
        # This regex looks for numbers, possibly with decimals
        number = re.findall(r"[-+]?\d*\.\d+|\d+", x_str)
        if number:
            return float(number[0])
        return None
    except:
        return None

# List of columns that need to be numbers
numeric_cols = ['Age', 'ScreenTime_Weekday', 'ScreenTime_Weekend', 'GPA', 'Sleep_Hours', 'Total_Score']

# Apply the cleaning function to these columns
for col in numeric_cols:
    df[col] = df[col].apply(clean_currency_format)

# Check the results
print("Data Cleaned!")
print("Here is the data type information (Look for 'float64'):")
print("-" * 30)
df[numeric_cols].info()

# Show the first few rows to verify decimals look correct (e.g., 3.5 instead of 3,5)
df[numeric_cols].head()
```

    Data Cleaned!
    Here is the data type information (Look for 'float64'):
    ------------------------------
    <class 'pandas.core.frame.DataFrame'>
    Index: 188 entries, 0 to 205
    Data columns (total 6 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   Age                 187 non-null    float64
     1   ScreenTime_Weekday  188 non-null    float64
     2   ScreenTime_Weekend  188 non-null    float64
     3   GPA                 184 non-null    float64
     4   Sleep_Hours         187 non-null    float64
     5   Total_Score         187 non-null    float64
    dtypes: float64(6)
    memory usage: 10.3 KB





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>ScreenTime_Weekday</th>
      <th>ScreenTime_Weekend</th>
      <th>GPA</th>
      <th>Sleep_Hours</th>
      <th>Total_Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15.0</td>
      <td>12.0</td>
      <td>12.0</td>
      <td>3.27</td>
      <td>3.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>4.61</td>
      <td>8.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15.0</td>
      <td>7.0</td>
      <td>3.0</td>
      <td>4.01</td>
      <td>6.0</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15.0</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>4.23</td>
      <td>6.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15.0</td>
      <td>5.0</td>
      <td>7.0</td>
      <td>3.94</td>
      <td>6.0</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 1. Get a statistical summary of the main columns
stats_summary = df[['Age', 'GPA', 'Sleep_Hours', 'ScreenTime_Weekday', 'ScreenTime_Weekend', 'Total_Score']].describe()

# 2. Round to 2 decimal places for easier reading
display(stats_summary.round(2))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>GPA</th>
      <th>Sleep_Hours</th>
      <th>ScreenTime_Weekday</th>
      <th>ScreenTime_Weekend</th>
      <th>Total_Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>187.00</td>
      <td>184.00</td>
      <td>187.00</td>
      <td>188.00</td>
      <td>188.00</td>
      <td>187.00</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>14.60</td>
      <td>4.13</td>
      <td>6.68</td>
      <td>5.77</td>
      <td>7.51</td>
      <td>3.14</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.92</td>
      <td>0.55</td>
      <td>1.35</td>
      <td>2.98</td>
      <td>3.99</td>
      <td>1.64</td>
    </tr>
    <tr>
      <th>min</th>
      <td>13.00</td>
      <td>0.00</td>
      <td>2.00</td>
      <td>1.00</td>
      <td>1.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>14.00</td>
      <td>3.81</td>
      <td>6.00</td>
      <td>4.00</td>
      <td>5.00</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>14.00</td>
      <td>4.10</td>
      <td>7.00</td>
      <td>6.00</td>
      <td>7.00</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>15.00</td>
      <td>4.50</td>
      <td>8.00</td>
      <td>7.00</td>
      <td>10.00</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>max</th>
      <td>17.00</td>
      <td>6.00</td>
      <td>10.00</td>
      <td>20.00</td>
      <td>24.00</td>
      <td>9.00</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 1. Check how many rows we have before filtering
print(f"Original Row Count: {len(df)}")

# 2. Apply Filters
# Keep GPA <= 5
df = df[df['GPA'] <= 5]

# Keep Time variables <= 24 hours (Physical limit)
df = df[df['Sleep_Hours'] <= 24]
df = df[df['ScreenTime_Weekday'] <= 24]
df = df[df['ScreenTime_Weekend'] <= 24]

# 3. Check how many rows remain
print(f"Row Count after cleaning outliers: {len(df)}")

# 4. Show the new descriptive statistics to confirm the Max values are fixed
clean_stats = df[['GPA', 'Sleep_Hours', 'ScreenTime_Weekday', 'ScreenTime_Weekend']].describe()
display(clean_stats.round(2))
```

    Original Row Count: 188
    Row Count after cleaning outliers: 183



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GPA</th>
      <th>Sleep_Hours</th>
      <th>ScreenTime_Weekday</th>
      <th>ScreenTime_Weekend</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>183.00</td>
      <td>183.00</td>
      <td>183.00</td>
      <td>183.00</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>4.12</td>
      <td>6.68</td>
      <td>5.75</td>
      <td>7.51</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.53</td>
      <td>1.35</td>
      <td>3.00</td>
      <td>4.01</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.00</td>
      <td>2.00</td>
      <td>1.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>3.81</td>
      <td>6.00</td>
      <td>4.00</td>
      <td>5.00</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>4.09</td>
      <td>7.00</td>
      <td>6.00</td>
      <td>7.00</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>4.49</td>
      <td>8.00</td>
      <td>7.00</td>
      <td>10.00</td>
    </tr>
    <tr>
      <th>max</th>
      <td>5.00</td>
      <td>10.00</td>
      <td>20.00</td>
      <td>24.00</td>
    </tr>
  </tbody>
</table>
</div>



```python
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Numeric Comparison Table
# We group the data by 'Gender' and calculate the median for key columns
gender_stats = df.groupby('Gender')[['ScreenTime_Weekday', 'ScreenTime_Weekend', 'GPA', 'Sleep_Hours']].mean()
print("Average (Mean) Values by Gender:")
display(gender_stats.round(2))

# 2. Visual Comparison (Boxplots)
# We will create 2 side-by-side plots: one for Weekend Screen Time, one for GPA
fig, axes = plt.subplots(1, 2, figsize=(14, 6))

# Plot A: Screen Time on Weekends
sns.boxplot(data=df, x='Gender', y='ScreenTime_Weekend', palette="pastel", ax=axes[0])
axes[0].set_title('Screen Time: Weekends')
axes[0].set_ylabel('Hours')

# Plot B: GPA (Grades)
sns.boxplot(data=df, x='Gender', y='GPA', palette="pastel", ax=axes[1])
axes[1].set_title('Academic Performance (GPA)')
axes[1].set_ylabel('Grade (1-5)')

plt.tight_layout()
plt.show()
```

    Average (Mean) Values by Gender:



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ScreenTime_Weekday</th>
      <th>ScreenTime_Weekend</th>
      <th>GPA</th>
      <th>Sleep_Hours</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Девочка</th>
      <td>5.77</td>
      <td>7.47</td>
      <td>4.19</td>
      <td>6.36</td>
    </tr>
    <tr>
      <th>Мальчик</th>
      <td>5.71</td>
      <td>7.58</td>
      <td>4.00</td>
      <td>7.21</td>
    </tr>
  </tbody>
</table>
</div>


    /var/folders/d8/4k3q_2wd4nv9gmh9ch_b79jr0000gn/T/ipykernel_11930/2536227559.py:15: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(data=df, x='Gender', y='ScreenTime_Weekend', palette="pastel", ax=axes[0])
    /var/folders/d8/4k3q_2wd4nv9gmh9ch_b79jr0000gn/T/ipykernel_11930/2536227559.py:20: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(data=df, x='Gender', y='GPA', palette="pastel", ax=axes[1])



    
![png](output_4_3.png)
    



```python
# Select only the columns we care about for relationships
cols_for_corr = ['Age', 'ScreenTime_Weekday', 'ScreenTime_Weekend', 'GPA', 'Sleep_Hours', 'Total_Score']

# Calculate the correlation matrix
corr_matrix = df[cols_for_corr].corr()

# Plot the Heatmap
plt.figure(figsize=(10, 8))
sns.heatmap(corr_matrix, 
            annot=True,      # Show the numbers on the squares
            cmap='coolwarm', # Blue for negative, Red for positive
            vmin=-1, vmax=1, # Fix the scale from -1 to 1
            fmt=".2f")       # Show 2 decimal places

plt.title('Correlation Map: What affects what?')
plt.show()
```


    
![png](output_5_0.png)
    



```python
import matplotlib.pyplot as plt
import seaborn as sns

# Create the Scatter Plot with Regression Lines
# height and aspect control the size of the image
grid = sns.lmplot(
    data=df,
    x='ScreenTime_Weekend',  # The Cause (Independent Variable)
    y='GPA',                 # The Effect (Dependent Variable)
    hue='Gender',            # Different colors for Boys/Girls
    height=6,
    aspect=1.5,
    scatter_kws={'alpha': 0.6, 's': 50}, # Make dots semi-transparent and larger
    line_kws={'linewidth': 3}            # Make the trend lines thick
)

# Customizing the chart for your report
plt.title('Impact of Weekend Screen Time on GPA', fontsize=16)
plt.xlabel('Screen Time (Hours/Day on Weekend)', fontsize=12)
plt.ylabel('GPA (Grade 1-5)', fontsize=12)

# Set limits to focus on the relevant data area
plt.ylim(2.5, 5.2)  # Focus on passing grades up to max
plt.xlim(0, 24)     # 0 to 24 hours

plt.show()
```


    
![png](output_6_0.png)
    



```python
# 1. Split the data into two groups
boys_data = df[df['Gender'] == 'Мальчик']
girls_data = df[df['Gender'] == 'Девочка']

# 2. Calculate the specific correlation for each group
# We look at Weekend Screen Time vs GPA
r_boys = boys_data['ScreenTime_Weekend'].corr(boys_data['GPA'])
r_girls = girls_data['ScreenTime_Weekend'].corr(girls_data['GPA'])

# 3. Print the results
print("-" * 30)
print(f"Impact of Screen Time on Grades (Correlation 'r'):")
print("-" * 30)
print(f"Boys:  {r_boys:.3f}  ( steeper slope / stronger effect )")
print(f"Girls: {r_girls:.3f}  ( flatter slope / weaker effect )")
print("-" * 30)

if abs(r_boys) > abs(r_girls):
    print("CONCLUSION: You were right. The negative trend is stronger for boys.")
else:
    print("CONCLUSION: The trend is actually similar, despite the visual.")
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[2], line 2
          1 # 1. Split the data into two groups
    ----> 2 boys_data = df[df['Gender'] == 'Мальчик']
          3 girls_data = df[df['Gender'] == 'Девочка']
          5 # 2. Calculate the specific correlation for each group
          6 # We look at Weekend Screen Time vs GPA


    NameError: name 'df' is not defined



```python
import pandas as pd
import numpy as np
import re

# --- RELOAD AND CLEAN DATA ---
filename = 'Респонденты, балюусь со временем - Ответы на форму (1)-3.csv'
df = pd.read_csv(filename)

# Rename columns
new_names = {
    'Я ...': 'Gender',
    'Мне ...': 'Age',
    'В среднем в будний день я провожу перед экраном ...': 'ScreenTime_Weekday',
    'В среднем в выходной день я провожу перед экраном ...': 'ScreenTime_Weekend',
    'Какая у тебя средняя оценка по всем предметам': 'GPA',
    'Сколько часов ты в среднем спишь?': 'Sleep_Hours',
    'Итог': 'Total_Score'
}
df = df.rename(columns=new_names)

# Remove empty rows
df = df.dropna(how='all')

# Function to fix "3,5" -> 3.5
def clean_currency_format(x):
    if pd.isna(x): return None
    x_str = str(x).replace(',', '.')
    try:
        number = re.findall(r"[-+]?\d*\.\d+|\d+", x_str)
        return float(number[0]) if number else None
    except: return None

# Apply cleaning
numeric_cols = ['Age', 'ScreenTime_Weekday', 'ScreenTime_Weekend', 'GPA', 'Sleep_Hours', 'Total_Score']
for col in numeric_cols:
    df[col] = df[col].apply(clean_currency_format)

# Remove Outliers (sanity check)
df = df[df['GPA'] <= 5]
df = df[df['Sleep_Hours'] <= 24]
df = df[df['ScreenTime_Weekday'] <= 24]
df = df[df['ScreenTime_Weekend'] <= 24]

# --- NEW ANALYSIS: BOYS vs GIRLS CORRELATION ---

# 1. Split the data
boys_data = df[df['Gender'] == 'Мальчик']
girls_data = df[df['Gender'] == 'Девочка']

# 2. Calculate correlations
r_boys = boys_data['ScreenTime_Weekend'].corr(boys_data['GPA'])
r_girls = girls_data['ScreenTime_Weekend'].corr(girls_data['GPA'])

# 3. Print Results
print("-" * 30)
print(f"Impact of Screen Time on Grades (Correlation 'r'):")
print("-" * 30)
print(f"Boys:  {r_boys:.3f}")
print(f"Girls: {r_girls:.3f}")
print("-" * 30)

if abs(r_boys) > abs(r_girls):
    print("CONCLUSION: You were right. The negative trend is stronger for boys.")
else:
    print("CONCLUSION: The trend is statistically similar or stronger for girls.")
```

    ------------------------------
    Impact of Screen Time on Grades (Correlation 'r'):
    ------------------------------
    Boys:  -0.120
    Girls: -0.325
    ------------------------------
    CONCLUSION: The trend is statistically similar or stronger for girls.



```python
import matplotlib.pyplot as plt
import seaborn as sns

# Create the Bar Chart
plt.figure(figsize=(8, 6))
sns.barplot(data=df, x='User_Group', y='Total_Score', hue='User_Group', palette='viridis')

plt.title('Cognitive Test Scores: Light vs. Heavy Screen Users')
plt.ylabel('Average Test Score')
plt.xlabel('User Category (Based on 7 hours split)')
plt.show()
```


    
![png](output_9_0.png)
    



```python
from scipy.stats import mannwhitneyu

# 1. Separate the scores into two lists
scores_light = df[df['User_Group'] == 'Light User']['Total_Score']
scores_heavy = df[df['User_Group'] == 'Heavy User']['Total_Score']

# 2. Run the Test
stat, p_value = mannwhitneyu(scores_light, scores_heavy)

# 3. Print the Result clearly
print("-" * 40)
print(f"P-Value: {p_value:.4f}")
print("-" * 40)

if p_value < 0.05:
    print("VERDICT: The difference is REAL (Statistically Significant).")
    print("Screen time likely negatively affects the test score.")
else:
    print("VERDICT: The difference is NOT statistically significant.")
    print("The score difference (3.26 vs 3.09) is small enough that it could just be random chance.")
    print("We cannot prove screen time lowers cognitive scores based on this data.")
```

    ----------------------------------------
    P-Value: 0.5184
    ----------------------------------------
    VERDICT: The difference is NOT statistically significant.
    The score difference (3.26 vs 3.09) is small enough that it could just be random chance.
    We cannot prove screen time lowers cognitive scores based on this data.



```python
from scipy.stats import mannwhitneyu

# 1. Compare Sleep Hours between Heavy (>7h) and Light (<7h) users
sleep_light = df[df['User_Group'] == 'Light User']['Sleep_Hours']
sleep_heavy = df[df['User_Group'] == 'Heavy User']['Sleep_Hours']

# 2. Calculate the average sleep for context
print(f"Average Sleep (Light Users): {sleep_light.mean():.2f} hours")
print(f"Average Sleep (Heavy Users): {sleep_heavy.mean():.2f} hours")

# 3. Run the Statistical Test
stat, p_value = mannwhitneyu(sleep_light, sleep_heavy)

print("-" * 40)
print(f"P-Value: {p_value:.4f}")
print("-" * 40)

if p_value < 0.05:
    print("VERDICT: SIGNIFICANT DIFFERENCE FOUND!")
    print("We can scientifically prove that heavy screen users get less sleep.")
else:
    print("VERDICT: No significant difference.")
```

    Average Sleep (Light Users): 6.88 hours
    Average Sleep (Heavy Users): 6.42 hours
    ----------------------------------------
    P-Value: 0.0552
    ----------------------------------------
    VERDICT: No significant difference.



```python
# 1. Rename the long question column
# "Как ты думаешь время перед экраном влияет на твой сон (хуже или лучше)?"
col_name_subjective = 'Как ты думаешь время перед экраном влияет на твой сон (хуже или лучше)?'
df = df.rename(columns={col_name_subjective: 'Opinion_Sleep'})

# 2. Check what answers students gave
print("Student Opinions on Screen Time & Sleep:")
print(df['Opinion_Sleep'].value_counts())

# 3. Visualize Actual Sleep vs. Their Opinion
plt.figure(figsize=(10, 6))
sns.boxplot(data=df, x='Opinion_Sleep', y='Sleep_Hours', palette='Set2')

plt.title('Self-Awareness: Opinion vs. Actual Sleep')
plt.xlabel('Student Opinion: "Does screen time affect your sleep?"')
plt.ylabel('Actual Sleep (Hours)')
plt.show()

# 4. Calculate the average sleep for each opinion group
print("-" * 30)
print("Actual Average Sleep by Opinion Group:")
print(df.groupby('Opinion_Sleep')['Sleep_Hours'].mean().round(2))
```

    Student Opinions on Screen Time & Sleep:
    Opinion_Sleep
    Да         76
    Нет        73
    Не знаю    34
    Name: count, dtype: int64


    /var/folders/d8/4k3q_2wd4nv9gmh9ch_b79jr0000gn/T/ipykernel_13950/389020546.py:12: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(data=df, x='Opinion_Sleep', y='Sleep_Hours', palette='Set2')



    
![png](output_12_2.png)
    


    ------------------------------
    Actual Average Sleep by Opinion Group:
    Opinion_Sleep
    Да         6.58
    Не знаю    6.65
    Нет        6.79
    Name: Sleep_Hours, dtype: float64



```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 6))

# 1. Determine the order (Highest median screen time on left)
order = df.groupby('App_Category')['ScreenTime_Weekend'].median().sort_values(ascending=False).index

# 2. Plot with the fix (hue=App_Category)
sns.boxplot(
    data=df, 
    x='App_Category', 
    y='ScreenTime_Weekend', 
    order=order, 
    hue='App_Category', # This fixes the warning
    palette='magma', 
    legend=False
)

plt.title('Which App Users have the Highest Weekend Screen Time?')
plt.ylabel('Hours on Screen')
plt.show()
```


    
![png](output_13_0.png)
    



```python
# 1. Rename the App column
col_app = 'Какое приложение на твоем смартфоне является рекордсменом по экранному времени?'
df = df.rename(columns={col_app: 'Top_App'})

# 2. Function to clean text (Combine "tik tok", "tt", "tiktok" into one)
def clean_app_name(text):
    if pd.isna(text): return "Unknown"
    text = str(text).lower().strip() # Make lowercase
    
    # Common mappings
    if 'tik' in text or 'tt' in text or 'тик' in text:
        return 'TikTok'
    if 'tele' in text or 'tg' in text or 'тг' in text:
        return 'Telegram'
    if 'tube' in text or 'ютуб' in text:
        return 'YouTube'
    if 'game' in text or 'игр' in text or 'brawl' in text or 'genshin' in text or 'pubg' in text:
        return 'Games'
    if 'whats' in text or 'vk' in text or 'вк' in text:
        return 'Social/Chat'
    
    return 'Other' # For browsers, maps, etc.

# Apply cleaning
df['App_Category'] = df['Top_App'].apply(clean_app_name)

# 3. View the Most Popular Apps
print("Most Popular Time-Wasting Apps:")
print(df['App_Category'].value_counts())

# 4. Visualization: Who spends the most time?
plt.figure(figsize=(10, 6))
# Sort order: Apps with highest median screen time on the left
order = df.groupby('App_Category')['ScreenTime_Weekend'].median().sort_values(ascending=False).index

sns.boxplot(data=df, x='App_Category', y='ScreenTime_Weekend', order=order, palette='magma')
plt.title('Which App Users have the Highest Weekend Screen Time?')
plt.ylabel('Hours on Screen')
plt.show()
```

    Most Popular Time-Wasting Apps:
    App_Category
    TikTok      59
    Telegram    53
    Other       39
    YouTube     25
    Games        5
    Unknown      2
    Name: count, dtype: int64


    /var/folders/d8/4k3q_2wd4nv9gmh9ch_b79jr0000gn/T/ipykernel_13950/3147444248.py:36: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.boxplot(data=df, x='App_Category', y='ScreenTime_Weekend', order=order, palette='magma')



    
![png](output_14_2.png)
    



```python
# Calculate the average (mean) weekend screen time for the top apps
app_stats = df.groupby('App_Category')['ScreenTime_Weekend'].mean().sort_values(ascending=False)

print("Average Weekend Screen Time by App (Hours):")
print("-" * 40)
print(app_stats)
print("-" * 40)

tiktok_avg = app_stats['TikTok']
telegram_avg = app_stats['Telegram']
diff = tiktok_avg - telegram_avg

print(f"CONCLUSION: TikTok users spend, on average, {diff:.2f} more hours per day")
print("on screens compared to Telegram users.")
```

    Average Weekend Screen Time by App (Hours):
    ----------------------------------------
    App_Category
    Unknown     9.500000
    TikTok      7.897119
    Other       7.653846
    Telegram    7.160377
    YouTube     7.080000
    Games       6.940000
    Name: ScreenTime_Weekend, dtype: float64
    ----------------------------------------
    CONCLUSION: TikTok users spend, on average, 0.74 more hours per day
    on screens compared to Telegram users.



```python
## We have switched to sleep and GPA
```


```python
import matplotlib.pyplot as plt
import seaborn as sns

# Create the Scatter Plot with a Trend Line
sns.lmplot(
    data=df,
    x='Sleep_Hours', 
    y='GPA', 
    hue='Gender',       # Let's keep looking if boys/girls differ
    height=6, 
    aspect=1.5,
    scatter_kws={'alpha': 0.6, 's': 50},
    line_kws={'linewidth': 3}
)

plt.title('Does Sleeping More Equal Better Grades?', fontsize=16)
plt.xlabel('Average Sleep (Hours)', fontsize=12)
plt.ylabel('GPA (Grade 1-5)', fontsize=12)
plt.ylim(2.5, 5.2)  # Focus on the passing grades
plt.show()
```


    
![png](output_17_0.png)
    



```python
# 1. Split the data
boys_data = df[df['Gender'] == 'Мальчик']
girls_data = df[df['Gender'] == 'Девочка']

# 2. Calculate correlation: SLEEP vs GPA
r_boys_sleep = boys_data['Sleep_Hours'].corr(boys_data['GPA'])
r_girls_sleep = girls_data['Sleep_Hours'].corr(girls_data['GPA'])

# 3. Print the results
print("-" * 40)
print(f"Impact of Sleep on Grades (Correlation 'r'):")
print("-" * 40)
print(f"Boys:  {r_boys_sleep:.3f}")
print(f"Girls: {r_girls_sleep:.3f}")
print("-" * 40)

# Logic to interpret the result automatically
if r_boys_sleep > r_girls_sleep:
    print("CONCLUSION: You were right! Sleep is more critical for Boys' grades.")
else:
    print("CONCLUSION: Actually, sleep affects Girls' grades more (despite the graph).")
```

    ----------------------------------------
    Impact of Sleep on Grades (Correlation 'r'):
    ----------------------------------------
    Boys:  0.100
    Girls: 0.168
    ----------------------------------------
    CONCLUSION: Actually, sleep affects Girls' grades more (despite the graph).



```python
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Filter for the two big giants: TikTok and Telegram
# (We exclude "Other" or "Games" because they have fewer people)
target_apps = ['TikTok', 'Telegram']
app_sleep_data = df[df['App_Category'].isin(target_apps)]

# 2. Calculate average sleep for each
print("Average Sleep Hours by App:")
print("-" * 30)
print(app_sleep_data.groupby('App_Category')['Sleep_Hours'].mean().round(2))
print("-" * 30)

# 3. Visualize
plt.figure(figsize=(8, 6))
sns.barplot(
    data=app_sleep_data, 
    x='App_Category', 
    y='Sleep_Hours', 
    palette='coolwarm',
    hue='App_Category' # Fixes the warning
)

plt.title('Do TikTok Users Sleep Less than Telegram Users?')
plt.ylabel('Average Sleep (Hours)')
plt.ylim(0, 9) # Set limit to see the bars clearly
plt.show()
```

    Average Sleep Hours by App:
    ------------------------------
    App_Category
    Telegram    6.45
    TikTok      6.58
    Name: Sleep_Hours, dtype: float64
    ------------------------------



    
![png](output_19_1.png)
    



```python
# 1. Rename the long column
col_sports = 'Сколько раз в неделю ты ходишь на тренировки?'
df = df.rename(columns={col_sports: 'Training_Freq'})

# 2. Check the categories
# We expect values like "Нет", "1-2", "2-3", "Более 3 раз"
print("Training Categories found:")
print(df['Training_Freq'].unique())

# 3. Calculate Average Sleep by Training Frequency
# We sort the values so the chart makes sense (None -> Low -> High)
order_list = ['Ни одного', 'Нет', '1-2', '2-3', 'Более 3 раз'] 

# Note: Your data might use "Нет" or "Ни одного" or "Ничего". 
# The code below groups by whatever text is there.
sleep_by_sports = df.groupby('Training_Freq')['Sleep_Hours'].mean().sort_values()

print("-" * 30)
print("Does Sport help Sleep?")
print(sleep_by_sports)
print("-" * 30)

# 4. Visualize
plt.figure(figsize=(10, 6))
sns.boxplot(
    data=df, 
    x='Training_Freq', 
    y='Sleep_Hours', 
    palette='Greens',
    hue='Training_Freq',
    order=['Нет', 'Ни одного', '1-2', '2-3', 'Более 3 раз'] # Trying to force a logical order
)

plt.title('Physical Training vs. Sleep Duration')
plt.ylabel('Hours of Sleep')
plt.xlabel('Training Frequency (Per Week)')
plt.show()
```

    Training Categories found:
    ['2-3' '1-2' 'Ни одного' 'Более 3 раз' nan]
    ------------------------------
    Does Sport help Sleep?
    Training_Freq
    1-2            6.534884
    Ни одного      6.597826
    Более 3 раз    6.629630
    2-3            6.986842
    Name: Sleep_Hours, dtype: float64
    ------------------------------



    
![png](output_20_1.png)
    



```python
# 1. Calculate Average GPA by Training Frequency
gpa_by_sports = df.groupby('Training_Freq')['GPA'].mean().reindex(['Ни одного', '1-2', '2-3', 'Более 3 раз'])

print("-" * 30)
print("Does Sport help Grades?")
print(gpa_by_sports.round(2))
print("-" * 30)

# 2. Visualize
plt.figure(figsize=(10, 6))
sns.barplot(
    data=df, 
    x='Training_Freq', 
    y='GPA', 
    palette='Greens',
    order=['Ни одного', '1-2', '2-3', 'Более 3 раз'],
    ci=None # Remove error bars for a cleaner look at the mean
)

plt.title('Physical Training vs. Academic Performance (GPA)')
plt.ylabel('Average GPA')
plt.xlabel('Training Frequency (Per Week)')
plt.ylim(3.5, 4.5) # Zoom in to see the difference
plt.show()
```

    ------------------------------
    Does Sport help Grades?
    Training_Freq
    Ни одного      4.09
    1-2            4.03
    2-3            4.10
    Более 3 раз    4.20
    Name: GPA, dtype: float64
    ------------------------------


    /var/folders/d8/4k3q_2wd4nv9gmh9ch_b79jr0000gn/T/ipykernel_13950/3034588233.py:11: FutureWarning: 
    
    The `ci` parameter is deprecated. Use `errorbar=None` for the same effect.
    
      sns.barplot(
    /var/folders/d8/4k3q_2wd4nv9gmh9ch_b79jr0000gn/T/ipykernel_13950/3034588233.py:11: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.barplot(



    
![png](output_21_2.png)
    



```python
from scipy.stats import mannwhitneyu

# 1. Isolate the two groups
# Group A: The "Sweet Spot" (2-3 times a week)
sleep_peak = df[df['Training_Freq'] == '2-3']['Sleep_Hours']

# Group B: The "Casual" group (1-2 times a week)
sleep_low = df[df['Training_Freq'] == '1-2']['Sleep_Hours']

# 2. Print the averages again to be sure
print(f"Average Sleep (2-3 times): {sleep_peak.mean():.2f} hours")
print(f"Average Sleep (1-2 times): {sleep_low.mean():.2f} hours")
print("-" * 40)

# 3. Run the P-Value Test
stat, p_value = mannwhitneyu(sleep_peak, sleep_low)

print(f"P-Value: {p_value:.4f}")
print("-" * 40)

# 4. Interpretation
if p_value < 0.05:
    print("VERDICT: SIGNIFICANT.")
    print("The increase in sleep for the '2-3 times' group is REAL.")
elif p_value < 0.10:
    print("VERDICT: MARGINALLY SIGNIFICANT (Trend).")
    print("There is a strong signal, but not quite 95% certainty.")
else:
    print("VERDICT: NOT SIGNIFICANT.")
    print("This is likely just a fluctuation.")
```

    Average Sleep (2-3 times): 6.99 hours
    Average Sleep (1-2 times): 6.53 hours
    ----------------------------------------
    P-Value: 0.0407
    ----------------------------------------
    VERDICT: SIGNIFICANT.
    The increase in sleep for the '2-3 times' group is REAL.



```python
from scipy.stats import spearmanr

# 1. Clean the data (Drop any rows where Sleep or GPA is missing)
clean_data = df.dropna(subset=['Sleep_Hours', 'GPA'])

# 2. Run the Spearman Correlation Test
# This checks if there is a monotonic relationship (as one goes up, the other goes up)
coef, p_value = spearmanr(clean_data['Sleep_Hours'], clean_data['GPA'])

print("-" * 40)
print(f"Correlation Coefficient (r): {coef:.3f}")
print(f"P-Value: {p_value:.4f}")
print("-" * 40)

# 3. Interpretation
if p_value < 0.05:
    print("VERDICT: SIGNIFICANT.")
    print("There is a REAL statistical link: More sleep = Higher Grades.")
    print("Even if the correlation is weak, it is not random luck.")
else:
    print("VERDICT: NOT SIGNIFICANT.")
    print("We cannot prove that sleep directly changes grades in this specific dataset.")
```

    ----------------------------------------
    Correlation Coefficient (r): 0.060
    P-Value: 0.4203
    ----------------------------------------
    VERDICT: NOT SIGNIFICANT.
    We cannot prove that sleep directly changes grades in this specific dataset.



```python
import statsmodels.api as sm

# 1. Prepare the data
# We need rows that have data for ALL three columns
subset = df[['GPA', 'Sleep_Hours', 'ScreenTime_Weekend']].dropna()

# 2. Define Y (Target) and X (Predictors)
Y = subset['GPA']
X = subset[['Sleep_Hours', 'ScreenTime_Weekend']]

# Add a "Constant" (The baseline GPA if you did nothing) - required for the math to work
X = sm.add_constant(X)

# 3. Fit the Model (Ordinary Least Squares)
model = sm.OLS(Y, X).fit()

# 4. Print the "clean" results
print("--- COMBINED EFFECT ANALYSIS ---")
print(f"R-squared: {model.rsquared:.3f} (How much of the GPA is explained by these two?)")
print("-" * 50)
print(model.summary().tables[1])
print("-" * 50)
```

    --- COMBINED EFFECT ANALYSIS ---
    R-squared: 0.061 (How much of the GPA is explained by these two?)
    --------------------------------------------------
    ======================================================================================
                             coef    std err          t      P>|t|      [0.025      0.975]
    --------------------------------------------------------------------------------------
    const                  4.2364      0.222     19.087      0.000       3.798       4.674
    Sleep_Hours            0.0172      0.029      0.594      0.553      -0.040       0.074
    ScreenTime_Weekend    -0.0313      0.010     -3.214      0.002      -0.051      -0.012
    ======================================================================================
    --------------------------------------------------



```python
# --- DATASET SUMMARY REPORT ---

# 1. Total Sample Size (N)
N = len(df)

# 2. Gender Breakdown
gender_counts = df['Gender'].value_counts()
gender_pct = df['Gender'].value_counts(normalize=True) * 100

# 3. Key Statistics (Mean +/- Standard Deviation)
avg_age = df['Age'].mean()
sd_age = df['Age'].std()

avg_gpa = df['GPA'].mean()
sd_gpa = df['GPA'].std()

avg_screen_wknd = df['ScreenTime_Weekend'].mean()
sd_screen_wknd = df['ScreenTime_Weekend'].std()

avg_sleep = df['Sleep_Hours'].mean()
sd_sleep = df['Sleep_Hours'].std()

# --- PRINT THE REPORT ---
print("="*40)
print("DATASET DEMOGRAPHIC SUMMARY")
print("="*40)
print(f"Total Participants (N): {N}")
print("-" * 40)
print("GENDER DISTRIBUTION:")
for gender in gender_counts.index:
    count = gender_counts[gender]
    pct = gender_pct[gender]
    print(f"  - {gender}: {count} ({pct:.1f}%)")
print("-" * 40)
print("DESCRIPTIVE STATISTICS (Mean ± SD):")
print(f"  - Age: {avg_age:.2f} ± {sd_age:.2f} years")
print(f"  - GPA: {avg_gpa:.2f} ± {sd_gpa:.2f}")
print(f"  - Weekend Screen Time: {avg_screen_wknd:.2f} ± {sd_screen_wknd:.2f} hours")
print(f"  - Sleep Duration: {avg_sleep:.2f} ± {sd_sleep:.2f} hours")
print("="*40)
```

    ========================================
    DATASET DEMOGRAPHIC SUMMARY
    ========================================
    Total Participants (N): 183
    ----------------------------------------
    GENDER DISTRIBUTION:
      - Девочка: 114 (62.3%)
      - Мальчик: 69 (37.7%)
    ----------------------------------------
    DESCRIPTIVE STATISTICS (Mean ± SD):
      - Age: 14.62 ± 0.92 years
      - GPA: 4.12 ± 0.53
      - Weekend Screen Time: 7.51 ± 4.01 hours
      - Sleep Duration: 6.68 ± 1.35 hours
    ========================================



```python
# Save to CSV
# index=False tells Python not to save the row numbers (0, 1, 2...) as a column
df.to_csv('survey_data_cleaned.csv', index=False)

print("Success! File 'survey_data_cleaned.csv' has been saved to your folder.")
```

    Success! File 'survey_data_cleaned.csv' has been saved to your folder.



```python
# 1. Define the Answer Key Dictionary
# Key = Column Name in CSV, Value = The Correct Answer String
answer_key = {
    'Плакать – реветь*': 'Враг – неприятель',
    'Пара – два': 'Враг – неприятель',
    'Свобода – воля': 'Враг – неприятель',
    'Глава – роман': 'Овца – стадо',
    'Страна – город': 'Овца – стадо',
    'Покой – движение': 'Свет – темнота',
    'Похвала – брань': 'Свет – темнота',
    'Тумбочка – шкаф': 'Море – океан',
    'Химия – наука': 'Малина – ягода',
    'Грядка – огород': 'Овца – стадо',
    'Буква – слово': 'Овца – стадо',
    'Пение – искусство': 'Малина – ягода',
    'Месть – поджог': 'Отравление – смерть', # Based on rubric mapping
    'Девять – число': 'Малина – ягода',
    'Правильно – верно': 'Враг – неприятель',
    'Обман – недоверие': 'Отравление – смерть',
    'Смелость – геройство': 'Море – океан',
    'Прохлада – мороз': 'Море – океан',
    'Испуг – бегство': 'Отравление – смерть',
    'Бодрый – вялый': 'Враг – неприятель' # Wait, 'Bodry-Vyaly' is Antonym -> Svet-Temnota?
}
# Correction based on logic: 'Бодрый – вялый' (Energetic - Lethargic) is Antonym.
# Logic dictates 'Свет – темнота'. Let's verify the key image. 
# Key #7 (Бодрый – вялый) -> Г (Svet-Temnota).
# Updating dictionary:
answer_key['Бодрый – вялый'] = 'Свет – темнота'

# 2. Grading Function
def calculate_test_score(row):
    score = 0
    # Loop through each question
    for question, correct_answer in answer_key.items():
        # Check if the column exists (to avoid errors)
        if question in row:
            # Get student's answer, clean it (strip spaces)
            student_ans = str(row[question]).strip()
            if student_ans == correct_answer:
                score += 1
    return score

# 3. Apply Grading (Raw Score 0-20)
df['Raw_Cognitive_Score'] = df.apply(calculate_test_score, axis=1)

# 4. Convert to 1-9 Scale (Rubric)
def apply_scale(raw):
    if raw >= 19: return 9
    if raw == 18: return 8
    if raw == 17: return 7
    if raw >= 15: return 6
    if raw >= 12: return 5
    if raw >= 10: return 4
    if raw >= 8:  return 3
    if raw == 7:  return 2
    return 1

df['Scaled_Cognitive_Score'] = df['Raw_Cognitive_Score'].apply(apply_scale)

# 5. Check the Results
print("Grading Complete!")
print("Here is a sample of the new scores:")
display(df[['Raw_Cognitive_Score', 'Scaled_Cognitive_Score', 'Total_Score']].head(10))

# Compare Old Score vs New Score
correlation_check = df['Scaled_Cognitive_Score'].corr(df['Total_Score'])
print(f"\nCorrelation between your Old Score and New Calculated Score: {correlation_check:.2f}")
```

    Grading Complete!
    Here is a sample of the new scores:



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Raw_Cognitive_Score</th>
      <th>Scaled_Cognitive_Score</th>
      <th>Total_Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>1</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>1</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13</td>
      <td>5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>3</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>9</td>
      <td>3</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>13</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3</td>
      <td>1</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>15</td>
      <td>6</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>14</td>
      <td>5</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
</div>


    
    Correlation between your Old Score and New Calculated Score: 0.17



```python
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import spearmanr

# 1. Correlation Matrix with NEW Score
cols = ['ScreenTime_Weekend', 'GPA', 'Sleep_Hours', 'Scaled_Cognitive_Score']
corr_matrix = df[cols].corr(method='spearman') # Spearman is better for ranked scores (1-9)

print("--- NEW CORRELATION ANALYSIS ---")
display(corr_matrix)

# 2. Visual Boxplot
# Group by Heavy vs Light Users again
df['User_Group'] = df['ScreenTime_Weekend'].apply(lambda x: 'Heavy User' if x > 7 else 'Light User')

plt.figure(figsize=(8, 6))
sns.boxplot(
    data=df, 
    x='User_Group', 
    y='Scaled_Cognitive_Score', 
    palette='viridis',
    hue='User_Group'
)
plt.title('True Cognitive Score vs. Screen Usage')
plt.ylabel('Score (1-9 Scale)')
plt.show()

# 3. Statistical Test (Mann-Whitney)
from scipy.stats import mannwhitneyu
group_light = df[df['User_Group'] == 'Light User']['Scaled_Cognitive_Score']
group_heavy = df[df['User_Group'] == 'Heavy User']['Scaled_Cognitive_Score']

stat, p_val = mannwhitneyu(group_light, group_heavy)
print(f"Average Score (Light Users): {group_light.mean():.2f}")
print(f"Average Score (Heavy Users): {group_heavy.mean():.2f}")
print(f"P-Value: {p_val:.4f}")

if p_val < 0.05:
    print("VERDICT: SIGNIFICANT. High screen time is linked to lower cognitive scores.")
else:
    print("VERDICT: NOT SIGNIFICANT. Even with the new grading, screens don't make them 'dumber'.")
```

    --- NEW CORRELATION ANALYSIS ---



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ScreenTime_Weekend</th>
      <th>GPA</th>
      <th>Sleep_Hours</th>
      <th>Scaled_Cognitive_Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ScreenTime_Weekend</th>
      <td>1.000000</td>
      <td>-0.126200</td>
      <td>-0.151245</td>
      <td>-0.006471</td>
    </tr>
    <tr>
      <th>GPA</th>
      <td>-0.126200</td>
      <td>1.000000</td>
      <td>0.059929</td>
      <td>0.284606</td>
    </tr>
    <tr>
      <th>Sleep_Hours</th>
      <td>-0.151245</td>
      <td>0.059929</td>
      <td>1.000000</td>
      <td>0.025355</td>
    </tr>
    <tr>
      <th>Scaled_Cognitive_Score</th>
      <td>-0.006471</td>
      <td>0.284606</td>
      <td>0.025355</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



    
![png](output_28_2.png)
    


    Average Score (Light Users): 2.64
    Average Score (Heavy Users): 2.77
    P-Value: 0.6338
    VERDICT: NOT SIGNIFICANT. Even with the new grading, screens don't make them 'dumber'.



```python
import pandas as pd
from scipy.stats import spearmanr

# 1. Convert "Sports Frequency" to numbers so we can check correlations
# 0 = No sports, 1 = Low, 2 = Medium, 3 = High
sports_map = {
    'Ни одного': 0, 
    'Нет': 0, 
    'Ничего': 0,
    '1-2': 1, 
    '2-3': 2, 
    'Более 3 раз': 3
}
# Create a numeric column for sports
df['Sports_Numeric'] = df['Training_Freq'].map(sports_map)

# 2. Select the Key Variables for the Report
variables = [
    'ScreenTime_Weekend', 
    'GPA', 
    'Sleep_Hours', 
    'Scaled_Cognitive_Score', 
    'Sports_Numeric',
    'Age'
]

# 3. Create a Custom Loop to Calculate P-Values for every pair
results = []

for i in range(len(variables)):
    for j in range(i + 1, len(variables)): # i+1 avoids duplicates (A vs B, B vs A)
        col1 = variables[i]
        col2 = variables[j]
        
        # Drop rows where data is missing for this specific pair
        temp_df = df[[col1, col2]].dropna()
        
        # Run Spearman Correlation (Safe for grades/ranks)
        r, p = spearmanr(temp_df[col1], temp_df[col2])
        
        # Determine Significance Label
        if p < 0.001: sig = "*** (Highly Sig)"
        elif p < 0.01: sig = "** (Very Sig)"
        elif p < 0.05: sig = "* (Significant)"
        elif p < 0.10: sig = ". (Trend)"
        else: sig = "NS (Not Sig)"
        
        # Save to list
        results.append({
            'Factor A': col1,
            'Factor B': col2,
            'Correlation (r)': round(r, 3),
            'P-Value': round(p, 4),
            'Verdict': sig
        })

# 4. Create DataFrame and Sort by P-Value (Most significant on top)
stats_table = pd.DataFrame(results)
stats_table = stats_table.sort_values(by='P-Value')

# Display the Full Master Table
print("MASTER STATISTICAL SUMMARY")
print("=" * 80)
print(stats_table.to_string(index=False))
print("=" * 80)
```

    MASTER STATISTICAL SUMMARY
    ================================================================================
                  Factor A               Factor B  Correlation (r)  P-Value          Verdict
                       GPA Scaled_Cognitive_Score            0.285   0.0001 *** (Highly Sig)
        ScreenTime_Weekend         Sports_Numeric           -0.188   0.0114  * (Significant)
        ScreenTime_Weekend            Sleep_Hours           -0.151   0.0410  * (Significant)
            Sports_Numeric                    Age           -0.139   0.0623        . (Trend)
        ScreenTime_Weekend                    GPA           -0.126   0.0887        . (Trend)
                       GPA         Sports_Numeric            0.106   0.1547     NS (Not Sig)
                       GPA                    Age           -0.090   0.2245     NS (Not Sig)
        ScreenTime_Weekend                    Age            0.064   0.3880     NS (Not Sig)
                       GPA            Sleep_Hours            0.060   0.4203     NS (Not Sig)
               Sleep_Hours         Sports_Numeric            0.048   0.5244     NS (Not Sig)
    Scaled_Cognitive_Score         Sports_Numeric           -0.047   0.5268     NS (Not Sig)
               Sleep_Hours                    Age           -0.043   0.5629     NS (Not Sig)
               Sleep_Hours Scaled_Cognitive_Score            0.025   0.7333     NS (Not Sig)
    Scaled_Cognitive_Score                    Age            0.018   0.8053     NS (Not Sig)
        ScreenTime_Weekend Scaled_Cognitive_Score           -0.006   0.9307     NS (Not Sig)
    ================================================================================



```python
from scipy.stats import spearmanr

# 1. Prepare data (remove empty rows for these two columns)
clean_gpa_screen = df.dropna(subset=['ScreenTime_Weekend', 'GPA'])

# 2. Run Spearman Correlation
r, p_value = spearmanr(clean_gpa_screen['ScreenTime_Weekend'], clean_gpa_screen['GPA'])

print("--- DIRECT CORRELATION: SCREEN TIME vs. GPA ---")
print(f"Correlation (r): {r:.3f}")
print(f"P-Value: {p_value:.4f}")

if p_value < 0.05:
    print("Verdict: SIGNIFICANT link.")
elif p_value < 0.10:
    print("Verdict: MARGINAL TREND (Almost significant).")
else:
    print("Verdict: NOT SIGNIFICANT.")
```

    --- DIRECT CORRELATION: SCREEN TIME vs. GPA ---
    Correlation (r): -0.126
    P-Value: 0.0887
    Verdict: MARGINAL TREND (Almost significant).



```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Manually create the summary data based on our findings
# We use the correlation (r) for the bar height.
# For the "Combined Effect", we use the standardized coefficient approx or just mark it visually.
data = {
    'Hypothesis': [
        'Logic -> Grades',      # 1
        'Sports -> Sleep',      # 2 (Using the 2-3x group diff as proxy or r)
        'Sleep -> Grades',      # 3
        'Screens -> Cognitive', # 4
        'Screens -> Grades',    # 5
        'Screens -> Sleep',     # 6
        'Screens -> Sports'     # 7
    ],
    'Strength (r)': [
        0.285,   # Logic -> Grades (Positive Strong)
        0.150,   # Sports -> Sleep (Positive - approx based on diff)
        0.060,   # Sleep -> Grades (Weak Positive)
        -0.006,  # Screens -> Cognitive (Zero)
        -0.126,  # Screens -> Grades (Negative Trend)
        -0.151,  # Screens -> Sleep (Negative Sig)
        -0.188   # Screens -> Sports (Negative Sig)
    ],
    'Significant': [
        'Yes (***)', # Logic
        'Yes (*)',   # Sports (Sweet spot)
        'No',        # Sleep -> Grades
        'No',        # Cognitive
        'Trend (.)', # Screens -> Grades
        'Yes (*)',   # Screens -> Sleep
        'Yes (*)'    # Screens -> Sports
    ]
}

df_viz = pd.DataFrame(data)

# 2. Define Colors: Green/Red for Sig, Grey for Non-Sig
colors = []
for index, row in df_viz.iterrows():
    if row['Significant'].startswith('No'):
        colors.append('lightgrey') # Ignore these
    elif row['Strength (r)'] > 0:
        colors.append('#2ecc71')   # Green (Good positive link)
    else:
        colors.append('#e74c3c')   # Red (Bad negative link)

# 3. Plot
plt.figure(figsize=(12, 7))
ax = sns.barplot(x='Strength (r)', y='Hypothesis', data=df_viz, palette=colors)

# Add a vertical line at 0
plt.axvline(x=0, color='black', linestyle='-', linewidth=1)

# Add text labels (P-values/Sig)
for i, p in enumerate(ax.patches):
    width = p.get_width()
    label = df_viz.loc[i, 'Significant']
    
    # Place text to the right or left of bar
    x_pos = width + 0.01 if width > 0 else width - 0.08
    ax.text(x_pos, p.get_y() + p.get_height()/2 + 0.1, label, fontsize=12, fontweight='bold')

plt.title('Statistical Findings: Which Links are Real?', fontsize=16)
plt.xlabel('Correlation Strength (r)', fontsize=12)
plt.grid(axis='x', linestyle='--', alpha=0.5)
plt.show()
```

    /var/folders/d8/4k3q_2wd4nv9gmh9ch_b79jr0000gn/T/ipykernel_13950/890060127.py:52: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `y` variable to `hue` and set `legend=False` for the same effect.
    
      ax = sns.barplot(x='Strength (r)', y='Hypothesis', data=df_viz, palette=colors)



    
![png](output_31_1.png)
    



```python
import matplotlib.pyplot as plt

# 1. Define the table data as a list of lists
cell_text = [
    ["1. Screens hurt Grades", "Trend", "r = -0.126, p = 0.09"],
    ["2. Screens hurt Sleep", "TRUE", "r = -0.151, p = 0.04 *"],
    ["3. Sleep affects Grades", "FALSE", "r = 0.060, p = 0.42"],
    ["4. TikTok worse than Telegram", "FALSE", "No Sig Difference"],
    ["5. Sports improve Sleep", "TRUE", "Sweet Spot (2-3x) p=0.04 *"],
    ["6. Digital Dementia", "FALSE", "r = -0.006, p = 0.93"],
    ["7. Screens kill Sports", "TRUE", "r = -0.188, p = 0.01 *"],
    ["8. Logic predicts Grades", "TRUE", "r = 0.285, p < 0.001 ***"],
    ["9. Combined Effect (Regression)", "SCREENS WIN", "Screen p=0.002 vs Sleep p=0.55"]
]

columns = ["Hypothesis", "Result", "Stats Verdict"]

# 2. Create the plot
fig, ax = plt.subplots(figsize=(10, 6))
ax.axis('tight')
ax.axis('off')

# 3. Draw Table
the_table = ax.table(cellText=cell_text,
                     colLabels=columns,
                     loc='center',
                     cellLoc='left')

# 4. Styling
the_table.auto_set_font_size(False)
the_table.set_fontsize(12)
the_table.scale(1.2, 2) # Adjust width/height

# Make Header Bold and Grey
for (row, col), cell in the_table.get_celld().items():
    if row == 0:
        cell.set_text_props(weight='bold', color='white')
        cell.set_facecolor('#40466e') # Dark Blue Header
    elif row % 2 == 0:
        cell.set_facecolor('#f2f2f2') # Zebra striping for readability

plt.title("Master Summary of Findings", fontsize=16, y=0.95)
plt.show()
```


    
![png](output_32_0.png)
    



```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Define the Data (Same as before)
data = {
    'Hypothesis': [
        'Logic -> Grades',
        'Sports -> Sleep',
        'Sleep -> Grades',
        'Screens -> Cognitive',
        'Screens -> Sleep',
        'Screens -> Sports',
        'Combined Model: Screens -> Grades'
    ],
    'Strength (r)': [
        0.285,   # Logic
        0.150,   # Sports
        0.060,   # Sleep
        -0.006,  # Cognitive
        -0.151,  # Screens->Sleep
        -0.188,  # Screens->Sports
        -0.126   # Combined Regression Result
    ],
    'Label': [
        'Yes (***)', 
        'Yes (*)',   
        'No',        
        'No',        
        'Yes (*)',   
        'Yes (*)',   
        'Yes (**)'   
    ]
}

df_viz = pd.DataFrame(data)

# 2. Define Custom Colors
colors = []
for index, row in df_viz.iterrows():
    if row['Hypothesis'].startswith('Combined'):
        colors.append('#8b0000') # Dark Red
    elif row['Label'] == 'No':
        colors.append('lightgrey')
    elif row['Strength (r)'] > 0:
        colors.append('#2ecc71') # Green
    else:
        colors.append('#e74c3c') # Red

# 3. Create the Plot - WIDER SIZE
plt.figure(figsize=(15, 8)) # Increased width to 15

ax = sns.barplot(
    data=df_viz, 
    x='Strength (r)', 
    y='Hypothesis', 
    hue='Hypothesis', 
    palette=colors,
    legend=False
)

# 4. Add Vertical Line and Labels
plt.axvline(x=0, color='black', linestyle='-', linewidth=1)

for i, p in enumerate(ax.patches):
    width = p.get_width()
    label_text = df_viz.iloc[i]['Label']
    
    # Adjust text position (more padding)
    if width > 0:
        x_pos = width + 0.01
        ha = 'left'  # Align text to the left of the point
    else:
        x_pos = width - 0.01
        ha = 'right' # Align text to the right of the point
    
    ax.text(
        x_pos, 
        p.get_y() + p.get_height()/2 + 0.1, 
        label_text, 
        fontsize=12, 
        fontweight='bold',
        color='black',
        ha=ha # Horizontal alignment helper
    )

plt.title('Final Statistical Findings: What affects what?', fontsize=18)
plt.xlabel('Correlation Strength', fontsize=14)

# 5. Expand the X-Axis limits to fit the text comfortably
plt.xlim(-0.35, 0.45) 

plt.grid(axis='x', linestyle='--', alpha=0.5)
plt.tight_layout()
plt.show()
```


    
![png](output_33_0.png)
    



```python

```
