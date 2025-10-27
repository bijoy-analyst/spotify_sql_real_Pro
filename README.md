# 🎵 Spotify Music Data Analysis Using SQL

Welcome to my **Spotify SQL Data Analysis Project**!  
In this project, I used SQL to explore and analyze a **Spotify dataset**, uncovering insights about tracks, artists, albums, and streaming trends.  

---

## 📊 Project Overview

This project focuses on analyzing key metrics from Spotify data such as:
- Track popularity and stream counts  
- Artist performance  
- Album insights  
- Comparison between Spotify and YouTube streams  
- Use of **aggregate functions**, **subqueries**, and **window functions**

---

## 🧠 Skills & Concepts Used

✅ SQL Clauses: `SELECT`, `WHERE`, `GROUP BY`, `ORDER BY`  
✅ Aggregate Functions: `COUNT()`, `SUM()`, `AVG()`, `MAX()`  
✅ Conditional Logic: `CASE WHEN`  
✅ Subqueries  
✅ Common Table Expressions (CTEs)  
✅ Window Functions: `DENSE_RANK()`  
✅ Data Cleaning and Analysis  

---

## 🗂️ Dataset

The dataset includes columns such as:
- `track` — Track name  
- `artist` — Artist name  
- `album`, `album_type`  
- `views`, `likes`, `comments`  
- `stream`, `licensed`, `official_video`  
- `danceability`, `energy`, `liveness`  
- `most_played_on` — Platform with most streams  

---

## 🧾 SQL Queries

### 🔹 1. Retrieve tracks with more than 1 billion streams
```sql
SELECT track, stream
FROM spotify
WHERE stream > 1000000000;

## 🧾 SQL Queries

### 🟢 2️⃣ List all albums along with their respective artists
```sql
SELECT
  DISTINCT album,
  artist
FROM spotify
ORDER BY 1;

## 🧾 SQL Queries

### 🟡 10️⃣ Retrieve the track names that have been streamed on Spotify more than YouTube
```sql
SELECT *
FROM (
  SELECT
    track,
    COALESCE(SUM(CASE WHEN most_played_on = 'Spotify' THEN stream END), 0) AS stream_on_spotify,
    COALESCE(SUM(CASE WHEN most_played_on = 'Youtube' THEN stream END), 0) AS stream_on_youtube
  FROM spotify
  GROUP BY 1
) AS t1
WHERE stream_on_spotify > stream_on_youtube
  AND stream_on_youtube <> 0;
## 📈 Insights Discovered

🎧 **Albums and Artists:**  
Each album is uniquely tied to an artist, helping identify the most active and productive creators on Spotify.

💬 **Licensed Tracks:**  
Licensed tracks generated a significantly higher number of comments, suggesting that verified or official releases gain more listener engagement and audience trust.

💿 **Album Type (Single):**  
A majority of the tracks belong to the **‘single’** album type — showing that most artists release standalone tracks rather than full albums to maximize reach and visibility.

💃 **Danceability Trends:**  
Certain albums displayed a higher **average danceability score**, meaning they contain tracks that are more rhythm-based, energetic, and enjoyable for upbeat listeners.

---

✨ **Overall Insight:**  
Spotify’s dataset reflects a trend toward **individual track releases** and **highly engaging licensed content**, with a strong audience preference for **energetic and danceable music.**

---

Would you like me to combine this with the 📈 **Insights Discovered** section into one professional README block (like a full portfolio piece for GitHub)?
