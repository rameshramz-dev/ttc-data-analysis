# Welcome to the TTC Data Analysis README!

# Project Background
The Toronto Transit Commission (TTC) operates one of the most heavily used public transit networks in North America, delivering hundreds of millions of passenger trips annually across its subway, streetcar, and bus systems. Maintaining schedule reliability, operational efficiency, and rider satisfaction requires continuous monitoring of service disruptions, mechanical incidents, and peak-hour network bottlenecks.

This project analyzes historical TTC subway operational and delay data (focusing on 2025 data) to identify core service patterns, evaluate transit reliability across routes, and diagnose key drivers of delays. Using Python (`pandas`) for data cleaning and exploratory data analysis (EDA), data wrangling operations were performed to standardise incident logs and evaluate incident frequencies and severity.

**Key Focus Areas & Analytical Scope:**
- **Delay Frequency & Severity:** Total number of delays by line, station, and temporal periods (months, time-of-day).
- **Station Hotspots:** Top stations experiencing the highest delay volume and total delay duration.
- **Temporal Patterns:** Seasonal and month-over-month incident trends and severity distributions.
- **Data Quality & Wrangling:** Handling missing directional/line metadata and non-delay incident logs.

---

# Data Structure & Initial Checks

The raw dataset comprises **40,656 total records** across 11 core attributes, merged with a secondary lookup table containing official TTC delay code descriptions:

- **Primary Dataset Columns:** `Date`, `Time`, `Day`, `Station`, `Code`, `Min Delay`, `Min Gap`, `Bound`, `Line`, `Vehicle`.
- **Lookup Dataset (`Code Descriptions.csv`):** Mapped `Code` to `DESCRIPTION` via a left join to provide readable incident descriptions.
- **Data Cleaning & Engineering:**
  - Standardized date formatting with `pd.to_datetime()` and derived temporal features (`Year`, `Month`, `Month_Name`, `Hour`).
  - Evaluated missing values in `Line` and `Bound` columns.
  - Isolated non-zero delays (`Min Delay != 0`) to separate actual operational disruptions from general reporting logs.

---

# Executive Summary

### Overview of Findings

Analysis of the 2025 TTC Subway delay dataset reveals **25,737 total delay incidents**, with an overall average delay duration of **7.78 minutes per incident** (excluding zero-delay events). 

1. **Volume vs. Duration Disconnect:** High incident volume does not directly correlate with long delay durations. While summer months (August with 2,719 incidents) experience peak incident counts, winter months (February with 2,274 incidents) suffer from significantly higher operational severity, averaging **9.56 minutes per delay**.
2. **Station Bottlenecks:** Major transfer hubs—specifically **Bloor Station (915 incidents)** and **Kennedy Station (866 incidents)**—lead in incident frequency, whereas **Eglinton Station** suffers the highest cumulative delay impact with **2,822 total delay minutes** (average 4.28 minutes/incident).
3. **Outlier Impact:** Severe incident disruptions (>180 minutes delay) distort overall system averages, highlighting vulnerability to catastrophic mechanical or signal failures.

---

# Insights Deep Dive

### Category 1: Station Hotspots & Disruption Impact
* **Incident Volume Leaders:** **Bloor Station** (915 incidents, avg 1.85 min) and **Kennedy Station** (866 incidents, avg 2.14 min) record the highest frequency of delay logs, primarily driven by high passenger volumes and transfer bottlenecks.
* **Duration Severity Leader:** **Eglinton Station** accumulated **2,822 total delay minutes** across 660 incidents, with a substantially higher average delay duration of **4.28 minutes**, indicating slower incident resolution at this location.
* **Key Hub Hotspots:** Finch (791 count), Kipling (783 count), Wilson (620 count), and Warden (544 count) round out the top station disruption points.

### Category 2: Seasonal & Monthly Dynamics
* **Peak Volume Months:** **August** (2,719 delays), **February** (2,274 delays), and **December** (2,242 delays) logged the highest total delay counts in 2025.
* **Peak Severity Month:** **February** recorded the highest mean delay severity (**9.56 minutes**), likely influenced by severe winter weather conditions and cold-weather mechanical strain.
* **Lowest Impact Periods:** September logged both the lowest volume (1,813 delays) and lowest average delay duration (6.83 minutes).

### Category 3: Cause Code Analysis & Zero-Delay Reporting
* **Code Descriptions:** Merging standardized code lookup descriptions highlighted distinct failure categories ranging from speed control and signal anomalies to passenger/medical emergencies.
* **Zero-Delay Logging:** A subset of records log `Min Delay = 0`. Evaluating zero-delay instances by `Line` and `Code` reveals operational reporting entries that record minor incidents without impacting schedule timelines.

### Category 4: Vehicle & Outlier Performance
* **Vehicle Reliability:** Aggregating delays by `Vehicle` (filtering for vehicles with >60 incidents) isolates repeating vehicle-level mechanical issues.
* **Extreme Outliers:** Incidents exceeding **180 minutes (3 hours)** contribute disproportionately to total line downtime and require dedicated emergency response protocols.

---

# Recommendations

* **Targeted Station Maintenance at Eglinton:** Investigate root causes for Eglinton Station’s elevated average delay duration (4.28 mins vs ~1.8 mins at Bloor) to streamline incident resolution times.
* **Winter Weather Preparedness:** Implement pre-winter mechanical checks ahead of February to mitigate the spike in delay severity (9.56 min avg).
* **High-Volume Hub Crowd Control:** Deploy specialized platform management at Bloor and Kennedy stations during peak hours to reduce passenger-induced delay triggers.
* **Outlier Incident Protocols:** Develop rapid response mechanisms specifically for high-impact (>180 min) signal and equipment failures.

---

# Assumptions and Caveats

* **Zero-Delay Exclusions:** Operational average delay calculations excluded `Min Delay == 0` rows to measure active disruption severity accurately.
* **Missing Line Metadata:** Missing `Line` or `Bound` records were preserved for volume analysis but excluded from line-specific aggregations.
* **Data Timeframe:** Analysis focuses on 2025 data slice extracted from the TTC Subway Delay dataset.

---
**Data Source:** [TTC Subway Delay Data - Open Data Toronto](https://open.toronto.ca/dataset/ttc-subway-delay-data/)
