# 📊 Data Anomalies – Third Normal Form (3NF) [Exercise]

This repository contains SQL scripts and explanatory notes for normalising a database to the **Third Normal Form (3NF)**. The database used in this exercise is `SoftDevEmployees.db`, which models a simplified structure of a software development employee system. The primary focus is on identifying and resolving **transitive dependencies** to improve **data integrity**, **reduce redundancy**, and **minimize anomalies**.

---

## 🎯 Learning Objectives

By completing this exercise, you will:

- Understand the requirements for a database to meet **Third Normal Form (3NF)**.
- Identify and eliminate **transitive dependencies** by decomposing tables.
- Apply SQL statements to restructure and populate normalized tables.
- Understand how database normalisation reduces data anomalies such as update, insert, and delete anomalies.

---

## 📁 Structure
```
├── README.md
├── SoftDevEmployees.db # SQLite database file (version 3NF modified)
├── create_tables.sql # SQL script to create 3NF tables
├── insert_data.sql # SQL script to populate tables after normalisation
├── queries.sql # SQL statements to query and validate normalisation
└── screenshots/ # Optional: visual snapshots of ERD or query results
```

---

## 🔄 Normalisation Workflow

### ✅ Step 1: Start from a 2NF database  
Ensure the database is already normalized to **Second Normal Form (2NF)** before continuing.

### ✅ Step 2: Identify Transitive Dependencies  
Separate fields such as `OccupationBand` and `Salary` which are not directly dependent on the **primary key** of the employee but are dependent on another non-key attribute.

### ✅ Step 3: Create New Tables  
- `OccupationBands_3NF` — Stores unique occupation bands.
- `Salaries_3NF` — Links salaries to occupation bands via foreign keys.

### ✅ Step 4: Insert and Relink Data  
Use `JOIN`s to connect decomposed tables and preserve referential integrity.

---

## ⚙️ Technologies Used

- **SQLite3** (local database)
- **DB Browser for SQLite** / **Jupyter Notebook (ipython-sql magic)** for interactive querying
- **SQL (DDL & DML)** — for table creation, inserts, joins, and updates

---

## 📌 Prerequisites

- Python with `ipython-sql` OR
- SQLite database GUI (e.g., [DB Browser for SQLite](https://sqlitebrowser.org/))
- Clone/download the repo and load `SoftDevEmployees.db` into your local SQLite environment

---

## 🧪 Example SQL: Decomposition of Transitive Dependency

```sql
-- Create OccupationBands Table
CREATE TABLE OccupationBands_3NF (
    BandID INTEGER PRIMARY KEY AUTOINCREMENT,
    OccupationBand TEXT NOT NULL
);

-- Create Salaries Table
CREATE TABLE Salaries_3NF (
    SalaryID INTEGER PRIMARY KEY AUTOINCREMENT,
    Salary REAL NOT NULL,
    BandID INTEGER,
    FOREIGN KEY (BandID) REFERENCES OccupationBands_3NF (BandID)
);

-- Insert Occupation Bands
INSERT INTO OccupationBands_3NF (OccupationBand)
SELECT DISTINCT OccupationBand FROM Employees_2NF;

-- Insert Salaries with BandID
INSERT INTO Salaries_3NF (Salary, BandID)
SELECT e.Salary, ob.BandID
FROM Employees_2NF e
JOIN OccupationBands_3NF ob ON e.OccupationBand = ob.OccupationBand;
```
## 📌 What is 3NF?
A table is in **Third Normal Form (3NF)** if:

It is in **Second Normal Form (2NF)**.

It does not contain transitive dependencies — non-key attributes should not depend on other non-key attributes.

## 📬 Contact
**Author**: Ibrahim Ambale
📍 Nairobi, Kenya
🔗 LinkedIn: [Ibrahim Ambale](https://www.linkedin.com/in/ibrahim-ambale/)
🌐 Website: [Ibrahim Ambale](https://tikeyambale.wixsite.com/ibrahim-ambale)



