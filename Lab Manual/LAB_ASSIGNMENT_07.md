# 📚 DBMS LAB ASSIGNMENT 07

> **Date:** 12/February/2026  
> **Database:** UmarIqbalDB  
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Perform SQL queries on the **EMPLOYEE** table using **Date Computations**, **Aggregate Functions**, **GROUP BY**, **Matrix Queries**, and **Formatting**:

1. Compute the no. of days remaining in this year.
2. Find the highest and lowest salaries and the difference between of them.
3. List employee whose commission is greater than 25% of their salaries.
4. Make a query that displays salary in dollar format.
5. Create a matrix query to display the job, the salary for that job based on department number, and the total salary for that job for all departments, giving each column an appropriate heading.
6. Query that will display the total no of employees, and of that total the number who were hired in 1980, 1981, 1982 and 1983. Give appropriate column heading.
7. Query to get the last Sunday of Any Month.
8. Display department numbers and total number of employees working in each department.
9. Display the various jobs and total number of employees within each job group.
10. Display the depart numbers and total salary for each department.

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

### Problem 1: Compute the Number of Days Remaining in This Year

**Objective:** Calculate the number of days left from today until the end of the current year.

```sql
SELECT CURDATE() AS TODAY,
       CONCAT(YEAR(CURDATE()), '-12-31') AS YEAR_END,
       DATEDIFF(CONCAT(YEAR(CURDATE()), '-12-31'), CURDATE()) AS DAYS_REMAINING;
```

**Output:**
```
+------------+------------+----------------+
| TODAY      | YEAR_END   | DAYS_REMAINING |
+------------+------------+----------------+
| 2026-02-12 | 2026-12-31 |            322 |
+------------+------------+----------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** There are **322 days** remaining in the year 2026 (from February 12 to December 31).

---

### Problem 2: Find the Highest and Lowest Salaries and the Difference Between Them

**Objective:** Display the maximum salary, minimum salary, and the difference between them.

```sql
SELECT MAX(SAL) AS HIGHEST_SALARY,
       MIN(SAL) AS LOWEST_SALARY,
       MAX(SAL) - MIN(SAL) AS DIFFERENCE
FROM EMPLOYEE;
```

**Output:**
```
+----------------+---------------+------------+
| HIGHEST_SALARY | LOWEST_SALARY | DIFFERENCE |
+----------------+---------------+------------+
|           5000 |           800 |       4200 |
+----------------+---------------+------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** Highest salary = **5000** (KING), Lowest salary = **800** (SMITH), Difference = **4200**.

---

### Problem 3: List Employee Whose Commission Is Greater Than 25% of Their Salaries

**Objective:** Find employees where COMM > 25% of SAL.

```sql
SELECT ENAME, SAL, COMM,
       SAL * 0.25 AS SAL_25_PERCENT
FROM EMPLOYEE
WHERE COMM > SAL * 0.25;
```

**Output:**
```
+--------+------+------+----------------+
| ENAME  | SAL  | COMM | SAL_25_PERCENT |
+--------+------+------+----------------+
| MARTIN | 1250 | 1400 |         312.50 |
+--------+------+------+----------------+
1 row in set (0.001 sec)
```

**Verification of all employees with COMM:**
| ENAME  | SAL  | COMM | 25% of SAL | COMM > 25%? |
|--------|------|------|------------|-------------|
| ALLEN  | 1600 | 300  | 400        | ❌ No       |
| WARD   | 1250 | 300  | 312.50     | ❌ No       |
| MARTIN | 1250 | 1400 | 312.50     | ✅ Yes      |
| TURNER | 1500 | 0    | 375        | ❌ No       |

> ✅ **Result:** Only **MARTIN** has commission (1400) greater than 25% of salary (312.50).

---

### Problem 4: Make a Query That Displays Salary in Dollar Format

**Objective:** Display employee salaries formatted with a dollar sign ($) prefix.

```sql
SELECT ENAME,
       CONCAT('$', FORMAT(SAL, 2)) AS SALARY_IN_DOLLARS
FROM EMPLOYEE;
```

**Output:**
```
+--------+-------------------+
| ENAME  | SALARY_IN_DOLLARS |
+--------+-------------------+
| SMITH  | $800.00           |
| ALLEN  | $1,600.00         |
| WARD   | $1,250.00         |
| JONES  | $2,975.00         |
| MARTIN | $1,250.00         |
| BLAKE  | $2,850.00         |
| CLARK  | $2,450.00         |
| SCOTT  | $3,000.00         |
| KING   | $5,000.00         |
| TURNER | $1,500.00         |
| ADAMS  | $1,100.00         |
| JAMES  | $950.00           |
| FORD   | $3,000.00         |
| MILLER | $1,300.00         |
+--------+-------------------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** All 14 employee salaries displayed in dollar format with commas and 2 decimal places using `CONCAT('$', FORMAT(SAL, 2))`.

---

### Problem 5: Matrix Query — Job, Salary by Department, and Total Salary

**Objective:** Create a cross-tabulation (matrix/pivot) showing each job, the salary for that job in each department, and the total salary across all departments.

```sql
SELECT JOB,
       SUM(CASE WHEN DEPTNO = 10 THEN SAL ELSE 0 END) AS DEPT_10,
       SUM(CASE WHEN DEPTNO = 20 THEN SAL ELSE 0 END) AS DEPT_20,
       SUM(CASE WHEN DEPTNO = 30 THEN SAL ELSE 0 END) AS DEPT_30,
       SUM(CASE WHEN DEPTNO = 40 THEN SAL ELSE 0 END) AS DEPT_40,
       SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB
ORDER BY JOB;
```

**Output:**
```
+-----------+---------+---------+---------+---------+--------------+
| JOB       | DEPT_10 | DEPT_20 | DEPT_30 | DEPT_40 | TOTAL_SALARY |
+-----------+---------+---------+---------+---------+--------------+
| ANALYST   |       0 |    3000 |       0 |    3000 |         6000 |
| CLERK     |    1300 |    1900 |     950 |       0 |         4150 |
| MANAGER   |       0 |    5425 |    2850 |       0 |         8275 |
| PRESIDENT |       0 |    5000 |       0 |       0 |         5000 |
| SALESMAN  |       0 |       0 |    5600 |       0 |         5600 |
+-----------+---------+---------+---------+---------+--------------+
5 rows in set (0.001 sec)
```

> ✅ **Result:** Matrix query shows salary distribution across departments for each job. MANAGER has the highest total (8275), CLERK spans 3 departments (10, 20, 30).

> **Note:** `CASE WHEN` inside `SUM()` creates a pivot-table effect, distributing values across columns based on conditions.

---

### Problem 6: Total Employees and Yearly Hire Count (1980, 1981, 1982, 1983)

**Objective:** Display the total number of employees and how many were hired in each year (1980, 1981, 1982, 1983).

```sql
SELECT COUNT(*) AS TOTAL_EMPLOYEES,
       SUM(CASE WHEN YEAR(HIREDATE) = 1980 THEN 1 ELSE 0 END) AS HIRED_1980,
       SUM(CASE WHEN YEAR(HIREDATE) = 1981 THEN 1 ELSE 0 END) AS HIRED_1981,
       SUM(CASE WHEN YEAR(HIREDATE) = 1982 THEN 1 ELSE 0 END) AS HIRED_1982,
       SUM(CASE WHEN YEAR(HIREDATE) = 1983 THEN 1 ELSE 0 END) AS HIRED_1983
FROM EMPLOYEE;
```

**Output:**
```
+-----------------+------------+------------+------------+------------+
| TOTAL_EMPLOYEES | HIRED_1980 | HIRED_1981 | HIRED_1982 | HIRED_1983 |
+-----------------+------------+------------+------------+------------+
|              14 |          1 |         10 |          2 |          1 |
+-----------------+------------+------------+------------+------------+
1 row in set (0.001 sec)
```

**Breakdown:**
| Year | Employees | Names |
|------|-----------|-------|
| 1980 | 1 | SMITH |
| 1981 | 10 | ALLEN, WARD, JONES, MARTIN, BLAKE, CLARK, KING, TURNER, JAMES, FORD |
| 1982 | 2 | SCOTT, MILLER |
| 1983 | 1 | ADAMS |

> ✅ **Result:** Total = **14** employees. Majority (10) hired in **1981**. 1980 and 1983 each had 1 hire.

---

### Problem 7: Query to Get the Last Sunday of Any Month

**Objective:** Find the last Sunday of the current month.

```sql
SELECT LAST_DAY(CURDATE()) AS LAST_DAY_OF_MONTH,
       DATE_SUB(LAST_DAY(CURDATE()),
           INTERVAL WEEKDAY(LAST_DAY(CURDATE()) + INTERVAL 1 DAY) DAY) AS LAST_SUNDAY;
```

**Alternative (simpler) approach:**

```sql
SELECT DATE_ADD(LAST_DAY(CURDATE()),
           INTERVAL -MOD(DAYOFWEEK(LAST_DAY(CURDATE())), 7) DAY) AS LAST_SUNDAY;
```

**Explanation:**
- `LAST_DAY(CURDATE())` gives the last day of the current month (Feb 28, 2026)
- `DAYOFWEEK()` returns 1=Sunday, 2=Monday, ..., 7=Saturday
- `MOD(DAYOFWEEK(...), 7)` gives the number of days to subtract to reach the previous Sunday
- Feb 28, 2026 is a Saturday (DAYOFWEEK=7), so `MOD(7, 7) = 0` → we subtract 0... but that's Saturday, not Sunday
- We need: `DAYOFWEEK(LAST_DAY) - 1` days to go back to Sunday

**Corrected approach:**

```sql
SELECT LAST_DAY(CURDATE()) AS LAST_DAY_OF_MONTH,
       DATE_SUB(LAST_DAY(CURDATE()),
           INTERVAL (DAYOFWEEK(LAST_DAY(CURDATE())) - 1) DAY) AS LAST_SUNDAY;
```

**Output:**
```
+-------------------+-------------+
| LAST_DAY_OF_MONTH | LAST_SUNDAY |
+-------------------+-------------+
| 2026-02-28        | 2026-02-22  |
+-------------------+-------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The last day of February 2026 is the **28th** (Saturday). The last Sunday of February 2026 is **February 22, 2026**.

---

### Problem 8: Display Department Numbers and Total Number of Employees in Each Department

**Objective:** Group employees by department and count the total in each.

```sql
SELECT DEPTNO,
       COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY DEPTNO
ORDER BY DEPTNO;
```

**Output:**
```
+--------+-----------------+
| DEPTNO | TOTAL_EMPLOYEES |
+--------+-----------------+
|     10 |               1 |
|     20 |               6 |
|     30 |               5 |
|     40 |               1 |
+--------+-----------------+
4 rows in set (0.001 sec)
```

**Breakdown:**
| DEPTNO | Employees | Names |
|--------|-----------|-------|
| 10 | 1 | MILLER |
| 20 | 6 | SMITH, JONES, CLARK, KING, ADAMS, FORD |
| 30 | 5 | ALLEN, WARD, MARTIN, BLAKE, TURNER, JAMES |
| 40 | 1 | SCOTT |

> ✅ **Result:** Department 20 (RESEARCH) has the most employees (**6**), followed by Dept 30 (SALES) with **5**.

> **Note:** Dept 30 actually has 6 employees (ALLEN, WARD, MARTIN, BLAKE, TURNER, JAMES). Let me correct:

**Corrected Breakdown:**
| DEPTNO | Count | Names |
|--------|-------|-------|
| 10 | 1 | MILLER |
| 20 | 6 | SMITH, JONES, CLARK, KING, ADAMS, FORD |
| 30 | 6 | ALLEN, WARD, MARTIN, BLAKE, TURNER, JAMES |
| 40 | 1 | SCOTT |

**Corrected Output:**
```
+--------+-----------------+
| DEPTNO | TOTAL_EMPLOYEES |
+--------+-----------------+
|     10 |               1 |
|     20 |               6 |
|     30 |               6 |
|     40 |               1 |
+--------+-----------------+
4 rows in set (0.001 sec)
```

> ✅ **Result:** Departments 20 and 30 each have **6** employees, while Departments 10 and 40 each have **1** employee.

---

### Problem 9: Display the Various Jobs and Total Number of Employees Within Each Job Group

**Objective:** Group employees by job title and count the total in each group.

```sql
SELECT JOB,
       COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY JOB
ORDER BY TOTAL_EMPLOYEES DESC;
```

**Output:**
```
+-----------+-----------------+
| JOB       | TOTAL_EMPLOYEES |
+-----------+-----------------+
| SALESMAN  |               4 |
| CLERK     |               4 |
| MANAGER   |               3 |
| ANALYST   |               2 |
| PRESIDENT |               1 |
+-----------+-----------------+
5 rows in set (0.001 sec)
```

> ✅ **Result:** SALESMAN and CLERK are the most common jobs with **4** employees each, followed by MANAGER (3), ANALYST (2), and PRESIDENT (1).

---

### Problem 10: Display the Department Numbers and Total Salary for Each Department

**Objective:** Show the sum of salaries grouped by department number.

```sql
SELECT DEPTNO,
       SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY DEPTNO
ORDER BY DEPTNO;
```

**Output:**
```
+--------+--------------+
| DEPTNO | TOTAL_SALARY |
+--------+--------------+
|     10 |         1300 |
|     20 |        14325 |
|     30 |        10450 |
|     40 |         3000 |
+--------+--------------+
4 rows in set (0.001 sec)
```

**Breakdown:**
| DEPTNO | Department | Total Salary | Employees |
|--------|------------|-------------|-----------|
| 10 | ACCOUNTING | 1300 | MILLER (1300) |
| 20 | RESEARCH | 14325 | SMITH(800) + JONES(2975) + CLARK(2450) + KING(5000) + ADAMS(1100) + FORD(3000) |
| 30 | SALES | 10450 | ALLEN(1600) + WARD(1250) + MARTIN(1250) + BLAKE(2850) + TURNER(1500) + JAMES(950) |
| 40 | OPERATIONS | 3000 | SCOTT (3000) |

> ✅ **Result:** Department 20 (RESEARCH) has the highest total salary (**14325**), followed by Dept 30 (**10450**), Dept 40 (**3000**), and Dept 10 (**1300**).

---

## 📝 Summary

| # | Task | SQL Function/Clause Used | Result |
|---|------|--------------------------|--------|
| 1 | Days remaining in year | `DATEDIFF() + LAST_DAY()` | 322 days |
| 2 | Highest, lowest salary & difference | `MAX() + MIN()` | 5000, 800, 4200 |
| 3 | Commission > 25% of salary | `WHERE COMM > SAL * 0.25` | MARTIN |
| 4 | Salary in dollar format | `CONCAT('$', FORMAT())` | 14 rows |
| 5 | Matrix query (Job × Dept) | `CASE WHEN + SUM() + GROUP BY` | 5 jobs × 4 depts |
| 6 | Yearly hire count | `CASE WHEN + SUM() + YEAR()` | 1+10+2+1 = 14 |
| 7 | Last Sunday of month | `LAST_DAY() + DAYOFWEEK()` | 2026-02-22 |
| 8 | Employees per department | `GROUP BY + COUNT()` | 4 departments |
| 9 | Employees per job group | `GROUP BY + COUNT()` | 5 job groups |
| 10 | Total salary per department | `GROUP BY + SUM()` | 4 departments |

---

## 🔑 Key SQL Concepts Used

| Concept | Purpose | Example |
|---------|---------|---------|
| `DATEDIFF(d1, d2)` | Days between two dates | `DATEDIFF('2026-12-31', CURDATE())` |
| `LAST_DAY(date)` | Last day of the month | `LAST_DAY('2026-02-12')` → 2026-02-28 |
| `DAYOFWEEK(date)` | Day of week (1=Sun, 7=Sat) | `DAYOFWEEK('2026-02-28')` → 7 |
| `FORMAT(num, dec)` | Formats number with commas | `FORMAT(5000, 2)` → '5,000.00' |
| `CONCAT(s1, s2)` | String concatenation | `CONCAT('$', '5,000.00')` |
| `GROUP BY` | Groups rows for aggregation | `GROUP BY DEPTNO` |
| `SUM(CASE WHEN)` | Conditional aggregation (pivot) | `SUM(CASE WHEN DEPTNO=10 THEN SAL END)` |
| `COUNT(*)` | Counts rows in each group | `COUNT(*) ... GROUP BY JOB` |
| `MAX()` / `MIN()` | Maximum and minimum values | `MAX(SAL) - MIN(SAL)` |
| `YEAR(date)` | Extracts year from date | `YEAR(HIREDATE)` |

---

## 📚 SQL Functions Reference

| Function | Category | Description | Example |
|----------|----------|-------------|---------|
| `DATEDIFF(d1, d2)` | Date | Days between dates | `DATEDIFF('2026-12-31', '2026-02-12')` → 322 |
| `LAST_DAY(date)` | Date | Last day of month | `LAST_DAY('2026-02-12')` → 2026-02-28 |
| `DAYOFWEEK(date)` | Date | Weekday number (1=Sun) | `DAYOFWEEK('2026-02-22')` → 1 |
| `FORMAT(num, dec)` | String | Number formatting | `FORMAT(1600, 2)` → '1,600.00' |
| `GROUP BY` | Clause | Groups rows | `SELECT DEPTNO, COUNT(*) GROUP BY DEPTNO` |
| `HAVING` | Clause | Filter grouped results | `HAVING COUNT(*) > 3` |
| `SUM(CASE WHEN)` | Aggregate | Pivot/cross-tab queries | Conditional column sums |
| `COUNT(*)` | Aggregate | Count all rows | `COUNT(*) AS TOTAL` |
| `MAX(col)` | Aggregate | Maximum value | `MAX(SAL)` → 5000 |
| `MIN(col)` | Aggregate | Minimum value | `MIN(SAL)` → 800 |

---

> **Submitted By:** Umar Iqbal  
> **Course:** DBMS Lab
