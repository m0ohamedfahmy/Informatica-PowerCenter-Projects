
# 🚗 ETL Project using Informatica PowerCenter

## 📌 Project Description

This is an end-to-end ETL project developed using **Informatica PowerCenter**. The goal of the project is to clean and transform raw car registration data and prepare it for analysis and reporting. The project simulates a real-world client scenario by handling data quality issues, transforming fields, handling missing and illogical values, and detecting outliers.

---


## 🔁 ETL Flow

1. **Extract** raw data from source (flat file or database).
2. **Transform** data using various transformations including:
   - Data type conversion
   - Handling null and illogical values
   - Date conversion and age calculation
   - Outlier detection
3. **Load** the cleaned data into the target table.

---

## 🔧 Data Transformations

### 🧮 Conversion & Cleanup

1. ✅ `yearOfRegistration` converted to decimal using:
   ```sql
   TO_DECIMAL(yearOfRegistration)
   ```

2. ✅ Date formatting for `dateCreated`:
   ```sql
   IIF(ISNULL(dateCreated), NULL, TO_DATE(dateCreated, 'YYYY/MM/DD HH24:MI:SS'))
   ```

3. ✅ Calculate age of the car:
   ```sql
   IIF(ISNULL(yearOfRegistration), NULL, GET_DATE_PART(SYSDATE, 'YYY') - yearOfRegistration)
   ```

4. ✅ Extracted **Day**, **Month**, and **Year** from relevant date columns.

---

### ⚠️ Data Quality Rules

5. ✅ **yearOfRegistration**: Remove illogical values. Assumed valid range is between **1910** and **2022**.

6. ✅ **monthOfRegistration**:
   - Handled value `0` (non-logical).
   - Replaced with **mode** value of the column using a **Mapplet**.

7. ✅ **powerPS**:
   - Treated values (0, 1, 2) as illogical.
   - Replaced them with **mean** value of `powerPS`.

---

### 📉 Outlier Detection

8. ✅ Used **Z-Score method** to detect outliers:
   - Calculated upper and lower limits.
   - Applied filter to remove outliers.
   - Logic encapsulated inside a **Mapplet**.

---

## 🔄 Transformations Used

- **Expression**
- **Filter**
- **Aggregator**
- **Joiner**
- **Mapplet**
  - For outlier calculation
  - For mode calculation

---

## 🖼️ Screenshots

| Component         | Screenshot |
|------------------|------------|
| Mapping Overview | ![Mapping](images/mapping.png) |
| Workflow         | ![Workflow](images/workflow.png) |
| Outlier Mapplet  | ![Outlier Mapplet](images/outlier_mapplet.png) |
| Mode Mapplet     | ![Mode Mapplet](images/mode_mapplet.png) |

> **Note**: Make sure to replace the paths above with the actual GitHub path after uploading your images in the `images/` folder.

---

## 📚 Additional Notes

- Project developed as part of an ETL simulation to mirror real-world data engineering scenarios.
- All transformations and logic follow best practices in data cleaning and preparation.
