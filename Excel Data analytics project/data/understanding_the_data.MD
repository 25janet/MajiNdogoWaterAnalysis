# Integrated Project: Access to Drinking Water  
**Understanding the Data**

##  Project Overview
This integrated project investigates **global access to safe and affordable drinking water**, aligned with **United Nations Sustainable Development Goal 6 (Clean Water and Sanitation)**.

The project is divided into two main parts:
1. **Understanding the Data**
2. **Transforming the Data**

This document focuses on **Understanding the Data**, which prepares the dataset for analysis through exploration, cleaning, and visualization.

---

##  Dataset Description
The dataset used is the **WHO/UNICEF Joint Monitoring Programme (JMP) – Estimates on the Use of Water (2020)**.

It contains **16 original features**, primarily percentage-based indicators of water service access across different population groups.

### Key Features
| Feature | Description |
|------|------------|
| `name` | Country or area name |
| `income_group` | Country income classification |
| `pop_n` | National population (in thousands) |
| `pop_u` | Urban population share (%) |
| `wat_bas_n` | National basic water access (%) |
| `wat_lim_n` | National limited water access (%) |
| `wat_unimp_n` | National unimproved water access (%) |
| `wat_sur_n` | National surface water access (%) |
| `wat_bas_r / u` | Rural / Urban basic access (%) |
| `wat_lim_r / u` | Rural / Urban limited access (%) |
| `wat_unimp_r / u` | Rural / Urban unimproved access (%) |
| `wat_sur_r / u` | Rural / Urban surface access (%) |

> ℹ️ The dataset includes **four service levels** (basic, limited, unimproved, surface), where *basic* combines safely managed and basic services.

---

##  Importing the Data
The dataset is imported into **Google Sheets** using the CSV format.

### Import Challenges
- Some rows used **semicolons (`;`) instead of commas**, causing incorrect column separation.
- Missing values are represented as `NAN`.

### Data Cleaning Steps
1. Import CSV into Google Sheets  
2. Use **Data → Split text to columns** to fix delimiter issues  
3. Confirm **16 columns per row**
4. Create a helper column `value_cnt` using `COUNTA()`  
5. Filter rows where `value_cnt ≠ 16` and fix them manually  

---

##  Investigating Population Size

### Global Comparison
- Estimated world population (2020): **7.821 billion**
- Estimated urban population share: **55%**

### New Features Created
- `pop_u_val` – Urban population value per country  
- `pop_r` – Rural population share (%)  
- `pop_n (m)` – National population rounded to nearest million  

### Analysis Goals
- Compare dataset population totals with global estimates
- Calculate **percentage differences**
- Understand why population *counts* and *shares* differ numerically

### Visualization
- Line chart comparing:
  - National population size
  - Urban vs rural population share
- Adjusted x-axis to reduce outlier distortion

---

##  Investigating Access by Area

### Areas Analyzed
- National
- Rural
- Urban

### Statistical Measures Calculated
- Minimum & Maximum
- Mean, Median, Mode
- Quartiles (Q1, Q3)
- Interquartile Range (IQR)
- Standard Deviation

### Data Quality Fix
- Created `wat_bas_n (rounded)` to cap values exceeding 100%
- Replaced formula errors with `NAN`

### Visualization
- **Box and Whisker (Candlestick) plots** for:
  - 12 access features (4 service levels × 3 areas)

---

## Investigating Access by Population Size

### Visualizations Used
- **100% Stacked Column Charts** showing:
  - National access vs population size
  - Urban access vs urban population share
  - Rural access vs rural population share

### Additional Features
- `pop_u (rounded)`
- `pop_r (rounded)`

### Key Insight
Access to water services varies more strongly by **area type** (urban vs rural) than by population size alone.

---

##  Investigating Access by Income Group

### Income Groups
- Low income
- Lower-middle income
- Upper-middle income
- High income

### Pivot Table Summary
Grouped by `income_group`, calculating:
- Total population
- Average urban share
- Average access to each service level

### Income Group Encoding
| Income Group | Code |
|------------|------|
| NAN | 0 |
| Low | 1 |
| Lower-middle | 2 |
| Upper-middle | 3 |
| High | 4 |

### Findings
- Higher income groups tend to be:
  - More urbanized
  - More likely to have basic water access
- Lower income groups show higher reliance on unimproved and surface water sources

---

##  Outputs Created

### Dataset Sheet
- Original 16 features
- 7 newly engineered features  
**Total: 23 features**

### Global 2020 Report Sheet
- Population comparison summary
- Percentage difference calculations
- Line charts
- Box and whisker plots
- Three 100% stacked column charts
- Income-group pivot table and visualization

---



---

##  Conclusion
This analysis provides a structured understanding of **global water access disparities**, highlighting how **income level, urbanization, and population distribution** influence access to drinking water services worldwide.

---


