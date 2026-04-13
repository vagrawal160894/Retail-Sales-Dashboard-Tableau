# 🛒 Retail Sales Performance Analysis — Tableau Dashboard

> An interactive Tableau dashboard analyzing retail store sales performance across 45 stores, exploring the influence of economic indicators, seasonal trends, holidays, and promotional activity on weekly sales.

---

## 📌 Table of Contents

- [Project Overview](#project-overview)
- [Business Objectives](#business-objectives)
- [Intended Audience & Personas](#intended-audience--personas)
- [Dataset](#dataset)
- [Data Cleaning & Preparation](#data-cleaning--preparation)
- [Dashboard Design](#dashboard-design)
  - [KPI Monitoring](#kpi-monitoring)
  - [Pre-Attentive Attributes & Visual Design](#pre-attentive-attributes--visual-design)
  - [Interactive Features](#interactive-features)
- [Key Design Choices](#key-design-choices)
- [Insights & Findings](#insights--findings)
- [Limitations](#limitations)
- [Tableau Public Dashboard](#tableau-public-dashboard)
- [Conclusion & Reflection](#conclusion--reflection)

---

## Project Overview

This project analyzes weekly retail sales data from 45 stores over a 3-year period (2010–2012). By combining sales data with economic indicators (CPI, fuel prices, unemployment) and event markers (holidays, promotions), the dashboard helps stakeholders quickly understand performance trends, seasonal effects, and external drivers of demand.

The final deliverable is a multi-view Tableau Public dashboard that supports both high-level executive monitoring and deeper exploratory data analysis.

---

## Business Objectives

1. Identify sales trends across stores and departments over time
2. Understand the impact of holidays and promotions on weekly sales
3. Examine whether economic indicators (CPI, unemployment, fuel prices) affect retail sales
4. Identify top-performing and underperforming stores and departments
5. Provide actionable, data-driven insights for sales planning and promotional strategy

---

## Intended Audience & Personas

### 👩‍💼 Persona 1 — Retail Operations Manager

| Attribute | Detail |
|-----------|--------|
| **Name** | Sarah Mitchell |
| **Age** | 42 |
| **Role** | Retail Operations Manager |
| **Goals** | Monitor overall store performance; identify underperforming stores/departments; understand how holidays and promotions affect sales |
| **Challenges** | Large datasets are hard to interpret quickly; needs anomaly highlights and fast store comparisons |
| **Context of Use** | Views dashboard during weekly performance review meetings to guide promotional strategy |

### 👨‍💻 Persona 2 — Sales Data Analyst

| Attribute | Detail |
|-----------|--------|
| **Name** | Daniel Watson |
| **Age** | 30 |
| **Role** | Sales Data Analyst |
| **Goals** | Analyze trends and correlations; investigate external factors influencing sales; identify forecasting patterns |
| **Challenges** | Needs interactive, filterable visualizations to explore variable relationships |
| **Context of Use** | Uses dashboard for exploratory analysis and to present insights to leadership teams |

---

## Dataset

- **Source:** [Kaggle — Retail Data Analytics](https://www.kaggle.com/)
- **Scope:** 45 retail stores, historical weekly sales data
- **Original size:** ~420,000 rows across 3 CSV files

### Key Variables

| Variable | Description |
|----------|-------------|
| `Store ID` | Unique store identifier |
| `Department ID` | Unique department identifier |
| `Date` | Week of sales record |
| `Weekly Sales` | Total sales for that store/department/week |
| `Temperature` | Average temperature for the region |
| `Fuel Price` | Regional fuel price |
| `CPI` | Consumer Price Index |
| `Unemployment` | Regional unemployment rate |
| `IsHoliday` | Boolean flag for holiday weeks |
| `MarkDown1–5` | Promotional markdown amounts |

---

## Data Cleaning & Preparation

All cleaning was performed in Python using `pandas` before importing into Tableau Public.

**Steps taken:**

1. **Merged datasets** — Three CSV files (sales, store info, economic indicators) were joined on common keys into a single dataframe
2. **Sampled data** — Reduced from ~420,000 rows to a random 20,000-row sample to optimize Tableau Public performance while preserving overall data distribution
3. **Date formatting** — Converted the `Date` column to `datetime` format for correct time-series handling
4. **Missing values** — Replaced `NaN` values in all MarkDown columns with `0`, representing absence of promotional discounts
5. **Feature engineering** — Extracted `Month` and `Year` columns from the `Date` field to simplify filtering and aggregation in Tableau

The cleaned dataset was exported as a `.csv` file and imported into Tableau Public.

---

## Dashboard Design

### KPI Monitoring

The top row of the dashboard features five KPI cards that provide an instant performance snapshot:

| KPI | Purpose |
|-----|---------|
| **Total Sales** | Overall revenue generated across all stores |
| **Average Weekly Sales** | Typical weekly performance benchmark ($16,047.60) |
| **Total Stores** | Scale indicator (45 stores) |
| **Total Departments** | Scope indicator (79 departments) |
| **Holiday Sales Impact %** | Sales lift during holiday vs. non-holiday weeks (3.52%) |

Each KPI card includes a **sparkline** to show directional trend at a glance. KPI values dynamically update when filters are applied.

---

### Pre-Attentive Attributes & Visual Design

The dashboard applies core pre-attentive attributes to enable rapid interpretation:

#### 🎨 Color
Stores and departments in horizontal bar charts are segmented into four performance tiers:

| Color | Category |
|-------|----------|
| 🟢 Dark Green | Top 3 Performers |
| 🟩 Light Green | Above Average |
| ⬜ Grey | Below Average |
| 🔴 Red | Bottom 3 Performers |

This encoding allows users to identify high and low performers instantly, without reading numeric values.

#### 📐 Size
KPI metric values use larger font sizes to establish visual hierarchy, ensuring critical numbers register at a glance.

#### 📊 Layout (Visual Hierarchy)
The dashboard is structured in three logical tiers:

```
[ TOP ROW ]     KPI Cards — Quick summary metrics
[ MIDDLE ROW ]  Sales Trend Line Chart — Time-series performance
[ BOTTOM ROW ]  Comparison Charts + Scatter Plots — Detailed analysis
```

This layout guides users from high-level overview → trend context → granular investigation.

---

### Interactive Features

| Feature | Description |
|---------|-------------|
| **Year Filter** | Filter all views by calendar year |
| **Store Type Filter** | Analyze by Large / Medium / Small store type |
| **Department Filter** | Drill into specific departments |
| **Performance Segment Filter** | Isolate Top 3 or Bottom 3 performers |
| **Holiday Toggle** | Compare holiday vs. non-holiday periods |
| **Dashboard Highlight Action** | Selecting a store in the bar chart highlights it in the scatter plot for cross-view comparison |

---

## Key Design Choices

### Design Choice 1 — Color Encoding + Interactive Filtering
Horizontal bar charts for Sales by Store and Sales by Department use a four-tier color scheme to make performance differences immediately visible. Combined with interactive segment filters, this enables operations managers to rapidly isolate stores or departments that need attention — directly addressing Sarah Mitchell's need for fast, actionable monitoring.

### Design Choice 2 — Sales Trend Line with Reference Line & Labels
A 36-month time-series line chart plots monthly sales with an average reference line, labeled data points, and values displayed in millions. This allows sales analysts like Daniel Watson to detect seasonal patterns, above/below-average months, and potential forecasting signals at a single glance.

### Design Choice 3 — Scatter Plots with Trend Lines for Economic Factors
Scatter plots visualize the relationship between sales and external variables (store size, CPI). Trend lines reveal direction and strength of correlations, and filters for store type and year allow segment-level exploration. These charts convert complex multivariate data into visual patterns that support both exploratory analysis and executive-level reporting.

---

## Insights & Findings

- **Store size positively correlates with sales** — Larger stores consistently generate higher weekly sales, suggesting scale drives revenue
- **Holiday impact is modest but measurable** — Holiday weeks show approximately a **3.52% lift** in sales compared to non-holiday weeks
- **Large sales disparity across stores** — Some stores significantly outperform others; Store 13 and Store 14 rank among the top performers
- **Department 92 leads in department sales** — With ~$21.7M in total weekly sales, it ranks as the top-performing department
- **Economic indicators show weak correlations** — CPI, fuel price, temperature, and unemployment rate all exhibit correlation coefficients close to zero, suggesting macroeconomic factors have limited direct impact on weekly retail sales in this dataset
- **Sales trend is relatively stable over 2010–2012** — Monthly sales range between ~$7.9M and ~$13.4M, with no dramatic multi-year growth or decline

---

## Limitations

- The dataset was **downsampled from ~420,000 to 20,000 rows** for performance. This may have reduced the statistical power of correlation analyses involving economic indicators.
- The **External Factors dashboard** (fuel price, temperature, unemployment deep-dives) was partially constrained by dashboard space; these relationships warrant further analysis.
- The dataset covers only **2010–2012**, limiting the generalizability of seasonal trend findings to a broader time horizon.

---

## Tableau Public Dashboard

🔗 **[View the Live Dashboard on Tableau Public](https://public.tableau.com/app/profile/vishal.agrawal4785/viz/RetailSalesPerformanceDashboard-Advanced/RetailSalesPerformanceDashboard-Advanced)**

The dashboard is publicly accessible and fully interactive. Use the filters on the right panel to explore performance by year, store type, and department.

---

## Conclusion & Reflection

The final dashboard closely follows the original project proposal, successfully implementing all five core objectives: sales trend analysis, holiday impact measurement, economic factor exploration, store/department performance ranking, and actionable data storytelling.

Key enhancements beyond the initial proposal include:
- Sparklines added to KPI cards for directional context
- A correlation heatmap for multi-variable economic analysis
- Improved layout and visual hierarchy for a cleaner user experience

This project reinforced the importance of designing **with the audience in mind** — a manager and an analyst have different needs, and effective dashboards must serve both. The process also highlighted the value of data cleaning, sampling strategy, and iterative design refinement in producing reliable, performant, and interpretable visualizations.

---

*Built with Tableau Public | Data sourced from Kaggle — Retail Data Analytics dataset*
