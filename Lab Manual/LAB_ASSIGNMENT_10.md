<div align="center">
  <h1>Experiment 10</h1>
</div>

**Question 1:** Display names of employees from department 10 with salary greater than that of ANY employee working in other departments.

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ANY (SELECT SAL FROM EMPLOYEE WHERE DEPTNO != 10);
```

**Output:**
```
+--------+------+
| ENAME  | SAL  |
+--------+------+
| CLARK  | 2450 |
| KING   | 5000 |
| MILLER | 1300 |
+--------+------+
3 rows in set (0.001 sec)
```

**Question 2:** Display names of employees from department 10 with salary greater than that of ALL employees working in other departments.

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ALL (SELECT SAL FROM EMPLOYEE WHERE DEPTNO != 10);
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

**Question 3:** Display details of employees who are in sales dept and grade is C.

```sql
SELECT E.EMPNO, E.ENAME, E.JOB, E.SAL, S.GRADE, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE D.DNAME = 'SALES'
AND S.GRADE = 'C';
```

**Output:**
```
+-------+--------+----------+------+-------+-------+
| EMPNO | ENAME  | JOB      | SAL  | GRADE | DNAME |
+-------+--------+----------+------+-------+-------+
|  7499 | ALLEN  | SALESMAN | 1600 | C     | SALES |
|  7844 | TURNER | SALESMAN | 1500 | C     | SALES |
+-------+--------+----------+------+-------+-------+
2 rows in set (0.001 sec)
```

**Question 4:** Display those who are not managers and who manages anyone.

```sql
SELECT EMPNO, ENAME, JOB
FROM EMPLOYEE
WHERE JOB != 'MANAGER'
AND EMPNO IN (SELECT MGR FROM EMPLOYEE);
```

**Output:**
```
+-------+-------+-----------+
| EMPNO | ENAME | JOB       |
+-------+-------+-----------+
|  7839 | KING  | PRESIDENT |
|  7788 | SCOTT | ANALYST   |
|  7902 | FORD  | ANALYST   |
+-------+-------+-----------+
3 rows in set (0.001 sec)
```

**Question 5:** Display employees whose manager name is JONES.

```sql
SELECT E.EMPNO, E.ENAME, E.JOB, E.SAL, M.ENAME AS MANAGER_NAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

**Output:**
```
+-------+-------+---------+------+--------------+
| EMPNO | ENAME | JOB     | SAL  | MANAGER_NAME |
+-------+-------+---------+------+--------------+
|  7788 | SCOTT | ANALYST | 3000 | JONES        |
|  7902 | FORD  | ANALYST | 3000 | JONES        |
+-------+-------+---------+------+--------------+
2 rows in set (0.001 sec)
```

**Question 6:** Display employee names who are working in sales dept.

```sql
SELECT E.ENAME, E.JOB, E.SAL
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME = 'SALES';
```

**Output:**
```
+--------+----------+------+
| ENAME  | JOB      | SAL  |
+--------+----------+------+
| ALLEN  | SALESMAN | 1600 |
| WARD   | SALESMAN | 1250 |
| MARTIN | SALESMAN | 1250 |
| BLAKE  | MANAGER  | 2850 |
| TURNER | SALESMAN | 1500 |
| JAMES  | CLERK    |  950 |
+--------+----------+------+
6 rows in set (0.001 sec)
```

**Question 7:** Display employee name, deptname, salary and comm for those sal between 2000 to 5000 while location is chennai.

```sql
SELECT E.ENAME, D.DNAME, E.SAL, IFNULL(E.COMM, 0) AS COMM
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.SAL BETWEEN 2000 AND 5000
AND D.LOCATION = 'CHENNAI';
```

**Output:**
```
+-------+----------+------+------+
| ENAME | DNAME    | SAL  | COMM |
+-------+----------+------+------+
| JONES | RESEARCH | 2975 |    0 |
| SCOTT | RESEARCH | 3000 |    0 |
| FORD  | RESEARCH | 3000 |    0 |
+-------+----------+------+------+
3 rows in set (0.001 sec)
```

**Question 8:** Display employees whose salary greater than his manager salary.

```sql
SELECT E.EMPNO, E.ENAME, E.SAL AS EMP_SAL, M.ENAME AS MANAGER, M.SAL AS MGR_SAL
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

**Output:**
```
Empty set (0.001 sec)
```

**Question 9:** Display employees who are working in the same dept where his manager is working.

```sql
SELECT E.EMPNO, E.ENAME, E.JOB, E.DEPTNO, M.ENAME AS MANAGER
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.DEPTNO = M.DEPTNO;
```

**Output:**
```
+-------+--------+---------+--------+---------+
| EMPNO | ENAME  | JOB     | DEPTNO | MANAGER |
+-------+--------+---------+--------+---------+
|  7876 | ADAMS  | CLERK   |     20 | SCOTT   |
|  7499 | ALLEN  | SALESMAN|     30 | BLAKE   |
|  7654 | MARTIN | SALESMAN|     30 | BLAKE   |
|  7844 | TURNER | SALESMAN|     30 | BLAKE   |
|  7900 | JAMES  | CLERK   |     30 | BLAKE   |
|  7934 | MILLER | CLERK   |     10 | CLARK   |
+-------+--------+---------+--------+---------+
6 rows in set (0.001 sec)
```

**Question 10:** Display grade and employees name for the dept no 10 or 30 but grade is not D, while joined the company before 31-Dec-82.

```sql
SELECT S.GRADE, E.ENAME, E.HIREDATE, E.DEPTNO, E.SAL
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.DEPTNO IN (10, 30)
AND S.GRADE != 'D'
AND E.HIREDATE < '1982-12-31'
ORDER BY S.GRADE, E.ENAME;
```

**Output:**
```
+-------+--------+------------+--------+------+
| GRADE | ENAME  | HIREDATE   | DEPTNO | SAL  |
+-------+--------+------------+--------+------+
| A     | JAMES  | 1981-12-03 |     30 |  950 |
| B     | MILLER | 1982-01-23 |     10 | 1300 |
| C     | ALLEN  | 1981-02-20 |     30 | 1600 |
| C     | MARTIN | 1981-09-28 |     30 | 1250 |
| C     | TURNER | 1981-09-08 |     30 | 1500 |
| C     | WARD   | 1981-02-22 |     30 | 1250 |
| E     | KING   | 1981-11-17 |     10 | 5000 |
+-------+--------+------------+--------+------+
7 rows in set (0.001 sec)
```
