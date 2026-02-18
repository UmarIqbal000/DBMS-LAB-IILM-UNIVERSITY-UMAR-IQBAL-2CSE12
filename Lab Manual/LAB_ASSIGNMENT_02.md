<div align="center">
  <h1>Experiment 02</h1>
</div>

**Question 1:** List all distinct jobs in EMPLOYEE.

```sql
SELECT DISTINCT JOB
FROM EMPLOYEE;
```

**Output:**
```
+-----------+
| JOB       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
5 rows in set (0.001 sec)
```

**Question 2:** List all information about employees in Department Number 30.

```sql
SELECT *
FROM EMPLOYEE
WHERE DEPTNO = 30;
```

**Output:**
```
+-------+--------+-----------+------+------------+------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+--------+-----------+------+------------+------+------+--------+
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 |  300 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 |  300 |     30 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 |    0 |     30 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+--------+-----------+------+------------+------+------+--------+
6 rows in set (0.001 sec)
```

**Question 3:** Find all department numbers with department names greater than 20.

```sql
SELECT DEPTNO, DNAME
FROM DEPARTMENT
WHERE DEPTNO > 20;
```

**Output:**
```
+--------+------------+
| DEPTNO | DNAME      |
+--------+------------+
|     30 | SALES      |
|     40 | OPERATIONS |
+--------+------------+
2 rows in set (0.001 sec)
```

**Question 4:** Find all information about managers and clerks in Department 30.

```sql
SELECT *
FROM EMPLOYEE
WHERE DEPTNO = 30
AND JOB IN ('MANAGER', 'CLERK');
```

**Output:**
```
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-05-01 | 2850 | NULL |     30 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 |  950 | NULL |     30 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
```

**Question 5:** List Employee name, Employee number, and department of all clerks.

```sql
SELECT ENAME, EMPNO, DEPTNO
FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

**Output:**
```
+--------+-------+--------+
| ENAME  | EMPNO | DEPTNO |
+--------+-------+--------+
| SMITH  |  7369 |     20 |
| ADAMS  |  7876 |     20 |
| JAMES  |  7900 |     30 |
| MILLER |  7934 |     10 |
+--------+-------+--------+
4 rows in set (0.001 sec)
```

**Question 6:** Find all managers not in Department 30.

```sql
SELECT *
FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND DEPTNO <> 30;
```

**Output:**
```
+-------+-------+---------+------+------------+------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
+-------+-------+---------+------+------------+------+------+--------+
|  7566 | JONES | MANAGER | 7839 | 1981-04-02 | 2975 | NULL |     20 |
|  7782 | CLARK | MANAGER | 7839 | 1981-06-09 | 2450 | NULL |     20 |
+-------+-------+---------+------+------------+------+------+--------+
2 rows in set (0.001 sec)
```

**Question 7:** List information about employees in Department 10 who are not managers or clerks.

```sql
SELECT *
FROM EMPLOYEE
WHERE DEPTNO = 10
AND JOB NOT IN ('MANAGER', 'CLERK');
```

**Output:**
```
Empty set (0.001 sec)
```

**Question 8:** Find employees and jobs earning between 1200 and 1400.

```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE SAL BETWEEN 1200 AND 1400;
```

**Output:**
```
+--------+----------+------+
| ENAME  | JOB      | SAL  |
+--------+----------+------+
| WARD   | SALESMAN | 1250 |
| MARTIN | SALESMAN | 1250 |
| MILLER | CLERK    | 1300 |
+--------+----------+------+
3 rows in set (0.001 sec)
```

**Question 9:** List Name and Department Number of employees who are clerks, analysts, or salesmen.

```sql
SELECT ENAME, DEPTNO
FROM EMPLOYEE
WHERE JOB IN ('CLERK', 'ANALYST', 'SALESMAN');
```

**Output:**
```
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| SMITH  |     20 |
| ALLEN  |     30 |
| WARD   |     30 |
| MARTIN |     30 |
| SCOTT  |     40 |
| TURNER |     30 |
| ADAMS  |     20 |
| JAMES  |     30 |
| FORD   |     20 |
| MILLER |     10 |
+--------+--------+
10 rows in set (0.001 sec)
```

**Question 10:** List Name and Department Number of employees whose names begin with M.

```sql
SELECT ENAME, DEPTNO
FROM EMPLOYEE
WHERE ENAME LIKE 'M%';
```

**Output:**
```
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| MARTIN |     30 |
| MILLER |     10 |
+--------+--------+
2 rows in set (0.001 sec)
```
