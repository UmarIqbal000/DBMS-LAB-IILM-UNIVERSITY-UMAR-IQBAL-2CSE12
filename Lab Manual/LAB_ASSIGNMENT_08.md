# 📚 DBMS LAB ASSIGNMENT 08

> **Date:** 12/February/2026  
> **Database:** UmarIqbalDB  
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Perform advanced SQL **JOIN** queries on the **EMPLOYEE**, **DEPARTMENT**, and **SALGRADE** tables including INNER JOIN, LEFT JOIN, self-joins, and multi-table queries:

1. Display all employees with their dept name.
2. Display those employees whose manager names is jones, and also display their manager name.
3. Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.
4. List out all the employees name, job, and salary grade and department name for everyone in the company except 'clerk'. Sort on salary display the highest salary.
5. Display employee name, his job and his manager. Display also employees who are without manager.
6. List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks.
7. List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks.
8. List out all employees by name and number along with their manager's name and number also display 'no manager' who has no manager.
9. Select dept name, dept no and sum of sal.
10. Display employee number, name and location of the department in which he is working.
11. Display employee name and department name for each employee.

---

## 📊 Reference Tables

### EMPLOYEE Table

| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
|-------|--------|-----------|------|------------|------|------|--------|
| 7369  | SMITH  | CLERK     | 7902 | 1980-12-17 | 800  | NULL | 20     |
| 7499  | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 | 300  | 30     |
| 7521  | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 | 300  | 30     |
| 7566  | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975 | NULL | 20     |
| 7654  | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 | 30     |
| 7698  | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL | 30     |
| 7782  | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450 | NULL | 20     |
| 7788  | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL | 40     |
| 7839  | KING   | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL | 20     |
| 7844  | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 | 0    | 30     |
| 7876  | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100 | NULL | 20     |
| 7900  | JAMES  | CLERK     | 7698 | 1981-12-03 | 950  | NULL | 30     |
| 7902  | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL | 20     |
| 7934  | MILLER | CLERK     | 7782 | 1982-01-23 | 1300 | NULL | 10     |

### DEPARTMENT Table

| DEPTNO | DNAME      | LOC      |
|--------|------------|----------|
| 10     | ACCOUNTING | NEW YORK |
| 20     | RESEARCH   | DALLAS   |
| 30     | SALES      | CHICAGO  |
| 40     | OPERATIONS | BOSTON    |

### SALGRADE Table

| GRADE | LOSAL | HISAL |
|-------|-------|-------|
| 1     | 700   | 1200  |
| 2     | 1201  | 1400  |
| 3     | 1401  | 2000  |
| 4     | 2001  | 3000  |
| 5     | 3001  | 9999  |

---

## 🔧 Database Connection & Prerequisites

```sql
-- Connect to MySQL/MariaDB
C:\xampp\mysql\bin> mysql -u root

-- Select the database
USE UmarIqbalDB;
```

### Create SALGRADE Table (if not exists)

```sql
CREATE TABLE IF NOT EXISTS SALGRADE (
    GRADE INT,
    LOSAL INT,
    HISAL INT
);

INSERT INTO SALGRADE VALUES (1, 700, 1200);
INSERT INTO SALGRADE VALUES (2, 1201, 1400);
INSERT INTO SALGRADE VALUES (3, 1401, 2000);
INSERT INTO SALGRADE VALUES (4, 2001, 3000);
INSERT INTO SALGRADE VALUES (5, 3001, 9999);
```

### Add LOC Column to DEPARTMENT (if not exists)

```sql
ALTER TABLE DEPARTMENT ADD COLUMN LOC VARCHAR(20);

UPDATE DEPARTMENT SET LOC = 'NEW YORK' WHERE DEPTNO = 10;
UPDATE DEPARTMENT SET LOC = 'DALLAS' WHERE DEPTNO = 20;
UPDATE DEPARTMENT SET LOC = 'CHICAGO' WHERE DEPTNO = 30;
UPDATE DEPARTMENT SET LOC = 'BOSTON' WHERE DEPTNO = 40;
```

---

## ✅ Problem Solutions

### Problem 1: Display All Employees with Their Dept Name

**Objective:** Join EMPLOYEE and DEPARTMENT tables to show each employee with their department name.

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

> ✅ **Result:** All 14 employees displayed with their department names using INNER JOIN.

---

### Problem 2: Display Employees Whose Manager Is JONES, Along with Manager Name

**Objective:** Use a self-join to find employees managed by JONES (EMPNO 7566).

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

> ✅ **Result:** **SCOTT** and **FORD** are managed by JONES. Both are ANALYSTs reporting to JONES (EMPNO 7566).

---

### Problem 3: Display Employee Details with Job, Dept Name, Manager Name, and Grade — Department Wise

**Objective:** Multi-table join combining EMPLOYEE, DEPARTMENT, SALGRADE, and self-join for manager, ordered by department.

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

> ✅ **Result:** All 14 employees displayed with their job, department, manager, and salary grade ordered by department. KING has NULL manager (PRESIDENT). Grades range from 1 (low salary) to 5 (KING).

---

### Problem 4: List Employees (Except Clerks) with Job, Grade, and Dept Name — Sorted by Highest Salary

**Objective:** Exclude CLERKs and display remaining employees with salary grade and department, sorted by salary descending.

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

> ✅ **Result:** 10 employees (excluding 4 CLERKs: SMITH, ADAMS, JAMES, MILLER) displayed sorted by salary descending. KING tops with SAL=5000 (Grade 5).

---

### Problem 5: Display Employee Name, Job, and Manager (Including Employees Without Manager)

**Objective:** Use LEFT JOIN to include employees who have no manager (MGR is NULL).

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

> ✅ **Result:** All 14 employees displayed. **KING** (PRESIDENT) shows `NULL` as manager because he has no manager (MGR IS NULL). LEFT JOIN ensures KING is included unlike INNER JOIN.

---

### Problem 6: List Employees Who Earn 36000 a Year OR Who Are Not Clerks

**Objective:** Multi-table join with OR condition — annual salary ≥ 36000 OR job is not CLERK.

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

> ✅ **Result:** 10 employees qualify — all non-CLERKs are included (OR condition). CLERKs (SMITH, ADAMS, JAMES, MILLER) are excluded as they earn less than 36000 annually.

---

### Problem 7: List Employees Who Earn 30000 Per Year AND Are Not Clerks

**Objective:** Multi-table join with AND condition — annual salary ≥ 30000 AND job is not CLERK.

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

> ✅ **Result:** 5 employees earn ≥ 30000 annually AND are not CLERKs. CLARK (SAL=2450, annual=29400) is excluded as 29400 < 30000.

---

### Problem 8: List Employees with Manager's Name and Number — Show 'NO MANAGER' for Those Without

**Objective:** Use LEFT JOIN with IFNULL to display 'NO MANAGER' for employees without a manager.

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

> ✅ **Result:** All 14 employees listed with their managers. **KING** displays `NO MANAGER` and `N/A` for manager number using the `IFNULL()` function.

---

### Problem 9: Select Dept Name, Dept No, and Sum of Salary

**Objective:** Join DEPARTMENT with EMPLOYEE and calculate the total salary for each department.

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

**Breakdown:**
| DNAME | Employees & Salaries | Total |
|-------|----------------------|-------|
| ACCOUNTING | MILLER(1300) | 1300 |
| RESEARCH | SMITH(800) + JONES(2975) + CLARK(2450) + KING(5000) + ADAMS(1100) + FORD(3000) | 15325 |
| SALES | ALLEN(1600) + WARD(1250) + MARTIN(1250) + BLAKE(2850) + TURNER(1500) + JAMES(950) | 9400 |
| OPERATIONS | SCOTT(3000) | 3000 |

> ✅ **Result:** RESEARCH department has the highest total salary (**15325**), followed by SALES (**9400**).

---

### Problem 10: Display Employee Number, Name, and Location of Department

**Objective:** Join EMPLOYEE and DEPARTMENT to show the location (LOC) where each employee works.

```sql
SELECT E.EMPNO, E.ENAME, D.LOC
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

**Output:**
```
+-------+--------+----------+
| EMPNO | ENAME  | LOC      |
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

> ✅ **Result:** All 14 employees displayed with their department location. DALLAS has 6 employees, CHICAGO has 6, NEW YORK has 1, and BOSTON has 1.

---

### Problem 11: Display Employee Name and Department Name for Each Employee

**Objective:** Simple join between EMPLOYEE and DEPARTMENT to display names.

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

> ✅ **Result:** All 14 employees displayed with department names, sorted alphabetically by department and then by employee name.

---

## 📝 Summary

| # | Task | JOIN Type Used | Result |
|---|------|----------------|--------|
| 1 | Employees with dept name | `INNER JOIN` | 14 rows |
| 2 | Employees under manager JONES | Self-join `INNER JOIN` | 2 (SCOTT, FORD) |
| 3 | Full employee details with grade | Multi-table + Self + `LEFT JOIN` | 14 rows |
| 4 | Non-clerks with grade, sorted by salary | Multi-table `JOIN` + `ORDER BY` | 10 rows |
| 5 | Employees with/without manager | Self `LEFT JOIN` | 14 rows |
| 6 | Earn 36000/yr OR not clerk | Multi-table `JOIN` + `OR` | 10 rows |
| 7 | Earn 30000/yr AND not clerk | Multi-table `JOIN` + `AND` | 5 rows |
| 8 | Employee-Manager with 'NO MANAGER' | Self `LEFT JOIN` + `IFNULL` | 14 rows |
| 9 | Dept name & total salary | `JOIN` + `GROUP BY` + `SUM` | 4 depts |
| 10 | Employee with dept location | `JOIN` on LOC | 14 rows |
| 11 | Employee & department names | `JOIN` + `ORDER BY` | 14 rows |

---

## 🔑 Key SQL Concepts Used

| Concept | Purpose | Example |
|---------|---------|---------|
| `INNER JOIN` | Matches rows from both tables | `E JOIN D ON E.DEPTNO = D.DEPTNO` |
| `LEFT JOIN` | Includes unmatched rows from left table | `E LEFT JOIN M ON E.MGR = M.EMPNO` |
| Self-join | Joins table to itself | `EMPLOYEE E JOIN EMPLOYEE M ON E.MGR = M.EMPNO` |
| Multi-table JOIN | Joins 3+ tables | `E JOIN D ... JOIN S ...` |
| `BETWEEN` in JOIN | Range-based join condition | `E.SAL BETWEEN S.LOSAL AND S.HISAL` |
| `IFNULL(expr, alt)` | Replace NULL with value | `IFNULL(M.ENAME, 'NO MANAGER')` |
| Table Aliases | Short names for tables | `EMPLOYEE E`, `DEPARTMENT D` |
| `GROUP BY` with JOIN | Aggregate across joined tables | `GROUP BY D.DEPTNO, D.DNAME` |

---

## 📚 SQL Functions Reference

| Function | Category | Description | Example |
|----------|----------|-------------|---------|
| `INNER JOIN` | Join | Returns matching rows | `A JOIN B ON A.id = B.id` |
| `LEFT JOIN` | Join | All left rows + matches | `A LEFT JOIN B ON A.id = B.id` |
| `RIGHT JOIN` | Join | All right rows + matches | `A RIGHT JOIN B ON A.id = B.id` |
| `CROSS JOIN` | Join | Cartesian product | `A CROSS JOIN B` |
| `IFNULL(e, v)` | Function | Returns v if e is NULL | `IFNULL(NULL, 'N/A')` → 'N/A' |
| `COALESCE(e1, e2)` | Function | First non-NULL value | `COALESCE(NULL, 'X')` → 'X' |
| `BETWEEN` | Operator | Range check | `SAL BETWEEN 700 AND 1200` |
| `GROUP BY` | Clause | Groups for aggregation | `GROUP BY DEPTNO` |
| `SUM()` | Aggregate | Sum of values | `SUM(SAL)` |

---

> **Submitted By:** Umar Iqbal  
> **Course:** DBMS Lab
