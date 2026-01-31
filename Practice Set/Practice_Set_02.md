# 📝 Practice Set 02 - HOMEWORK Q1

> **Database:** UmarIqbalDB
> **Table:** Student

---

## 📋 Objective

1. Create a database named `UmarIqbalDB`
2. Create a table called `Student` with appropriate columns, data types, and constraints
3. Insert 5 records into the table
4. Learn how to declare DEFAULT values for attributes
5. Learn how to declare FOREIGN KEY in CREATE TABLE command

---

## 📊 Table Structure: Student

| Column Name | Data Type      | Constraints       | Description                  |
|-------------|----------------|-------------------|------------------------------|
| student_id  | INT            | PRIMARY KEY       | Unique ID for each student   |
| first_name  | VARCHAR(50)    | NOT NULL          | Student's first name         |
| last_name   | VARCHAR(50)    | NOT NULL          | Student's last name          |
| email       | VARCHAR(100)   | UNIQUE, NOT NULL  | Student's email address      |
| dob         | DATE           | NOT NULL          | Date of birth                |
| course      | VARCHAR(50)    | NOT NULL          | Course enrolled              |
| fees        | DECIMAL(8,2)   | CHECK (fees > 0)  | Course fees                  |

---

## 🔧 SQL Queries & Solutions

### Step 1: Create Database

```sql
CREATE DATABASE UmarIqbalDB;
```

**Output:**
```
Query OK, 1 row affected (0.001 sec)
```

### Step 2: Use Database

```sql
USE UmarIqbalDB;
```

**Output:**
```
Database changed
```

---

### Step 3: Create Student Table

```sql
CREATE TABLE Student (
    student_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    dob DATE NOT NULL,
    course VARCHAR(50) NOT NULL,
    fees DECIMAL(8,2) CHECK (fees > 0)
);
```

**Output:**
```
Query OK, 0 rows affected (0.025 sec)
```

---

### Step 4: Verify Table Structure

```sql
DESCRIBE Student;
```

**Expected Output:**
```
+------------+---------------+------+-----+---------+-------+
| Field      | Type          | Null | Key | Default | Extra |
+------------+---------------+------+-----+---------+-------+
| student_id | int(11)       | NO   | PRI | NULL    |       |
| first_name | varchar(50)   | NO   |     | NULL    |       |
| last_name  | varchar(50)   | NO   |     | NULL    |       |
| email      | varchar(100)  | NO   | UNI | NULL    |       |
| dob        | date          | NO   |     | NULL    |       |
| course     | varchar(50)   | NO   |     | NULL    |       |
| fees       | decimal(8,2)  | YES  |     | NULL    |       |
+------------+---------------+------+-----+---------+-------+
7 rows in set (0.015 sec)
```

---

### Step 5: Insert 5 Records

```sql
INSERT INTO Student (student_id, first_name, last_name, email, dob, course, fees)
VALUES
    (1, 'Umar', 'Iqbal', 'umar.iqbal@iilm.edu', '2005-03-15', 'B.Tech CSE', 150000.00),
    (2, 'Rahul', 'Sharma', 'rahul.sharma@iilm.edu', '2004-07-22', 'B.Tech CSE', 150000.00),
    (3, 'Priya', 'Singh', 'priya.singh@iilm.edu', '2005-01-10', 'BBA', 120000.00),
    (4, 'Amit', 'Kumar', 'amit.kumar@iilm.edu', '2004-11-05', 'B.Tech ECE', 140000.00),
    (5, 'Sneha', 'Verma', 'sneha.verma@iilm.edu', '2005-06-18', 'B.Com', 100000.00);
```

**Output:**
```
Query OK, 5 rows affected (0.012 sec)
Records: 5  Duplicates: 0  Warnings: 0
```

---

### Step 6: View All Records

```sql
SELECT * FROM Student;
```

**Expected Output:**
```
+------------+------------+-----------+------------------------+------------+------------+-----------+
| student_id | first_name | last_name | email                  | dob        | course     | fees      |
+------------+------------+-----------+------------------------+------------+------------+-----------+
|          1 | Umar       | Iqbal     | umar.iqbal@iilm.edu    | 2005-03-15 | B.Tech CSE | 150000.00 |
|          2 | Rahul      | Sharma    | rahul.sharma@iilm.edu  | 2004-07-22 | B.Tech CSE | 150000.00 |
|          3 | Priya      | Singh     | priya.singh@iilm.edu   | 2005-01-10 | BBA        | 120000.00 |
|          4 | Amit       | Kumar     | amit.kumar@iilm.edu    | 2004-11-05 | B.Tech ECE | 140000.00 |
|          5 | Sneha      | Verma     | sneha.verma@iilm.edu   | 2005-06-18 | B.Com      | 100000.00 |
+------------+------------+-----------+------------------------+------------+------------+-----------+
5 rows in set (0.001 sec)
```

---

## 📚 Additional Concepts

### Q2: How to Declare DEFAULT Value for Attributes

The `DEFAULT` constraint provides a default value for a column when no value is specified during insertion.

#### Syntax:

```sql
column_name data_type DEFAULT default_value
```

#### Example:

```sql
CREATE TABLE Student_Demo (
    student_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    dob DATE NOT NULL,
    course VARCHAR(50) DEFAULT 'B.Tech CSE',        -- Default course
    fees DECIMAL(8,2) DEFAULT 150000.00,            -- Default fees
    enrollment_date DATE DEFAULT CURRENT_DATE,      -- Default to current date
    status VARCHAR(20) DEFAULT 'Active'             -- Default status
);
```

#### Inserting Without Specifying Default Columns:

```sql
INSERT INTO Student_Demo (student_id, first_name, last_name, email, dob)
VALUES (1, 'Umar', 'Iqbal', 'umar@iilm.edu', '2005-03-15');
```

**Result:** The `course`, `fees`, `enrollment_date`, and `status` columns will automatically use their default values.

---

### Q3: How to Declare FOREIGN KEY in CREATE TABLE Command

A `FOREIGN KEY` establishes a relationship between two tables by referencing the PRIMARY KEY of another table.

#### Syntax:

```sql
FOREIGN KEY (column_name) REFERENCES parent_table(parent_column)
```

#### Example: Creating a Related Table Structure

**Step 1: Create Parent Table (Department)**

```sql
CREATE TABLE Department (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL
);
```

**Step 2: Create Child Table (Student) with FOREIGN KEY**

```sql
CREATE TABLE Student_With_Dept (
    student_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    dob DATE NOT NULL,
    course VARCHAR(50) NOT NULL,
    fees DECIMAL(8,2) CHECK (fees > 0),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES Department(dept_id)
);
```

#### Alternative Syntax (Inline):

```sql
CREATE TABLE Student_Inline (
    student_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    dept_id INT REFERENCES Department(dept_id)  -- Inline FOREIGN KEY
);
```

#### FOREIGN KEY with ON DELETE and ON UPDATE Actions:

```sql
CREATE TABLE Student_Cascade (
    student_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES Department(dept_id)
        ON DELETE CASCADE       -- Delete student if department is deleted
        ON UPDATE CASCADE       -- Update dept_id if parent changes
);
```

| Action | Description |
|--------|-------------|
| `CASCADE` | Automatically delete/update child records |
| `SET NULL` | Set foreign key to NULL when parent is deleted |
| `RESTRICT` | Prevent deletion of parent if child exists |
| `NO ACTION` | Similar to RESTRICT |

---

## 🔑 Key Concepts Summary

| Constraint | Purpose | Example |
|------------|---------|---------|
| `PRIMARY KEY` | Unique identifier for each row | `student_id INT PRIMARY KEY` |
| `NOT NULL` | Column cannot have NULL values | `first_name VARCHAR(50) NOT NULL` |
| `UNIQUE` | All values must be distinct | `email VARCHAR(100) UNIQUE` |
| `CHECK` | Validates data against a condition | `CHECK (fees > 0)` |
| `DEFAULT` | Provides default value if none given | `status VARCHAR(20) DEFAULT 'Active'` |
| `FOREIGN KEY` | Links to another table's PRIMARY KEY | `FOREIGN KEY (dept_id) REFERENCES Department(dept_id)` |

---

> **Submitted By:** Umar Iqbal  
> **Course:** DBMS Lab
