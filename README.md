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
