# 🎵 Spotify SQL Data Analysis Project  

![Spotify Banner](https://github.com/bijoy-analyst/bijoy-analyst/blob/main/Navy%20Blue%20Geometric%20Technology%20LinkedIn%20Banner.png)

---

## 🧠 Project Overview  

This project analyzes **Spotify Music Data** using **SQL** — focusing on tracks, artists, albums, and audience engagement.  
It covers queries from **Beginner → Advanced Level**, showcasing real-world data analysis skills for a Data Analyst portfolio.

---

## 🟢 Basic Level Queries  

---

### 2️⃣ 🎤 List all albums along with their respective artists
```sql
SELECT
  DISTINCT album,
  artist
FROM spotify
ORDER BY 1;
```

---

### 3️⃣ 💬 Get the total number of comments for tracks where licensed = TRUE
```sql
SELECT
  SUM(comments)
FROM spotify
WHERE licensed = 'true';
```

---

### 4️⃣ 🎶 Find all tracks that belong to the album type 'single'
```sql
SELECT
  track,
  album_type
FROM spotify
WHERE album_type = 'single';
```

---

### 5️⃣ 🎧 Count the total number of tracks by each artist
```sql
SELECT
  artist,
  COUNT(*) AS total_song
FROM spotify
GROUP BY 1
ORDER BY 2 DESC;
```

---

## 🟡 Medium Level Queries  

---

### 6️⃣ 💃 Calculate the average danceability of tracks in each album
```sql
SELECT
  album,
  AVG(danceability) AS avg_danceability
FROM spotify
GROUP BY 1
ORDER BY 2 DESC;
```

---

### 7️⃣ ⚡ Find the top 5 tracks with the highest energy values
```sql
SELECT
  track,
  MAX(energy) AS energy
FROM spotify
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5;
```

---

### 8️⃣ 🎬 List all tracks along with their views and likes where official_video = TRUE
```sql
SELECT 
  track,
  SUM(views) AS total_views,
  SUM(likes) AS total_likes
FROM spotify
WHERE official_video = 'true'
GROUP BY 1
ORDER BY 2 DESC;
```

---

### 9️⃣ 👁️‍🗨️ For each album, calculate the total views of all associated tracks
```sql
SELECT
  album,
  track,
  SUM(views) AS total_views
FROM spotify
GROUP BY 1, 2
ORDER BY 3 DESC;
```

---

### 🔟 🆚 Retrieve the track names that have been streamed more on Spotify than on YouTube
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
```

---

## 🔴 Advanced Level Queries  

---

### 11️⃣ 🏆 Find the top 3 most-viewed tracks for each artist using window functions
```sql
WITH cte AS (
  SELECT 
    artist,
    track,
    SUM(views) AS total_view,
    DENSE_RANK() OVER(PARTITION BY artist ORDER BY SUM(views) DESC) AS rank
  FROM spotify
  GROUP BY 1, 2
  ORDER BY 1, 3 DESC
)
SELECT * 
FROM cte
WHERE rank <= 3;
```

---

### 12️⃣ 🎤 Find tracks where the liveness score is above the average
```sql
SELECT 
  track,
  liveness
FROM spotify
WHERE liveness > (SELECT AVG(liveness) FROM spotify);
```

---

## 📈 Insights Discovered  

🎶 Many tracks have crossed **1 Billion+ streams** on Spotify.  
👩‍🎤 Top artists have significantly higher total track counts and engagement.  
💃 Albums with higher **danceability** tend to perform better in streaming.  
🎥 Tracks with **official videos** get more views and likes.  
🆚 Some songs perform better on **Spotify** than **YouTube**, showing audience preference.  
🏆 Window functions reveal **Top 3 most-viewed tracks per artist** efficiently.  
🎤 Tracks with above-average **liveness** are often energetic or live performances.  

---

## ⚙️ Tools & Technologies  

🧩 SQL (MySQL / PostgreSQL)  
🧮 Data Aggregation & Grouping  
🪄 CTE & Window Functions  
📊 Analytical Reporting  

---

## 🚀 How to Run  

1. Import your `spotify.csv` or `spotify` table into your SQL environment.  
2. Run each query step-by-step in order.  
3. Observe and interpret the query results to generate insights.  

---

## 👨‍💻 Author  

**Md Bijoy Hossen**  
📊 *Data Analyst | Excel | SQL | Power BI | Python*  
🔗 [GitHub Profile](https://github.com/bijoy-analyst)  

---

⭐ *If you found this project helpful, don’t forget to star this repository!* 🌟
