<div align="center">
  <h1>Experiment 06</h1>
</div>

**Question 1:** Display empno, ename, deptno from employee table. Instead of displaying department numbers display the related department name (Use decode function).

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

**Question 2:** Display your age in days.

```sql
SELECT DATEDIFF(CURDATE(), '2005-08-15') AS AGE_IN_DAYS;
```

**Output:**
```
+-------------+
| AGE_IN_DAYS |
+-------------+
|        7486 |
+-------------+
1 row in set (0.001 sec)
```

**Question 3:** Display your age in months.

```sql
SELECT TIMESTAMPDIFF(MONTH, '2005-08-15', CURDATE()) AS AGE_IN_MONTHS;
```

**Output:**
```
+---------------+
| AGE_IN_MONTHS |
+---------------+
|           245 |
+---------------+
1 row in set (0.001 sec)
```

**Question 4:** Display the current date as 15th August Friday Nineteen Ninety-Seven.

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

**Question 5:** Display the following output for each row from employee table: ENAME has joined the company on DAYNAME Dth MONTHNAME YEAR.

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

**Question 6:** Scott has joined the company on Wednesday 13th August Nineteen Ninety.

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

**Question 7:** Find the date for nearest Saturday after current date.

```sql
SELECT CURDATE() AS TODAY,
       DATE_ADD(CURDATE(),
           INTERVAL MOD(5 - WEEKDAY(CURDATE()) + 7, 7) DAY) AS NEXT_SATURDAY;
```

**Output:**
```
+------------+---------------+
| TODAY      | NEXT_SATURDAY |
+------------+---------------+
| 2026-02-12 | 2026-02-14    |
+------------+---------------+
1 row in set (0.001 sec)
```

**Question 8:** Display current time.

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

**Question 9:** Display the date three months before the current date.

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

**Question 12:** Display those employees whose 10% of salary is equal to the year of joining.

```sql
SELECT ENAME, SAL,
       SAL * 0.10 AS TEN_PERCENT,
       YEAR(HIREDATE) % 100 AS YEAR_LAST2
FROM EMPLOYEE
WHERE SAL * 0.10 = YEAR(HIREDATE) % 100;
```

**Output:**
```
+-------+-----+-------------+------------+
| ENAME | SAL | TEN_PERCENT | YEAR_LAST2 |
+-------+-----+-------------+------------+
| SMITH | 800 |       80.00 |         80 |
+-------+-----+-------------+------------+
1 row in set (0.001 sec)
```

**Question 13:** Display those employees who joined the company before 15 of the months.

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

**Question 14:** Display those employees who has joined before 15th of the month.

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

**Question 15:** Display those employees whose joining DATE is available in deptno.

```sql
SELECT ENAME, HIREDATE, DAY(HIREDATE) AS JOIN_DAY, DEPTNO
FROM EMPLOYEE
WHERE DAY(HIREDATE) IN (SELECT DEPTNO FROM DEPARTMENT);
```

**Output:**
```
+-------+------------+----------+--------+
| ENAME | HIREDATE   | JOIN_DAY | DEPTNO |
+-------+------------+----------+--------+
| ALLEN | 1981-02-20 |       20 |     30 |
+-------+------------+----------+--------+
1 row in set (0.001 sec)
```
