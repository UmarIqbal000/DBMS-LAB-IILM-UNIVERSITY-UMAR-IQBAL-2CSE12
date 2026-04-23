<div align="center">
  <h1>Experiment 09</h1>
</div>

**Question 1:** Display the name of employee who earns highest salary.

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

**Output:**
```
+-------+------+
| ENAME | SAL  |
+-------+------+
| KING  | 5000 |
+-------+------+
1 row in set (0.001 sec)
```

**Question 2:** Display the employee number and name of employee working as clerk and earning highest salary among clerks.

```sql
SELECT EMPNO, ENAME, SAL
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

**Output:**
```
+-------+--------+------+
| EMPNO | ENAME  | SAL  |
+-------+--------+------+
|  7934 | MILLER | 1300 |
+-------+--------+------+
1 row in set (0.001 sec)
```

**Question 3:** Display the names of the salesman who earns a salary more than the highest salary of any clerk.

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE JOB = 'SALESMAN'
AND SAL > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

**Output:**
```
+--------+------+
| ENAME  | SAL  |
+--------+------+
| ALLEN  | 1600 |
| TURNER | 1500 |
+--------+------+
2 rows in set (0.001 sec)
```

**Question 4:** Display the names of clerks who earn salary more than that of James and that of salary lesser than that of Scott.

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
AND SAL < (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

**Output:**
```
+--------+------+
| ENAME  | SAL  |
+--------+------+
| ADAMS  | 1100 |
| MILLER | 1300 |
+--------+------+
2 rows in set (0.001 sec)
```

**Question 5:** Display the names of employees who earn a salary more than that of James or that of salary greater than that of Scott.

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
OR SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

**Output:**
```
+--------+------+
| ENAME  | SAL  |
+--------+------+
| ALLEN  | 1600 |
| WARD   | 1250 |
| JONES  | 2975 |
| MARTIN | 1250 |
| BLAKE  | 2850 |
| CLARK  | 2450 |
| SCOTT  | 3000 |
| KING   | 5000 |
| TURNER | 1500 |
| ADAMS  | 1100 |
| MILLER | 1300 |
| FORD   | 3000 |
+--------+------+
12 rows in set (0.001 sec)
```

**Question 6:** Display the names of employees who earn highest salary in their respective departments.

```sql
SELECT ENAME, DEPTNO, SAL
FROM EMPLOYEE E
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE DEPTNO = E.DEPTNO);
```

**Output:**
```
+--------+--------+------+
| ENAME  | DEPTNO | SAL  |
+--------+--------+------+
| KING   |     10 | 5000 |
| SCOTT  |     20 | 3000 |
| FORD   |     20 | 3000 |
| BLAKE  |     30 | 2850 |
+--------+--------+------+
4 rows in set (0.001 sec)
```

**Question 7:** Display the names of employees who earn highest salaries in their respective job groups.

```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE E
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = E.JOB);
```

**Output:**
```
+--------+-----------+------+
| ENAME  | JOB       | SAL  |
+--------+-----------+------+
| MILLER | CLERK     | 1300 |
| SCOTT  | ANALYST   | 3000 |
| FORD   | ANALYST   | 3000 |
| JONES  | MANAGER   | 2975 |
| KING   | PRESIDENT | 5000 |
| ALLEN  | SALESMAN  | 1600 |
+--------+-----------+------+
6 rows in set (0.001 sec)
```

**Question 8:** Display the employee names who are working in accounting dept.

```sql
SELECT E.ENAME, E.SAL, E.JOB
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME = 'ACCOUNTING';
```

**Output:**
```
+--------+------+-----------+
| ENAME  | SAL  | JOB       |
+--------+------+-----------+
| CLARK  | 2450 | MANAGER   |
| KING   | 5000 | PRESIDENT |
| MILLER | 1300 | CLERK     |
+--------+------+-----------+
3 rows in set (0.001 sec)
```

**Question 9:** Display the employee names who are working in Mumbai.

```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO
    FROM DEPARTMENT
    WHERE LOC = 'MUMBAI'
);
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| CLARK  |
| KING   |
| MILLER |
+--------+
3 rows in set (0.001 sec)
```

**Question 10:** Display the job groups having total salary greater than the maximum salary for managers.

```sql
SELECT JOB, SUM(SAL) AS TOTAL_SALARY, COUNT(*) AS EMP_COUNT
FROM EMPLOYEE
GROUP BY JOB
HAVING SUM(SAL) > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'MANAGER');
```

**Output:**
```
+-----------+--------------+-----------+
| JOB       | TOTAL_SALARY | EMP_COUNT |
+-----------+--------------+-----------+
| ANALYST   |         6000 |         2 |
| CLERK     |         4150 |         4 |
| MANAGER   |         8275 |         3 |
| PRESIDENT |         5000 |         1 |
| SALESMAN  |         5600 |         4 |
+-----------+--------------+-----------+
5 rows in set (0.001 sec)
```
