# 🎧 Spotify 2023 Data Analysis

This project Contains dataset of spotify artist and how their music are trending what are the names of the artist and other things.

---

## Project Objective:
- The Objective is that which artist has the highest track from top 10 artists.

### Explanation:
I started by loading the data and accessing the data

```python
import pandas as pd
import matplotlib.pyplot as plt
from datasets import load_dataset
import seaborn as sns

df = pd.read_csv('D:\python practice/Data Analytics/Real Dataset Practice/Spotify customers/spotify-2023.csv',encoding='latin1')
```

Then i used a copy method so that it does not effect the orginal data frame:
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

I used groupby() method and grouped it by artist name and added an agg method.At last i used the melt method so that it becomes Easy to plot the graph.

```python
    artist_stats = df_t.groupby('artist(s)_name').agg({
    'track_name' : 'count',
    'in_spotify_playlists' : 'sum',
    'in_apple_playlists':'sum'
}).reset_index()

artist_stats.columns = ['Artist', 'Number of Tracks', 'Spotify Playlists', 'Apple Playlists']

top_by_playlist = artist_stats.sort_values(by='Spotify Playlists', ascending=False).head(10)


melted = top_by_playlist.melt(
    id_vars='Artist', 
    value_vars=['Spotify Playlists', 'Apple Playlists'], 
    var_name='Platform', 
    value_name='Playlist Count')

# Plotting the graph for better Visualization
plt.figure(figsize=(12, 6))
sns.barplot(data=melted, x='Artist', y='Playlist Count', hue='Platform')
plt.title("Top 10 Artists by Playlist Inclusions")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Result:

![Top Artists Chart](images\output.png)