<div align="center">
  <h1>Experiment 05</h1>
</div>

**Question 1:** Display the total number of employees working in the company.

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

**Question 2:** Display the total salary being paid to all employees.

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

**Question 3:** Display the maximum salary from employee table.

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

**Question 4:** Display the minimum salary from employee table.

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

**Question 5:** Display the average salary from employee table.

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

**Question 6:** Display the maximum salary being paid to clerk.

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

**Question 7:** Display the maximum salary being paid in dept no 20.

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

**Question 8:** Display the minimum salary paid to any salesman.

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

**Question 9:** Display the average salary drawn by managers.

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

**Question 10:** Display the total salary drawn by analyst working in dept no 40.

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

**Question 11:** Display the names of the employee in Uppercase.

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

**Question 12:** Display the names of the employee in Lowercase.

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

**Question 13:** Display the names of the employee in Proper case.

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

**Question 14:** Display the length of your name using appropriate function.

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

**Question 15:** Display the length of all the employee names.

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
