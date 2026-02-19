<div align="center">
  <h1>DBMS LAB - IILM University</h1>
  <p><strong>Umar Iqbal</strong> | 2CSE12</p>
</div>

## Repository Structure

```
DBMS LAB/
├── Lab Manual/
│   ├── LAB_ASSIGNMENT_01.md    Done
│   ├── LAB_ASSIGNMENT_02.md    Done
│   ├── LAB_ASSIGNMENT_03.md    Done
│   ├── LAB_ASSIGNMENT_04.md    Done
│   ├── LAB_ASSIGNMENT_05.md    Done
│   ├── LAB_ASSIGNMENT_06.md    Done
│   ├── LAB_ASSIGNMENT_07.md    Done
│   ├── LAB_ASSIGNMENT_08.md    Not Done
│   ├── LAB_ASSIGNMENT_09.md    Not Done
│   ├── LAB_ASSIGNMENT_10.md    Not Done
│   ├── LAB_ASSIGNMENT_11.md    Not Done
│   └── LAB_ASSIGNMENT_12.md    Not Done
│
├── Practice Set/
│   ├── Practice_Set_01.md      Database & Table Creation
│   ├── Practice_Set_02.md      Constraints & Foreign Keys
│   └── Practice_Set_03.md      Advanced Queries
│
└── README.md
```

## Lab Assignments

| # | Assignment | Topic |
|---|------------|-------|
| 1 | [LAB_ASSIGNMENT_01](Lab%20Manual/LAB_ASSIGNMENT_01.md) | DDL & DML Operations (CREATE, INSERT, UPDATE, DELETE, ALTER, DROP) |
| 2 | [LAB_ASSIGNMENT_02](Lab%20Manual/LAB_ASSIGNMENT_02.md) | Data Retrieval (SELECT, DISTINCT, WHERE, IN, BETWEEN, LIKE) |
| 3 | [LAB_ASSIGNMENT_03](Lab%20Manual/LAB_ASSIGNMENT_03.md) | Advanced Retrieval (ORDER BY, Pattern Matching, NULL Handling) |
| 4 | [LAB_ASSIGNMENT_04](Lab%20Manual/LAB_ASSIGNMENT_04.md) | String Functions, Computed Columns, UPDATE & Date Filtering |
| 5 | [LAB_ASSIGNMENT_05](Lab%20Manual/LAB_ASSIGNMENT_05.md) | Aggregate Functions (COUNT, SUM, MAX, MIN, AVG) & String Functions |
| 6 | [LAB_ASSIGNMENT_06](Lab%20Manual/LAB_ASSIGNMENT_06.md) | Date Functions (DATEDIFF, DATE_FORMAT, DAYNAME), CASE/DECODE & Subqueries |
| 7 | [LAB_ASSIGNMENT_07](Lab%20Manual/LAB_ASSIGNMENT_07.md) | Aggregate Functions, GROUP BY, Matrix Queries & Dollar Formatting |
| 8 | [LAB_ASSIGNMENT_08](Lab%20Manual/LAB_ASSIGNMENT_08.md) | JOINs (INNER, LEFT, Self-Join), SALGRADE, IFNULL & Multi-Table Queries |
| 9 | [LAB_ASSIGNMENT_09](Lab%20Manual/LAB_ASSIGNMENT_09.md) | Subqueries, Correlated Subqueries & GROUP BY with HAVING |
| 10 | [LAB_ASSIGNMENT_10](Lab%20Manual/LAB_ASSIGNMENT_10.md) | ALL/ANY Operators, Self-Joins & Complex Multi-Table Filters |
| 11 | [LAB_ASSIGNMENT_11](Lab%20Manual/LAB_ASSIGNMENT_11.md) | DELETE with JOIN, LIMIT, Manager-Employee Comparisons |
| 12 | [LAB_ASSIGNMENT_12](Lab%20Manual/LAB_ASSIGNMENT_12.md) | NOT EXISTS, String Functions & Complex Comparisons |

## Practice Sets

| # | Practice Set | Topic |
|---|--------------|-------|
| 1 | [Practice_Set_01](Practice%20Set/Practice_Set_01.md) | Database & Table Creation |
| 2 | [Practice_Set_02](Practice%20Set/Practice_Set_02.md) | Constraints, DEFAULT & FOREIGN KEY |
| 3 | [Practice_Set_03](Practice%20Set/Practice_Set_03.md) | Advanced SQL Queries |

## Database Schema

| Table | Description |
|-------|-------------|
| `DEPARTMENT` | Stores department information (DEPTNO, DNAME) |
| `EMPLOYEE` | Stores employee details (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO) |
| `SALGRADE` | Stores salary grade ranges (GRADE, LOSAL, HISAL) |

## Setup Instructions

**Prerequisites:** XAMPP (with MySQL/MariaDB)

```sql
-- Open Command Prompt and navigate to XAMPP MySQL
C:\xampp\mysql\bin> mysql -u root

-- Show all databases
SHOW DATABASES;

-- Use the lab database
USE UmarIqbalDB;

-- Show all tables
SHOW TABLES;
```

## SQL Topics Covered

**Data Definition Language (DDL):** CREATE, ALTER, DROP, TRUNCATE

**Data Manipulation Language (DML):** INSERT, UPDATE, DELETE

**Data Query Language (DQL):** SELECT, DISTINCT, WHERE, IN, NOT IN, BETWEEN, LIKE, ORDER BY, GROUP BY, HAVING

**Joins:** INNER JOIN, LEFT JOIN, RIGHT JOIN, CROSS JOIN, Self-Join

**Subqueries:** Scalar, Correlated, ANY/ALL/SOME, EXISTS/NOT EXISTS

**Aggregate Functions:** COUNT, SUM, MAX, MIN, AVG

**Constraints:** PRIMARY KEY, FOREIGN KEY, NOT NULL, UNIQUE, CHECK, DEFAULT
