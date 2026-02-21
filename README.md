# ☕ Stories Coffee Hackathon
## 📊 Branch Segmentation, Anomaly Detection, Forecasting, and Profit Levers

## 🎯 Business Problem
Stories Coffee operates **25 branches across Lebanon**. Branches are often managed using similar decisions and targets, despite differences in seasonality, ramp-up behavior, and category mix.

This project answers:
> **“How can Stories use its data to make more money?”** 💰

We focus on four practical needs:
1) Understand branch seasonality patterns (manage branches by type)  
2) Detect unusual branches early (investigate issues quickly) 🚨  
3) Forecast year-end revenue by June for mature branches (intervene earlier) 📈  
4) Identify a clear profitability lever (category mix) 🧾  

---

## 🧠 Approach and Methodology

### 📂 Data
Raw POS exports (messy format, repeated headers, inconsistent branch names):
- `REP_S_00134_SMRY.csv` (monthly sales by branch, 2025 + Jan 2026)
- `rep_s_00673_SMRY.csv` (category profit summary by branch)
- (Optional / available) `rep_s_00014_SMRY.csv`, `rep_s_00191_SMRY-3.csv`

### 🔁 Pipeline (High Level)
1) **Cleaning and structuring** 🧹  
   - Convert the monthly sales export into a structured branch-by-month table (2025)  
   - Compute annual totals and monthly share features  

2) **Branch segmentation (unsupervised)** 🧩  
   - K-Means on monthly sales shares  
   - Result: **6 seasonality profiles (k=6)**  

3) **Anomaly detection (unsupervised)** 🔍  
   - Isolation Forest on monthly-share features  
   - Result: **3 structural outliers flagged**  

4) **Revenue forecasting (supervised)** ⏳  
   - Ridge regression predicting full-year revenue from Jan–Jun  
   - Forecast scope: “mature” branches where Jan–Jun revenue ≥ 10% of annual revenue  
   - Result: **15 forecast-eligible branches**, strong accuracy (**5-fold CV R² ≈ 0.95**)  

5) **Profit lever (category mix)** 💡  
   - Compute revenue as `Total Cost + Total Profit` (POS export truncation issue on Total Price)  
   - Compare branch margin vs beverage revenue share  
   - Result: beverage share correlates strongly with margin (**corr ≈ 0.73**) ✅  

---

## ✅ Key Findings and Visualizations
### Key Findings
- **6 branch types** exist based on seasonality patterns (stable, summer-driven, early-year heavy, late-year/event-driven) 🗓️  
- **3 anomaly branches** are structurally unusual and should be managed separately 🚨:
  - `Stories.`
  - `Stories Faqra`
  - `Stories Event Starco`
- **June forecasting works well for mature branches** 📈  
  - Eligible branches: **15/25**  
  - **5-fold CV R² ≈ 0.95** (Ridge regression)  
- **Profitability lever:** branches with higher beverage share tend to have higher overall margin ☕➡️💰  
  - Correlation between beverage revenue share and margin: **≈ 0.73**  

### Visualizations Produced
The notebook generates:
- Cluster prototype curves (monthly share per cluster) 📉  
- Top anomaly score chart 🚨  
- Forecast: predicted vs actual (eligible branches) 📈  
- Profit insight table + (optional) beverage share vs margin relationship 💡  

---

### How to Run

1. Place the 4 CSV files in the same directory as the notebook.
2. Open stories_analysis.ipynb
3. Run all cells.
