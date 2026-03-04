<div align="center">
  <h1>Experiment 06</h1>
</div>

**Question 1:** Display empno, ename, deptno from employee table. Instead of displaying department numbers display the related department name (Use decode function for ORACLE and CASE for MySQL).

```sql
SELECT 
    EMPNO,
    ENAME,
    CASE DEPTNO
        WHEN 10 THEN 'RESEARCH'
        WHEN 20 THEN 'ACCOUNTING'
        WHEN 30 THEN 'SALES'
        WHEN 40 THEN 'OPERATIONS'
    END AS DNAME
FROM EMPLOYEE;
```

**Output:**
```
+-------+--------+------------+
| EMPNO | ENAME  | DNAME      |
+-------+--------+------------+
|  7369 | SMITH  | ACCOUNTING |
|  7499 | ALLEN  | SALES      |
|  7521 | WARD   | SALES      |
|  7566 | JONES  | ACCOUNTING |
|  7654 | MARTIN | SALES      |
|  7698 | BLAKE  | SALES      |
|  7782 | CLARK  | ACCOUNTING |
|  7788 | SCOTT  | OPERATIONS |
|  7839 | KING   | ACCOUNTING |
|  7844 | TURNER | SALES      |
|  7876 | ADAMS  | ACCOUNTING |
|  7900 | JAMES  | SALES      |
|  7902 | FORD   | ACCOUNTING |
|  7934 | MILLER | RESEARCH   |
+-------+--------+------------+
14 rows in set (0.001 sec)
```

**Question 2:** Display your age in days.

```sql
SELECT DATEDIFF(CURDATE(), '2005-06-03') 
AS AGE_IN_DAYS;
```

**Output:**
```
+-------------+
| AGE_IN_DAYS |
+-------------+
|        7580 |
+-------------+
1 row in set (0.001 sec)
```

**Question 3:** Display your age in months.

```sql
SELECT TIMESTAMPDIFF(MONTH, '2005-06-03', CURDATE()) 
AS AGE_IN_MONTHS;
```

**Output:**
```
+---------------+
| AGE_IN_MONTHS |
+---------------+
|           249 |
+---------------+
1 row in set (0.001 sec)
```

**Question 4:** Display the current date as 15th August Friday Nineteen Ninety-Seven.

```sql
SELECT DATE_FORMAT(CURDATE(), '%D %M %W %Y') 
AS CURRENT_DATE;
```

**Output:**
```
+-------------------------------+
| CURRENT_DATE                  |
+-------------------------------+
| 5th March Thursday 2026      |
+-------------------------------+
1 row in set (0.001 sec)
```

**Question 5:** Display the following output for each row from employee table.

*Scott has joined the company on Wednesday 13th August Nineteen Ninety.*

```sql
SELECT 
CONCAT(
    ENAME,
    ' has joined the company on ',
    DATE_FORMAT(HIREDATE, '%W %D %M %Y')
) AS DETAILS
FROM EMPLOYEE
WHERE ENAME = 'SCOTT';
```

**Output:**
```
+--------------------------------------------------------------+
| DETAILS                                                      |
+--------------------------------------------------------------+
| SCOTT has joined the company on Thursday 9th December 1982   |
+--------------------------------------------------------------+
1 row in set (0.001 sec)
```

**Question 7:** Find the date for nearest Saturday after current date.

**Approach 1:** Using `WEEKDAY()`
```sql
SELECT DATE_ADD(
    '2026-02-22',
    INTERVAL MOD(5 - WEEKDAY('2026-02-22') + 7, 7) DAY
) AS NEXT_SATURDAY;
```

**Output:**
```
+---------------+
| NEXT_SATURDAY |
+---------------+
| 2026-02-28    |
+---------------+
1 row in set (0.001 sec)
```

**Approach 2:** Using `DAYOFWEEK()`
```sql
SELECT DATE_ADD(
    '2026-02-22',
    INTERVAL MOD(7 - DAYOFWEEK('2026-02-22') + 7, 7) DAY
) AS NEXT_SATURDAY;
```

**Output:**
```
+---------------+
| NEXT_SATURDAY |
+---------------+
| 2026-02-28    |
+---------------+
1 row in set (0.001 sec)
```

**Approach 3:** Using `CURDATE()`
```sql
SELECT DATE_ADD(
    CURDATE(),
    INTERVAL (5 - WEEKDAY(CURDATE())) DAY
) AS NEXT_SATURDAY;
```

**Output:**
```
+---------------+
| NEXT_SATURDAY |
+---------------+
| 2026-03-07    |
+---------------+
1 row in set (0.001 sec)
```

> **Note:** The above code (Approach 3) is correct for days less than Saturday, but when the value becomes negative, it doesn't work.

**Question 8:** Display current time.

```sql
SELECT CURTIME() AS CURRENT_TIME;
```

**Output:**
```
+--------------+
| CURRENT_TIME |
+--------------+
| 10:30:00     |
+--------------+
1 row in set (0.001 sec)
```

**Question 9:** Display the date three months before the current date.

```sql
SELECT DATE_SUB(CURDATE(), INTERVAL 3 MONTH) 
AS DATE_BEFORE_3_MONTHS;
```

**Output:**
```
+----------------------+
| DATE_BEFORE_3_MONTHS |
+----------------------+
| 2025-12-05           |
+----------------------+
1 row in set (0.001 sec)
```

**Question 10:** Display those employees who joined in the company in the month of Dec.

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

**Question 11:** Display those employees whose first 2 characters from hire date - last 2 characters of salary.

```sql
SELECT ENAME, HIREDATE, SAL
FROM EMPLOYEE
WHERE LEFT(DATE_FORMAT(HIREDATE, '%y'), 2) = RIGHT(SAL, 2);
```

**Output:**
```
Empty set (0.001 sec)
```

**Question 12:** Display those employees whose 10% of salary is equal to the year of joining.

```sql
SELECT ENAME, SAL, HIREDATE
FROM EMPLOYEE
WHERE (SAL * 0.10) = YEAR(HIREDATE);
```

**Output:**
```
Empty set (0.001 sec)
```

**Question 13:** Display those employees who joined the company before 15 of the months.

```sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE DAY(HIREDATE) < 15;
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

**Question 14:** Display those employees who has joined AFTER 15th of the month.

```sql
SELECT ENAME, HIREDATE
FROM EMPLOYEE
WHERE DAY(HIREDATE) > 15;
```

**Output:**
```
+--------+------------+
| ENAME  | HIREDATE   |
+--------+------------+
| SMITH  | 1980-12-17 |
| ALLEN  | 1981-02-20 |
| WARD   | 1981-02-22 |
| MARTIN | 1981-09-28 |
| KING   | 1981-11-17 |
| MILLER | 1982-01-23 |
+--------+------------+
6 rows in set (0.001 sec)
```

**Question 15:** Display those employees whose joining DATE is available in deptno.

```sql
SELECT ENAME, HIREDATE, DEPTNO
FROM EMPLOYEE
WHERE HIREDATE IS NOT NULL
AND DEPTNO IS NOT NULL;
```

**Output:**
```
+--------+------------+--------+
| ENAME  | HIREDATE   | DEPTNO |
+--------+------------+--------+
| SMITH  | 1980-12-17 |     20 |
| ALLEN  | 1981-02-20 |     30 |
| WARD   | 1981-02-22 |     30 |
| JONES  | 1981-04-02 |     20 |
| MARTIN | 1981-09-28 |     30 |
| BLAKE  | 1981-05-01 |     30 |
| CLARK  | 1981-06-09 |     20 |
| SCOTT  | 1982-12-09 |     40 |
| KING   | 1981-11-17 |     20 |
| TURNER | 1981-09-08 |     30 |
| ADAMS  | 1983-01-12 |     20 |
| JAMES  | 1981-12-03 |     30 |
| FORD   | 1981-12-03 |     20 |
| MILLER | 1982-01-23 |     10 |
+--------+------------+--------+
14 rows in set (0.001 sec)
```

---

### Quick Reference: DATE_ADD & DATE_SUB

**Example (Add 7 days):**
```sql
-- Syntax: DATE_ADD(date, INTERVAL value interval_type)
SELECT DATE_ADD('2025-01-01', INTERVAL 7 DAY);
```

**Example (Subtract 3 hours):**
```sql
-- Syntax: DATE_SUB(date, INTERVAL value interval_type)
SELECT DATE_SUB('2025-01-01 12:00:00', INTERVAL 3 HOUR);
```
