# Spotify Songs' Genre Segmentation

Clustering ~32,000 Spotify songs by their audio features and building a content-based song recommender.

## Overview
Spotify groups songs with similar audio characteristics to power its recommendations. In this project I use the Spotify songs dataset (audio features, playlist names, playlist genres and subgenres) to:

1. Pre-process the data (missing values, duplicate songs, feature engineering, scaling)
2. Explore it visually (distributions, genre profiles, popularity and release-year trends)
3. Compute and interpret the correlation matrix of the audio features
4. Cluster songs with **K-Means (k = 6)** and compare the clusters with playlist genres, subgenres and playlist names
5. Build a **content-based recommender** (K-Means cluster + cosine similarity)

## Files
| File | Description |
|---|---|
| `Spotify_Genre_Segmentation.ipynb` | Full analysis with outputs and plots |
| `Spotify_Genre_Segmentation.html` | Same notebook as a web page (no Python needed) |
| `spotify_songs.csv` | Dataset (32,833 playlist entries, 23 columns) |

## Key results
- Genres have distinct audio fingerprints: rap is high in speechiness and danceability, EDM in energy, loudness and tempo, rock is the least danceable, r&b is the most acoustic, and latin has the highest valence.
- Energy and loudness are strongly positively correlated (r = 0.68); both are negatively correlated with acousticness. Popularity is barely explained by audio features (all |r| <= 0.12).
- K-Means clusters have clear sonic identities (e.g. a rap-dominated and an EDM-dominated cluster), but song-level clusters only partly match playlist genres (ARI ~ 0.07) because genres overlap in sound. Playlist-level clustering matches genre better (ARI ~ 0.27).
- The recommender's top-10 lists match the query song's genre ~40% of the time vs ~17% by chance.

## How to run
```bash
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
jupyter notebook Spotify_Genre_Segmentation.ipynb
```
Keep `spotify_songs.csv` in the same folder as the notebook.

## Limitations and future work
Silhouette scores are modest (songs form a continuum rather than separate groups) and only audio features are used. Adding lyrics, artist information and listening history (collaborative filtering), or comparing other algorithms (Gaussian Mixture, hierarchical clustering, DBSCAN), could improve results.
