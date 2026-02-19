<div align="center">
  <h1>Experiment 07</h1>
</div>

**Question 1:** Compute the no. of days remaining in this year.

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

**Question 2:** Find the highest and lowest salaries and the difference between of them.

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

**Question 3:** List employee whose commission is greater than 25% of their salaries.

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

**Question 4:** Make a query that displays salary in dollar format.

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

**Question 5:** Create a matrix query to display the job, the salary for that job based on department number, and the total salary for that job for all departments, giving each column an appropriate heading.

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

**Question 6:** Query that will display the total no of employees, and of that total the number who were hired in 1980, 1981, 1982 and 1983. Give appropriate column heading.

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

**Question 7:** Query to get the last Sunday of Any Month.

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

**Question 8:** Display department numbers and total number of employees working in each department.

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
|     30 |               6 |
|     40 |               1 |
+--------+-----------------+
4 rows in set (0.001 sec)
```

**Question 9:** Display the various jobs and total number of employees within each job group.

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

**Question 10:** Display the depart numbers and total salary for each department.

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
