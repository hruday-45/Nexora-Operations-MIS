# 🧹 Nexora Operations – Data Quality and Cleaning Log

## 1. 📋 Overview

This document records the data quality issues identified in the original Nexora Operations dataset and the corrective actions performed during data preparation.

The objective was to improve data consistency, accuracy, and reliability before performing operational analysis.

- **Source Dataset:** `Nexora_Operations_Raw_Data_10000.csv`
- **Original Records:** 10,000
- **Final Cleaned Records:** 9,995

---

## 2. 🔍 Data Quality Assessment

The following issues were identified during the initial validation process:

| Data Quality Issue | Records Identified |
| :--- | :---: |
| Duplicate `Record_ID`s | 5 |
| Missing `Employee_ID` | 3 |
| Missing `Employee_Name` | 4 |
| Negative `Daily_Target` | 1 |
| `Quality_Passed` greater than `Quality_Checked` | 1 |
| `SLA_Met` greater than `SLA_Eligible` | 1 |
| Unmatched nonblank `Employee_ID`s | 0 |

---

## 3. 🛠️ Data Cleaning Actions

### 3.1 🗑️ Duplicate Record Removal
- **Issue:** Five duplicate operational records were identified.
- **Action:** Used Excel's **Remove Duplicates** functionality across all 15 original columns.
- **Result:** Removed five duplicate rows.
- **Final Record Count:** `9,995`

---

### 3.2 🆔 Missing Employee ID Recovery
- **Issue:** Three records contained missing `Employee_ID` values.
- **Action:** Matched employee names against the `Employee_Master` table and recovered the corresponding employee IDs.
- **Validation:** No unmatched nonblank `Employee_ID` values remained.

---

### 3.3 👤 Missing Employee Name Recovery
- **Issue:** Four records contained missing `Employee_Name` values.
- **Action:** Used `XLOOKUP` against the `Employee_Master` table to retrieve the corresponding employee names.

---

### 3.4 🔤 Text Standardization
- **Issue:** Inconsistent text formatting was identified in the `Team` field, including lowercase text and unnecessary spaces.
- **Action:** Used `TRIM` and `PROPER` functions to standardize the affected values.
- **Result:** Team names were standardized for consistent reporting.

---

### 3.5 🔢 Numerical Data Corrections
The following numerical anomalies were identified and corrected in `Cleaned_Data`:

| Record_ID | Field | Original Value | Corrected Value |
| :--- | :--- | :---: | :---: |
| `OPSO5801` | `Daily_Target` | -50 | 0 |
| `OPSO6801` | `Quality_Passed` | 101 | 98 |
| `OPSO7801` | `SLA_Met` | 96 | 94 |

**Correction Logic:**
- Negative `Daily_Target` was changed to zero.
- `Quality_Passed` was capped at `Quality_Checked`.
- `SLA_Met` was capped at `SLA_Eligible`.

> ⚠️ **Important:** These were conservative validation corrections. The original source values were not independently verified against an authoritative operational system. The original `Raw_Data` worksheet was preserved without modification.

---

## 4. ✅ Final Data Validation

After cleaning, the following validation checks were performed:

| Validation Check | Final Result |
| :--- | :---: |
| Duplicate `Record_ID`s | 0 |
| Missing `Employee_ID` | 0 |
| Missing `Employee_Name` | 0 |
| Negative `Daily_Target` | 0 |
| `Quality_Passed` greater than `Quality_Checked` | 0 |
| `SLA_Met` greater than `SLA_Eligible` | 0 |

*All six final validation checks returned zero exceptions.*

---

## 5. 🔄 Data Preparation Workflow

1. Imported the original CSV datasets into Excel.
2. Converted the datasets into structured Excel Tables.
3. Performed initial data quality assessment.
4. Identified duplicate and missing records.
5. Recovered missing employee information using `Employee_Master`.
6. Standardized inconsistent text values.
7. Corrected numerical validation exceptions.
8. Removed duplicate records.
9. Converted the cleaned dataset into an Excel Table.
10. Performed final validation checks.

---

## 6. 🔒 Data Integrity and Traceability

The project maintains separate worksheets for:
- `Raw_Data`: Original imported dataset.
- `Cleaned_Data`: Corrected and validated dataset.

This separation preserves the original source data and allows the cleaning process to be reviewed. The three numerical corrections are documented explicitly rather than being presented as verified original values.

---

## 7. 🏁 Conclusion

The data preparation process transformed the original 10,000-record dataset into a cleaned dataset containing 9,995 unique operational records.

The final dataset was used for KPI calculations, PivotTable analysis, and the interactive MIS dashboard.