# 🦠 COVID-19 Global Data Analysis — Big Data Fundamentals Project

> **Course:** Big Data Fundamentals  
> **Dataset:** Our World in Data – COVID-19 Complete Dataset  
> **Stack:** Python · Pandas · PySpark · Scikit-learn · Power BI

---

## 📋 Project Description

This project builds an **end-to-end Big Data pipeline** to analyze the global COVID-19 pandemic using data from 15 countries spanning 2020–2023 (~21,000 records). The pipeline covers data acquisition, preprocessing, exploratory analysis, large-scale processing with PySpark, predictive modeling with Random Forest, and a multi-page Power BI dashboard.

**Business questions answered:**
- How did COVID-19 waves evolve globally and by region?
- What was the relationship between vaccination rates and case fatality?
- Can we predict near-future case counts using time-series lag features?

---

## 🏗️ Architecture Diagram

```
[Data Source]          [Processing]              [Output]
Our World in Data  →   Python / Pandas      →    Cleaned Dataset
owid-covid-data.csv    (preprocessing, EDA)       (21k rows)
                            ↓
                       PySpark                →   Aggregated CSVs
                       (window functions,          for Power BI
                        SQL queries,
                        monthly rollups)
                            ↓
                       Scikit-learn           →   Prediction Results
                       (RandomForest,              (R² = 0.89)
                        LinearRegression)
                            ↓
                       Power BI               →   Interactive Dashboard
                       (5-page report)             (cases, deaths,
                                                    vaccination, forecast)
```

---

## 📁 Repository Structure

```
covid-19-big-data/
│
├── data/
│   └── owid-covid-data.csv          # Source dataset (OWID, download instructions below)
│
├── notebooks/
│   └── covid19_analysis.ipynb       # Main Jupyter notebook (all steps)
│
├── outputs/
│   ├── 01_missing_values.png        # EDA: missing data overview
│   ├── 02_global_trend.png          # EDA: global cases & deaths over time
│   ├── 03_cases_per_million.png     # EDA: normalized country comparison
│   ├── 04_vaccination_trend.png     # EDA: vaccination progress by continent
│   ├── 05_cfr_heatmap.png           # EDA: case fatality rate heatmap
│   ├── 06_correlation.png           # EDA: correlation matrix
│   ├── 07_prediction.png            # ML: actual vs predicted
│   ├── 08_feature_importance.png    # ML: Random Forest feature importance
│   ├── powerbi_full_dataset.csv     # Power BI: full cleaned dataset
│   ├── powerbi_monthly_global.csv   # Power BI: PySpark monthly aggregation
│   └── powerbi_country_summary.csv  # Power BI: per-country peak stats
│
└── README.md
```

---

## ⚙️ Installation & Usage

### 1. Clone the repository

```bash
git clone https://your-username@bitbucket.org/your-username/covid-19-big-data.git
cd covid-19-big-data
```

### 2. Install dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn pyspark jupyter
```

> **Java required for PySpark:** Install JDK 11+  
> Windows: https://adoptium.net/ | macOS: `brew install openjdk@11`

### 3. Download the dataset

The dataset is **not included** in the repository due to size. Download it from Our World in Data:

```bash
# Option A – Direct download
curl -L https://covid.ourworldindata.org/data/owid-covid-data.csv -o data/owid-covid-data.csv

# Option B – Python
python -c "
import urllib.request
urllib.request.urlretrieve(
    'https://covid.ourworldindata.org/data/owid-covid-data.csv',
    'data/owid-covid-data.csv'
)
print('Downloaded!')
"
```

### 4. Run the notebook

```bash
jupyter notebook notebooks/covid19_analysis.ipynb
```

Run all cells in order (Cell → Run All). Expected runtime: ~3–5 minutes (PySpark initialization takes ~30s).

### 5. Open the Power BI dashboard

1. Open Power BI Desktop
2. **Get Data → Text/CSV** → load `outputs/powerbi_full_dataset.csv`
3. Also load `outputs/powerbi_monthly_global.csv` and `outputs/powerbi_country_summary.csv`
4. Build visuals as described in the notebook (Step 6 – Power BI section)

---

## 📊 Pipeline Steps

| Step | Tool | Description |
|------|------|-------------|
| 1. Data Acquisition | Python / OWID URL | Load 21k+ rows, 19 columns, 15 countries |
| 2. Preprocessing | Pandas | Handle missing values, forward-fill vaccination data, derive CFR |
| 3. EDA | Matplotlib / Seaborn | 6 visualizations: trends, heatmaps, correlations |
| 4. Big Data Processing | PySpark | Window functions, SQL queries, monthly aggregations |
| 5. Predictive Modeling | Scikit-learn | Lag features + Random Forest for 7-day case forecasting |
| 6. Visualization | Power BI | 5-page interactive dashboard |

---

## 🔍 Key Findings

1. **Three major pandemic waves** were identified globally: mid-2020 (initial), late-2021 (Delta), and early-2022 (Omicron — highest case volume by far).

2. **Case Fatality Rate declined significantly** — from ~2.5% in 2020 to under 0.5% in 2023, attributed to vaccination rollout and improved medical response.

3. **Vaccination impact is clear:** Countries that reached 60%+ vaccination coverage showed a visible decoupling between rising case numbers and mortality rates from late 2021 onwards.

4. **PySpark window functions** enabled efficient rolling-average computation and peak-wave detection across the full multi-country dataset — demonstrating scalability to production-level data volumes.

5. **Random Forest outperformed Linear Regression** for 7-day-ahead case forecasting (R² ≈ 0.89 vs 0.72). The most important predictors were 7-day and 14-day lag features of new cases per million.

---

## 🛠️ Technologies Used

| Library | Version | Purpose |
|---------|---------|---------|
| Python | 3.10+ | Core language |
| Pandas | 2.x | Data manipulation & cleaning |
| NumPy | 1.x | Numerical operations |
| Matplotlib / Seaborn | latest | EDA visualizations |
| PySpark | 3.5+ | Big Data processing |
| Scikit-learn | 1.x | Predictive modeling |
| Jupyter | latest | Interactive notebook |
| Power BI Desktop | latest | Dashboard |

---

## 📚 Data Source

**Our World in Data — COVID-19 Dataset**  
- URL: https://covid.ourworldindata.org/data/owid-covid-data.csv  
- GitHub: https://github.com/owid/covid-19-data  
- License: Creative Commons BY 4.0  
- Coverage: All countries, Jan 2020 – Aug 2024  

Citation: *Mathieu, E., Ritchie, H., Ortiz-Ospina, E. et al. A global database of COVID-19 vaccinations. Nat Hum Behav 5, 947–953 (2021).*

---

## 👤 Author

**[Popa Rares-Stefan]**
Big Data Fundamentals — [BI2-ULBS], [2026] 
