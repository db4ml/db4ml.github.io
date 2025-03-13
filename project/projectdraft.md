# 📄 DRAFT -  Database Project

## 📌 Objective
This project builds a **structured SQLite3 database** using real-time weather data from the **Finnish Meteorological Institute (FMI)**. The database:
- **Fetches station metadata (ID, name, latitude, longitude)**
- **Retrieves real-time weather data (temperature, wind speed, cloud cover, precipitation)**
- **Stores the data in BCNF-compliant tables**
- **Prints structured tables for analysis**

---

## 📚 Learning Outcomes
By completing this assignment, students will:
✔ **Learn how to work with APIs** (`fmiopendata` for real-time data).  
✔ **Understand database schema design** (BCNF normalization).  
✔ **Store and query structured weather data** using SQLite3.  
✔ **Ensure data integrity** (handle `None` and `NaN` values).  
✔ **Optimize queries and handle database locks** in concurrent processes.  
✔ **Present query results in a tabular format** using `tabulate`.  

---

## 📁 Project Workflow

### 1️⃣ Create a SQLite3 Database
The database contains **six normalized tables**:

| Table Name               | Description |
|--------------------------|-------------|
| **Locations**             | Stores FMI weather stations (ID, name, latitude, longitude) |
| **WeatherTimestamps**     | Stores timestamps linked to stations |
| **TemperatureReadings**   | Stores temperature data |
| **WindReadings**          | Stores wind speed data |
| **CloudinessReadings**    | Stores cloud cover percentage |
| **PrecipitationReadings** | Stores precipitation amounts |

---

### 2️⃣ Fetch FMI Weather Stations
- Uses the **FMI API** to retrieve station metadata:
  - **Station ID**
  - **Station Name**
  - **Latitude & Longitude**
- Stores the stations in the **`Locations`** table.

📌 **SQL Schema Example:**
```sql
CREATE TABLE Locations (
    station_id INTEGER PRIMARY KEY,
    station_name TEXT UNIQUE NOT NULL,
    latitude REAL NOT NULL,
    longitude REAL NOT NULL
);

### 3. Fetch & Process FMI Weather Data

- Retrieves real-time **temperature, wind speed, cloudiness, and precipitation** from the **FMI API**.
- Handles **missing values** (`None` → `0.0` for precipitation).
- Stores data **only for known stations**, ensuring referential integrity.

### 4. Insert Data into SQLite3

- Ensures **no duplicate timestamps** using `INSERT OR IGNORE`.
- Handles **missing values gracefully**.
- Optimizes **performance using WAL mode**.

#### Example Data Insert:
```sql
INSERT OR IGNORE INTO WeatherTimestamps (station_id, timestamp)
VALUES (101, '2025-03-13 14:00:00');'```

### 5. Query & Display Data

- Uses **tabulate** to present query results in a **structured format**.
- Prints tables such as **Locations, WeatherTimestamps, and Readings**.

#### Example Query to View Recent Observations:
```sql
SELECT WT.timestamp, L.station_name, T.temperature, W.wind_speed, C.cloud_coverage, P.precipitation
FROM WeatherTimestamps WT
JOIN Locations L ON WT.station_id = L.station_id
LEFT JOIN TemperatureReadings T ON WT.timestamp_id = T.timestamp_id
LEFT JOIN WindReadings W ON WT.timestamp_id = W.timestamp_id
LEFT JOIN CloudinessReadings C ON WT.timestamp_id = C.timestamp_id
LEFT JOIN PrecipitationReadings P ON WT.timestamp_id = P.timestamp_id
ORDER BY WT.timestamp DESC LIMIT 5;
