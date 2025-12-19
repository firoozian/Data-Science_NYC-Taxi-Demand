# NYC Yellow Taxi 2019 – ELT + ML on Databricks (PySpark)

End-to-end ELT + Machine Learning pipeline on Databricks (Apache Spark / PySpark) to forecast hourly NYC yellow taxi demand per pickup zone.
---

## 🎯 Project Goal
Build a reproducible, production-style data pipeline to:
- Ingest NYC Yellow Taxi trip data (Feb–May 2019)
- Create CLEAN and FEATURE Delta tables
- Analyze temporal and spatial demand patterns
- Train, evaluate, and persist ML models for inference

---

## 🧰 Tech Stack
- Azure Databricks (Community Edition)
- Apache Spark / PySpark
- Delta Lake (RAW → CLEAN → FEATURE)
- Spark ML (Pipeline, OHE, Linear Regression, Random Forest)
- Pandas & Matplotlib (EDA & visualization)

---

## 📊 Dataset
NYC Yellow Taxi Trip Records (2019) + Taxi Zone Lookup  
Source: NYC TLC Open Data

---

## 🧱 Pipeline Overview

### RAW → CLEAN
- Load monthly parquet files (Feb–May 2019)
- Schema normalization, type casting, and quality filtering
- Time feature extraction (hour, day-of-week, month)
- Persisted as Delta tables

### FEATURE
Hourly aggregation per pickup zone:
- `trip_count` (target)
- `sum_passengers`
- `avg_trip_distance`
- `avg_total_amount`

Joined with zone metadata and stored as:
- Delta dataset
- SQL table: `nyc_taxi_2019.hourly_demand_features`

---

## 📈 Key EDA Insights
- Clear daily and weekly seasonality
- Strong demand concentration in Manhattan zones
- Zone-level patterns dominate borough-level behavior

---

## 🤖 ML Modeling

**Train/Test Split**
- Train: Feb–Apr 2019  
- Test: May 2019 (time-based)

**Models**
- Baseline: Linear Regression  
- Main: Random Forest Regressor  

---

## 🧪 Model Performance (Test Set – May 2019)

| Model             | RMSE | MAE | R²   |
|-------------------|------|-----|------|
| Linear Regression | 9.57 | 4.94| 0.995|
| Random Forest     |21.23 | 9.09| 0.978|

**Result:**  
Linear Regression outperformed Random Forest, indicating that NYC taxi demand is largely driven by strong linear temporal and spatial patterns.

---

## 🔍 Feature Importance – Key Insights
- Strongest positive drivers:  
  Upper East Side South (+10.10), Penn Station / Madison Sq West (+9.58), Midtown East (+9.15)
- Strongest negative drivers:  
  Central Park (−6.76), Times Sq / Theatre District (−6.42), Lower East Side (−4.54)

**Key takeaway:**  
NYC taxi demand is highly **local and micro-spatial**, with zone-level effects dominating broader borough signals.

---

## 🧱 Reproducibility & Inference
- Feature pipeline and trained model are saved and reloadable
- Single-hour inference function provided
- Ready for downstream deployment (e.g., Streamlit or API)

---

## 📌 Resume Bullet
Built an end-to-end ELT and ML pipeline on Azure Databricks using PySpark and Delta Lake to forecast hourly NYC taxi demand per zone, achieving **R² = 0.995** on a time-based holdout set.

---

## 🧑‍💻 Author
**Sina Firuzian**  
📧 [sina.firuzian@gmail.com]  
