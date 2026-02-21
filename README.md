# 📊 Stories Coffee Hackathon
## Branch Segmentation, Anomaly Detection & Revenue Forecasting

---

## 🧠 Business Problem

Stories Coffee operates 25 branches across Lebanon.  
Management currently applies similar strategies across all branches despite differences in seasonality and ramp-up behavior.

This project answers:

> "How can Stories use its sales data to make more money?"

---

## What This Project Delivers

1. Branch clustering (6 behavioral profiles)
2. Anomaly detection (structural outliers)
3. Early-year revenue forecasting (Jan–Jun → full year)

---

## Methodology

- Data cleaning of messy POS exports
- Monthly sales share normalization
- K-Means clustering (k=6)
- Isolation Forest anomaly detection
- Ridge regression forecasting
- 5-fold cross-validation

---

## Key Results

- 6 distinct branch types identified
- 3 structural anomalies detected
- Forecasting accuracy (eligible branches):
  - 5-fold CV R² ≈ 0.95
  - Holdout R² ≈ 0.96

---

## How to Run

1. Place the 4 CSV files in the same directory as the notebook.
2. Open `stories_analysis.ipynb`
3. Run all cells.

---

## Output

- Final branch classification table
- Cluster prototype visualization
- Anomaly ranking
- Forecast vs actual comparison