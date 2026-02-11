# 📚 DBMS LAB ASSIGNMENT 06

> **Date:** 12/February/2026  
> **Database:** UmarIqbalDB  
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Perform SQL queries on the **EMPLOYEE** table using **Date Functions**, **CASE (DECODE equivalent)**, and **String Functions**:

1. Display empno, ename, deptno from employee table. Instead of display department numbers display the related department name (Use decode function).
2. Display your age in days.
3. Display your age in months.
4. Display the current date as 15th August Friday Nineteen Ninety-Seven.
5. Display the following output for each row from employee table.
6. Scott has joined the company on Wednesday 13th August Nineteen Ninety.
7. Find the date for nearest Saturday after current date.
8. Display current time.
9. Display the date three months Before the current date.
10. Display those employees who joined in the company in the month of Dec.
11. Display those employees whose first 2 characters from hire date - last 2 characters of salary.
12. Display those employees whose 10% of salary is equal to the year of joining.
13. Display those employees who joined the company before 15 of the months.
14. Display those employees who has joined before 15th of the month.
15. Display those employees whose joining DATE is available in deptno.

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

### DEPARTMENT Table

| DEPTNO | DNAME      |
|--------|------------|
| 10     | ACCOUNTING |
| 20     | RESEARCH   |
| 30     | SALES      |
| 40     | OPERATIONS |

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

### Problem 1: Display Empno, Ename, Deptno with Department Name (Using CASE/DECODE)

**Objective:** Replace department numbers with their corresponding department names using CASE (MySQL/MariaDB equivalent of Oracle's DECODE function).

```sql
SELECT EMPNO, ENAME,
       CASE DEPTNO
           WHEN 10 THEN 'ACCOUNTING'
           WHEN 20 THEN 'RESEARCH'
           WHEN 30 THEN 'SALES'
           WHEN 40 THEN 'OPERATIONS'
       END AS DEPARTMENT_NAME
FROM EMPLOYEE;
```

> **Note:** Oracle uses `DECODE(DEPTNO, 10, 'ACCOUNTING', 20, 'RESEARCH', ...)` but MySQL/MariaDB uses the `CASE WHEN` statement as the equivalent.

**Output:**
```
+-------+--------+-----------------+
| EMPNO | ENAME  | DEPARTMENT_NAME |
+-------+--------+-----------------+
|  7369 | SMITH  | RESEARCH        |
|  7499 | ALLEN  | SALES           |
|  7521 | WARD   | SALES           |
|  7566 | JONES  | RESEARCH        |
|  7654 | MARTIN | SALES           |
|  7698 | BLAKE  | SALES           |
|  7782 | CLARK  | RESEARCH        |
|  7788 | SCOTT  | OPERATIONS      |
|  7839 | KING   | RESEARCH        |
|  7844 | TURNER | SALES           |
|  7876 | ADAMS  | RESEARCH        |
|  7900 | JAMES  | SALES           |
|  7902 | FORD   | RESEARCH        |
|  7934 | MILLER | ACCOUNTING      |
+-------+--------+-----------------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** All 14 employees displayed with department names instead of numbers. CASE statement maps: 10→ACCOUNTING, 20→RESEARCH, 30→SALES, 40→OPERATIONS.

---

### Problem 2: Display Your Age in Days

**Objective:** Calculate your age in days using the DATEDIFF() function.

```sql
SELECT DATEDIFF(CURDATE(), '2005-08-15') AS AGE_IN_DAYS;
```

> **Note:** Replace `'2005-08-15'` with your actual date of birth.

**Output:**
```
+-------------+
| AGE_IN_DAYS |
+-------------+
|        7486 |
+-------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** Age in days is **7486** days (from August 15, 2005 to February 12, 2026).

---

### Problem 3: Display Your Age in Months

**Objective:** Calculate your age in months using the TIMESTAMPDIFF() function.

```sql
SELECT TIMESTAMPDIFF(MONTH, '2005-08-15', CURDATE()) AS AGE_IN_MONTHS;
```

> **Note:** Replace `'2005-08-15'` with your actual date of birth.

**Output:**
```
+---------------+
| AGE_IN_MONTHS |
+---------------+
|           245 |
+---------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** Age in months is **245** months (from August 15, 2005 to February 12, 2026).

---

### Problem 4: Display the Current Date in Formatted Style

**Objective:** Display the current date in the format: **"12th February Thursday 2026"** (equivalent to Oracle's `TO_CHAR(SYSDATE, 'DDth Month Day Year')`).

```sql
SELECT DATE_FORMAT(CURDATE(), '%D %M %W %Y') AS FORMATTED_DATE;
```

**Output:**
```
+----------------------------------+
| FORMATTED_DATE                   |
+----------------------------------+
| 12th February Thursday 2026     |
+----------------------------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** Current date displayed as **"12th February Thursday 2026"** using `DATE_FORMAT()` with `%D` (day with suffix), `%M` (month name), `%W` (weekday name), `%Y` (year).

> **Note:** Oracle equivalent: `SELECT TO_CHAR(SYSDATE, 'DDth Month Day Year') FROM DUAL;` which outputs the year in words (e.g., "Nineteen Ninety-Seven"). MySQL/MariaDB does not natively support year in words.

---

### Problem 5: Display Formatted Joining Details for Each Employee

**Objective:** Display a formatted sentence for each employee showing their joining details.

**Expected Format:** `ENAME has joined the company on DAYNAME Dth MONTHNAME YEAR`

```sql
SELECT CONCAT(ENAME, ' has joined the company on ',
       DAYNAME(HIREDATE), ' ',
       DATE_FORMAT(HIREDATE, '%D'), ' ',
       MONTHNAME(HIREDATE), ' ',
       YEAR(HIREDATE)) AS EMPLOYEE_JOINING
FROM EMPLOYEE;
```

**Output:**
```
+-----------------------------------------------------------------------+
| EMPLOYEE_JOINING                                                      |
+-----------------------------------------------------------------------+
| SMITH has joined the company on Wednesday 17th December 1980          |
| ALLEN has joined the company on Friday 20th February 1981             |
| WARD has joined the company on Sunday 22nd February 1981              |
| JONES has joined the company on Thursday 2nd April 1981               |
| MARTIN has joined the company on Monday 28th September 1981           |
| BLAKE has joined the company on Friday 1st May 1981                   |
| CLARK has joined the company on Tuesday 9th June 1981                 |
| SCOTT has joined the company on Thursday 9th December 1982            |
| KING has joined the company on Tuesday 17th November 1981             |
| TURNER has joined the company on Tuesday 8th September 1981           |
| ADAMS has joined the company on Wednesday 12th January 1983           |
| JAMES has joined the company on Thursday 3rd December 1981            |
| FORD has joined the company on Thursday 3rd December 1981             |
| MILLER has joined the company on Saturday 23rd January 1982           |
+-----------------------------------------------------------------------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** All 14 employees' joining details displayed in a readable sentence format using CONCAT, DAYNAME, DATE_FORMAT, MONTHNAME, and YEAR functions.

---

### Problem 6: Display Specific Employee Joining Detail (SCOTT)

**Objective:** Display Scott's joining information in the formatted sentence style.

```sql
SELECT CONCAT(ENAME, ' has joined the company on ',
       DAYNAME(HIREDATE), ' ',
       DATE_FORMAT(HIREDATE, '%D'), ' ',
       MONTHNAME(HIREDATE), ' ',
       YEAR(HIREDATE)) AS EMPLOYEE_JOINING
FROM EMPLOYEE
WHERE ENAME = 'SCOTT';
```

**Output:**
```
+--------------------------------------------------------------+
| EMPLOYEE_JOINING                                             |
+--------------------------------------------------------------+
| SCOTT has joined the company on Thursday 9th December 1982   |
+--------------------------------------------------------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** SCOTT joined the company on **Thursday, 9th December 1982**.

---

### Problem 7: Find the Date for Nearest Saturday After Current Date

**Objective:** Calculate the next Saturday from today's date.

```sql
SELECT CURDATE() AS TODAY,
       DATE_ADD(CURDATE(),
           INTERVAL MOD(5 - WEEKDAY(CURDATE()) + 7, 7) DAY) AS NEXT_SATURDAY;
```

**Explanation:**
- `WEEKDAY()` returns 0=Monday, 1=Tuesday, ..., 5=Saturday, 6=Sunday
- Formula `MOD(5 - WEEKDAY(CURDATE()) + 7, 7)` calculates days until next Saturday
- For Thursday (WEEKDAY=3): `MOD(5-3+7, 7)` = `MOD(9,7)` = **2 days**

**Output:**
```
+------------+---------------+
| TODAY      | NEXT_SATURDAY |
+------------+---------------+
| 2026-02-12 | 2026-02-14    |
+------------+---------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** The nearest Saturday after February 12, 2026 (Thursday) is **February 14, 2026**.

---

### Problem 8: Display Current Time

**Objective:** Display the current system time.

```sql
SELECT CURTIME() AS CURRENT_TIME;
```

**Output:**
```
+--------------+
| CURRENT_TIME |
+--------------+
| 00:29:00     |
+--------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** Current time displayed as **00:29:00** using the `CURTIME()` function.

> **Additional:** You can also use `NOW()` to get both date and time: `SELECT NOW() AS CURRENT_DATETIME;`

---

### Problem 9: Display the Date Three Months Before the Current Date

**Objective:** Calculate and display the date that is 3 months before today.

```sql
SELECT CURDATE() AS TODAY,
       DATE_SUB(CURDATE(), INTERVAL 3 MONTH) AS THREE_MONTHS_BEFORE;
```

**Output:**
```
+------------+---------------------+
| TODAY      | THREE_MONTHS_BEFORE |
+------------+---------------------+
| 2026-02-12 | 2025-11-12          |
+------------+---------------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** Three months before February 12, 2026 is **November 12, 2025**.

---

### Problem 10: Display Employees Who Joined in the Month of December

**Objective:** Retrieve employees whose hire date falls in the month of December.

```sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE MONTH(HIREDATE) = 12;
```

**Output:**
```
+-------+------------+
| ENAME | HIREDATE   |
+-------+------------+
| SMITH | 1980-12-17 |
| SCOTT | 1982-12-09 |
| JAMES | 1981-12-03 |
| FORD  | 1981-12-03 |
+-------+------------+
4 rows in set (0.001 sec)
```

> ✅ **Result:** 4 employees joined in December: SMITH (Dec 1980), SCOTT (Dec 1982), JAMES (Dec 1981), FORD (Dec 1981).

---

### Problem 11: Display First 2 Characters from Hire Date and Last 2 Characters of Salary

**Objective:** Concatenate the first 2 characters of the HIREDATE with the last 2 characters of the salary for each employee.

```sql
SELECT ENAME,
       HIREDATE,
       SAL,
       CONCAT(LEFT(HIREDATE, 2), RIGHT(CAST(SAL AS CHAR), 2)) AS RESULT
FROM EMPLOYEE;
```

**Output:**
```
+--------+------------+------+--------+
| ENAME  | HIREDATE   | SAL  | RESULT |
+--------+------------+------+--------+
| SMITH  | 1980-12-17 |  800 | 1900   |
| ALLEN  | 1981-02-20 | 1600 | 1900   |
| WARD   | 1981-02-22 | 1250 | 1950   |
| JONES  | 1981-04-02 | 2975 | 1975   |
| MARTIN | 1981-09-28 | 1250 | 1950   |
| BLAKE  | 1981-05-01 | 2850 | 1950   |
| CLARK  | 1981-06-09 | 2450 | 1950   |
| SCOTT  | 1982-12-09 | 3000 | 1900   |
| KING   | 1981-11-17 | 5000 | 1900   |
| TURNER | 1981-09-08 | 1500 | 1900   |
| ADAMS  | 1983-01-12 | 1100 | 1900   |
| JAMES  | 1981-12-03 |  950 | 1950   |
| FORD   | 1981-12-03 | 3000 | 1900   |
| MILLER | 1982-01-23 | 1300 | 1900   |
+--------+------------+------+--------+
14 rows in set (0.001 sec)
```

> ✅ **Result:** First 2 chars of HIREDATE (always '19') concatenated with last 2 chars of SAL displayed for all 14 employees.

---

### Problem 12: Display Employees Whose 10% of Salary Equals the Year of Joining

**Objective:** Find employees where 10% of their salary equals the last two digits of their joining year.

```sql
SELECT ENAME, SAL,
       SAL * 0.10 AS TEN_PERCENT,
       YEAR(HIREDATE) % 100 AS YEAR_LAST2
FROM EMPLOYEE
WHERE SAL * 0.10 = YEAR(HIREDATE) % 100;
```

**Explanation:** Since full YEAR values (1980-1983) are much larger than 10% of any salary, the comparison uses the last 2 digits of the year.

**Output:**
```
+-------+-----+-------------+------------+
| ENAME | SAL | TEN_PERCENT | YEAR_LAST2 |
+-------+-----+-------------+------------+
| SMITH | 800 |       80.00 |         80 |
+-------+-----+-------------+------------+
1 row in set (0.001 sec)
```

> ✅ **Result:** Only **SMITH** qualifies — 10% of 800 = **80**, which matches the year **1980** (last 2 digits = 80).

---

### Problem 13: Display Employees Who Joined Before 15th of the Month

**Objective:** Retrieve employees whose hire day-of-month is less than 15.

```sql
SELECT ENAME, HIREDATE, DAY(HIREDATE) AS JOIN_DAY
FROM EMPLOYEE
WHERE DAY(HIREDATE) < 15;
```

**Output:**
```
+--------+------------+----------+
| ENAME  | HIREDATE   | JOIN_DAY |
+--------+------------+----------+
| JONES  | 1981-04-02 |        2 |
| BLAKE  | 1981-05-01 |        1 |
| CLARK  | 1981-06-09 |        9 |
| SCOTT  | 1982-12-09 |        9 |
| TURNER | 1981-09-08 |        8 |
| ADAMS  | 1983-01-12 |       12 |
| JAMES  | 1981-12-03 |        3 |
| FORD   | 1981-12-03 |        3 |
+--------+------------+----------+
8 rows in set (0.001 sec)
```

> ✅ **Result:** 8 employees joined before the 15th of their respective months.

---

### Problem 14: Display Employees Who Joined Before 15th of the Month

**Objective:** Retrieve employees who joined on a day earlier than the 15th of the month (alternative approach using DATE_FORMAT).

```sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE DATE_FORMAT(HIREDATE, '%d') < 15;
```

**Output:**
```
+--------+------------+
| ENAME  | HIREDATE   |
+--------+------------+
| JONES  | 1981-04-02 |
| BLAKE  | 1981-05-01 |
| CLARK  | 1981-06-09 |
| SCOTT  | 1982-12-09 |
| TURNER | 1981-09-08 |
| ADAMS  | 1983-01-12 |
| JAMES  | 1981-12-03 |
| FORD   | 1981-12-03 |
+--------+------------+
8 rows in set (0.001 sec)
```

> ✅ **Result:** Same 8 employees as Problem 13, using `DATE_FORMAT('%d')` as an alternative to `DAY()`.

> **Note:** Both `DAY(HIREDATE)` and `DATE_FORMAT(HIREDATE, '%d')` extract the day of the month. Employees NOT in the list (SMITH-17th, ALLEN-20th, WARD-22nd, MARTIN-28th, KING-17th, MILLER-23rd) joined on or after the 15th.

---

### Problem 15: Display Employees Whose Joining DATE Is Available in DEPTNO

**Objective:** Find employees where the day-of-month from their hire date matches any existing department number.

```sql
SELECT ENAME, HIREDATE, DAY(HIREDATE) AS JOIN_DAY, DEPTNO
FROM EMPLOYEE
WHERE DAY(HIREDATE) IN (SELECT DEPTNO FROM DEPARTMENT);
```

**Explanation:** DEPARTMENT table has DEPTNO values: 10, 20, 30, 40. We check if the day portion of HIREDATE matches any of these values.

**Output:**
```
+-------+------------+----------+--------+
| ENAME | HIREDATE   | JOIN_DAY | DEPTNO |
+-------+------------+----------+--------+
| ALLEN | 1981-02-20 |       20 |     30 |
+-------+------------+----------+--------+
1 row in set (0.001 sec)
```

> ✅ **Result:** Only **ALLEN** qualifies — joined on the **20th** of February 1981, and **20** is a valid DEPTNO in the DEPARTMENT table. No other employee's hire day matches any DEPTNO (10, 20, 30, 40).

---

## 📝 Summary

| # | Task | SQL Function Used | Result |
|---|------|-------------------|--------|
| 1 | Department name using CASE | `CASE WHEN` | 14 rows |
| 2 | Age in days | `DATEDIFF()` | 7486 days |
| 3 | Age in months | `TIMESTAMPDIFF()` | 245 months |
| 4 | Formatted current date | `DATE_FORMAT()` | Formatted string |
| 5 | Formatted joining details (all) | `CONCAT() + DAYNAME() + MONTHNAME()` | 14 rows |
| 6 | Formatted joining detail (SCOTT) | `CONCAT() + DAYNAME() + MONTHNAME()` | 1 row |
| 7 | Next Saturday | `DATE_ADD() + WEEKDAY()` | 2026-02-14 |
| 8 | Current time | `CURTIME()` | 00:29:00 |
| 9 | 3 months before current date | `DATE_SUB()` | 2025-11-12 |
| 10 | Employees joined in December | `MONTH()` | 4 employees |
| 11 | First 2 chars of date + last 2 of salary | `LEFT() + RIGHT() + CONCAT()` | 14 rows |
| 12 | 10% of SAL = year of joining | Arithmetic + `YEAR()` | SMITH |
| 13 | Joined before 15th (using DAY) | `DAY()` | 8 employees |
| 14 | Joined before 15th (using DATE_FORMAT) | `DATE_FORMAT('%d')` | 8 employees |
| 15 | Hire day matches DEPTNO | `DAY() + Subquery` | ALLEN |

---

## 🔑 Key SQL Concepts Used

| Concept | Purpose | Example |
|---------|---------|---------|
| `CASE WHEN` | Conditional logic (DECODE equivalent) | `CASE DEPTNO WHEN 10 THEN 'ACCOUNTING' END` |
| `DATEDIFF(d1, d2)` | Difference between two dates in days | `DATEDIFF(CURDATE(), '2005-08-15')` |
| `TIMESTAMPDIFF(unit, d1, d2)` | Difference in specified unit | `TIMESTAMPDIFF(MONTH, '2005-08-15', CURDATE())` |
| `DATE_FORMAT(date, fmt)` | Formats a date value | `DATE_FORMAT(CURDATE(), '%D %M %W %Y')` |
| `DAYNAME(date)` | Returns day of week name | `DAYNAME('1982-12-09')` → Thursday |
| `MONTHNAME(date)` | Returns month name | `MONTHNAME('1982-12-09')` → December |
| `CURDATE()` | Returns current date | `SELECT CURDATE()` |
| `CURTIME()` | Returns current time | `SELECT CURTIME()` |
| `DATE_ADD(date, INTERVAL)` | Adds interval to date | `DATE_ADD(CURDATE(), INTERVAL 2 DAY)` |
| `DATE_SUB(date, INTERVAL)` | Subtracts interval from date | `DATE_SUB(CURDATE(), INTERVAL 3 MONTH)` |
| `WEEKDAY(date)` | Returns weekday index (0=Mon) | `WEEKDAY('2026-02-12')` → 3 |
| `MONTH(date)` | Extracts month number | `MONTH('1981-12-03')` → 12 |
| `DAY(date)` | Extracts day of month | `DAY('1981-02-20')` → 20 |
| `YEAR(date)` | Extracts year | `YEAR('1980-12-17')` → 1980 |
| `CONCAT(s1, s2, ...)` | Concatenates strings | `CONCAT('A', ' ', 'B')` → 'A B' |

---

## 📚 SQL Functions Reference

| Function | Category | Description | Example |
|----------|----------|-------------|---------|
| `CASE WHEN` | Conditional | Equivalent to Oracle DECODE | `CASE col WHEN val THEN result END` |
| `DATEDIFF(d1, d2)` | Date | Days between two dates | `DATEDIFF('2026-02-12', '2005-08-15')` → 7486 |
| `TIMESTAMPDIFF(unit, d1, d2)` | Date | Difference in unit | `TIMESTAMPDIFF(MONTH, d1, d2)` |
| `DATE_FORMAT(date, fmt)` | Date | Format date as string | `DATE_FORMAT(CURDATE(), '%D %M')` |
| `DAYNAME(date)` | Date | Day name of the week | `DAYNAME('2026-02-12')` → Thursday |
| `MONTHNAME(date)` | Date | Full month name | `MONTHNAME('2026-02-12')` → February |
| `CURDATE()` | Date | Current date | Returns `2026-02-12` |
| `CURTIME()` | Date | Current time | Returns `HH:MM:SS` |
| `NOW()` | Date | Current date and time | Returns `2026-02-12 00:29:00` |
| `DATE_ADD()` | Date | Add interval to date | `DATE_ADD(d, INTERVAL 3 MONTH)` |
| `DATE_SUB()` | Date | Subtract interval from date | `DATE_SUB(d, INTERVAL 3 MONTH)` |
| `WEEKDAY()` | Date | Weekday index (0=Mon, 6=Sun) | `WEEKDAY('2026-02-14')` → 5 (Sat) |
| `LEFT(str, n)` | String | First n characters | `LEFT('1980-12-17', 2)` → '19' |
| `RIGHT(str, n)` | String | Last n characters | `RIGHT('800', 2)` → '00' |

---

> **Submitted By:** Umar Iqbal  
> **Course:** DBMS Lab
