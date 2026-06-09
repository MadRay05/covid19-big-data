# Power BI Dashboard Setup Guide

## Files to import
Load these 3 CSV files from the `outputs/` folder:
- `powerbi_full_dataset.csv` — full cleaned dataset (main table)
- `powerbi_monthly_global.csv` — monthly global rollup (from PySpark)
- `powerbi_country_summary.csv` — country peak stats (from PySpark)

---

## Suggested Dashboard Pages

### Page 1 — Overview
- **KPI Cards:** Total Cases (SUM total_cases), Total Deaths, Max Vax %
- **Line Chart:** Date vs new_cases (7d avg) — all countries combined
- **Map:** location by total_cases_per_million (bubble size)

### Page 2 — Country Deep-Dive
- **Slicer:** Filter by `location`
- **Area Chart:** Date vs new_cases_per_million
- **Gauge:** case_fatality_rate (0–5% range)
- **Bar Chart:** new_deaths by year

### Page 3 — Vaccination Impact
- **Scatter Plot:** X = people_vaccinated_per_hundred, Y = case_fatality_rate, color = continent
- **Line Chart:** Dual axis — new_cases vs people_vaccinated_per_hundred over time

### Page 4 — Wave Analysis (use powerbi_monthly_global.csv)
- **Matrix/Heatmap:** year_month vs total_new_cases
- **Bar Chart:** Monthly new cases — color by wave period
- **Table:** Peak day per country (from powerbi_country_summary.csv)

### Page 5 — Country Comparison
- **Clustered Bar:** peak_total_cases by location
- **Stacked Bar:** max_vax_pct vs avg_cfr by location

---

## Useful DAX Measures

```dax
// Case Fatality Rate %
CFR % = DIVIDE(SUM('powerbi_full_dataset'[total_deaths]), SUM('powerbi_full_dataset'[total_cases])) * 100

// 7-Day Rolling Average New Cases
Cases 7d Avg = 
AVERAGEX(
    DATESINPERIOD('powerbi_full_dataset'[date], LASTDATE('powerbi_full_dataset'[date]), -7, DAY),
    CALCULATE(SUM('powerbi_full_dataset'[new_cases]))
)

// Vaccination Coverage %
Vax Coverage % = AVERAGE('powerbi_full_dataset'[people_vaccinated_per_hundred])
```

---

## Color Theme Suggestion
- Cases: #4285F4 (blue)
- Deaths: #EA4335 (red)  
- Vaccinations: #34A853 (green)
- Background: #F8F9FA (light gray)
- Accent: #FBBC04 (amber)
