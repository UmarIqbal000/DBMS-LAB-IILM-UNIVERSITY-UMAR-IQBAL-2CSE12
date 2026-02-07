# 📚 DBMS LAB ASSIGNMENT 03

> **Date:** 04/February/2026  
> **Database:** UmarIqbalDB  
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Perform advanced data retrieval queries using **ORDER BY**, **LIKE patterns**, **IN**, **IS NULL**, and **calculated columns**:

1. List all employees and jobs in Department 30 in descending order of salary
2. List job and department number of employees whose name is five letters long, starts with 'A' and ends with 'N'
3. Display the names of employees whose name starts with 'S'
4. Display the names of employees whose name ends with 'S'
5. Display names of employees working in department 10, 20, or 40 OR working as clerk, salesman, or analyst
6. Display employee number and names for employees who earn commission
7. Display employee number and total salary for each employee
8. Display employee number and annual salary for each employee
9. Display names of all employees working as clerks and earning more than 3000
10. Display names of employees working as clerk, salesman, or analyst and earning more than 3000

---

## 📊 Reference Table: EMPLOYEE

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

### Problem 1: List All Employees and Jobs in Department 30 (Descending Order of Salary)

**Objective:** Retrieve employees from Department 30 sorted by salary in descending order.

```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE DEPTNO = 30
ORDER BY SAL DESC;
```

**Output:**
```
+--------+----------+------+
| ENAME  | JOB      | SAL  |
+--------+----------+------+
| BLAKE  | MANAGER  | 2850 |
| ALLEN  | SALESMAN | 1600 |
| TURNER | SALESMAN | 1500 |
| WARD   | SALESMAN | 1250 |
| MARTIN | SALESMAN | 1250 |
| JAMES  | CLERK    |  950 |
+--------+----------+------+
6 rows in set (0.001 sec)
```

> ✅ **Result:** 6 employees in Department 30 sorted by salary (highest first)

---

### Problem 2: Employees Whose Name is 5 Letters, Starts with 'A' and Ends with 'N'

**Objective:** Use pattern matching to find employees with specific name format.

```sql
SELECT JOB, DEPTNO
FROM EMPLOYEE
WHERE ENAME LIKE 'A___N';
```

> 📌 **Note:** Each underscore `_` represents exactly one character.

**Output:**
```
+----------+--------+
| JOB      | DEPTNO |
+----------+--------+
| SALESMAN |     30 |
+----------+--------+
1 row in set (0.001 sec)
```

> ✅ **Result:** ALLEN matches the pattern (A-L-L-E-N = 5 letters)

---

### Problem 3: Display Names of Employees Whose Name Starts with 'S'

**Objective:** Find employees whose name begins with the letter 'S'.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE 'S%';
```

**Output:**
```
+-------+
| ENAME |
+-------+
| SMITH |
| SCOTT |
+-------+
2 rows in set (0.001 sec)
```

> ✅ **Result:** 2 employees found: SMITH, SCOTT

---

### Problem 4: Display Names of Employees Whose Name Ends with 'S'

**Objective:** Find employees whose name ends with the letter 'S'.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '%S';
```

**Output:**
```
+-------+
| ENAME |
+-------+
| JONES |
| ADAMS |
| JAMES |
+-------+
3 rows in set (0.001 sec)
```

> ✅ **Result:** 3 employees found: JONES, ADAMS, JAMES

---

### Problem 5: Employees in Department 10/20/40 OR Working as Clerk/Salesman/Analyst

**Objective:** Use compound conditions with `OR` and `IN` operators.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO IN (10, 20, 40)
OR JOB IN ('CLERK', 'SALESMAN', 'ANALYST');
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| JAMES  |
| FORD   |
| MILLER |
+--------+
13 rows in set (0.001 sec)
```

> ✅ **Result:** 13 employees match the criteria

---

### Problem 6: Employees Who Earn Commission

**Objective:** Find employees with non-null and positive commission values.

```sql
SELECT EMPNO, ENAME
FROM EMPLOYEE
WHERE COMM IS NOT NULL
AND COMM > 0;
```

**Output:**
```
+-------+--------+
| EMPNO | ENAME  |
+-------+--------+
|  7499 | ALLEN  |
|  7521 | WARD   |
|  7654 | MARTIN |
+-------+--------+
3 rows in set (0.001 sec)
```

> ✅ **Result:** 3 employees earn commission: ALLEN (300), WARD (300), MARTIN (1400)

---

### Problem 7: Display Employee Number and Total Salary (Salary + Commission)

**Objective:** Calculate total salary including commission using `IFNULL()` function.

```sql
SELECT EMPNO, (SAL + IFNULL(COMM, 0)) AS TOTAL_SALARY
FROM EMPLOYEE;
```

> 📌 **Note:** `IFNULL(COMM, 0)` returns 0 if COMM is NULL (MySQL/MariaDB).  
> For Oracle, use `NVL(COMM, 0)` instead.

**Output:**
```
+-------+--------------+
| EMPNO | TOTAL_SALARY |
+-------+--------------+
|  7369 |          800 |
|  7499 |         1900 |
|  7521 |         1550 |
|  7566 |         2975 |
|  7654 |         2650 |
|  7698 |         2850 |
|  7782 |         2450 |
|  7788 |         3000 |
|  7839 |         5000 |
|  7844 |         1500 |
|  7876 |         1100 |
|  7900 |          950 |
|  7902 |         3000 |
|  7934 |         1300 |
+-------+--------------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** Total salary calculated for all 14 employees

---

### Problem 8: Display Employee Number and Annual Salary

**Objective:** Calculate annual salary (monthly salary × 12).

```sql
SELECT EMPNO, (SAL * 12) AS ANNUAL_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+-------+---------------+
| EMPNO | ANNUAL_SALARY |
+-------+---------------+
|  7369 |          9600 |
|  7499 |         19200 |
|  7521 |         15000 |
|  7566 |         35700 |
|  7654 |         15000 |
|  7698 |         34200 |
|  7782 |         29400 |
|  7788 |         36000 |
|  7839 |         60000 |
|  7844 |         18000 |
|  7876 |         13200 |
|  7900 |         11400 |
|  7902 |         36000 |
|  7934 |         15600 |
+-------+---------------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** Annual salary computed for all employees

---

### Problem 9: Clerks Earning More Than 3000

**Objective:** Find clerks with salary greater than 3000.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > 3000;
```

**Output:**
```
Empty set (0.001 sec)
```

> ⚠️ **Result:** No rows returned. All clerks (SMITH, ADAMS, JAMES, MILLER) have salary ≤ 1300.

---

### Problem 10: Clerks, Salesmen, or Analysts Earning More Than 3000

**Objective:** Find employees in specific jobs earning more than 3000.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB IN ('CLERK', 'SALESMAN', 'ANALYST')
AND SAL > 3000;
```

**Output:**
```
Empty set (0.001 sec)
```

> ⚠️ **Result:** No rows returned. The highest salary among these jobs is 3000 (SCOTT, FORD - ANALYST), which is not greater than 3000.

---

## 📝 Summary

| # | Task | SQL Clause Used | Records Found |
|---|------|-----------------|---------------|
| 1 | Employees in Dept 30 (sorted) | `ORDER BY DESC` | 6 |
| 2 | Name 5 letters: A___N | `LIKE 'A___N'` | 1 |
| 3 | Name starts with 'S' | `LIKE 'S%'` | 2 |
| 4 | Name ends with 'S' | `LIKE '%S'` | 3 |
| 5 | Dept 10/20/40 OR specific jobs | `IN`, `OR` | 13 |
| 6 | Employees with commission | `IS NOT NULL`, `> 0` | 3 |
| 7 | Total salary (SAL + COMM) | `IFNULL()`, Alias | 14 |
| 8 | Annual salary | Arithmetic (`* 12`) | 14 |
| 9 | Clerks earning > 3000 | `AND` with conditions | 0 |
| 10 | Clerks/Salesmen/Analysts > 3000 | `IN`, `AND` | 0 |

---

## 🔑 Key SQL Concepts Used

| Concept | Purpose | Example |
|---------|---------|---------|
| `ORDER BY` | Sort results | `ORDER BY SAL DESC` |
| `ORDER BY DESC` | Sort in descending order | `ORDER BY SAL DESC` |
| `LIKE` with `%` | Match any characters | `LIKE 'S%'` |
| `LIKE` with `_` | Match single character | `LIKE 'A___N'` |
| `IS NOT NULL` | Check for non-null values | `WHERE COMM IS NOT NULL` |
| `IFNULL()` | Replace NULL with value | `IFNULL(COMM, 0)` |
| Arithmetic | Calculated columns | `SAL * 12`, `SAL + COMM` |
| Alias (`AS`) | Rename column in output | `AS TOTAL_SALARY` |

---

## 📚 Pattern Matching Reference

| Pattern | Description | Example |
|---------|-------------|---------|
| `'S%'` | Starts with 'S' | SMITH, SCOTT |
| `'%S'` | Ends with 'S' | JONES, ADAMS, JAMES |
| `'%AR%'` | Contains 'AR' | WARD, MARTIN, CLARK |
| `'A___N'` | 5 chars: A + 3 any + N | ALLEN |
| `'_____'` | Exactly 5 characters | SMITH, JONES, etc. |

---

## 🔄 NULL Handling Functions

| Database | Function | Example |
|----------|----------|---------|
| MySQL/MariaDB | `IFNULL(col, value)` | `IFNULL(COMM, 0)` |
| Oracle | `NVL(col, value)` | `NVL(COMM, 0)` |
| SQL Server | `ISNULL(col, value)` | `ISNULL(COMM, 0)` |
| PostgreSQL | `COALESCE(col, value)` | `COALESCE(COMM, 0)` |

---

> **Submitted By:** Umar Iqbal  
> **Course:** DBMS Lab
