# 📚 DBMS LAB ASSIGNMENT 01

> **Date:** 28/January/2026  
> **Database:** UmarIqbalDB  
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Create two tables (`DEPARTMENT` and `EMPLOYEE`) and perform the following operations:

1. Create `EMPLOYEE_MASTER` table with data from `EMPLOYEE` table
2. Delete all records from `EMPLOYEE_MASTER` where `DEPTNO = 10`
3. Update salary by 10% increase for `DEPTNO = 20` in `EMPLOYEE_MASTER`
4. Alter `SAL` column to `DECIMAL(10,2)` in `EMPLOYEE_MASTER`
5. Drop `EMPLOYEE_MASTER` table

---

## 📊 Table Structures

### Table 1: DEPARTMENT

| Field  | Type        | Null | Key | Default | Extra |
|--------|-------------|------|-----|---------|-------|
| DEPTNO | INT(2)      | NO   | PRI | NULL    |       |
| DNAME  | VARCHAR(15) | NO   |     | NULL    |       |

### Table 2: EMPLOYEE

| Field    | Type        | Null | Key | Default | Extra       |
|----------|-------------|------|-----|---------|-------------|
| EMPNO    | INT(4)      | NO   | PRI | NULL    |             |
| ENAME    | VARCHAR(20) | NO   |     | NULL    |             |
| JOB      | VARCHAR(20) | YES  |     | NULL    |             |
| MGR      | INT(4)      | YES  |     | NULL    |             |
| HIREDATE | DATE        | YES  |     | NULL    |             |
| SAL      | INT(10)     | YES  |     | NULL    |             |
| COMM     | INT(7)      | YES  |     | NULL    |             |
| DEPTNO   | INT(2)      | YES  | MUL | NULL    | Foreign Key |

---

## 📁 Sample Data

### DEPARTMENT Table

| DEPTNO | DNAME      |
|--------|------------|
| 10     | RESEARCH   |
| 20     | ACCOUNTING |
| 30     | SALES      |
| 40     | OPERATIONS |

### EMPLOYEE Table

| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
|-------|--------|-----------|------|------------|------|------|--------|
| 7369  | SMITH  | CLERK     | 7902 | 1980-12-17 | 800  | NULL | 20     |
| 7499  | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 | 300  | 30     |
| 7521  | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 | 300  | 30     |
| 7566  | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975 | NULL | 20     |
| 7654  | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 | 30     |
| 7698  | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL | 30     |
| 7782  | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450 | NULL | 20     |
| 7788  | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL | 40     |
| 7839  | KING   | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL | 20     |
| 7844  | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 | 0    | 30     |
| 7876  | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100 | NULL | 20     |
| 7900  | JAMES  | CLERK     | 7698 | 1981-12-03 | 950  | NULL | 30     |
| 7902  | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL | 20     |
| 7934  | MILLER | CLERK     | 7782 | 1982-01-23 | 1300 | NULL | 10     |

---

## 🔧 SQL Queries & Solutions

### Step 0: Database Connection & Setup

```sql
-- Connect to MySQL/MariaDB
C:\xampp\mysql\bin> mysql -u root

-- Show available databases
SHOW DATABASES;

-- Select the database
USE UmarIqbalDB;
```

---

### Step 1: Create Tables

#### Create DEPARTMENT Table

```sql
CREATE TABLE DEPARTMENT (
    DEPTNO INT(2) PRIMARY KEY,
    DNAME VARCHAR(15) NOT NULL
);
```

**Output:**
```
Query OK, 0 rows affected (0.017 sec)
```

#### Create EMPLOYEE Table

```sql
CREATE TABLE EMPLOYEE (
    EMPNO INT(4) PRIMARY KEY,
    ENAME VARCHAR(20) NOT NULL,
    JOB VARCHAR(20),
    MGR INT(4),
    HIREDATE DATE,
    SAL INT(10),
    COMM INT(7),
    DEPTNO INT(2),
    FOREIGN KEY (DEPTNO) REFERENCES DEPARTMENT(DEPTNO)
);
```

**Output:**
```
Query OK, 0 rows affected (0.040 sec)
```

#### Verify Tables Created

```sql
SHOW TABLES;
```

**Output:**
```
+-----------------------+
| Tables_in_umariqbaldb |
+-----------------------+
| department            |
| employee              |
+-----------------------+
2 rows in set (0.001 sec)
```

---

### Step 2: Insert Data

#### Insert into DEPARTMENT

```sql
INSERT INTO DEPARTMENT (DEPTNO, DNAME) VALUES
    (10, 'RESEARCH'),
    (20, 'ACCOUNTING'),
    (30, 'SALES'),
    (40, 'OPERATIONS');
```

**Output:**
```
Query OK, 4 rows affected (0.088 sec)
Records: 4  Duplicates: 0  Warnings: 0
```

#### Insert into EMPLOYEE

```sql
INSERT INTO EMPLOYEE (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES
    (7369, 'SMITH', 'CLERK', 7902, '1980-12-17', 800, NULL, 20),
    (7499, 'ALLEN', 'SALESMAN', 7698, '1981-02-20', 1600, 300, 30),
    (7521, 'WARD', 'SALESMAN', 7698, '1981-02-22', 1250, 300, 30),
    (7566, 'JONES', 'MANAGER', 7839, '1981-04-02', 2975, NULL, 20),
    (7654, 'MARTIN', 'SALESMAN', 7698, '1981-09-28', 1250, 1400, 30),
    (7698, 'BLAKE', 'MANAGER', 7839, '1981-05-01', 2850, NULL, 30),
    (7782, 'CLARK', 'MANAGER', 7839, '1981-06-09', 2450, NULL, 20),
    (7788, 'SCOTT', 'ANALYST', 7566, '1982-12-09', 3000, NULL, 40),
    (7839, 'KING', 'PRESIDENT', NULL, '1981-11-17', 5000, NULL, 20),
    (7844, 'TURNER', 'SALESMAN', 7698, '1981-09-08', 1500, 0, 30),
    (7876, 'ADAMS', 'CLERK', 7788, '1983-01-12', 1100, NULL, 20),
    (7900, 'JAMES', 'CLERK', 7698, '1981-12-03', 950, NULL, 30),
    (7902, 'FORD', 'ANALYST', 7566, '1981-12-03', 3000, NULL, 20),
    (7934, 'MILLER', 'CLERK', 7782, '1982-01-23', 1300, NULL, 10);
```

**Output:**
```
Query OK, 14 rows affected (0.013 sec)
Records: 14  Duplicates: 0  Warnings: 0
```

---

## ✅ Problem Solutions

### Problem 1: Create EMPLOYEE_MASTER Table

**Objective:** Create `EMPLOYEE_MASTER` table with data from `EMPLOYEE` table.

```sql
CREATE TABLE EMPLOYEE_MASTER AS
SELECT * FROM EMPLOYEE;
```

**Output:**
```
Query OK, 14 rows affected (0.022 sec)
Records: 14  Duplicates: 0  Warnings: 0
```

**Verification:**

```sql
SELECT * FROM EMPLOYEE_MASTER;
```

**Output:**
```
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975 | NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450 | NULL |     20 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL |     40 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300 | NULL |     10 |
+-------+--------+-----------+------+------------+------+------+--------+
14 rows in set (0.001 sec)
```

---

### Problem 2: Delete Records Where DEPTNO = 10

**Objective:** Delete all records from `EMPLOYEE_MASTER` where `DEPTNO = 10`.

```sql
DELETE FROM EMPLOYEE_MASTER
WHERE DEPTNO = 10;
```

**Output:**
```
Query OK, 1 row affected (0.004 sec)
```

**Verification:**

```sql
SELECT * FROM EMPLOYEE_MASTER WHERE DEPTNO = 10;
```

**Output:**
```
Empty set (0.001 sec)
```

> ✅ **Result:** 1 record (MILLER) was deleted successfully.

---

### Problem 3: Update Salary by 10% for DEPTNO = 20

**Objective:** Increase salary by 10% for all employees in `DEPTNO = 20`.

```sql
UPDATE EMPLOYEE_MASTER
SET SAL = SAL * 1.10
WHERE DEPTNO = 20;
```

**Output:**
```
Query OK, 6 rows affected (0.005 sec)
Rows matched: 6  Changed: 6  Warnings: 0
```

**Verification:**

```sql
SELECT EMPNO, ENAME, SAL FROM EMPLOYEE_MASTER WHERE DEPTNO = 20;
```

**Output:**
```
+-------+-------+------+
| EMPNO | ENAME | SAL  |
+-------+-------+------+
|  7369 | SMITH |  880 |
|  7566 | JONES | 3273 |
|  7782 | CLARK | 2695 |
|  7839 | KING  | 5500 |
|  7876 | ADAMS | 1210 |
|  7902 | FORD  | 3300 |
+-------+-------+------+
6 rows in set (0.001 sec)
```

> ✅ **Result:** Salary increased by 10% for 6 employees in DEPTNO 20.

---

### Problem 4: Alter SAL Column to DECIMAL(10,2)

**Objective:** Modify the `SAL` column to store decimal values with 2 decimal places.

```sql
ALTER TABLE EMPLOYEE_MASTER
MODIFY SAL DECIMAL(10,2);
```

**Output:**
```
Query OK, 13 rows affected (0.067 sec)
Records: 13  Duplicates: 0  Warnings: 0
```

**Verification:**

```sql
DESCRIBE EMPLOYEE_MASTER;
```

**Output:**
```
+----------+---------------+------+-----+---------+-------+
| Field    | Type          | Null | Key | Default | Extra |
+----------+---------------+------+-----+---------+-------+
| EMPNO    | int(4)        | NO   |     | NULL    |       |
| ENAME    | varchar(20)   | NO   |     | NULL    |       |
| JOB      | varchar(20)   | YES  |     | NULL    |       |
| MGR      | int(4)        | YES  |     | NULL    |       |
| HIREDATE | date          | YES  |     | NULL    |       |
| SAL      | decimal(10,2) | YES  |     | NULL    |       |
| COMM     | int(7)        | YES  |     | NULL    |       |
| DEPTNO   | int(2)        | YES  |     | NULL    |       |
+----------+---------------+------+-----+---------+-------+
8 rows in set (0.043 sec)
```

> ✅ **Result:** SAL column type changed from `INT(10)` to `DECIMAL(10,2)`.

---

### Problem 5: Drop EMPLOYEE_MASTER Table

**Objective:** Remove the `EMPLOYEE_MASTER` table from the database.

```sql
DROP TABLE EMPLOYEE_MASTER;
```

**Output:**
```
Query OK, 0 rows affected (0.013 sec)
```

> ✅ **Result:** `EMPLOYEE_MASTER` table dropped successfully.

---

## 📝 Summary

| # | Task | Query Type | Status |
|---|------|------------|--------|
| 1 | Create EMPLOYEE_MASTER from EMPLOYEE | CREATE TABLE AS SELECT | ✅ Done |
| 2 | Delete records where DEPTNO = 10 | DELETE | ✅ Done |
| 3 | Update salary (+10%) for DEPTNO = 20 | UPDATE | ✅ Done |
| 4 | Alter SAL to DECIMAL(10,2) | ALTER TABLE | ✅ Done |
| 5 | Drop EMPLOYEE_MASTER table | DROP TABLE | ✅ Done |

---

## 🔑 Key SQL Concepts Used

| Concept | Command | Description |
|---------|---------|-------------|
| **DDL** | CREATE, ALTER, DROP | Data Definition Language - defines structure |
| **DML** | INSERT, UPDATE, DELETE | Data Manipulation Language - modifies data |
| **DQL** | SELECT | Data Query Language - retrieves data |
| **Constraints** | PRIMARY KEY, FOREIGN KEY, NOT NULL | Ensures data integrity |

---

> **Submitted By:** Umar Iqbal  
> **Course:** DBMS Lab
