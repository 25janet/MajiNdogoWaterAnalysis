# Global Access to Drinking Water (2000–2020)  
**Data Transformation, Analysis, and Visualization Project**

##  Project Overview
This project analyzes global access to drinking water services between **2000 and 2020**, using national, rural, and urban indicators. The goal is to understand **levels of access**, **rates of change over time**, and **inequalities across regions and income groups** through structured data transformation, statistical analysis, and visualization.

The project was initially developed in **Google Sheets** and focuses on real-world data cleaning, feature engineering, descriptive statistics, and visual analytics.

---

##  Dataset Description
The primary dataset contains country-level estimates of access to drinking water services, including:

- **Basic access**
- **Limited access**
- **Unimproved access**
- **Surface water access**

These indicators are reported separately for:
- National population  
- Rural population  
- Urban population  

Additional supporting datasets (e.g. `Regions.csv`) are used to enrich the analysis with **regional classifications**.

---

##  Data Preparation & Feature Engineering

### 1. Population Features
- **`pop_n`** – Total national population  
- **`pop_u`** – Urban population share (%)  
- **`pop_u_val`** – Estimated urban population (absolute values)  
- **`pop_r`** – Rural population share (%)  
  > Calculated as: `pop_r = 100 − pop_u`

To improve visualization clarity:
- **`pop_u (rounded)`** was created by rounding urban population share to the nearest whole number.

---

### 2. Year Difference
- **`y_diff`** – Year difference between consecutive observations for the same country  
  - Calculated only when two consecutive rows belong to the same country
  - Used to confirm consistent reporting intervals

---

### 3. Annual Rate of Change (ARC)
The **Annual Rate of Change (ARC)** measures how access to basic drinking water services changes per year.

General formula:

ARC_x = (wat_bas_x(n+1) − wat_bas_x(n)) / (year(n+1) − year(n))

Where `x` represents:
- `n` → national
- `r` → rural
- `u` → urban

Calculated features:
- **`ARC_n`** – National ARC  
- **`ARC_r`** – Rural ARC  
- **`ARC_u`** – Urban ARC  

Error handling:
- ARC values are only calculated when consecutive rows belong to the same country.
- Errors caused by missing values are handled using `IFERROR`, returning blanks instead of invalid numbers.

---

### 4. Filtered ARC Features
To avoid misleading results caused by countries that already have **100% access**, additional filtered features were created:

- **`ARC_n_filtered`**
- **`ARC_r_filtered`**
- **`ARC_u_filtered`**

**Logic:**
- ARC values are only calculated if access is **less than 100%**
- Countries with full access in both years are excluded from ARC calculations

This ensures that ARC averages reflect **actual progress**, not countries that have already reached saturation.

---

### 5. Full Access Identification
A categorical feature was added to flag countries with no remaining room for improvement:
- **`ARC_x_full` = "Full access"**  
  - Assigned when access is 100% in both reported years

---

##  Statistical Analysis

The project includes:
- **Measures of central tendency**
  - Mean
  - Median
  - Mode
- **Measures of spread**
  - Minimum
  - Maximum
  - Interquartile Range (IQR)
  - Standard deviation

These were computed for **12 service-level features** across national, rural, and urban populations.

---

##  Visualizations

### Key Charts Created
- **100% stacked column charts**
  - Distribution of water service levels
  - Separate views for national, rural, and urban populations

- **Line charts**
  - Urban vs rural population share across population sizes

- **Box & whisker plots**
  - Distribution of access levels across service categories

- **Histograms**
  - Year distribution
  - ARC differences (`ARC_diff`)

- **Bubble chart**
  - National ARC vs Rural ARC
  - Bubble size: national population
  - Color/series: region

---

##  Regional & Income Group Analysis
Using a pivot table and region mapping:
- Number of countries per region
- Average ARC by region (national, rural, urban)
- Comparison of progress across income groups

Income groups were numerically encoded to allow proper sorting:
- 0 – NAN  
- 1 – Low income  
- 2 – Lower middle income  
- 3 – Upper middle income  
- 4 – High income  

---

##  Key Insights
- A lower average ARC does **not necessarily imply slower progress**; it may reflect countries that have already achieved full access.
- Rural areas often show higher ARC values, indicating **catch-up growth**, but with larger disparities.
- Regional and income-based differences remain significant across all service levels.

---

##  Tools Used
- Google Sheets (data cleaning, formulas, pivot tables, charts)
- CSV integration for region mapping
- GitHub for version control and documentation

---



