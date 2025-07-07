# 🎧 Spotify 2023 Data Analysis

This project Contains dataset of spotify artist and how their music are trending what are the names of the artist and other things.

---

## Project Objective:
- This Objective is that which artist has the highest track from top 10 artists.

### Explanation:
I started b loading the data and accessing the data

```python
import pandas as pd
import matplotlib.pyplot as plt
from datasets import load_dataset
import seaborn as sns

df = pd.read_csv('D:\python practice/Data Analytics/Real Dataset Practice/Spotify customers/spotify-2023.csv',encoding='latin1')
```

Then i used a copy method so that i dont effect the orginal data frame:
```python
df_t = df.copy()
```

I Use the str split() method to split the string
```python
df_t['artist(s)_name'] = df_t['artist(s)_name'].str.split(',')
```

Used Explode() method to explode the artist_name column and then run the value_counts() and reseted the index.
```python
top_artist = df_t['artist(s)_name'].value_counts().reset_index()
top_artist.columns = ['Artist','number of tracks']
```