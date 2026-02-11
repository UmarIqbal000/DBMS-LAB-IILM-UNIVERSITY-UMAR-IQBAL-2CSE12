# 📚 DBMS LAB ASSIGNMENT 09

> **Date:** 12/February/2026
> **Database:** UmarIqbalDB
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Perform advanced SQL queries using subqueries, joins, and aggregate functions:

1. Display the name of employee who earns highest salary
2. Display the employee number and name of employee working as clerk and earning highest salary among clerks
3. Display the names of the salesman who earns a salary more than the highest salary of any clerk
4. Display the names of clerks who earn salary more than that of james and that of salary lesser than that of scott
5. Display the names of employees who earn a salary more than that of james or that of salary greater than that of scott
6. Display the names of the employees who earn highest salary in their respective departments
7. Display the names of employees who earn highest salaries in their respective job groups
8. Display the employee names who are working in accounting dept
9. Display the employee names who are working in chicago
10. Display the job groups having total salary greater than the maximum salary for managers

---

## 📊 Reference Tables

### DEPARTMENT Table

| DEPTNO | DNAME      | LOC       |
|--------|------------|-----------|
| 10     | RESEARCH   | DALLAS    |
| 20     | ACCOUNTING | NEW YORK  |
| 30     | SALES      | CHICAGO   |
| 40     | OPERATIONS | BOSTON    |

### EMPLOYEE Table

| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL  | COMM | DEPTNO |
|-------|--------|-----------|------|------------|------|------|--------|
| 7369  | SMITH  | CLERK     | 7902 | 1980-12-17 | 800  | NULL | 20     |
| 7499  | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600 | 300  | 30     |
| 7521  | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250 | 500  | 30     |
| 7566  | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975 | NULL | 20     |
| 7654  | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250 | 1400 | 30     |
| 7698  | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850 | NULL | 30     |
| 7782  | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450 | NULL | 10     |
| 7788  | SCOTT  | ANALYST   | 7566 | 1982-12-09 | 3000 | NULL | 20     |
| 7839  | KING   | PRESIDENT | NULL | 1981-11-17 | 5000 | NULL | 10     |
| 7844  | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500 | 0    | 30     |
| 7876  | ADAMS  | CLERK     | 7788 | 1983-01-12 | 1100 | NULL | 20     |
| 7900  | JAMES  | CLERK     | 7698 | 1981-12-03 | 950  | NULL | 30     |
| 7902  | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000 | NULL | 20     |
| 7934  | MILLER | CLERK     | 7782 | 1982-01-23 | 1300 | NULL | 10     |

---

## 🔧 Database Connection

```sql
-- Connect to MySQL/MariaDB
C:\xampp\mysql\bin> mysql -u root

-- Select the database
USE UmarIqbalDB;
```

---

## ✅ Problem Solutions

### Problem 1: Display the Name of Employee Who Earns Highest Salary

**Objective:** Find the employee with the maximum salary using a subquery.

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

> ✅ **Result:** KING earns the highest salary of 5000

---

### Problem 2: Employee Number and Name of Clerk Earning Highest Salary Among Clerks

**Objective:** Find the clerk with the maximum salary using a correlated subquery.

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

> ✅ **Result:** MILLER (EMPNO: 7934) is the highest paid clerk with salary 1300

---

### Problem 3: Salesman Who Earns More Than the Highest Salary of Any Clerk

**Objective:** Find salesmen earning more than the maximum clerk salary.

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

> ✅ **Result:** 2 salesmen earn more than the highest clerk salary (1300): ALLEN (1600) and TURNER (1500)

---

### Problem 4: Clerks Who Earn More Than James and Less Than Scott

**Objective:** Find clerks with salary between James' and Scott's salary (exclusive).

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

> ✅ **Result:** 2 clerks found: ADAMS (1100) and MILLER (1300) — both earn more than JAMES (950) and less than SCOTT (3000)

---

### Problem 5: Employees Who Earn More Than James or More Than Scott

**Objective:** Find employees with salary greater than either James or Scott (OR condition).

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

> ✅ **Result:** 12 employees found. Only SMITH (800) and JAMES (950) are excluded.

---

### Problem 6: Employees Who Earn Highest Salary in Their Respective Departments

**Objective:** Find top earners in each department using correlated subquery.

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

> ✅ **Result:** Highest earners by department:
> - DEPT 10 (RESEARCH): KING (5000)
> - DEPT 20 (ACCOUNTING): SCOTT and FORD (3000 each)
> - DEPT 30 (SALES): BLAKE (2850)

---

### Problem 7: Employees Who Earn Highest Salaries in Their Respective Job Groups

**Objective:** Find top earners in each job category using correlated subquery.

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

> ✅ **Result:** Highest earners by job:
> - CLERK: MILLER (1300)
> - ANALYST: SCOTT and FORD (3000)
> - MANAGER: JONES (2975)
> - PRESIDENT: KING (5000)
> - SALESMAN: ALLEN (1600)

---

### Problem 8: Employee Names Working in Accounting Department

**Objective:** Find employees in the ACCOUNTING department using JOIN.

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

> ✅ **Result:** 3 employees work in ACCOUNTING department (DEPTNO 10): CLARK, KING, and MILLER

---

### Problem 9: Employee Names Working in Chicago

**Objective:** Find employees working in Chicago location using JOIN.

```sql
SELECT E.ENAME, E.JOB, E.SAL
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.LOC = 'CHICAGO';
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

> ✅ **Result:** 6 employees work in CHICAGO (DEPTNO 30 - SALES department)

---

### Problem 10: Job Groups with Total Salary Greater Than Maximum Manager Salary

**Objective:** Find job groups where sum of salaries exceeds the highest manager salary using HAVING clause.

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

> ✅ **Result:** Maximum manager salary is 2975 (JONES). All job groups have total salary greater than 2975.

---

## 📝 Summary

| # | Task | SQL Concept Used | Records Found |
|---|------|------------------|---------------|
| 1 | Highest salary earner | `MAX()` subquery | 1 |
| 2 | Highest paid clerk | `MAX()` with filter | 1 |
| 3 | Salesmen > max clerk salary | Subquery comparison | 2 |
| 4 | Clerks between James & Scott | Multiple subqueries | 2 |
| 5 | Employees > James OR > Scott | OR with subqueries | 12 |
| 6 | Highest earners by department | Correlated subquery | 4 |
| 7 | Highest earners by job | Correlated subquery | 6 |
| 8 | Employees in ACCOUNTING | `JOIN` with filter | 3 |
| 9 | Employees in CHICAGO | `JOIN` with filter | 6 |
| 10 | Job groups by total salary | `GROUP BY`, `HAVING` | 5 |

---

## 🔑 Key SQL Concepts Used

| Concept | Purpose | Example |
|---------|---------|---------|
| **Subquery** | Query within query | `(SELECT MAX(SAL) FROM EMPLOYEE)` |
| **Correlated Subquery** | Uses outer query values | `WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE DEPTNO = E.DEPTNO)` |
| **JOIN** | Combine tables | `FROM EMPLOYEE E JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO` |
| **GROUP BY** | Group rows by column | `GROUP BY JOB` |
| **HAVING** | Filter grouped results | `HAVING SUM(SAL) > (SELECT MAX(SAL)...)` |
| **Aggregate Functions** | Calculate summaries | `MAX()`, `SUM()`, `COUNT()` |

---

## 📚 Subquery Types Reference

| Type | Description | Example |
|------|-------------|---------|
| **Scalar Subquery** | Returns single value | `(SELECT MAX(SAL) FROM EMPLOYEE)` |
| **Correlated Subquery** | References outer query | `WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE DEPTNO = E.DEPTNO)` |
| **Multiple Subqueries** | Using AND/OR | `SAL > (SELECT...) AND SAL < (SELECT...)` |

---

## 🔄 Comparison Operators with Subqueries

| Operator | Usage | Example |
|----------|-------|---------|
| `=` | Equal to single value | `SAL = (SELECT MAX(SAL)...)` |
| `>` | Greater than | `SAL > (SELECT SAL FROM...)` |
| `<` | Less than | `SAL < (SELECT SAL FROM...)` |
| `IN` | Match any in list | `DEPTNO IN (SELECT DEPTNO...)` |

---

> **Submitted By:** Umar Iqbal
> **Course:** DBMS Lab
