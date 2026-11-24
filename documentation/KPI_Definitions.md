# 📈 Nexora Operations – KPI Definitions

## 1. 📋 Overview

This document defines the seven Key Performance Indicators (KPIs) used in the **Nexora Operations MIS Reporting Dashboard**.

These KPIs measure operational output, target achievement, productivity, quality, SLA compliance, and employee attendance. All KPI calculations are based on the cleaned operational dataset.

---

## 2. 📊 KPI Summary

| KPI | Calculation | Format |
| :--- | :--- | :--- |
| **Total Units Processed** | `Sum of Units_Processed` | Whole Number |
| **Target Achievement %** | `Total Units Processed / Total Daily Target` | Percentage |
| **Productivity %** | `Total Units Processed / Target for Present Records` | Percentage |
| **Quality Pass %** | `Total Quality_Passed / Total Quality_Checked` | Percentage |
| **Error Rate %** | `1 - Quality Pass %` | Percentage |
| **SLA Compliance %** | `Total SLA_Met / Total SLA_Eligible` | Percentage |
| **Attendance %** | `Present Records / Total Cleaned Records` | Percentage |

---

## 3. 🔍 Detailed KPI Definitions

### 3.1 📦 Total Units Processed

- **Formula:**
  ```excel
  SUM(Units_Processed)
  ```
- **Business Purpose:** Measures the total operational output generated during the reporting period.
- **Interpretation:** A higher value indicates greater overall processing volume. It should be interpreted alongside quality and SLA performance.

---

### 3.2 🎯 Target Achievement %

- **Formula:**
  ```excel
  (Total Units Processed / Total Daily Target) × 100
  ```
- **Business Purpose:** Measures actual operational output against the total assigned targets.
- **Interpretation:**
  - `100%` = Target achieved.
  - `Above 100%` = Target exceeded.
  - `Below 100%` = Target not fully achieved.

---

### 3.3 ⚡ Productivity %

- **Formula:**
  ```excel
  (Total Units Processed / Target for Present Records) × 100
  ```
- **Business Purpose:** Measures operational output against the expected target for records where employees were marked present.
- **Interpretation:** This KPI evaluates output relative to the target associated with employee attendance.
  > **Important:** This project calculates productivity using the target associated with **Present** records, whereas **Target Achievement** uses the total target across all cleaned records.

---

### 3.4 ✅ Quality Pass %

- **Formula:**
  ```excel
  (Total Quality_Passed / Total Quality_Checked) × 100
  ```
- **Business Purpose:** Measures the proportion of quality-checked units that successfully passed quality checks.
- **Interpretation:** A higher percentage indicates stronger quality performance.

---

### 3.5 ❌ Error Rate %

- **Formula:**
  ```excel
  (1 - Quality Pass Rate) × 100
  ```
- **Business Purpose:** Measures the proportion of quality-checked units that did not pass quality checks.
- **Interpretation:** A lower error rate indicates better operational quality.

---

### 3.6 ⏱️ SLA Compliance %

- **Formula:**
  ```excel
  (Total SLA_Met / Total SLA_Eligible) × 100
  ```
- **Business Purpose:** Measures the percentage of SLA-eligible cases or units completed within the required service-level agreement.
- **Interpretation:** A higher percentage indicates stronger compliance with service-level expectations.

---

### 3.7 📅 Attendance %

- **Formula:**
  ```excel
  (Present Records / Total Cleaned Operational Records) × 100
  ```
- **Business Purpose:** Measures the proportion of cleaned employee-day records marked as Present.
- **Interpretation:** A higher percentage indicates stronger attendance across the recorded scheduled working days.
- **Denominator:** `9,995` cleaned employee-day records after duplicate removal.

---

## 4. 🧮 Aggregation Methodology

For accurate management reporting, percentage KPIs must be calculated using aggregated numerators and denominators.

For example:
```excel
Quality Pass % = SUM(Quality_Passed) / SUM(Quality_Checked)
```

> ⚠️ **Do not** use a simple average of individual employee-day percentages to represent the overall weighted quality pass rate. The same weighted calculation principle applies to **Target Achievement** and **SLA Compliance**.

---

## 5. 🎛️ Dashboard Filtering

The dashboard supports interactive filtering through three slicers:
- **Department**
- **Shift**
- **Location**

The KPI values and charts update dynamically according to the selected filter combinations.

---

## 6. 📝 Reporting Notes

- KPI results are based on cleaned operational records.
- Zero denominators are handled using `IFERROR` in the Excel calculations.
- Percentage results are displayed to two decimal places (`0.00%`).
- KPI comparisons should be interpreted together rather than in isolation.