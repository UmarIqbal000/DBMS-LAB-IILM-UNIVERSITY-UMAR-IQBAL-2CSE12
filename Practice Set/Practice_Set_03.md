# 📝 Practice Set 03 - HW Question 2

> **Database:** UmarIqbalDB 
> **Table:** MOVIE

---

## 📋 Objective

1. Create the MOVIE table with 5 datatypes and 5 constraints
2. Insert 6 records into the table
3. Write queries to display various results

---

## 📊 Table Structure: MOVIE

| Column Name     | Data Type      | Constraints           | Description              |
|-----------------|----------------|-----------------------|--------------------------|
| MovieID         | CHAR(3)        | PRIMARY KEY           | Unique movie identifier  |
| MovieName       | VARCHAR(50)    | NOT NULL              | Name of the movie        |
| Category        | VARCHAR(20)    | NOT NULL              | Genre of the movie       |
| ReleaseDate     | DATE           | DEFAULT NULL          | Movie release date       |
| ProductionCost  | INT            | CHECK (ProductionCost > 0) | Cost of production  |
| BusinessCost    | INT            | DEFAULT NULL          | Revenue generated        |

### 5 Datatypes Used:
1. `CHAR(3)` - Fixed length string
2. `VARCHAR(50)` - Variable length string
3. `DATE` - Date values
4. `INT` - Integer numbers
5. `VARCHAR(20)` - Variable length string

### 5 Constraints Used:
1. `PRIMARY KEY` - Unique identifier
2. `NOT NULL` - Mandatory field
3. `CHECK` - Validates ProductionCost > 0
4. `DEFAULT` - Default value for NULL
5. `UNIQUE` (implicit with PRIMARY KEY)

---

## 🔧 SQL Solutions

### Q1: Create MOVIE Table

```sql
CREATE TABLE MOVIE (
    MovieID CHAR(3) PRIMARY KEY,
    MovieName VARCHAR(50) NOT NULL,
    Category VARCHAR(20) NOT NULL,
    ReleaseDate DATE DEFAULT NULL,
    ProductionCost INT CHECK (ProductionCost > 0),
    BusinessCost INT DEFAULT NULL
);
```

**Output:**
```
Query OK, 0 rows affected (0.025 sec)
```

---

### Q2: Insert Values into MOVIE Table

```sql
INSERT INTO MOVIE (MovieID, MovieName, Category, ReleaseDate, ProductionCost, BusinessCost)
VALUES
    ('001', 'Hindi_Movie', 'Musical', '2018-04-23', 124500, 130000),
    ('002', 'Tamil_Movie', 'Action', '2016-05-17', 112000, 118000),
    ('003', 'English_Movie', 'Horror', '2017-08-06', 245000, 360000),
    ('004', 'Bengali_Movie', 'Adventure', '2017-01-04', 72000, 100000),
    ('005', 'Telugu_Movie', 'Action', NULL, 100000, NULL),
    ('006', 'Punjabi_Movie', 'Comedy', NULL, 30500, NULL);
```

**Output:**
```
Query OK, 6 rows affected (0.015 sec)
Records: 6  Duplicates: 0  Warnings: 0
```

#### Verify Data:

```sql
SELECT * FROM MOVIE;
```

**Output:**
```
+---------+---------------+-----------+-------------+----------------+--------------+
| MovieID | MovieName     | Category  | ReleaseDate | ProductionCost | BusinessCost |
+---------+---------------+-----------+-------------+----------------+--------------+
| 001     | Hindi_Movie   | Musical   | 2018-04-23  |         124500 |       130000 |
| 002     | Tamil_Movie   | Action    | 2016-05-17  |         112000 |       118000 |
| 003     | English_Movie | Horror    | 2017-08-06  |         245000 |       360000 |
| 004     | Bengali_Movie | Adventure | 2017-01-04  |          72000 |       100000 |
| 005     | Telugu_Movie  | Action    | NULL        |         100000 |         NULL |
| 006     | Punjabi_Movie | Comedy    | NULL        |          30500 |         NULL |
+---------+---------------+-----------+-------------+----------------+--------------+
6 rows in set (0.001 sec)
```

---

## 📝 Q3: Query Solutions

### Q3(a): List Business Done by Movies

**Query:** Show MovieID, MovieName, and BusinessCost.

```sql
SELECT MovieID, MovieName, BusinessCost
FROM MOVIE;
```

**Output:**
```
+---------+---------------+--------------+
| MovieID | MovieName     | BusinessCost |
+---------+---------------+--------------+
| 001     | Hindi_Movie   |       130000 |
| 002     | Tamil_Movie   |       118000 |
| 003     | English_Movie |       360000 |
| 004     | Bengali_Movie |       100000 |
| 005     | Telugu_Movie  |         NULL |
| 006     | Punjabi_Movie |         NULL |
+---------+---------------+--------------+
6 rows in set (0.001 sec)
```

---

### Q3(b): List Different Categories (Using DISTINCT)

**Query:** List all unique movie categories.

```sql
SELECT DISTINCT Category
FROM MOVIE;
```

**Output:**
```
+-----------+
| Category  |
+-----------+
| Musical   |
| Action    |
| Horror    |
| Adventure |
| Comedy    |
+-----------+
5 rows in set (0.001 sec)
```

---

### Q3(c): Find Net Profit of Each Movie

**Query:** Show ID, Name, and Net Profit (BusinessCost - ProductionCost).

```sql
SELECT MovieID, MovieName, (BusinessCost - ProductionCost) AS NetProfit
FROM MOVIE;
```

**Output:**
```
+---------+---------------+-----------+
| MovieID | MovieName     | NetProfit |
+---------+---------------+-----------+
| 001     | Hindi_Movie   |      5500 |
| 002     | Tamil_Movie   |      6000 |
| 003     | English_Movie |    115000 |
| 004     | Bengali_Movie |     28000 |
| 005     | Telugu_Movie  |      NULL |
| 006     | Punjabi_Movie |      NULL |
+---------+---------------+-----------+
6 rows in set (0.001 sec)
```

#### 📌 Important Observations:

| Question | Answer |
|----------|--------|
| Is `NetProfit` now part of MOVIE table? | **No**, it's a computed/derived column |
| What is such a column called? | **Derived Column** or **Calculated Column** or **Virtual Column** |
| What about unreleased movies? | They show `NULL` (not zero) because `BusinessCost` is NULL |
| Does query show profit as zero? | **No**, it shows `NULL` because any arithmetic with NULL results in NULL |

---

### Q3(d): Movies with ProductionCost Between 80,000 and 1,25,000

**Query:** List movies where ProductionCost > 80,000 AND ProductionCost < 1,25,000.

```sql
SELECT MovieID, MovieName, ProductionCost
FROM MOVIE
WHERE ProductionCost > 80000 AND ProductionCost < 125000;
```

**Output:**
```
+---------+---------------+----------------+
| MovieID | MovieName     | ProductionCost |
+---------+---------------+----------------+
| 001     | Hindi_Movie   |         124500 |
| 002     | Tamil_Movie   |         112000 |
| 005     | Telugu_Movie  |         100000 |
+---------+---------------+----------------+
3 rows in set (0.001 sec)
```

#### Alternative using BETWEEN:

```sql
SELECT MovieID, MovieName, ProductionCost
FROM MOVIE
WHERE ProductionCost BETWEEN 80001 AND 124999;
```

---

### Q3(e): Movies in Category Comedy or Action

**Query:** List movies in Comedy or Action category.

```sql
SELECT *
FROM MOVIE
WHERE Category = 'Comedy' OR Category = 'Action';
```

**Output:**
```
+---------+---------------+----------+-------------+----------------+--------------+
| MovieID | MovieName     | Category | ReleaseDate | ProductionCost | BusinessCost |
+---------+---------------+----------+-------------+----------------+--------------+
| 002     | Tamil_Movie   | Action   | 2016-05-17  |         112000 |       118000 |
| 005     | Telugu_Movie  | Action   | NULL        |         100000 |         NULL |
| 006     | Punjabi_Movie | Comedy   | NULL        |          30500 |         NULL |
+---------+---------------+----------+-------------+----------------+--------------+
3 rows in set (0.001 sec)
```

#### Alternative using IN:

```sql
SELECT *
FROM MOVIE
WHERE Category IN ('Comedy', 'Action');
```

---

### Q3(f): Movies Not Yet Released

**Query:** List movies where ReleaseDate is NULL.

```sql
SELECT *
FROM MOVIE
WHERE ReleaseDate IS NULL;
```

**Output:**
```
+---------+---------------+----------+-------------+----------------+--------------+
| MovieID | MovieName     | Category | ReleaseDate | ProductionCost | BusinessCost |
+---------+---------------+----------+-------------+----------------+--------------+
| 005     | Telugu_Movie  | Action   | NULL        |         100000 |         NULL |
| 006     | Punjabi_Movie | Comedy   | NULL        |          30500 |         NULL |
+---------+---------------+----------+-------------+----------------+--------------+
2 rows in set (0.001 sec)
```

> ⚠️ **Note:** Use `IS NULL` instead of `= NULL` to check for NULL values.

---

## 🔑 Key Concepts Summary

| Concept | Syntax | Example |
|---------|--------|---------|
| Select Specific Columns | `SELECT col1, col2 FROM table` | `SELECT MovieID, MovieName FROM MOVIE` |
| Distinct Values | `SELECT DISTINCT col FROM table` | `SELECT DISTINCT Category FROM MOVIE` |
| Calculated Column | `SELECT (expr) AS alias` | `SELECT (BusinessCost - ProductionCost) AS NetProfit` |
| Range Condition | `WHERE col > val AND col < val` | `WHERE ProductionCost > 80000 AND ProductionCost < 125000` |
| Multiple Values | `WHERE col IN (val1, val2)` | `WHERE Category IN ('Comedy', 'Action')` |
| NULL Check | `WHERE col IS NULL` | `WHERE ReleaseDate IS NULL` |

---

> **Submitted By:** Umar Iqbal  
> **Course:** DBMS Lab
