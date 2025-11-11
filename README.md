# Healthcare Patient Database Project

A SQL project demonstrating database creation, data insertion, data cleaning, and extracting insights from a patient healthcare dataset. The project showcases how to manage and query structured data, calculate derived metrics, and visualize key statistics.

---

## Project Overview

This project uses a synthetic healthcare dataset to simulate real-world patient admissions. The database includes patient demographics, medical conditions, admission and discharge dates, doctors, admission types, and test results. The goal is to practice:

- Creating SQL tables
- Inserting large datasets
- Cleaning and formatting data
- Calculating derived metrics
- Querying and extracting insights

The project demonstrates handling real-world challenges in database management, such as cleaning messy `INSERT` statements, calculating derived metrics, and working with large datasets.

---

## Workflow Steps

1. **Create the database**
    - File: `healthcare.db`
    - SQLite was used as the database engine.
    - The `CREATE TABLE patients` statement defines all columns including patient demographics, admission details, and test results.

2. **Prepare and insert data**
    - The dataset was provided as a CSV file.
    - `INSERT INTO` statements were generated from the CSV using tools like **DBeaver** and CSV-to-SQL converters.
    - Large-scale cleaning was performed:
        - Removed duplicate `INSERT INTO` headers repeated every 10 rows
        - Ensured proper comma and semicolon syntax
        - Consolidated all inserts into a single statement where possible
    - Final SQL file included `CREATE TABLE` + cleaned `INSERT` statements.

3. **Load data in DBeaver**
    - DBeaver was used to run the SQL script and verify the `patients` table.
    - The database connection allowed querying, refreshing data, and checking record counts.
    - 218 patient records were successfully inserted.

4. **Calculate derived metrics**
    - Added a new column for patient stay duration:

    ```sql
    ALTER TABLE patients
    ADD COLUMN stay_duration_days INTEGER;

    UPDATE patients
    SET stay_duration_days = julianday(discharge_date) - julianday(date_of_admission);
    ```

`julianday()` converts dates to Julian days, allowing calculation of duration between admission and discharge.

### Example Queries

**Select all patients with their stay duration:**

```sql
SELECT name, date_of_admission, discharge_date, stay_duration_days
FROM patients;
```
Average stay by admission type:
```sql
SELECT admission_type, AVG(stay_duration_days) AS avg_stay
FROM patients
GROUP BY admission_type;
```

Count patients by medical condition:
```sql
SELECT medical_condition, COUNT(*) AS num_patients
FROM patients
GROUP BY medical_condition;
```
### Key Learnings
Learned to manage large datasets in SQL.

- Practiced creating tables, inserting data, and ensuring data integrity.
- Generated and cleaned INSERT INTO statements from CSV files.
- Calculated derived metrics using date functions (julianday) in SQLite.
- Used DBeaver to explore, query, and validate the database.
- Demonstrated handling large datasets, cleaning messy SQL, and preparing reproducible workflows.
- Documented process for clarity and version control on GitHub.

### Tools Used
SQLite – Database engine

DBeaver – Database visualization, insert generation, and query execution

VS Code – Editing SQL files and preparing cleaned inserts

GitHub – Version control and repository hosting

### Dataset
Synthetic healthcare data generated for practice purposes.

Contains patient name, age, gender, medical condition, admission/discharge dates, doctor, admission type, and test results.

All data is anonymised and safe for public use.
