# 📖 Nexora Operations – Data Dictionary

## 1. 📊 Dataset Information

| Attribute | Description |
| :--- | :--- |
| **Dataset Name** | Nexora Operations Cleaned Dataset |
| **Reporting Period** | January–December 2025 |
| **Total Records** | 9,995 |
| **Number of Columns** | 18 |
| **Record Granularity** | One employee's operational performance per scheduled working day |
| **Source** | Nexora Operations Raw Dataset |

---

## 2. 🗂️ Column Definitions

### A. 👤 Employee and Operational Information

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `Record_ID` | Text | Unique identifier assigned to each operational record |
| `Date` | Date | Date on which the employee's operational activity was recorded |
| `Employee_ID` | Text | Unique employee identification number |
| `Employee_Name` | Text | Name of the employee |
| `Department` | Text | Department to which the employee belongs |
| `Team` | Text | Operational team within the department |
| `Shift` | Text | Employee's assigned working shift |
| `Location` | Text | Operational work location |

### B. ⚡ Attendance and Productivity Information

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `Attendance_Status` | Text | Employee's attendance status for the scheduled working day |
| `Daily_Target` | Number | Number of units expected from the employee for that day |
| `Units_Processed` | Number | Actual number of operational units processed by the employee |

### C. ✅ Quality and SLA Information

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `Quality_Checked` | Number | Total number of processed units checked for quality |
| `Quality_Passed` | Number | Number of quality-checked units that passed |
| `SLA_Eligible` | Number | Number of cases or units eligible for SLA measurement |
| `SLA_Met` | Number | Number of SLA-eligible cases or units that met the SLA requirement |

### D. 🧮 Calculated Performance Columns

| Column Name | Data Type | Calculation | Description |
| :--- | :--- | :--- | :--- |
| `Target_Achievement_%` | Percentage | `Units_Processed / Daily_Target` | Daily achievement against the assigned target |
| `Quality_Pass_%` | Percentage | `Quality_Passed / Quality_Checked` | Daily quality pass rate |
| `SLA_Compliance_%` | Percentage | `SLA_Met / SLA_Eligible` | Daily SLA compliance rate |

> *Note: The three calculated percentage fields use `IFERROR` to return zero when the denominator is zero.*

---

## 3. 🔗 Dataset Relationships

### 🧑‍💼 Employee Master
The `Employee_Master` table contains employee reference information and is used to validate and recover employee details in the operational dataset.

- **Relationship:** `Employee_Master[Employee_ID]` → `Cleaned_Data[Employee_ID]`

---

## 4. 🔍 Data Granularity

Each row represents one employee's operational performance for one scheduled working day. The dataset is therefore structured at an **employee-day level**.

---

## 5. ⚠️ Important Notes

- `Record_ID` is used to identify duplicate operational records.
- `Employee_ID` is used to connect operational records with the Employee Master.
- `Daily_Target`, `Units_Processed`, `Quality_Checked`, `Quality_Passed`, `SLA_Eligible`, and `SLA_Met` are numerical measures.
- Percentage columns represent individual employee-day rates and **should not simply be averaged** when calculating overall weighted performance.
- For overall performance reporting, calculate percentages using the appropriate aggregated numerator and denominator.