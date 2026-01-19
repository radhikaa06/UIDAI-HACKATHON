# UIDAI Aadhaar Demographic Anomaly Detection

## Overview
UIDAI manages Aadhaar enrolment at a national scale, making manual identification of regional irregularities impractical.  
This project implements an **explainable, data-driven anomaly detection system** to identify districts and states with abnormal Aadhaar enrolment patterns, enabling **targeted audits and improved governance**.

---

## Problem Statement
To detect unusual demographic distributions and abnormal enrolment volumes in Aadhaar data that may indicate:
- Data quality issues  
- Operational inefficiencies  
- Potential misuse or irregular practices  

The solution is designed to be **transparent, interpretable, and policy-ready**.

---

## Dataset
**Source:** UIDAI Aadhaar Enrolment & Update Demographic Datasets (CSV)

### Key Columns Used
- `state`
- `district`
- `pincode`
- `demo_age_5_17`
- `demo_age_17_`

> Time-based (date) columns were excluded as the focus is on **regional and demographic analysis**, not time-series trends.

---

## Methodology

### 1. Data Preparation
- Merged multiple CSV files into a single dataset  
- Removed irrelevant columns  
- Handled missing values  
- Filtered zero-enrolment districts  

---

### 2. District-Level Analysis
- Aggregated data so each row represents **one district**
- Computed:
  - Total Aadhaar enrolment  
  - Age 17+ enrolment ratio  

---

### 3. Anomaly Detection
- **Demographic anomalies:**  
  Z-score applied on age 17+ ratio (`|z| > 2`)
- **Volume anomalies:**  
  Z-score applied on total enrolment (`|z| > 3`)
- **Final flag:**  
  A district is flagged if **either condition is met**

---

### 4. Severity Ranking
A severity score was calculated to prioritize districts:

5. State‑Level Aggregation
Aggregated district anomalies per state

Identified states with higher proportions of anomalous districts

6. Pincode‑Level Drill‑Down
For the most anomalous district, analysis was performed at pincode level

Localized the exact pincodes driving the anomaly

Key Results
~1000 districts analyzed

29 districts flagged with significant demographic anomalies

Extreme outliers observed (z‑score > 10)

State‑level patterns revealed systemic regional risks

Pincode drill‑down enabled actionable, on‑ground insights

Visual Analysis
Demographic ratio distributions

Demographic vs enrolment anomaly scatter plots

Top anomalous districts and states

Pincode‑level anomaly charts (case study)

Tech Stack
Python

Pandas, NumPy

SciPy

Matplotlib, Seaborn

Jupyter Notebook

Relevance to UIDAI
This solution helps UIDAI:

Prioritize audits efficiently

Detect demographic irregularities early

Focus investigations at district and pincode level

Improve data quality and governance
