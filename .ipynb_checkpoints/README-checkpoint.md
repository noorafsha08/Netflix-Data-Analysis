# 📺 Netflix Data Analysis

This project analyses a Netflix dataset to extract meaningful insights about its content library using **Python, Pandas, and Matplotlib**.

## 🔍 Overview

- Analyse number of movies vs TV shows
- Find top genres on Netflix
- Year-wise content addition trend
- Country-wise distribution of content
- Visualise data for better understanding

## 🗂️ Dataset

- [Netflix Titles Dataset on Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)

## 🛠️ Tech Stack

- Python
- Pandas
- Matplotlib
- Seaborn (optional for better visuals)

## 📊 Results

Include plots here after running your notebook.

## 🚀 How to Run

1. Clone this repo
2. Install requirements (Pandas, Matplotlib, Seaborn)
3. Open `netflix_analysis.ipynb` and run all cells

```bash
pip install pandas matplotlib seaborn

---
```
### ✅ **4. Stepwise Code Plan**

#### 📌 **Step 1. Setup**
```
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Read dataset
df = pd.read_csv('netflix_titles.csv')
df.head()

```
#### 📌 **Step 2. Data Cleaning**

```python
# Check for null values
print(df.isnull().sum())

# Fill or drop if needed
df['country'].fillna('Unknown', inplace=True)
df['director'].fillna('Not Specified', inplace=True)
df['cast'].fillna('Not Specified', inplace=True)
df['date_added'].fillna('Not Specified', inplace=True)
df.dropna(inplace=True)  # optional for rows with few missing

```
#### 📌 **Step 3. Movies vs TV Shows**

```python
sns.countplot(x='type', data=df)
plt.title('Count of Movies and TV Shows on Netflix')
plt.show()

```
#### 📌 **Step 4. Top 10 Genres**
```python
# Split multiple listed genres and count
from collections import Counter

genre_count = Counter()

for genres in df['listed_in']:
    genre_count.update([genre.strip() for genre in genres.split(',')])

# Convert to dataframe
genre_df = pd.DataFrame(genre_count.items(), columns=['Genre', 'Count']).sort_values(by='Count', ascending=False).head(10)

# Plot
sns.barplot(x='Count', y='Genre', data=genre_df)
plt.title('Top 10 Genres on Netflix')
plt.show()

```
#### 📌 **Step 5. Year-wise Content Added**
```python
# Extract year from date_added
df['year_added'] = pd.to_datetime(df['date_added'], errors='coerce').dt.year

# Drop NaT rows
df = df.dropna(subset=['year_added'])

# Convert to int
df['year_added'] = df['year_added'].astype(int)

# Plot
df['year_added'].value_counts().sort_index().plot(kind='bar', figsize=(12,6))
plt.title('Content Added per Year')
plt.xlabel('Year')
plt.ylabel('Number of Titles')
plt.show()

```
#### 📌 **Step 6. Country-wise Distribution (Top 10)**
```python
country_count = df['country'].value_counts().head(10)

# Plot
country_count.plot(kind='barh')
plt.title('Top 10 Countries with Most Content on Netflix')
plt.xlabel('Number of Titles')
plt.show()

✅ 5. Final: Push to GitHub

