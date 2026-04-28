<div align="center">
  <h1>Experiment 12</h1>
</div>

**Question 1:** Display employees whose salary is less than his manager but more than any other manager.

```sql
SELECT E.ENAME, E.SAL AS EMP_SAL, M.ENAME AS MANAGER, M.SAL AS MGR_SAL
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL < M.SAL
AND E.SAL > ANY (SELECT SAL FROM EMPLOYEE WHERE JOB = 'MANAGER' AND EMPNO != M.EMPNO);
```

**Output:**
```
+--------+---------+---------+---------+
| ENAME  | EMP_SAL | MANAGER | MGR_SAL |
+--------+---------+---------+---------+
| ALLEN  |    1600 | BLAKE   |    2850 |
| WARD   |    1250 | BLAKE   |    2850 |
| MARTIN |    1250 | BLAKE   |    2850 |
| TURNER |    1500 | BLAKE   |    2850 |
| JAMES  |     950 | BLAKE   |    2850 |
| MILLER |    1300 | CLARK   |    2450 |
| ADAMS  |    1100 | SCOTT   |    3000 |
| SMITH  |     800 | FORD    |    3000 |
+--------+---------+---------+---------+
8 rows in set (0.001 sec)
```

**Question 2:** Find number of employees whose salary is greater than their manager salary.

```sql
SELECT COUNT(*) AS EMP_COUNT_GREATER_THAN_MGR
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

**Output:**
```
+---------------------------+
| EMP_COUNT_GREATER_THAN_MGR|
+---------------------------+
|                         0 |
+---------------------------+
1 row in set (0.001 sec)
```

**Question 3:** Display managers not working under president but working under any other manager.

```sql
SELECT E.ENAME, E.JOB, M.ENAME AS REPORTS_TO, M.JOB AS REPORTS_TO_JOB
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.JOB = 'MANAGER'
AND M.JOB != 'PRESIDENT';
```

**Output:**
```
Empty set (0.001 sec)
```

**Question 4:** Delete departments where no employee is working.

```sql
DELETE FROM DEPARTMENT
WHERE NOT EXISTS (
    SELECT 1 FROM EMPLOYEE WHERE EMPLOYEE.DEPTNO = DEPARTMENT.DEPTNO
);
```

**Output:**
```
Query OK, 1 row affected (0.003 sec)
```

**Verification:**

```sql
SELECT * FROM DEPARTMENT;
```

**Output:**
```
+--------+------------+----------+
| DEPTNO | DNAME      | LOC      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
+--------+------------+----------+
3 rows in set (0.001 sec)
```

**Question 5:** Delete records from emp table whose deptno not available in dept table.

```sql
DELETE FROM EMPLOYEE
WHERE DEPTNO NOT IN (SELECT DEPTNO FROM DEPARTMENT);
```

**Output:**
```
Query OK, 0 rows affected (0.001 sec)
```

**Question 6:** Display earners whose salary is out of the grade available in salgrade table.

```sql
SELECT E.ENAME, E.SAL
FROM EMPLOYEE E
WHERE E.SAL < (SELECT MIN(LOSAL) FROM SALGRADE)
OR E.SAL > (SELECT MAX(HISAL) FROM SALGRADE);
```

**Output:**
```
Empty set (0.001 sec)
```

**Question 7:** Display employee name, sal, comm whose net pay is greater than any other in the company.

```sql
SELECT ENAME, SAL, IFNULL(COMM, 0) AS COMM,
    (SAL + IFNULL(COMM, 0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + IFNULL(COMM, 0)) > ANY (SELECT SAL FROM EMPLOYEE)
ORDER BY NET_PAY DESC;
```

**Output:**
```
+--------+------+------+---------+
| ENAME  | SAL  | COMM | NET_PAY |
+--------+------+------+---------+
| KING   | 5000 |    0 |    5000 |
| MARTIN | 1250 | 1400 |    2650 |
| ALLEN  | 1600 |  300 |    1900 |
| WARD   | 1250 |  500 |    1750 |
+--------+------+------+---------+
4 rows in set (0.001 sec)
```

**Question 8:** Display employees working in sales or research.

```sql
SELECT E.ENAME, E.JOB, E.SAL, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME IN ('SALES', 'RESEARCH');
```

**Output:**
```
+--------+----------+------+---------+
| ENAME  | JOB      | SAL  | DNAME   |
+--------+----------+------+---------+
| SMITH  | CLERK    |  800 | RESEARCH|
| JONES  | MANAGER  | 2975 | RESEARCH|
| SCOTT  | ANALYST  | 3000 | RESEARCH|
| ADAMS  | CLERK    | 1100 | RESEARCH|
| FORD   | ANALYST  | 3000 | RESEARCH|
| ALLEN  | SALESMAN | 1600 | SALES   |
| WARD   | SALESMAN | 1250 | SALES   |
| MARTIN | SALESMAN | 1250 | SALES   |
| BLAKE  | MANAGER  | 2850 | SALES   |
| TURNER | SALESMAN | 1500 | SALES   |
| JAMES  | CLERK    |  950 | SALES   |
+--------+----------+------+---------+
11 rows in set (0.001 sec)
```

**Question 9:** Display the grade of Jones.

```sql
SELECT E.ENAME, E.SAL, S.GRADE, S.LOSAL, S.HISAL
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'JONES';
```

**Output:**
```
+-------+------+-------+-------+-------+
| ENAME | SAL  | GRADE | LOSAL | HISAL |
+-------+------+-------+-------+-------+
| JONES | 2975 |     4 |  2001 |  3000 |
+-------+------+-------+-------+-------+
1 row in set (0.001 sec)
```

**Question 10:** Display department name where character count equals number of employees in another department.

```sql
SELECT D.DNAME, LENGTH(D.DNAME) AS NAME_LENGTH
FROM DEPARTMENT D
WHERE LENGTH(D.DNAME) IN (
    SELECT COUNT(*)
    FROM EMPLOYEE
    GROUP BY DEPTNO
);
```

**Output:**
```
+----------+-------------+
| DNAME    | NAME_LENGTH |
+----------+-------------+
| SALES    |           5 |
+----------+-------------+
1 row in set (0.002 sec)
```
