# 📚 DBMS LAB ASSIGNMENT 05

> **Date:** 12/February/2026  
> **Database:** UmarIqbalDB  
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Perform SQL queries on the **EMPLOYEE** table using **Aggregate Functions** (COUNT, SUM, MAX, MIN, AVG) and **String Functions** (UPPER, LOWER, INITCAP, LENGTH):

1. Display the total number of employee working in the company.
2. Display the total salary being paid to all employees.
3. Display the maximum salary from employee table.
4. Display the minimum salary from employee table.
5. Display the average salary from employee table.
6. Display the maximum salary being paid to clerk.
7. Display the maximum salary being paid in dept no 20.
8. Display the minimum salary paid to any salesman.
9. Display the average salary drawn by managers.
10. Display the total salary drawn by analyst working in dept no 40.
11. Display the names of the employee in Uppercase.
12. Display the names of the employee in Lowercase.
13. Display the names of the employee in Proper case.
14. Display the length of Your name using appropriate function.
15. Display the length of all the employee names.

---

## 📊 Reference Tables

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

### Problem 1: Display the Total Number of Employee Working in the Company

**Objective:** Count the total number of employees in the EMPLOYEE table.

```sql
SELECT COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE;
```

**Output:**
```
+-----------------+
| TOTAL_EMPLOYEES |
+-----------------+
|              14 |
+-----------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** There are **14** employees working in the company.

---

### Problem 2: Display the Total Salary Being Paid to All Employees

**Objective:** Calculate the sum of all employee salaries.

```sql
SELECT SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+--------------+
| TOTAL_SALARY |
+--------------+
|        29025 |
+--------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The total salary being paid to all employees is **29025**.

---

### Problem 3: Display the Maximum Salary from Employee Table

**Objective:** Find the highest salary in the EMPLOYEE table.

```sql
SELECT MAX(SAL) AS MAX_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+------------+
| MAX_SALARY |
+------------+
|       5000 |
+------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The maximum salary is **5000** (earned by KING).

---

### Problem 4: Display the Minimum Salary from Employee Table

**Objective:** Find the lowest salary in the EMPLOYEE table.

```sql
SELECT MIN(SAL) AS MIN_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+------------+
| MIN_SALARY |
+------------+
|        800 |
+------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The minimum salary is **800** (earned by SMITH).

---

### Problem 5: Display the Average Salary from Employee Table

**Objective:** Calculate the average salary of all employees.

```sql
SELECT AVG(SAL) AS AVG_SALARY
FROM EMPLOYEE;
```

**Output:**
```
+-------------+
| AVG_SALARY  |
+-------------+
| 2073.214286 |
+-------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The average salary of all employees is approximately **2073.21**.

---

### Problem 6: Display the Maximum Salary Being Paid to Clerk

**Objective:** Find the highest salary among employees with the job title CLERK.

```sql
SELECT MAX(SAL) AS MAX_CLERK_SALARY
FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

**Output:**
```
+------------------+
| MAX_CLERK_SALARY |
+------------------+
|             1300 |
+------------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The maximum salary paid to a CLERK is **1300** (earned by MILLER).

---

### Problem 7: Display the Maximum Salary Being Paid in Dept No 20

**Objective:** Find the highest salary in department number 20.

```sql
SELECT MAX(SAL) AS MAX_SAL_DEPT20
FROM EMPLOYEE
WHERE DEPTNO = 20;
```

**Output:**
```
+----------------+
| MAX_SAL_DEPT20 |
+----------------+
|           5000 |
+----------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The maximum salary in department 20 is **5000** (earned by KING).

---

### Problem 8: Display the Minimum Salary Paid to Any Salesman

**Objective:** Find the lowest salary among employees with the job title SALESMAN.

```sql
SELECT MIN(SAL) AS MIN_SALESMAN_SALARY
FROM EMPLOYEE
WHERE JOB = 'SALESMAN';
```

**Output:**
```
+---------------------+
| MIN_SALESMAN_SALARY |
+---------------------+
|                1250 |
+---------------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The minimum salary paid to a SALESMAN is **1250** (earned by WARD and MARTIN).

---

### Problem 9: Display the Average Salary Drawn by Managers

**Objective:** Calculate the average salary of all managers.

```sql
SELECT AVG(SAL) AS AVG_MANAGER_SALARY
FROM EMPLOYEE
WHERE JOB = 'MANAGER';
```

**Output:**
```
+--------------------+
| AVG_MANAGER_SALARY |
+--------------------+
|        2758.333333 |
+--------------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The average salary drawn by managers is approximately **2758.33** (JONES: 2975, BLAKE: 2850, CLARK: 2450).

---

### Problem 10: Display the Total Salary Drawn by Analyst Working in Dept No 40

**Objective:** Calculate the sum of salaries for analysts in department 40.

```sql
SELECT SUM(SAL) AS TOTAL_ANALYST_SAL_DEPT40
FROM EMPLOYEE
WHERE JOB = 'ANALYST'
  AND DEPTNO = 40;
```

**Output:**
```
+--------------------------+
| TOTAL_ANALYST_SAL_DEPT40 |
+--------------------------+
|                     3000 |
+--------------------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The total salary drawn by analysts in department 40 is **3000** (only SCOTT works as ANALYST in dept 40).

---

### Problem 11: Display the Names of the Employee in Uppercase

**Objective:** Show all employee names in uppercase using the UPPER() function.

```sql
SELECT UPPER(ENAME) AS EMPLOYEE_NAME_UPPER
FROM EMPLOYEE;
```

**Output:**
```
+---------------------+
| EMPLOYEE_NAME_UPPER |
+---------------------+
| SMITH               |
| ALLEN               |
| WARD                |
| JONES               |
| MARTIN              |
| BLAKE               |
| CLARK               |
| SCOTT               |
| KING                |
| TURNER              |
| ADAMS               |
| JAMES               |
| FORD                |
| MILLER              |
+---------------------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** All 14 employee names displayed in uppercase. Since names are already stored in uppercase, the output remains the same.

---

### Problem 12: Display the Names of the Employee in Lowercase

**Objective:** Show all employee names in lowercase using the LOWER() function.

```sql
SELECT LOWER(ENAME) AS EMPLOYEE_NAME_LOWER
FROM EMPLOYEE;
```

**Output:**
```
+---------------------+
| EMPLOYEE_NAME_LOWER |
+---------------------+
| smith               |
| allen               |
| ward                |
| jones               |
| martin              |
| blake               |
| clark               |
| scott               |
| king                |
| turner              |
| adams               |
| james               |
| ford                |
| miller              |
+---------------------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** All 14 employee names displayed in lowercase.

---

### Problem 13: Display the Names of the Employee in Proper Case

**Objective:** Show all employee names in proper case (first letter uppercase, rest lowercase). MariaDB/MySQL does not have a built-in INITCAP function, so we use CONCAT + UPPER + LOWER + SUBSTRING.

```sql
SELECT CONCAT(UPPER(SUBSTRING(ENAME, 1, 1)), LOWER(SUBSTRING(ENAME, 2))) AS EMPLOYEE_NAME_PROPER
FROM EMPLOYEE;
```

**Output:**
```
+----------------------+
| EMPLOYEE_NAME_PROPER |
+----------------------+
| Smith                |
| Allen                |
| Ward                 |
| Jones                |
| Martin               |
| Blake                |
| Clark                |
| Scott                |
| King                 |
| Turner               |
| Adams                |
| James                |
| Ford                 |
| Miller               |
+----------------------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** All 14 employee names displayed in proper case (title case) using CONCAT, UPPER, LOWER, and SUBSTRING functions.

---

### Problem 14: Display the Length of Your Name Using Appropriate Function

**Objective:** Use the LENGTH() function to find the length of your name.

```sql
SELECT LENGTH('Umar Iqbal') AS NAME_LENGTH;
```

**Output:**
```
+-------------+
| NAME_LENGTH |
+-------------+
|          10 |
+-------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The length of the name **"Umar Iqbal"** is **10** characters (including the space).

---

### Problem 15: Display the Length of All the Employee Names

**Objective:** Show the name and its length for all employees using the LENGTH() function.

```sql
SELECT ENAME, LENGTH(ENAME) AS NAME_LENGTH
FROM EMPLOYEE;
```

**Output:**
```
+--------+-------------+
| ENAME  | NAME_LENGTH |
+--------+-------------+
| SMITH  |           5 |
| ALLEN  |           5 |
| WARD   |           4 |
| JONES  |           5 |
| MARTIN |           6 |
| BLAKE  |           5 |
| CLARK  |           5 |
| SCOTT  |           5 |
| KING   |           4 |
| TURNER |           6 |
| ADAMS  |           5 |
| JAMES  |           5 |
| FORD   |           4 |
| MILLER |           6 |
+--------+-------------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** All 14 employee name lengths displayed. Shortest names are WARD, KING, FORD (4 chars); longest are MARTIN, TURNER, MILLER (6 chars).

---

## 📝 Summary

| # | Task | SQL Function Used | Result |
|---|------|-------------------|--------|
| 1 | Total number of employees | `COUNT(*)` | 14 |
| 2 | Total salary paid | `SUM(SAL)` | 29025 |
| 3 | Maximum salary | `MAX(SAL)` | 5000 |
| 4 | Minimum salary | `MIN(SAL)` | 800 |
| 5 | Average salary | `AVG(SAL)` | 2073.21 |
| 6 | Max salary for CLERK | `MAX(SAL)` with `WHERE` | 1300 |
| 7 | Max salary in dept 20 | `MAX(SAL)` with `WHERE` | 5000 |
| 8 | Min salary for SALESMAN | `MIN(SAL)` with `WHERE` | 1250 |
| 9 | Avg salary for MANAGER | `AVG(SAL)` with `WHERE` | 2758.33 |
| 10 | Total salary for ANALYST in dept 40 | `SUM(SAL)` with `WHERE` | 3000 |
| 11 | Names in Uppercase | `UPPER()` | 14 names |
| 12 | Names in Lowercase | `LOWER()` | 14 names |
| 13 | Names in Proper case | `CONCAT() + UPPER() + LOWER() + SUBSTRING()` | 14 names |
| 14 | Length of your name | `LENGTH()` | 10 |
| 15 | Length of all employee names | `LENGTH()` | 14 names |

---

## 🔑 Key SQL Concepts Used

| Concept | Purpose | Example |
|---------|---------|---------|
| `COUNT(*)` | Counts total rows | `SELECT COUNT(*) FROM EMPLOYEE` |
| `SUM(col)` | Adds all values in a column | `SELECT SUM(SAL) FROM EMPLOYEE` |
| `MAX(col)` | Returns the largest value | `SELECT MAX(SAL) FROM EMPLOYEE` |
| `MIN(col)` | Returns the smallest value | `SELECT MIN(SAL) FROM EMPLOYEE` |
| `AVG(col)` | Returns the average value | `SELECT AVG(SAL) FROM EMPLOYEE` |
| `UPPER(str)` | Converts string to uppercase | `SELECT UPPER(ENAME) FROM EMPLOYEE` |
| `LOWER(str)` | Converts string to lowercase | `SELECT LOWER(ENAME) FROM EMPLOYEE` |
| `SUBSTRING(str, pos, len)` | Extracts part of a string | `SUBSTRING(ENAME, 1, 1)` |
| `CONCAT(str1, str2)` | Joins strings together | `CONCAT(UPPER(...), LOWER(...))` |
| `LENGTH(str)` | Returns the length of a string | `SELECT LENGTH(ENAME) FROM EMPLOYEE` |

---

## 📚 SQL Functions Reference

| Function | Category | Description | Example |
|----------|----------|-------------|---------|
| `COUNT(*)` | Aggregate | Counts all rows | `COUNT(*)` → 14 |
| `COUNT(col)` | Aggregate | Counts non-NULL values | `COUNT(COMM)` → 4 |
| `SUM(col)` | Aggregate | Sum of column values | `SUM(SAL)` → 29025 |
| `MAX(col)` | Aggregate | Maximum value | `MAX(SAL)` → 5000 |
| `MIN(col)` | Aggregate | Minimum value | `MIN(SAL)` → 800 |
| `AVG(col)` | Aggregate | Average value | `AVG(SAL)` → 2073.21 |
| `UPPER(str)` | String | Converts to uppercase | `UPPER('smith')` → 'SMITH' |
| `LOWER(str)` | String | Converts to lowercase | `LOWER('SMITH')` → 'smith' |
| `LENGTH(str)` | String | Returns string length | `LENGTH('SMITH')` → 5 |
| `SUBSTRING(str, pos, len)` | String | Extracts substring | `SUBSTRING('SMITH', 1, 1)` → 'S' |
| `CONCAT(str1, str2)` | String | Concatenates strings | `CONCAT('A', 'B')` → 'AB' |

---

> **Submitted By:** Umar Iqbal  
> **Course:** DBMS Lab
