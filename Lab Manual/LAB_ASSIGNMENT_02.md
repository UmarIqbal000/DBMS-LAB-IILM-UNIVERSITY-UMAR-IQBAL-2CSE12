# 📚 DBMS LAB ASSIGNMENT 02

> **Date:** 08/February/2026  
> **Database:** UmarIqbalDB  
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Perform queries using the **EMPLOYEE** table to retrieve data using various SQL clauses:

1. List all distinct jobs in EMPLOYEE
2. List all information about employees in Department Number 30
3. Find all department numbers with department names greater than 20
4. Find all information about managers and clerks in Department 30
5. List Employee name, Employee number, and department of all clerks
6. Find all managers not in Department 30
7. List information about employees in Department 10 who are not managers or clerks
8. Find employees and jobs earning between 1200 and 1400
9. List Name and Department Number of employees who are clerks, analysts, or salesmen
10. List Name and Department Number of employees whose names begin with M

---

## 📊 Reference Tables

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

## 🔧 Database Connection

```sql
-- Connect to MySQL/MariaDB
C:\xampp\mysql\bin> mysql -u root

-- Select the database
USE UmarIqbalDB;
```

---

## ✅ Problem Solutions

### Problem 1: List All Distinct Jobs in EMPLOYEE

**Objective:** Retrieve all unique job titles from the EMPLOYEE table.

```sql
SELECT DISTINCT JOB
FROM EMPLOYEE;
```

**Output:**
```
+-----------+
| JOB       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
5 rows in set (0.001 sec)
```

> ✅ **Result:** 5 distinct jobs found: CLERK, SALESMAN, MANAGER, ANALYST, PRESIDENT

---

### Problem 2: List All Information About Employees in Department 30

**Objective:** Retrieve complete records of all employees working in Department 30.

```sql
SELECT *
FROM EMPLOYEE
WHERE DEPTNO = 30;
```

**Output:**
```
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+--------+-----------+------+------------+------+------+--------+
6 rows in set (0.001 sec)
```

> ✅ **Result:** 6 employees found in Department 30: ALLEN, WARD, MARTIN, BLAKE, TURNER, JAMES

---

### Problem 3: Find All Department Numbers with Department Names Greater Than 20

**Objective:** Retrieve department numbers and names where DEPTNO is greater than 20.

```sql
SELECT DEPTNO, DNAME
FROM DEPARTMENT
WHERE DEPTNO > 20;
```

**Output:**
```
+--------+------------+
| DEPTNO | DNAME      |
+--------+------------+
|     30 | SALES      |
|     40 | OPERATIONS |
+--------+------------+
2 rows in set (0.001 sec)
```

> ✅ **Result:** 2 departments found: SALES (30), OPERATIONS (40)

---

### Problem 4: Find All Information About Managers and Clerks in Department 30

**Objective:** Retrieve employees who are either MANAGER or CLERK in Department 30.

```sql
SELECT *
FROM EMPLOYEE
WHERE DEPTNO = 30
AND JOB IN ('MANAGER', 'CLERK');
```

**Output:**
```
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
```

> ✅ **Result:** Manager: BLAKE | Clerk: JAMES

---

### Problem 5: List Employee Name, Employee Number, and Department of All Clerks

**Objective:** Retrieve specific columns for employees with JOB = 'CLERK'.

```sql
SELECT ENAME, EMPNO, DEPTNO
FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

**Output:**
```
+--------+-------+--------+
| ENAME  | EMPNO | DEPTNO |
+--------+-------+--------+
| SMITH  |  7369 |     20 |
| ADAMS  |  7876 |     20 |
| JAMES  |  7900 |     30 |
| MILLER |  7934 |     10 |
+--------+-------+--------+
4 rows in set (0.001 sec)
```

> ✅ **Result:** 4 clerks found: SMITH (20), ADAMS (20), JAMES (30), MILLER (10)

---

### Problem 6: Find All Managers Not in Department 30

**Objective:** Retrieve managers who work in departments other than 30.

```sql
SELECT *
FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND DEPTNO <> 30;
```

**Output:**
```
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7566 | JONES | MANAGER | 7839 | 1981-04-02 | 2975 | NULL |     20 |
|  7782 | CLARK | MANAGER | 7839 | 1981-06-09 | 2450 | NULL |     20 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
```

> ✅ **Result:** 2 managers not in Department 30: JONES (20), CLARK (20)

---

### Problem 7: List Information About Employees in Department 10 Who Are Not Managers or Clerks

**Objective:** Retrieve employees in Department 10 excluding MANAGER and CLERK roles.

```sql
SELECT *
FROM EMPLOYEE
WHERE DEPTNO = 10
AND JOB NOT IN ('MANAGER', 'CLERK');
```

**Output:**
```
Empty set (0.001 sec)
```

> ⚠️ **Result:** No rows returned. Department 10 only has MILLER who is a CLERK.

---

### Problem 8: Find Employees and Jobs Earning Between 1200 and 1400

**Objective:** Retrieve employees with salary in the range 1200 to 1400 (inclusive).

```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE SAL BETWEEN 1200 AND 1400;
```

**Output:**
```
+--------+----------+------+
| ENAME  | JOB      | SAL  |
+--------+----------+------+
| WARD   | SALESMAN | 1250 |
| MARTIN | SALESMAN | 1250 |
| MILLER | CLERK    | 1300 |
+--------+----------+------+
3 rows in set (0.001 sec)
```

> ✅ **Result:** 3 employees found with salary between 1200-1400: WARD (1250), MARTIN (1250), MILLER (1300)

---

### Problem 9: List Name and Department Number of Clerks, Analysts, or Salesmen

**Objective:** Retrieve employees whose job is CLERK, ANALYST, or SALESMAN.

```sql
SELECT ENAME, DEPTNO
FROM EMPLOYEE
WHERE JOB IN ('CLERK', 'ANALYST', 'SALESMAN');
```

**Output:**
```
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| SMITH  |     20 |
| ALLEN  |     30 |
| WARD   |     30 |
| MARTIN |     30 |
| SCOTT  |     40 |
| TURNER |     30 |
| ADAMS  |     20 |
| JAMES  |     30 |
| FORD   |     20 |
| MILLER |     10 |
+--------+--------+
10 rows in set (0.001 sec)
```

> ✅ **Result:** 10 employees found (excludes MANAGER and PRESIDENT roles)

---

### Problem 10: List Name and Department Number of Employees Whose Names Begin with M

**Objective:** Retrieve employees whose name starts with the letter 'M'.

```sql
SELECT ENAME, DEPTNO
FROM EMPLOYEE
WHERE ENAME LIKE 'M%';
```

**Output:**
```
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| MARTIN |     30 |
| MILLER |     10 |
+--------+--------+
2 rows in set (0.001 sec)
```

> ✅ **Result:** 2 employees found: MARTIN (30), MILLER (10)

---

## 📝 Summary

| # | Task | SQL Clause Used | Records Found |
|---|------|-----------------|---------------|
| 1 | List distinct jobs | `SELECT DISTINCT` | 5 |
| 2 | Employees in DEPTNO 30 | `WHERE` | 6 |
| 3 | Departments > 20 | `WHERE` with `>` | 2 |
| 4 | Managers & Clerks in DEPTNO 30 | `WHERE` with `IN` | 2 |
| 5 | All clerks | `WHERE` | 4 |
| 6 | Managers not in DEPTNO 30 | `WHERE` with `<>` | 2 |
| 7 | DEPTNO 10, not Manager/Clerk | `WHERE` with `NOT IN` | 0 |
| 8 | Salary between 1200-1400 | `BETWEEN` | 3 |
| 9 | Clerks, Analysts, Salesmen | `WHERE` with `IN` | 10 |
| 10 | Names starting with 'M' | `LIKE 'M%'` | 2 |

---

## 🔑 Key SQL Concepts Used

| Clause | Purpose | Example |
|--------|---------|---------|
| `SELECT DISTINCT` | Returns unique values only | `SELECT DISTINCT JOB` |
| `WHERE` | Filters rows based on condition | `WHERE DEPTNO = 30` |
| `IN` | Matches any value in a list | `JOB IN ('CLERK', 'MANAGER')` |
| `NOT IN` | Excludes values in a list | `JOB NOT IN ('MANAGER', 'CLERK')` |
| `BETWEEN` | Range of values (inclusive) | `SAL BETWEEN 1200 AND 1400` |
| `LIKE` | Pattern matching with wildcards | `ENAME LIKE 'M%'` |
| `<>` or `!=` | Not equal comparison | `DEPTNO <> 30` |

---

## 📚 SQL Operators Reference

| Operator | Description | Example |
|----------|-------------|---------|
| `=` | Equal to | `DEPTNO = 30` |
| `<>` or `!=` | Not equal to | `DEPTNO <> 30` |
| `>` | Greater than | `DEPTNO > 20` |
| `<` | Less than | `SAL < 1500` |
| `>=` | Greater than or equal | `SAL >= 1200` |
| `<=` | Less than or equal | `SAL <= 1400` |
| `BETWEEN` | Within a range | `SAL BETWEEN 1200 AND 1400` |
| `LIKE` | Pattern matching | `ENAME LIKE 'M%'` |
| `IN` | Match any in list | `JOB IN ('CLERK', 'MANAGER')` |
| `NOT IN` | Not in list | `JOB NOT IN ('CLERK')` |

---

> **Submitted By:** Umar Iqbal  
> **Course:** DBMS Lab
