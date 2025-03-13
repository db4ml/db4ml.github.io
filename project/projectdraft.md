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
