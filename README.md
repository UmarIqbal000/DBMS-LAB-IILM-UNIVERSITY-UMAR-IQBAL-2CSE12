# 📚 DBMS LAB - IILM University

> **Student:** Umar Iqbal  
> **Class:** 2CSE12
> **Course:** Database Management System Lab  
> **Database:** UmarIqbalDB  
> **Server:** MariaDB 10.4.32 (XAMPP)

---

## 📁 Repository Structure

```
DBMS LAB/
├── 📂 Lab Manual/
│   ├── LAB_ASSIGNMENT_01.md    ✅ DDL & DML Operations
│   └── LAB_ASSIGNMENT_02.md    ✅ Data Retrieval Queries
│
├── 📂 Practice Set/
│   ├── Practice_Set_01.md      ✅ Database & Table Creation
│   ├── Practice_Set_02.md      ✅ Constraints & Foreign Keys
│   └── Practice_Set_03.md      ✅ Advanced Queries
│
└── README.md                   
```

---

## 📋 Lab Assignments

| # | Assignment | Topic | Status |
|---|------------|-------|--------|
| 1 | [LAB_ASSIGNMENT_01](Lab%20Manual/LAB_ASSIGNMENT_01.md) | DDL & DML Operations (CREATE, INSERT, UPDATE, DELETE, ALTER, DROP) | ✅ Completed |
| 2 | [LAB_ASSIGNMENT_02](Lab%20Manual/LAB_ASSIGNMENT_02.md) | Data Retrieval (SELECT, DISTINCT, WHERE, IN, BETWEEN, LIKE) | ✅ Completed |

---

## 📝 Practice Sets

| # | Practice Set | Topic | Status |
|---|--------------|-------|--------|
| 1 | [Practice_Set_01](Practice%20Set/Practice_Set_01.md) | Database & Table Creation | ✅ Completed |
| 2 | [Practice_Set_02](Practice%20Set/Practice_Set_02.md) | Constraints, DEFAULT & FOREIGN KEY | ✅ Completed |
| 3 | [Practice_Set_03](Practice%20Set/Practice_Set_03.md) | Advanced SQL Queries | ✅ Completed |

---

## 🗃️ Database Schema

### Tables Used

| Table | Description |
|-------|-------------|
| `DEPARTMENT` | Stores department information (DEPTNO, DNAME) |
| `EMPLOYEE` | Stores employee details (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO) |
| `Student` | Practice table for student records |

---

## 🔧 Setup Instructions

### Prerequisites
- XAMPP (with MySQL/MariaDB)
- MySQL Workbench (optional)

### Connect to Database

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

---

## 📖 SQL Topics Covered

### Data Definition Language (DDL)
- `CREATE DATABASE` / `CREATE TABLE`
- `ALTER TABLE`
- `DROP TABLE`
- `TRUNCATE TABLE`

### Data Manipulation Language (DML)
- `INSERT INTO`
- `UPDATE`
- `DELETE`

### Data Query Language (DQL)
- `SELECT` / `SELECT DISTINCT`
- `WHERE` clause with operators
- `IN`, `NOT IN`, `BETWEEN`
- `LIKE` with wildcards (`%`, `_`)
- `ORDER BY`, `GROUP BY`

### Constraints
- `PRIMARY KEY`
- `FOREIGN KEY`
- `NOT NULL`
- `UNIQUE`
- `CHECK`
- `DEFAULT`

---

## 📅 Progress Tracker

- [x] Lab Assignment 01 - DDL & DML Operations
- [x] Lab Assignment 02 - Data Retrieval Queries
- [ ] Lab Assignment 03 - *(Coming Soon)*
- [ ] Lab Assignment 04 - *(Coming Soon)*

---

## 🔗 Quick Links

| Resource | Link |
|----------|------|
| MariaDB Documentation | [https://mariadb.com/docs/](https://mariadb.com/docs/) |
| MySQL Tutorial | [https://www.w3schools.com/sql/](https://www.w3schools.com/sql/) |
| SQL Cheat Sheet | [https://www.sqltutorial.org/sql-cheat-sheet/](https://www.sqltutorial.org/sql-cheat-sheet/) |

---

> **Last Updated:** February 2026  
> **IILM University, Greater Noida** | DBMS Lab
