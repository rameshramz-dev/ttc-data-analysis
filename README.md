# Welcome to the TTC Data Analysis README!

# Project Background
The Toronto Transit Commission (TTC) operates one of the most heavily used public transit networks in North America, delivering hundreds of millions of passenger trips annually across its subway, streetcar, and bus systems. Maintaining schedule reliability, operational efficiency, and rider satisfaction requires continuous monitoring of service disruptions, mechanical incidents, and peak-hour network bottlenecks.

This project analyzes historical TTC subway operational and delay data spanning **January 2022 to June 2026 (4.5 years)** to identify core service patterns, evaluate transit reliability across routes, and diagnose long-term drivers of service disruptions. Using Python (`pandas`) for data cleaning and exploratory data analysis (EDA), data wrangling operations were performed to standardize multi-year incident logs and evaluate seasonal, station-level, and year-over-year delay trends.

**Key Focus Areas & Analytical Scope:**
- **Multi-Year Delay Trends & Volume Growth:** Year-over-year (YoY) incident counts and cumulative operational delay hours from 2022 to mid-2026.
- **Station Bottlenecks & Hotspots:** Multi-year ranking of top stations by incident frequency and total delay minutes.
- **Seasonal & Environmental Patterns:** Seasonal distribution (Winter, Spring, Summer, Fall) and monthly severity variations across multiple years.
- **Root Cause & Vehicle Reliability:** Code category breakdown (track intrusions, disorderly patrons, signal failures) and vehicle-level incident analysis.

---

# Data Structure & Initial Checks

The cleaned dataset (`TTC_Subway_Delay_Cleaned_2022_June2026.csv`) comprises **106,930 total records** across 22 engineered attributes:

- **Core Attributes:** `Date`, `Time`, `Day`, `Station`, `Code`, `Code_Description`, `Code_Category`, `Min Delay`, `Min Gap`, `Bound`, `Line`, `Vehicle`, `Year`, `Month`, `Month_Name`, `Season`, `Hour`, `Peak_Hour`, `DayName`, `Weekend`.
- **Data Cleaning & Wrangling:**
  - Standardized date & time parsing with engineered temporal features (`Year`, `Month`, `Season`, `Hour`, `Peak_Hour`).
  - Isolated **39,898 non-zero delay incidents** (`Min Delay != 0`) to separate active operational disruptions from non-impact reporting logs.
  - Category mapping for TTC delay codes into high-level cause categories (`Code_Category`).

---

# Executive Summary

### Overview of Findings

Across the **4.5-year evaluation period (2022 – June 2026)**, the TTC subway system experienced **39,898 active delay incidents**, resulting in **5,253.1 cumulative delay hours** (~218 days of downtime) with an overall mean delay severity of **7.90 minutes per incident**.

1. **Upward Volume Trajectory:** Annual delay incident volumes increased steadily from **18,576 in 2022** to a peak of **26,167 in 2024** (+40.9% overall growth). First-half 2026 data (14,745 incidents) indicates a continuing upward trajectory, pacing toward ~29,500 annualized incidents.
2. **Volume vs. Duration Hub Disconnect:** Major terminal and transfer stations lead in incident frequency (**Bloor Station** with 4,246 incidents and **Finch Station** with 4,210 incidents). However, **Eglinton Station** represents the single highest cumulative downtime burden, accumulating **10,432 total delay minutes** (average 3.49 mins/incident).
3. **Seasonal Severity Dynamics:** Winter months consistently exhibit elevated delay severity due to cold-weather track and vehicle strain, whereas summer months see high volume driven by passenger movement and outdoor track maintenance.

---

# Insights Deep Dive

### Category 1: Multi-Year Station Hotspots & Duration Impact
* **Incident Frequency Leaders:** **Bloor Station** (4,246 count, avg 1.93 min) and **Finch Station** (4,210 count, avg 2.20 min) recorded the highest overall disruption frequencies across the 4.5-year dataset.
* **Total Downtime Leader:** **Eglinton Station** accumulated **10,432 total delay minutes** across 2,986 incidents—exceeding Bloor Station's total delay time by over 2,200 minutes despite logging 1,260 fewer incidents.
* **Key Network Bottlenecks:** **Kennedy Station** (3,659 count, 8,807 mins) and **Kipling Station** (3,434 count, 8,849 mins) round out the top multi-year terminal hubs requiring operational focus.

### Category 2: Year-over-Year & Seasonal Dynamics
* **Annual Incident Volume Breakdown:**
  * **2022:** 18,576 records
  * **2023:** 22,012 records *(+18.5% YoY)*
  * **2024:** 26,167 records *(Peak volume year, +18.9% YoY)*
  * **2025:** 25,430 records
  * **2026 (Jan–June):** 14,745 records
* **Seasonal Volume Distribution:** Winter and Fall quarters consistently experience higher incident counts (e.g., 2022 Winter logged 4,844 delays vs. Summer's 4,417), while Summer months often experience higher average delay durations (e.g., August 2022 averaged 8.56 mins/delay).

### Category 3: Incident Root Causes & Code Breakdown
* **Top Cause Categories:** Grouping by `Code_Category` reveals that signal anomalies, track intrusions (`SUUT`), and disorderly patron incidents (`SUDP`) account for recurring delays at key interchange stations.
* **Zero-Delay Record Analysis:** Analyzing records with `Min Delay = 0` (over 67,000 logs) isolates administrative/reporting check-ins from genuine schedule disruptions.

### Category 4: Vehicle Reliability & Outlier Analysis
* **Vehicle Fleet Tracking:** Filtering for high-frequency vehicles (`size > 60`) identified specific vehicle units repeatedly associated with mechanical delay codes.
* **Extreme Delay Outliers:** Incidents exceeding **180 minutes (3 hours)** contribute disproportionately to annual line downtime, requiring targeted incident response protocols.

---

# Recommendations

* **Eglinton Incident Response Optimization:** Address systemic bottlenecks at Eglinton Station to reduce its 3.49-minute average delay time down toward system averages (1.9–2.2 mins).
* **Preventative Winter Maintenance:** Pre-deploy maintenance teams ahead of Q1 (January/February) to mitigate winter severity spikes.
* **Capacity Management at Terminal Hubs:** Implement improved passenger flow control at Bloor, Finch, and Kennedy stations to minimize boarding-related delay triggers.
* **Targeted Fleet Overhauls:** Use vehicle-level delay aggregations to schedule preventative maintenance for outlier vehicles causing recurring line disruptions.

---

# Assumptions and Caveats

* **Zero-Delay Exclusions:** Operational average delay duration calculations exclude `Min Delay == 0` records to reflect active disruption severity accurately.
* **Partial Year Data:** 2026 data covers January through June 2026 (6 months).
* **Missing Line/Bound Information:** A minority of incident logs lacked valid line or directional metadata and were excluded from line-specific breakdowns.

---
**Data Source:** [TTC Subway Delay Data - Open Data Toronto](https://open.toronto.ca/dataset/ttc-subway-delay-data/)
