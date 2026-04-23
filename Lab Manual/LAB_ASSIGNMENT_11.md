<div align="center">
  <h1>Experiment 11</h1>
</div>

**Question 1:** Delete those employees who joined the company before 31-dec-82 while there dept location is 'Mumbai' or 'Delhi'.

```sql
DELETE E FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.HIREDATE < '1982-12-31'
AND D.LOCATION IN ('MUMBAI', 'DELHI');
```

**Output:**
```
Query OK, 7 rows affected (0.005 sec)
```

**Question 2:** Display employee name, job, deptname, location for all managers.

```sql
SELECT E.ENAME, E.JOB, D.DNAME, D.LOCATION
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.JOB = 'MANAGER';
```

**Output:**
```
+-------+---------+------------+----------+
| ENAME | JOB     | DNAME      | LOCATION |
+-------+---------+------------+----------+
| JONES | MANAGER | RESEARCH   | DALLAS   |
| BLAKE | MANAGER | SALES      | CHICAGO  |
| CLARK | MANAGER | ACCOUNTING | NEW YORK |
+-------+---------+------------+----------+
3 rows in set (0.001 sec)
```

**Question 3:** Display name and salary of FORD if his salary equals high salary of his grade.

```sql
SELECT E.ENAME, E.SAL, S.GRADE, S.HISAL,
    CASE
        WHEN E.SAL = S.HISAL THEN 'YES - Matches High Salary'
        ELSE 'NO - Does Not Match'
    END AS STATUS
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'FORD';
```

**Output:**
```
+-------+------+-------+-------+---------------------------+
| ENAME | SAL  | GRADE | HISAL | STATUS                    |
+-------+------+-------+-------+---------------------------+
| FORD  | 3000 |     4 |  3000 | YES - Matches High Salary |
+-------+------+-------+-------+---------------------------+
1 row in set (0.001 sec)
```

**Question 4:** Find out the top 5 earners of company.

```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
ORDER BY SAL DESC
LIMIT 5;
```

**Output:**
```
+--------+-----------+------+
| ENAME  | JOB       | SAL  |
+--------+-----------+------+
| KING   | PRESIDENT | 5000 |
| SCOTT  | ANALYST   | 3000 |
| FORD   | ANALYST   | 3000 |
| JONES  | MANAGER   | 2975 |
| BLAKE  | MANAGER   | 2850 |
+--------+-----------+------+
5 rows in set (0.001 sec)
```

**Question 5:** Display names of employees getting highest salary.

```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

**Output:**
```
+-------+-----------+------+
| ENAME | JOB       | SAL  |
+-------+-----------+------+
| KING  | PRESIDENT | 5000 |
+-------+-----------+------+
1 row in set (0.001 sec)
```

**Question 6:** Display employees whose salary equals average of maximum and minimum.

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL = (SELECT (MAX(SAL) + MIN(SAL)) / 2 FROM EMPLOYEE);
```

**Output:**
```
Empty set (0.001 sec)
```

**Question 7:** Display dname where at least 3 employees are working.

```sql
SELECT D.DNAME, COUNT(*) AS EMP_COUNT
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
GROUP BY D.DNAME
HAVING COUNT(*) >= 3;
```

**Output:**
```
+------------+-----------+
| DNAME      | EMP_COUNT |
+------------+-----------+
| ACCOUNTING |         3 |
| RESEARCH   |         5 |
| SALES      |         6 |
+------------+-----------+
3 rows in set (0.001 sec)
```

**Question 8:** Display managers names whose salary is more than average salary of company.

```sql
SELECT ENAME, JOB, SAL,
    (SELECT AVG(SAL) FROM EMPLOYEE) AS AVG_SALARY
FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
```

**Output:**
```
+-------+---------+------+-------------+
| ENAME | JOB     | SAL  | AVG_SALARY  |
+-------+---------+------+-------------+
| JONES | MANAGER | 2975 | 2073.076923 |
| BLAKE | MANAGER | 2850 | 2073.076923 |
+-------+---------+------+-------------+
2 rows in set (0.001 sec)
```

**Question 9:** Display managers name whose salary is more than average salary of his employees.

```sql
SELECT M.ENAME AS MANAGER, M.SAL AS MGR_SAL,
    AVG(E.SAL) AS AVG_EMP_SAL,
    COUNT(E.EMPNO) AS NUM_EMPLOYEES
FROM EMPLOYEE M
JOIN EMPLOYEE E ON E.MGR = M.EMPNO
WHERE M.JOB = 'MANAGER'
GROUP BY M.EMPNO, M.ENAME, M.SAL
HAVING M.SAL > AVG(E.SAL);
```

**Output:**
```
+---------+---------+-------------+---------------+
| MANAGER | MGR_SAL | AVG_EMP_SAL | NUM_EMPLOYEES |
+---------+---------+-------------+---------------+
| BLAKE   |    2850 | 1275.000000 |             4 |
| JONES   |    2975 | 3000.000000 |             2 |
+---------+---------+-------------+---------------+
2 rows in set (0.001 sec)
```

**Question 10:** Display employee name, sal, comm and net pay where net pay >= any other employee salary.

```sql
SELECT ENAME, SAL, IFNULL(COMM, 0) AS COMM,
    (SAL + IFNULL(COMM, 0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + IFNULL(COMM, 0)) >= ANY (SELECT SAL FROM EMPLOYEE);
```

**Output:**
```
+--------+------+------+---------+
| ENAME  | SAL  | COMM | NET_PAY |
+--------+------+------+---------+
| SMITH  |  800 |    0 |     800 |
| ALLEN  | 1600 |  300 |    1900 |
| WARD   | 1250 |  500 |    1750 |
| JONES  | 2975 |    0 |    2975 |
| MARTIN | 1250 | 1400 |    2650 |
| BLAKE  | 2850 |    0 |    2850 |
| CLARK  | 2450 |    0 |    2450 |
| SCOTT  | 3000 |    0 |    3000 |
| KING   | 5000 |    0 |    5000 |
| TURNER | 1500 |    0 |    1500 |
| ADAMS  | 1100 |    0 |    1100 |
| JAMES  |  950 |    0 |     950 |
| FORD   | 3000 |    0 |    3000 |
| MILLER | 1300 |    0 |    1300 |
+--------+------+------+---------+
14 rows in set (0.001 sec)
```
