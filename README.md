# 🗳️ Election Analytics Dashboard: Tamil Nadu & West Bengal

An interactive, end-to-end Power BI business intelligence project that structures, processes, and visualizes regional election data. This project showcases the complete lifecycle of data analysis—moving from raw public web spaces and API endpoints to a highly synchronized, interactive geographic dashboard.

<img width="1438" height="795" alt="Screenshot 2026-05-23 213336" src="https://github.com/user-attachments/assets/93411a6b-ebdf-488a-973a-5a4926e28342" />
<img width="1429" height="801" alt="Screenshot 2026-05-23 213352" src="https://github.com/user-attachments/assets/5d58e2a2-42c2-403a-b613-4a720c59dc9f" />


---

## 🚀 Project Overview & Key Visualizations

The primary objective of this project was to bypass generic aggregated metrics and build a highly granular, localized visualization platform for two major state elections:

* **Tamil Nadu Assembly Elections (2026):** Implemented a complete geographic map interface displaying real-time seat distributions across all 234 individual assembly constituencies.
* **West Bengal Assembly Elections (2021 - 2026):** Mapped historical shifts, party leaderboards, and changing voting patterns over multiple election cycles to track dynamic political movements.

---

## 💡 Core Data Engineering Challenges (What I Learned)

Building this portfolio project was a masterclass in handling real-world data constraints, manual validation, and pipeline development when automated solutions hit a wall.

### 🔌 1. API Integration & Custom ETL Pipelines
Instead of downloading ready-made spreadsheets, I engineered a true extraction pipeline by connecting directly to structured data endpoints.

* **The Problem:** The initial raw data returned highly nested JSON/list structures where a single row contained a compressed array of values.
* **The ETL Solution:** I built a custom Power Query transformation pipeline to unpack, flatten, and expand these nested lists. This converted a highly compressed initial response into a fully expanded, structured tabular format exceeding 10,000 clean data rows.

### 🐍 2. Web Scraping & Truth Discovery
Faced with unverified or fragmented data from search recommendations, I took complete ownership of data validation. I wrote web scraping logic to target and extract raw, unstructured polling tables directly from authenticated public databases like *IndiaVotes*, converting chaotic web text into clean relational schemas.

### 🗺️ 3. Overcoming Custom Spatial Boundary Mismatches
Standard geographic map visuals inside Power BI fail to recognize hyper-local state assembly boundaries. To solve this, I integrated a specialized, open-source **TopoJSON** geographic framework.

* **The Mismatch:** The map file contained character limits that truncated long constituency strings (e.g., cutting `Chepauk-Thiruvallikeni` down to `Chepauk-Thiruvalliken`), breaking standard exact-match joins.
* **The Modeling Fix:** I designed a custom **Dimension/Bridge Table** mapping structural IDs (`AC No.`) to the distorted map strings. This created a clean relational translation layer that seamlessly linked my scraped election results to the physical map shapes without corrupting the master database.

---

## 🛠️ Tech Stack & Architecture

* **BI Tool:** Power BI Desktop
* **Cloud Deployment:** Microsoft Fabric / Power BI Service
* **Data Pipelines:** Power Query (M Code) for API queries and Web Scraping
* **Spatial Framework:** TopoJSON Custom Map Visuals
* **Modeling & Calculations:** DAX (Data Analysis Expressions)

---

## 🧮 Key DAX Measures Applied

To keep the dashboard fully responsive and dynamic, calculations are calculated on-the-fly rather than hardcoded. This allows full cross-filtering capabilities across the map canvas.

* **Dynamic Row Count Tally:**
  ```dax
  Seats_Won = COUNTROWS('TN_26')
