<div align="center">
  <h1>Experiment 08</h1>
</div>

**Table Structure for This Experiment:**
```sql
CREATE TABLE salgrade (
    grade CHAR(1),
    losal INT,
    hisal INT
);

INSERT INTO salgrade VALUES ('A', 700, 1200);
INSERT INTO salgrade VALUES ('B', 1201, 1400);
INSERT INTO salgrade VALUES ('C', 1401, 2000);
INSERT INTO salgrade VALUES ('D', 2001, 3000);
INSERT INTO salgrade VALUES ('E', 3001, 9999);

SELECT * FROM salgrade;
```

**Output:**
```
+-------+-------+-------+
| grade | losal | hisal |
+-------+-------+-------+
| A     |   700 |  1200 |
| B     |  1201 |  1400 |
| C     |  1401 |  2000 |
| D     |  2001 |  3000 |
| E     |  3001 |  9999 |
+-------+-------+-------+
```

**Question 1:** Display all employees with their dept name.

```sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
INNER JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

**Output:**
```
+--------+------------+
| ENAME  | DNAME      |
+--------+------------+
| SMITH  | RESEARCH   |
| ALLEN  | SALES      |
| WARD   | SALES      |
| JONES  | RESEARCH   |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| CLARK  | RESEARCH   |
| SCOTT  | OPERATIONS |
| KING   | RESEARCH   |
| TURNER | SALES      |
| ADAMS  | RESEARCH   |
| JAMES  | SALES      |
| FORD   | RESEARCH   |
| MILLER | ACCOUNTING |
+--------+------------+
14 rows in set (0.001 sec)
```

**Question 2:** Display those employees whose manager name is Jones, and also display their manager name.

```sql
SELECT E.ENAME AS EMPLOYEE_NAME,
       E.JOB,
       M.ENAME AS MANAGER_NAME
FROM EMPLOYEE E
INNER JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

**Output:**
```
+---------------+---------+--------------+
| EMPLOYEE_NAME | JOB     | MANAGER_NAME |
+---------------+---------+--------------+
| SCOTT         | ANALYST | JONES        |
| FORD          | ANALYST | JONES        |
+---------------+---------+--------------+
2 rows in set (0.001 sec)
```

**Question 3:** Display employee name, his job, his dept name, his manager name, his grade and make out an under department wise.

```sql
SELECT E.ENAME, E.JOB, D.DNAME,
       M.ENAME AS MANAGER,
       S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
ORDER BY D.DNAME;
```

**Output:**
```
+--------+-----------+------------+---------+-------+
| ENAME  | JOB       | DNAME      | MANAGER | GRADE |
+--------+-----------+------------+---------+-------+
| MILLER | CLERK     | ACCOUNTING | CLARK   |     2 |
| SCOTT  | ANALYST   | OPERATIONS | JONES   |     4 |
| SMITH  | CLERK     | RESEARCH   | FORD    |     1 |
| JONES  | MANAGER   | RESEARCH   | KING    |     4 |
| CLARK  | MANAGER   | RESEARCH   | KING    |     4 |
| KING   | PRESIDENT | RESEARCH   | NULL    |     5 |
| ADAMS  | CLERK     | RESEARCH   | SCOTT   |     1 |
| FORD   | ANALYST   | RESEARCH   | JONES   |     4 |
| ALLEN  | SALESMAN  | SALES      | BLAKE   |     3 |
| WARD   | SALESMAN  | SALES      | BLAKE   |     2 |
| MARTIN | SALESMAN  | SALES      | BLAKE   |     2 |
| BLAKE  | MANAGER   | SALES      | KING    |     4 |
| TURNER | SALESMAN  | SALES      | BLAKE   |     3 |
| JAMES  | CLERK     | SALES      | BLAKE   |     1 |
+--------+-----------+------------+---------+-------+
14 rows in set (0.001 sec)
```

**Question 4:** List out all the employees name, job, and salary grade and department name for everyone in the company except 'clerk'. Sort on salary display the highest salary.

```sql
SELECT E.ENAME, E.JOB, E.SAL,
       S.GRADE, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.JOB != 'CLERK'
ORDER BY E.SAL DESC;
```

**Output:**
```
+--------+-----------+------+-------+------------+
| ENAME  | JOB       | SAL  | GRADE | DNAME      |
+--------+-----------+------+-------+------------+
| KING   | PRESIDENT | 5000 |     5 | RESEARCH   |
| SCOTT  | ANALYST   | 3000 |     4 | OPERATIONS |
| FORD   | ANALYST   | 3000 |     4 | RESEARCH   |
| JONES  | MANAGER   | 2975 |     4 | RESEARCH   |
| BLAKE  | MANAGER   | 2850 |     4 | SALES      |
| CLARK  | MANAGER   | 2450 |     4 | RESEARCH   |
| ALLEN  | SALESMAN  | 1600 |     3 | SALES      |
| TURNER | SALESMAN  | 1500 |     3 | SALES      |
| WARD   | SALESMAN  | 1250 |     2 | SALES      |
| MARTIN | SALESMAN  | 1250 |     2 | SALES      |
+--------+-----------+------+-------+------------+
10 rows in set (0.001 sec)
```

**Question 5:** Display employee name, his job and his manager. Display also employees who are without manager.

```sql
SELECT E.ENAME, E.JOB,
       M.ENAME AS MANAGER
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```

**Output:**
```
+--------+-----------+---------+
| ENAME  | JOB       | MANAGER |
+--------+-----------+---------+
| SMITH  | CLERK     | FORD    |
| ALLEN  | SALESMAN  | BLAKE   |
| WARD   | SALESMAN  | BLAKE   |
| JONES  | MANAGER   | KING    |
| MARTIN | SALESMAN  | BLAKE   |
| BLAKE  | MANAGER   | KING    |
| CLARK  | MANAGER   | KING    |
| SCOTT  | ANALYST   | JONES   |
| KING   | PRESIDENT | NULL    |
| TURNER | SALESMAN  | BLAKE   |
| ADAMS  | CLERK     | SCOTT   |
| JAMES  | CLERK     | BLAKE   |
| FORD   | ANALYST   | JONES   |
| MILLER | CLERK     | CLARK   |
+--------+-----------+---------+
14 rows in set (0.001 sec)
```

**Question 6:** List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks.

```sql
SELECT E.ENAME, E.JOB,
       E.SAL * 12 AS ANNUAL_SALARY,
       E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.SAL * 12 >= 36000
   OR E.JOB != 'CLERK';
```

**Output:**
```
+--------+-----------+---------------+--------+------------+-------+
| ENAME  | JOB       | ANNUAL_SALARY | DEPTNO | DNAME      | GRADE |
+--------+-----------+---------------+--------+------------+-------+
| ALLEN  | SALESMAN  |         19200 |     30 | SALES      |     3 |
| WARD   | SALESMAN  |         15000 |     30 | SALES      |     2 |
| JONES  | MANAGER   |         35700 |     20 | RESEARCH   |     4 |
| MARTIN | SALESMAN  |         15000 |     30 | SALES      |     2 |
| BLAKE  | MANAGER   |         34200 |     30 | SALES      |     4 |
| CLARK  | MANAGER   |         29400 |     20 | RESEARCH   |     4 |
| SCOTT  | ANALYST   |         36000 |     40 | OPERATIONS |     4 |
| KING   | PRESIDENT |         60000 |     20 | RESEARCH   |     5 |
| TURNER | SALESMAN  |         18000 |     30 | SALES      |     3 |
| FORD   | ANALYST   |         36000 |     20 | RESEARCH   |     4 |
+--------+-----------+---------------+--------+------------+-------+
10 rows in set (0.001 sec)
```

**Question 7:** List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks.

```sql
SELECT E.ENAME, E.JOB,
       E.SAL * 12 AS ANNUAL_SAL,
       E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.SAL * 12 >= 30000
  AND E.JOB != 'CLERK';
```

**Output:**
```
+-------+-----------+------------+--------+------------+-------+
| ENAME | JOB       | ANNUAL_SAL | DEPTNO | DNAME      | GRADE |
+-------+-----------+------------+--------+------------+-------+
| JONES | MANAGER   |      35700 |     20 | RESEARCH   |     4 |
| BLAKE | MANAGER   |      34200 |     30 | SALES      |     4 |
| SCOTT | ANALYST   |      36000 |     40 | OPERATIONS |     4 |
| KING  | PRESIDENT |      60000 |     20 | RESEARCH   |     5 |
| FORD  | ANALYST   |      36000 |     20 | RESEARCH   |     4 |
+-------+-----------+------------+--------+------------+-------+
5 rows in set (0.001 sec)
```

**Table Modification for Question 8 onwards:**
```sql
ALTER TABLE department
ADD location VARCHAR(20);

UPDATE department SET location = 'MUMBAI'  WHERE deptno = 10;
UPDATE department SET location = 'CHENNAI' WHERE deptno = 20;
UPDATE department SET location = 'HYDERABAD' WHERE deptno = 30;
UPDATE department SET location = 'DELHI'   WHERE deptno = 40;

SELECT * FROM department;
```

**Output:**
```
+--------+------------+-----------+
| DEPTNO | DNAME      | location  |
+--------+------------+-----------+
|     10 | SALES      | MUMBAI    |
|     20 | RESEARCH   | CHENNAI   |
|     30 | SALES      | HYDERABAD |
|     40 | OPERATIONS | DELHI     |
+--------+------------+-----------+
```

**Question 8:** List out all employees by name and number along with their manager's name and number also display 'no manager' who has no manager.

```sql
SELECT E.EMPNO AS EMP_NO,
       E.ENAME AS EMP_NAME,
       IFNULL(CAST(M.EMPNO AS CHAR), 'N/A') AS MGR_NO,
       IFNULL(M.ENAME, 'NO MANAGER') AS MGR_NAME
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```

**Output:**
```
+--------+----------+--------+------------+
| EMP_NO | EMP_NAME | MGR_NO | MGR_NAME   |
+--------+----------+--------+------------+
|   7369 | SMITH    | 7902   | FORD       |
|   7499 | ALLEN    | 7698   | BLAKE      |
|   7521 | WARD     | 7698   | BLAKE      |
|   7566 | JONES    | 7839   | KING       |
|   7654 | MARTIN   | 7698   | BLAKE      |
|   7698 | BLAKE    | 7839   | KING       |
|   7782 | CLARK    | 7839   | KING       |
|   7788 | SCOTT    | 7566   | JONES      |
|   7839 | KING     | N/A    | NO MANAGER |
|   7844 | TURNER   | 7698   | BLAKE      |
|   7876 | ADAMS    | 7788   | SCOTT      |
|   7900 | JAMES    | 7698   | BLAKE      |
|   7902 | FORD     | 7566   | JONES      |
|   7934 | MILLER   | 7782   | CLARK      |
+--------+----------+--------+------------+
14 rows in set (0.001 sec)
```

**Question 9:** Select dept name, dept no and sum of sal.

```sql
SELECT D.DNAME, D.DEPTNO,
       SUM(E.SAL) AS TOTAL_SALARY
FROM DEPARTMENT D
JOIN EMPLOYEE E ON D.DEPTNO = E.DEPTNO
GROUP BY D.DEPTNO, D.DNAME
ORDER BY D.DEPTNO;
```

**Output:**
```
+------------+--------+--------------+
| DNAME      | DEPTNO | TOTAL_SALARY |
+------------+--------+--------------+
| ACCOUNTING |     10 |         1300 |
| RESEARCH   |     20 |        15325 |
| SALES      |     30 |         9400 |
| OPERATIONS |     40 |         3000 |
+------------+--------+--------------+
4 rows in set (0.001 sec)
```

**Question 10:** Display employee number, name and location of the department in which he is working.

```sql
SELECT E.EMPNO, E.ENAME, D.LOCATION
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

**Output:**
```
+-------+--------+----------+
| EMPNO | ENAME  | LOCATION |
+-------+--------+----------+
|  7369 | SMITH  | DALLAS   |
|  7499 | ALLEN  | CHICAGO  |
|  7521 | WARD   | CHICAGO  |
|  7566 | JONES  | DALLAS   |
|  7654 | MARTIN | CHICAGO  |
|  7698 | BLAKE  | CHICAGO  |
|  7782 | CLARK  | DALLAS   |
|  7788 | SCOTT  | BOSTON    |
|  7839 | KING   | DALLAS   |
|  7844 | TURNER | CHICAGO  |
|  7876 | ADAMS  | DALLAS   |
|  7900 | JAMES  | CHICAGO  |
|  7902 | FORD   | DALLAS   |
|  7934 | MILLER | NEW YORK |
+-------+--------+----------+
14 rows in set (0.001 sec)
```

**Question 11:** Display employee name and department name for each employee.

```sql
SELECT E.ENAME AS EMPLOYEE_NAME,
       D.DNAME AS DEPARTMENT_NAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
ORDER BY D.DNAME, E.ENAME;
```

**Output:**
```
+---------------+-----------------+
| EMPLOYEE_NAME | DEPARTMENT_NAME |
+---------------+-----------------+
| MILLER        | ACCOUNTING      |
| SCOTT         | OPERATIONS      |
| ADAMS         | RESEARCH        |
| CLARK         | RESEARCH        |
| FORD          | RESEARCH        |
| JONES         | RESEARCH        |
| KING          | RESEARCH        |
| SMITH         | RESEARCH        |
| ALLEN         | SALES           |
| BLAKE         | SALES           |
| JAMES         | SALES           |
| MARTIN        | SALES           |
| TURNER        | SALES           |
| WARD          | SALES           |
+---------------+-----------------+
14 rows in set (0.001 sec)
```
