# 📚 DBMS LAB ASSIGNMENT 11

> **Date:** 12/February/2026
> **Database:** UmarIqbalDB
> **Server:** MariaDB 10.4.32

---

## 📋 Objective

Perform advanced SQL queries using **DELETE with conditions**, **TOP/LIMIT**, **complex subqueries**, and **aggregate comparisons**:

1. Delete employees who joined before 31-Dec-82 with dept location 'NEW YORK' or 'CHICAGO'
2. Display employee name, job, deptname, location for all managers
3. Display name and salary of FORD if his salary equals high salary of his grade
4. Find out the top 5 earners of company
5. Display names of employees getting highest salary
6. Display employees whose salary equals average of maximum and minimum
7. Display dname where at least 3 employees are working
8. Display managers names whose salary is more than average salary of company
9. Display managers name whose salary is more than average salary of his employees
10. Display employee name, sal, comm and net pay where net pay >= any other employee salary

---

## 📊 Reference Tables

### DEPARTMENT Table

| DEPTNO | DNAME      | LOC       |
|--------|------------|-----------|
| 10     | ACCOUNTING | NEW YORK  |
| 20     | RESEARCH   | DALLAS    |
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

### SALGRADE Table

| GRADE | LOSAL | HISAL |
|-------|-------|-------|
| 1     | 700   | 1200  |
| 2     | 1201  | 1400  |
| 3     | 1401  | 2000  |
| 4     | 2001  | 3000  |
| 5     | 3001  | 9999  |

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

### Problem 1: Delete Employees Joined Before 31-Dec-82 in NEW YORK or CHICAGO

**Objective:** Delete employees based on hire date and department location using JOIN in DELETE.

```sql
DELETE E FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.HIREDATE < '1982-12-31'
AND D.LOC IN ('NEW YORK', 'CHICAGO');
```

> 📌 **Note:** This uses multi-table DELETE syntax. Alternatively, use a subquery:
> ```sql
> DELETE FROM EMPLOYEE
> WHERE HIREDATE < '1982-12-31'
> AND DEPTNO IN (SELECT DEPTNO FROM DEPARTMENT WHERE LOC IN ('NEW YORK', 'CHICAGO'));
> ```

**Affected Rows:**

```
Query OK, 7 rows affected (0.005 sec)
```

**Verification Query:**

```sql
SELECT E.ENAME, E.HIREDATE, D.LOC
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.LOC IN ('NEW YORK', 'CHICAGO');
```

**Output:**

```
Empty set (0.001 sec)
```

> ✅ **Result:** 7 employees deleted from NEW YORK (ACCOUNTING) and CHICAGO (SALES) who joined before 31-Dec-82.
> Deleted: ALLEN, WARD, MARTIN, BLAKE, TURNER, JAMES (from CHICAGO) and CLARK, KING, MILLER (from NEW YORK)

---

### Problem 2: Display Employee Name, Job, Deptname, Location for Managers

**Objective:** Display manager details with department information using JOIN.

```sql
SELECT E.ENAME, E.JOB, D.DNAME, D.LOC
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.JOB = 'MANAGER';
```

**Output:**

```
+-------+---------+------------+----------+
| ENAME | JOB     | DNAME      | LOC      |
+-------+---------+------------+----------+
| JONES | MANAGER | RESEARCH   | DALLAS   |
| BLAKE | MANAGER | SALES      | CHICAGO  |
| CLARK | MANAGER | ACCOUNTING | NEW YORK |
+-------+---------+------------+----------+
3 rows in set (0.001 sec)
```

> ✅ **Result:** 3 managers found with their department and location details.

---

### Problem 3: Display FORD if His Salary Equals High Salary of His Grade

**Objective:** Check if FORD's salary matches the HISAL for his salary grade.

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

> ✅ **Result:** FORD's salary (3000) exactly matches the high salary (HISAL=3000) of Grade 4.

---

### Problem 4: Find Out the Top 5 Earners of Company

**Objective:** Display top 5 highest paid employees using ORDER BY and LIMIT.

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

> ✅ **Result:** Top 5 earners: KING (5000), SCOTT/FORD (3000 each), JONES (2975), BLAKE (2850).

---

### Problem 5: Display Names of Employees Getting Highest Salary

**Objective:** Find all employees earning the maximum salary.

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

> ✅ **Result:** Only KING earns the highest salary of 5000.

---

### Problem 6: Display Employees Whose Salary Equals Average of Maximum and Minimum

**Objective:** Find employees whose salary equals (MAX_SAL + MIN_SAL) / 2.

```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL = (SELECT (MAX(SAL) + MIN(SAL)) / 2 FROM EMPLOYEE);
```

**Calculation:**
- MAX(SAL) = 5000 (KING)
- MIN(SAL) = 800 (SMITH)
- Average = (5000 + 800) / 2 = 2900

**Output:**

```
Empty set (0.001 sec)
```

> ⚠️ **Result:** No employee earns exactly 2900. JONES is closest at 2975, BLAKE at 2850.

---

### Problem 7: Display Dname Where At Least 3 Are Working

**Objective:** Find departments with 3 or more employees using GROUP BY and HAVING.

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

> ✅ **Result:** 3 departments have at least 3 employees: SALES (6), RESEARCH (5), ACCOUNTING (3).

---

### Problem 8: Display Managers Whose Salary > Average Salary of Company

**Objective:** Find managers earning more than the company average salary.

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

> ✅ **Result:** 2 managers (JONES - 2975, BLAKE - 2850) earn more than company average (2073.08).
> CLARK (2450) earns less than average.

---

### Problem 9: Display Managers Whose Salary > Average Salary of His Employees

**Objective:** Find managers who earn more than the average salary of their subordinates.

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

> ✅ **Result:** Only BLAKE (2850 > 1275) earns more than his employees' average. JONES (2975 < 3000) earns less than his employees' average (SCOTT and FORD both earn 3000).

---

### Problem 10: Display Net Pay >= Any Other Employee Salary

**Objective:** Find employees whose net pay (SAL + COMM) is greater than or equal to at least one other employee's salary.

```sql
SELECT ENAME, SAL, IFNULL(COMM, 0) AS COMM,
    (SAL + IFNULL(COMM, 0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + IFNULL(COMM, 0)) >= ANY (SELECT SAL FROM EMPLOYEE);
```

> 📌 **Note:** `>= ANY` means greater than or equal to the minimum value in the set. Since the minimum salary is 800, this will return all employees with NET_PAY >= 800.

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

> ✅ **Result:** All 14 employees qualify because their net pay is >= 800 (the minimum salary). MARTIN has highest net pay (2650) among those with commission.

---

## 📝 Summary

| # | Task | SQL Concept Used | Records Found |
|---|------|------------------|---------------|
| 1 | Delete employees by date & location | `DELETE` with `JOIN` | 7 deleted |
| 2 | Manager details with dept info | `JOIN` with filter | 3 |
| 3 | FORD salary vs grade high | `JOIN` with `CASE` | 1 |
| 4 | Top 5 earners | `ORDER BY` + `LIMIT` | 5 |
| 5 | Highest salary employees | `MAX()` subquery | 1 |
| 6 | Salary = (MAX+MIN)/2 | Aggregate calculation | 0 |
| 7 | Depts with >= 3 employees | `GROUP BY` + `HAVING` | 3 |
| 8 | Managers > company average | `AVG()` subquery | 2 |
| 9 | Managers > their employees avg | Self-`JOIN` + `HAVING` | 1 |
| 10 | Net pay >= any other salary | `>= ANY` operator | 14 |

---

## 🔑 Key SQL Concepts Used

| Concept | Purpose | Example |
|---------|---------|---------|
| **DELETE with JOIN** | Delete based on joined table | `DELETE E FROM EMPLOYEE E JOIN DEPARTMENT D...` |
| **LIMIT** | Restrict result count | `LIMIT 5` |
| **AVG()** | Calculate average | `AVG(SAL)` |
| **HAVING** | Filter grouped data | `HAVING COUNT(*) >= 3` |
| **Self-Join** | Compare manager with employees | `EMPLOYEE M JOIN EMPLOYEE E ON E.MGR = M.EMPNO` |
| **>= ANY** | Greater than minimum | `>= ANY (SELECT SAL...)` |

---

## 📚 Aggregate Functions Reference

| Function | Description | Example |
|----------|-------------|---------|
| `MAX()` | Maximum value | `MAX(SAL)` = 5000 |
| `MIN()` | Minimum value | `MIN(SAL)` = 800 |
| `AVG()` | Average value | `AVG(SAL)` = 2073.08 |
| `COUNT()` | Count rows | `COUNT(*)` = 14 |
| `SUM()` | Sum of values | `SUM(SAL)` = 29050 |

---

## 🔄 DELETE Operations Reference

| Operation | Syntax | Example |
|-----------|--------|---------|
| Simple DELETE | `DELETE FROM table WHERE...` | `DELETE FROM EMPLOYEE WHERE SAL < 1000` |
| DELETE with JOIN | `DELETE t1 FROM t1 JOIN t2...` | `DELETE E FROM EMPLOYEE E JOIN DEPT D...` |
| DELETE with Subquery | `DELETE FROM t WHERE col IN (SELECT...)` | `DELETE FROM EMP WHERE DEPTNO IN (SELECT...)` |

---

## ⚠️ Important Notes

- **Multi-table DELETE**: MySQL/MariaDB supports `DELETE t1 FROM t1 JOIN t2` syntax
- **Subquery in DELETE**: Alternative when JOIN syntax is not preferred
- **LIMIT clause**: Use to restrict rows in SELECT or DELETE (be careful with DELETE!)
- **HAVING vs WHERE**: `WHERE` filters rows before grouping, `HAVING` filters after grouping

---

> **Submitted By:** Umar Iqbal
> **Course:** DBMS Lab
