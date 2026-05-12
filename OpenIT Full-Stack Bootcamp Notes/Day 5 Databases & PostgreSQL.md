# Day 5 Databases & PostgreSQL

Tags: #openit-bootcamp #postgresql #sql #database #relational-model #schema-design #joins #indexes #normalization #obsidian

---

# Navigation

## A. Study Path and Big Picture

- [[#0. Suggested Study Path|0. Suggested Study Path]]
- [[#1. Session Overview|1. Session Overview]]
- [[#2. Why a Database|2. Why a Database]]
- [[#3. Static Lists vs PostgreSQL|3. Static Lists vs PostgreSQL]]
- [[#4. Core Mental Model|4. Core Mental Model]]

## B. Relational Model

- [[#5. Relational Model Core Concepts|5. Relational Model Core Concepts]]
- [[#6. Table, Row, Column, and Schema|6. Table, Row, Column, and Schema]]
- [[#7. Primary Keys and Foreign Keys|7. Primary Keys and Foreign Keys]]
- [[#8. Relationships Between Tables|8. Relationships Between Tables]]
- [[#9. Relational Model Compared to CSharp Classes|9. Relational Model Compared to CSharp Classes]]

## C. PostgreSQL Setup

- [[#10. PostgreSQL Installation Basics|10. PostgreSQL Installation Basics]]
- [[#11. Connecting with psql|11. Connecting with psql]]
- [[#12. pgAdmin Basics|12. pgAdmin Basics]]
- [[#13. Setup Tips and Common Mistakes|13. Setup Tips and Common Mistakes]]

## D. PostgreSQL Data Types

- [[#14. Data Types Overview|14. Data Types Overview]]
- [[#15. Numeric and Boolean Types|15. Numeric and Boolean Types]]
- [[#16. Text Types|16. Text Types]]
- [[#17. Date and Time Types|17. Date and Time Types]]
- [[#18. UUID, JSONB, and Arrays|18. UUID, JSONB, and Arrays]]
- [[#19. PostgreSQL to CSharp Type Mapping|19. PostgreSQL to CSharp Type Mapping]]
- [[#20. Data Type Tips|20. Data Type Tips]]

## E. Schema Design and Constraints

- [[#21. CREATE TABLE Basics|21. CREATE TABLE Basics]]
- [[#22. Library Schema Example|22. Library Schema Example]]
- [[#23. Constraint Quick Reference|23. Constraint Quick Reference]]
- [[#24. CHECK and DEFAULT Constraints|24. CHECK and DEFAULT Constraints]]
- [[#25. ON DELETE Behavior|25. ON DELETE Behavior]]
- [[#26. Schema Design Tips|26. Schema Design Tips]]

## F. SQL CRUD and Filtering

- [[#27. INSERT Basics|27. INSERT Basics]]
- [[#28. INSERT Multiple Rows and RETURNING|28. INSERT Multiple Rows and RETURNING]]
- [[#29. SELECT Basics|29. SELECT Basics]]
- [[#30. SELECT Specific Columns, Aliases, LIMIT, OFFSET, DISTINCT|30. SELECT Specific Columns, Aliases, LIMIT, OFFSET, DISTINCT]]
- [[#31. WHERE and Comparison Operators|31. WHERE and Comparison Operators]]
- [[#32. BETWEEN, IN, AND, OR|32. BETWEEN, IN, AND, OR]]
- [[#33. ILIKE and Pattern Matching|33. ILIKE and Pattern Matching]]
- [[#34. NULL Checks|34. NULL Checks]]
- [[#35. ORDER BY|35. ORDER BY]]
- [[#36. UPDATE and DELETE|36. UPDATE and DELETE]]
- [[#37. Soft Delete Pattern|37. Soft Delete Pattern]]
- [[#38. UPDATE and DELETE Safety Tips|38. UPDATE and DELETE Safety Tips]]

## G. JOINs

- [[#39. What JOINs Are|39. What JOINs Are]]
- [[#40. INNER JOIN|40. INNER JOIN]]
- [[#41. LEFT JOIN|41. LEFT JOIN]]
- [[#42. Multiple JOINs|42. Multiple JOINs]]
- [[#43. JOIN Aliases|43. JOIN Aliases]]
- [[#44. JOIN Tips and Common Mistakes|44. JOIN Tips and Common Mistakes]]

## H. Aggregates and GROUP BY

- [[#45. Aggregate Functions|45. Aggregate Functions]]
- [[#46. COUNT, SUM, AVG, MIN, MAX|46. COUNT, SUM, AVG, MIN, MAX]]
- [[#47. GROUP BY|47. GROUP BY]]
- [[#48. HAVING|48. HAVING]]
- [[#49. WHERE vs HAVING|49. WHERE vs HAVING]]
- [[#50. Aggregate Query Tips|50. Aggregate Query Tips]]

## I. Indexes and Performance

- [[#51. Constraints in Detail|51. Constraints in Detail]]
- [[#52. Indexes Overview|52. Indexes Overview]]
- [[#53. B-Tree, Unique, and Partial Indexes|53. B-Tree, Unique, and Partial Indexes]]
- [[#54. When to Add Indexes|54. When to Add Indexes]]
- [[#55. EXPLAIN ANALYZE Preview|55. EXPLAIN ANALYZE Preview]]
- [[#56. Index Tips|56. Index Tips]]

## J. Normalization

- [[#57. What Normalization Is|57. What Normalization Is]]
- [[#58. Unnormalized Design Problem|58. Unnormalized Design Problem]]
- [[#59. Normalized Design Example|59. Normalized Design Example]]
- [[#60. 1NF, 2NF, and 3NF|60. 1NF, 2NF, and 3NF]]
- [[#61. Normalization Tips|61. Normalization Tips]]

## K. Subqueries and CTEs

- [[#62. Subqueries|62. Subqueries]]
- [[#63. Scalar Subqueries and EXISTS|63. Scalar Subqueries and EXISTS]]
- [[#64. CTEs Common Table Expressions|64. CTEs Common Table Expressions]]
- [[#65. CTE vs Subquery|65. CTE vs Subquery]]
- [[#66. Subquery and CTE Tips|66. Subquery and CTE Tips]]

## L. Hands-On Labs

- [[#67. Library Schema Lab|67. Library Schema Lab]]
- [[#68. SQL Query Lab|68. SQL Query Lab]]
- [[#69. Student Enrollment Database Lab|69. Student Enrollment Database Lab]]
- [[#70. Student Enrollment Schema Solution Guide|70. Student Enrollment Schema Solution Guide]]
- [[#71. Student Enrollment Query Examples|71. Student Enrollment Query Examples]]
- [[#72. Index and EXPLAIN ANALYZE Lab|72. Index and EXPLAIN ANALYZE Lab]]

## M. Quick References

- [[#73. SQL Command Cheat Sheet|73. SQL Command Cheat Sheet]]
- [[#74. Clause Order Cheat Sheet|74. Clause Order Cheat Sheet]]
- [[#75. Common SQL Mistakes|75. Common SQL Mistakes]]
- [[#76. PostgreSQL Tips and Tricks|76. PostgreSQL Tips and Tricks]]
- [[#77. Final Key Takeaways|77. Final Key Takeaways]]
- [[#78. Final Review Checklist|78. Final Review Checklist]]

---

# 0. Suggested Study Path

## 30-Minute Quick Review

```text
5 min  - why databases are needed
5 min  - relational model
5 min  - data types and constraints
5 min  - CREATE, INSERT, SELECT
5 min  - WHERE, ORDER BY, UPDATE, DELETE
5 min  - JOINs and GROUP BY
```

Recommended sections:

```text
2, 5, 6, 14, 21, 27, 29, 31, 35, 39, 45, 47
```

## 1-Hour Review

```text
10 min - static lists vs PostgreSQL
10 min - relational model and setup
10 min - data types and schema design
10 min - SQL CRUD and filtering
10 min - JOINs and aggregates
10 min - indexes, normalization, CTEs
```

Recommended sections:

```text
2 to 13
14 to 26
27 to 38
39 to 50
51 to 66
```

## 2-Hour Deep Review

```text
15 min - database purpose and relational model
15 min - setup and pgAdmin
15 min - data types and constraints
20 min - SQL CRUD and filtering
20 min - JOINs and aggregate queries
20 min - indexes and normalization
15 min - subqueries and CTEs
20 min - student enrollment lab
```

Recommended sections:

```text
All sections from 1 to 78
```

[[#Navigation|⬆ Back to Navigation]]

---

# 1. Session Overview

This reviewer covers PostgreSQL database fundamentals.

Main topics:

```text
why databases are needed
relational model
PostgreSQL setup
pgAdmin usage
data types
schema design
SQL CREATE, INSERT, SELECT
WHERE, ORDER BY, LIMIT
JOINs
aggregate functions
GROUP BY
indexes
normalization
subqueries
CTEs
hands-on database design
```

Main goal:

```text
Understand how to design tables, insert data, query data, connect related tables, and improve query performance.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 2. Why a Database

A static list is useful for learning, but it has major limitations.

Problems with in-memory/static lists:

```text
data disappears after restart
no true persistence
poor multi-user support
manual querying only
no real relationships
no scaling across multiple servers
slow search for large data
```

A database solves these by providing:

```text
persistent storage
shared data source
structured tables
relationships
constraints
querying through SQL
indexes for performance
```

Static list:

```csharp
private static List<Book> _books = new();
```

Database table:

```sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    available BOOLEAN NOT NULL DEFAULT TRUE
);
```

Key takeaway:

```text
A database is used when data must survive restarts, support many users, and be queried efficiently.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 3. Static Lists vs PostgreSQL

In-memory list:

```text
App starts
↓
Seeded list is created
↓
POST adds item
↓
App stops
↓
Data disappears
```

PostgreSQL:

```text
App starts
↓
Connects to database
↓
POST inserts row
↓
App stops
↓
Database keeps row
```

Static list search:

```csharp
var result = books.Where(b => b.Title.Contains("Clean")).ToList();
```

SQL search:

```sql
SELECT *
FROM books
WHERE title ILIKE '%clean%';
```

Static list relationship:

```csharp
public string Author { get; set; } = string.Empty;
```

Relational design:

```text
authors table
books table
books.author_id references authors.id
```

Key takeaway:

```text
The API endpoint can stay the same, but the storage changes from RAM to PostgreSQL.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 4. Core Mental Model

Database mental model:

```text
Database
↓
Schema
↓
Tables
↓
Rows
↓
Columns
```

CSharp comparison:

```text
Table = class definition
Column = property
Row = object instance
Primary key = unique object identifier
Foreign key = reference to another object/table
Schema = overall structure
```

Example CSharp class:

```csharp
public class Book
{
    public int Id { get; set; }
    public string Title { get; set; } = string.Empty;
    public bool Available { get; set; }
}
```

Example SQL table:

```sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    available BOOLEAN NOT NULL DEFAULT TRUE
);
```

[[#Navigation|⬆ Back to Navigation]]

---

# 5. Relational Model Core Concepts

The relational model organizes data into tables.

Main concepts:

```text
table
row
column
primary key
foreign key
schema
relationship
constraint
```

A relational database avoids putting everything in one giant table.

Instead, each major entity gets its own table.

Example:

```text
authors
books
loans
```

Relationships connect them:

```text
books.author_id → authors.id
loans.book_id → books.id
```

Key takeaway:

```text
Relational databases separate data into tables and link those tables using keys.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 6. Table, Row, Column, and Schema

## Table

A table is a named set of rows and columns.

```sql
SELECT * FROM books;
```

## Row

A row is one record.

```text
1 | Clean Code | Robert Martin | true | 2008
```

## Column

A column is one named field.

```text
id
title
author_id
available
year
```

## Schema

A schema is the structure of the database.

It includes:

```text
tables
columns
data types
constraints
relationships
indexes
```

[[#Navigation|⬆ Back to Navigation]]

---

# 7. Primary Keys and Foreign Keys

## Primary Key

A primary key uniquely identifies each row.

```sql
id SERIAL PRIMARY KEY
```

Meaning:

```text
id is required
id is unique
id identifies one row
```

Primary key rules:

```text
cannot be null
must be unique
usually does not change
usually named id
```

## Foreign Key

A foreign key links one table to another.

```sql
author_id INT REFERENCES authors(id)
```

Meaning:

```text
books.author_id must refer to an existing authors.id
```

Complete example:

```sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    author_id INT REFERENCES authors(id)
);
```

Foreign key benefit:

```text
Prevents invalid relationships.
A book cannot point to an author that does not exist.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 8. Relationships Between Tables

## One-to-Many

One author can have many books.

```text
authors
1
↓
many
books
```

SQL:

```sql
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(150) NOT NULL
);

CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    author_id INT REFERENCES authors(id)
);
```

## Many-to-Many

One student can have many sections or courses. One section or course can have many students.

Use a junction table:

```sql
CREATE TABLE student_sections (
    id SERIAL PRIMARY KEY,
    student_id INT NOT NULL REFERENCES students(id),
    section_id INT NOT NULL REFERENCES sections(id),
    enrolled_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

[[#Navigation|⬆ Back to Navigation]]

---

# 9. Relational Model Compared to CSharp Classes

CSharp:

```csharp
public class Author
{
    public int Id { get; set; }
    public string FullName { get; set; } = string.Empty;
}
```

SQL:

```sql
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(150) NOT NULL
);
```

CSharp object:

```csharp
var author = new Author
{
    Id = 1,
    FullName = "Robert Martin"
};
```

SQL row:

```text
1 | Robert Martin
```

Mental model:

```text
class = table shape
property = column
object = row
list of objects = table rows
```

[[#Navigation|⬆ Back to Navigation]]

---

# 10. PostgreSQL Installation Basics

Typical setup:

```text
download PostgreSQL installer
install PostgreSQL
remember postgres password
use default port 5432
install pgAdmin
```

Default PostgreSQL port:

```text
5432
```

Important:

```text
Remember the password for postgres.
You will need it for psql, pgAdmin, and later app connection strings.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 11. Connecting with psql

Connect:

```bash
psql -U postgres
```

Then enter password.

Expected prompt:

```text
postgres=#
```

Useful psql commands:

```sql
\l
```

List databases.

```sql
\c librarydb
```

Connect to database.

```sql
\dt
```

List tables.

```sql
\d books
```

Describe table.

```sql
\q
```

Quit.

Create database:

```sql
CREATE DATABASE librarydb;
```

Connect:

```sql
\c librarydb
```

Tip:

```text
Always check which database you are connected to before running CREATE TABLE or INSERT.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 12. pgAdmin Basics

pgAdmin is a GUI for PostgreSQL.

Typical connection settings:

```text
Name: Local
Host: localhost
Port: 5432
Username: postgres
Password: your postgres password
```

To run SQL:

```text
Open pgAdmin
↓
Servers
↓
Databases
↓
librarydb
↓
Right-click / Query Tool
↓
Type SQL
↓
Run / F5
```

Tip:

```text
Use pgAdmin if psql feels intimidating.
Use psql if you want faster keyboard-based work.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 13. Setup Tips and Common Mistakes

Common mistakes:

```text
forgetting postgres password
connecting to wrong database
running query in postgres database instead of librarydb
PostgreSQL service not running
wrong port
forgetting semicolon
```

SQL statements usually end with:

```sql
;
```

If psql does not execute, check if the prompt changed to:

```text
librarydb-#
```

That usually means PostgreSQL is waiting for the rest of the statement.

Fix:

```sql
;
```

or cancel:

```text
Ctrl + C
```

[[#Navigation|⬆ Back to Navigation]]

---

# 14. Data Types Overview

Data types define what kind of value a column can store.

Examples:

```sql
id SERIAL PRIMARY KEY
title VARCHAR(255)
available BOOLEAN
created_at TIMESTAMPTZ
grade NUMERIC(5,2)
```

Data types affect:

```text
storage
validation
query behavior
performance
meaning of data
```

Key takeaway:

```text
Choose the data type that matches the data's meaning.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 15. Numeric and Boolean Types

Common numeric types:

```sql
SMALLINT
INTEGER / INT
BIGINT
SERIAL
BIGSERIAL
NUMERIC(p, s)
DECIMAL(p, s)
REAL
DOUBLE PRECISION
```

Use:

```text
INT = normal whole numbers
BIGINT = very large whole numbers
SERIAL = auto-increment integer primary key
NUMERIC/DECIMAL = exact decimal, good for money
REAL/DOUBLE = approximate decimals
```

Examples:

```sql
id SERIAL PRIMARY KEY
age INT
price NUMERIC(10, 2)
available BOOLEAN NOT NULL DEFAULT TRUE
```

Boolean stores true/false.

Valid PostgreSQL boolean-like values include:

```text
TRUE
FALSE
't'
'f'
'yes'
'no'
'1'
'0'
```

Tip:

```text
Use NUMERIC or DECIMAL for money, not REAL or DOUBLE PRECISION.
Use BOOLEAN when the value only has two states.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 16. Text Types

PostgreSQL text types:

```sql
CHAR(n)
VARCHAR(n)
TEXT
```

Meaning:

```text
CHAR(n) = fixed length, padded with spaces
VARCHAR(n) = variable length with limit
TEXT = unlimited length
```

Examples:

```sql
full_name VARCHAR(150) NOT NULL
title VARCHAR(255) NOT NULL
description TEXT
```

Tip:

```text
Use TEXT unless you specifically need to enforce a length limit.
Use VARCHAR(n) when the maximum length is part of the rule.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 17. Date and Time Types

Common types:

```sql
DATE
TIME
TIMESTAMP
TIMESTAMPTZ
```

Meaning:

```text
DATE = date only
TIME = time only
TIMESTAMP = date and time without timezone
TIMESTAMPTZ = timestamp with timezone handling
```

Examples:

```sql
created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
loaned_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
returned_at TIMESTAMPTZ
```

Tip:

```text
Use TIMESTAMPTZ for most created_at, updated_at, and loaned_at fields.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 18. UUID, JSONB, and Arrays

UUID:

```sql
id UUID PRIMARY KEY
```

Used for globally unique IDs.

JSONB:

```sql
metadata JSONB
```

Used for structured flexible data.

Array:

```sql
tags TEXT[]
```

Important normalization warning:

```text
Do not store important relational data as arrays just to avoid creating a table.
For student grades, use a student_grades table instead of grade arrays.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 19. PostgreSQL to CSharp Type Mapping

| PostgreSQL | CSharp |
|---|---|
| INT | int |
| BIGINT | long |
| NUMERIC / DECIMAL | decimal |
| BOOLEAN | bool |
| VARCHAR | string |
| TEXT | string |
| TIMESTAMP | DateTime |
| TIMESTAMPTZ | DateTime |
| UUID | Guid |

Tip:

```text
The database type controls storage.
The CSharp type controls how your app represents that value.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 20. Data Type Tips

```text
Use SERIAL for simple auto-increment primary keys.
Use TEXT for free-form text.
Use VARCHAR(n) when a max length is required.
Use BOOLEAN for true/false.
Use NUMERIC/DECIMAL for money or exact decimals.
Use TIMESTAMPTZ for timestamps.
Use INT for normal IDs and counts.
Use UUID when you need globally unique identifiers.
Avoid arrays for relational data that should be queried separately.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 21. CREATE TABLE Basics

Basic syntax:

```sql
CREATE TABLE table_name (
    column_name DATA_TYPE CONSTRAINTS,
    column_name DATA_TYPE CONSTRAINTS
);
```

Example:

```sql
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(150) NOT NULL,
    nationality VARCHAR(100),
    birth_year INT CHECK (birth_year > 1800 AND birth_year < 2010)
);
```

Tip:

```text
Create parent tables first.
Create child tables with foreign keys after.
```

Example order:

```text
authors first
books second
loans third
```

[[#Navigation|⬆ Back to Navigation]]

---

# 22. Library Schema Example

Authors:

```sql
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(150) NOT NULL,
    nationality VARCHAR(100),
    birth_year INT CHECK (birth_year > 1800 AND birth_year < 2010)
);
```

Books:

```sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    genre VARCHAR(80),
    year INT CHECK (year >= 1000 AND year <= 2030),
    available BOOLEAN NOT NULL DEFAULT TRUE,
    author_id INT REFERENCES authors(id) ON DELETE SET NULL
);
```

Loans:

```sql
CREATE TABLE loans (
    id SERIAL PRIMARY KEY,
    book_id INT NOT NULL REFERENCES books(id) ON DELETE CASCADE,
    member_name VARCHAR(150) NOT NULL,
    loaned_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    returned_at TIMESTAMPTZ
);
```

Meaning:

```text
authors stores author details
books stores book details and links to authors
loans stores borrowing records and links to books
```

[[#Navigation|⬆ Back to Navigation]]

---

# 23. Constraint Quick Reference

| Constraint | Meaning |
|---|---|
| PRIMARY KEY | unique + not null row identity |
| NOT NULL | value is required |
| UNIQUE | no duplicate values |
| CHECK | value must pass a condition |
| DEFAULT | use value when not provided |
| REFERENCES | foreign key to another table |

Examples:

```sql
id SERIAL PRIMARY KEY
title VARCHAR(255) NOT NULL
email VARCHAR(255) UNIQUE
year INT CHECK (year >= 1000 AND year <= 2030)
available BOOLEAN DEFAULT TRUE
author_id INT REFERENCES authors(id)
```

[[#Navigation|⬆ Back to Navigation]]

---

# 24. CHECK and DEFAULT Constraints

CHECK validates a column value.

```sql
year INT CHECK (year >= 1000 AND year <= 2030)
```

Grade example:

```sql
grade NUMERIC CHECK (grade >= 0 AND grade <= 100)
```

Student year example:

```sql
year INT CHECK (year BETWEEN 1 AND 4)
```

DEFAULT gives a value when INSERT does not provide one.

```sql
available BOOLEAN NOT NULL DEFAULT TRUE
created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
```

Tip:

```text
Use CHECK for rules that must always be true in the database.
Use DEFAULT for automatic values like timestamps and true/false defaults.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 25. ON DELETE Behavior

Foreign keys can define what happens when the referenced row is deleted.

```sql
author_id INT REFERENCES authors(id) ON DELETE SET NULL
```

Options:

| Option | Meaning |
|---|---|
| RESTRICT | block delete if referenced |
| CASCADE | delete child rows too |
| SET NULL | set foreign key to NULL |
| SET DEFAULT | set foreign key to default |

Examples:

```sql
author_id INT REFERENCES authors(id) ON DELETE SET NULL
book_id INT NOT NULL REFERENCES books(id) ON DELETE CASCADE
```

Tip:

```text
Use CASCADE carefully because it can delete many related rows automatically.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 26. Schema Design Tips

```text
Create parent tables before child tables.
Use primary keys on every table.
Use foreign keys for relationships.
Use NOT NULL for required fields.
Use UNIQUE for natural unique values.
Use CHECK for valid ranges.
Use DEFAULT for automatic values.
Avoid storing repeated information in multiple tables.
Avoid arrays for relational records such as grades.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 27. INSERT Basics

Insert one row:

```sql
INSERT INTO authors (full_name, nationality, birth_year)
VALUES ('Robert Martin', 'American', 1952);
```

Insert into child table:

```sql
INSERT INTO books (title, genre, year, available, author_id)
VALUES ('Clean Code', 'Programming', 2008, TRUE, 1);
```

Tip:

```text
List the target columns explicitly.
Do not rely on column order.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 28. INSERT Multiple Rows and RETURNING

Multiple rows:

```sql
INSERT INTO authors (full_name, nationality)
VALUES
('Jon Skeet', 'British'),
('Frank Herbert', 'American'),
('Yuval Harari', 'Israeli'),
('David Thomas', 'British');
```

RETURNING gives the inserted row or selected columns back immediately.

```sql
INSERT INTO books (title, genre, year, author_id)
VALUES ('Clean Architecture', 'Programming', 2017, 1)
RETURNING id, title;
```

Useful when:

```text
you need the generated id
you inserted a parent row and need to insert child rows
```

[[#Navigation|⬆ Back to Navigation]]

---

# 29. SELECT Basics

Select all columns:

```sql
SELECT * FROM books;
```

Select specific columns:

```sql
SELECT id, title, available
FROM books;
```

Tip:

```text
Use specific columns instead of SELECT * in production-style queries.
```

Why:

```text
clearer output
less unnecessary data
safer if schema changes
better habit for API/database work
```

[[#Navigation|⬆ Back to Navigation]]

---

# 30. SELECT Specific Columns, Aliases, LIMIT, OFFSET, DISTINCT

Column alias:

```sql
SELECT
    id,
    title AS book_title,
    available AS is_available
FROM books;
```

Limit:

```sql
SELECT *
FROM books
LIMIT 3;
```

Offset:

```sql
SELECT *
FROM books
LIMIT 3 OFFSET 2;
```

Distinct:

```sql
SELECT DISTINCT genre
FROM books;
```

Count:

```sql
SELECT COUNT(*)
FROM books;
```

Pagination formula:

```text
OFFSET = (page - 1) * pageSize
```

[[#Navigation|⬆ Back to Navigation]]

---

# 31. WHERE and Comparison Operators

WHERE filters rows.

```sql
SELECT *
FROM books
WHERE available = TRUE;
```

Comparison operators:

```text
=
<>
<
>
<=
>=
```

Examples:

```sql
SELECT *
FROM books
WHERE year > 2000;
```

```sql
SELECT *
FROM books
WHERE genre <> 'Fiction';
```

[[#Navigation|⬆ Back to Navigation]]

---

# 32. BETWEEN, IN, AND, OR

BETWEEN:

```sql
SELECT *
FROM books
WHERE year BETWEEN 1990 AND 2010;
```

IN:

```sql
SELECT *
FROM books
WHERE genre IN ('Fiction', 'History', 'Science');
```

AND:

```sql
SELECT *
FROM books
WHERE available = TRUE AND genre = 'Programming';
```

OR:

```sql
SELECT *
FROM books
WHERE genre = 'Fiction' OR genre = 'History';
```

Tip:

```text
Use parentheses when mixing AND and OR.
```

Example:

```sql
SELECT *
FROM books
WHERE available = TRUE
AND (genre = 'Fiction' OR genre = 'History');
```

[[#Navigation|⬆ Back to Navigation]]

---

# 33. ILIKE and Pattern Matching

Case-insensitive search:

```sql
SELECT *
FROM books
WHERE title ILIKE '%clean%';
```

Wildcard:

```text
% = any characters
```

Examples:

```sql
ILIKE 'clean%'   -- starts with clean
ILIKE '%clean'   -- ends with clean
ILIKE '%clean%'  -- contains clean
```

Tip:

```text
ILIKE is useful for beginner search features.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 34. NULL Checks

Do not use:

```sql
WHERE returned_at = NULL
```

Use:

```sql
WHERE returned_at IS NULL
```

Not null:

```sql
WHERE returned_at IS NOT NULL
```

Example:

```sql
SELECT *
FROM loans
WHERE returned_at IS NULL;
```

Meaning:

```text
books not yet returned
```

[[#Navigation|⬆ Back to Navigation]]

---

# 35. ORDER BY

Ascending:

```sql
SELECT *
FROM books
ORDER BY title ASC;
```

Descending:

```sql
SELECT *
FROM books
ORDER BY year DESC;
```

Multiple columns:

```sql
SELECT *
FROM books
ORDER BY genre ASC, year DESC;
```

Tip:

```text
Always use ORDER BY if result order matters.
Without ORDER BY, database row order is not guaranteed.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 36. UPDATE and DELETE

Update one row:

```sql
UPDATE books
SET available = FALSE
WHERE id = 3;
```

Update multiple columns:

```sql
UPDATE books
SET
    title = 'Clean Code (2nd Ed)',
    year = 2024,
    available = TRUE
WHERE id = 1;
```

With RETURNING:

```sql
UPDATE books
SET available = FALSE
WHERE id = 3
RETURNING id, title, available;
```

Delete one row:

```sql
DELETE FROM books
WHERE id = 5;
```

With RETURNING:

```sql
DELETE FROM books
WHERE id = 5
RETURNING id, title;
```

Critical tip:

```text
Always use WHERE with UPDATE and DELETE unless you truly mean every row.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 37. Soft Delete Pattern

Instead of deleting, mark as deleted.

Add column:

```sql
ALTER TABLE books
ADD COLUMN deleted_at TIMESTAMPTZ;
```

Soft delete:

```sql
UPDATE books
SET deleted_at = NOW()
WHERE id = 5;
```

Query active records:

```sql
SELECT *
FROM books
WHERE deleted_at IS NULL;
```

Use soft delete when:

```text
you need audit history
you need possible restore
you should not permanently remove records
```

[[#Navigation|⬆ Back to Navigation]]

---

# 38. UPDATE and DELETE Safety Tips

Before UPDATE:

```sql
SELECT *
FROM books
WHERE id = 3;
```

Then:

```sql
UPDATE books
SET available = FALSE
WHERE id = 3;
```

Before DELETE:

```sql
SELECT *
FROM books
WHERE id = 5;
```

Then:

```sql
DELETE FROM books
WHERE id = 5;
```

Safe habit:

```text
Write SELECT first.
Verify rows.
Change SELECT to UPDATE or DELETE.
Keep WHERE.
Use RETURNING to verify changes.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 39. What JOINs Are

A JOIN combines data from multiple tables.

Example:

```text
books table has author_id
authors table has id and full_name
JOIN connects books.author_id to authors.id
```

Basic pattern:

```sql
SELECT
    b.title,
    a.full_name AS author
FROM books AS b
INNER JOIN authors AS a ON b.author_id = a.id;
```

Key idea:

```text
JOIN is how relational databases avoid repeating the same data everywhere.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 40. INNER JOIN

INNER JOIN returns only matching rows from both tables.

```sql
SELECT
    b.id,
    b.title,
    b.genre,
    b.year,
    a.full_name AS author,
    a.nationality AS author_country
FROM books AS b
INNER JOIN authors AS a
ON b.author_id = a.id
WHERE b.available = TRUE
ORDER BY b.year DESC;
```

Meaning:

```text
Only books with matching authors are returned.
Books with NULL author_id are excluded.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 41. LEFT JOIN

LEFT JOIN returns all rows from the left table, plus matching rows from the right table.

```sql
SELECT
    b.title,
    a.full_name AS author
FROM books AS b
LEFT JOIN authors AS a ON b.author_id = a.id;
```

If a book has no author:

```text
author = NULL
```

Use LEFT JOIN when:

```text
you want all left-side rows even if no match exists
```

Example:

```text
show all books, even books without authors
show all sections, even sections with no students
```

[[#Navigation|⬆ Back to Navigation]]

---

# 42. Multiple JOINs

Join three tables:

```sql
SELECT
    b.title,
    a.full_name AS author,
    l.member_name,
    l.loaned_at
FROM loans AS l
INNER JOIN books AS b ON l.book_id = b.id
INNER JOIN authors AS a ON b.author_id = a.id
WHERE l.returned_at IS NULL
ORDER BY l.loaned_at DESC;
```

Meaning:

```text
Get active loans with book title and author name.
```

Flow:

```text
loans.book_id → books.id
books.author_id → authors.id
```

[[#Navigation|⬆ Back to Navigation]]

---

# 43. JOIN Aliases

Aliases make queries readable.

Without aliases:

```sql
SELECT books.title, authors.full_name
FROM books
INNER JOIN authors ON books.author_id = authors.id;
```

With aliases:

```sql
SELECT b.title, a.full_name
FROM books AS b
INNER JOIN authors AS a ON b.author_id = a.id;
```

Tip:

```text
Use aliases in longer JOIN queries.
Avoid aliases temporarily if you are still learning and need clearer table names.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 44. JOIN Tips and Common Mistakes

Tips:

```text
Know the relationship before writing the JOIN.
Usually join foreign key to primary key.
Use INNER JOIN when a match is required.
Use LEFT JOIN when missing matches should still appear.
Use aliases for readability.
```

Common mistakes:

```text
joining wrong columns
forgetting ON condition
using INNER JOIN when LEFT JOIN is needed
selecting ambiguous column names like id without table prefix
forgetting that NULLs appear in LEFT JOIN results
```

Ambiguous id fix:

```sql
SELECT
    books.id AS book_id,
    authors.id AS author_id
FROM books
INNER JOIN authors ON books.author_id = authors.id;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 45. Aggregate Functions

Aggregate functions summarize rows.

Common aggregates:

```text
COUNT
SUM
AVG
MIN
MAX
```

Example:

```sql
SELECT COUNT(*)
FROM books;
```

Aggregates are similar to LINQ:

```csharp
books.Count();
books.Average(b => b.Year);
books.Min(b => b.Year);
books.Max(b => b.Year);
```

[[#Navigation|⬆ Back to Navigation]]

---

# 46. COUNT, SUM, AVG, MIN, MAX

Count all rows:

```sql
SELECT COUNT(*)
FROM books;
```

Count only available books:

```sql
SELECT COUNT(*)
FROM books
WHERE available = TRUE;
```

Count non-null author IDs:

```sql
SELECT COUNT(author_id)
FROM books;
```

Summary query:

```sql
SELECT
    COUNT(*) AS total_books,
    ROUND(AVG(year), 0) AS average_year,
    MIN(year) AS oldest_year,
    MAX(year) AS newest_year
FROM books;
```

Difference:

```text
COUNT(*) counts rows.
COUNT(column) counts non-null values in that column.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 47. GROUP BY

GROUP BY groups rows with the same value.

Count books per genre:

```sql
SELECT
    genre,
    COUNT(*) AS total
FROM books
GROUP BY genre
ORDER BY total DESC;
```

Meaning:

```text
Group books by genre.
Count how many books each genre has.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 48. HAVING

HAVING filters groups.

```sql
SELECT
    genre,
    COUNT(*) AS total
FROM books
GROUP BY genre
HAVING COUNT(*) > 1;
```

Meaning:

```text
Only show genres with more than one book.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 49. WHERE vs HAVING

WHERE filters rows before grouping.

```sql
SELECT *
FROM books
WHERE available = TRUE;
```

HAVING filters groups after grouping.

```sql
SELECT genre, COUNT(*) AS total
FROM books
GROUP BY genre
HAVING COUNT(*) > 1;
```

Combined:

```sql
SELECT
    genre,
    COUNT(*) AS total,
    AVG(year) AS avg_year
FROM books
WHERE available = TRUE
GROUP BY genre
HAVING COUNT(*) >= 1
ORDER BY total DESC;
```

Rule:

```text
WHERE = filters individual rows
HAVING = filters aggregate/group results
```

[[#Navigation|⬆ Back to Navigation]]

---

# 50. Aggregate Query Tips

```text
Use GROUP BY when selecting normal columns with aggregates.
Use HAVING for aggregate filters.
Use aliases for aggregate results.
Use COUNT(*) for row count.
Use COUNT(column) if you only want non-null values.
Use LEFT JOIN if you want groups with zero related rows.
```

Example count books per author including authors with zero books:

```sql
SELECT
    a.full_name,
    COUNT(b.id) AS books_written
FROM authors AS a
LEFT JOIN books AS b ON b.author_id = a.id
GROUP BY a.id, a.full_name
ORDER BY books_written DESC;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 51. Constraints in Detail

Constraints protect data integrity.

Examples:

```sql
id SERIAL PRIMARY KEY
title VARCHAR(255) NOT NULL
email VARCHAR(255) UNIQUE
year INT CHECK (year >= 1000 AND year <= 2030)
author_id INT REFERENCES authors(id)
```

Named foreign key:

```sql
CONSTRAINT fk_books_author
FOREIGN KEY (author_id)
REFERENCES authors(id)
ON DELETE SET NULL
```

Add constraint later:

```sql
ALTER TABLE books
ADD CONSTRAINT uq_books_isbn UNIQUE (isbn);
```

[[#Navigation|⬆ Back to Navigation]]

---

# 52. Indexes Overview

Indexes improve query performance.

Without index:

```text
PostgreSQL may scan every row.
```

With index:

```text
PostgreSQL can find matching rows faster.
```

Example:

```sql
CREATE INDEX idx_books_genre
ON books (genre);
```

Use indexes on columns often used in:

```text
WHERE
JOIN
ORDER BY
```

[[#Navigation|⬆ Back to Navigation]]

---

# 53. B-Tree, Unique, and Partial Indexes

B-tree is the default PostgreSQL index type.

Good for:

```text
=
<
>
<=
>=
BETWEEN
ORDER BY
```

B-tree example:

```sql
CREATE INDEX idx_books_year
ON books (year);
```

Unique index:

```sql
CREATE UNIQUE INDEX idx_books_isbn
ON books (isbn);
```

Partial index:

```sql
CREATE INDEX idx_available_books
ON books (title)
WHERE available = TRUE;
```

Use partial index when:

```text
queries often filter the same subset
subset is smaller than full table
```

[[#Navigation|⬆ Back to Navigation]]

---

# 54. When to Add Indexes

Add indexes for:

```text
columns used frequently in WHERE
foreign key columns
columns used in JOIN
columns used in ORDER BY
unique lookup fields
```

Avoid unnecessary indexes on:

```text
small tables
columns that change very frequently
columns rarely searched
too many columns without reason
```

Important tradeoff:

```text
Indexes speed up reads.
Indexes can slow down writes because the index must also be updated.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 55. EXPLAIN ANALYZE Preview

EXPLAIN ANALYZE shows how PostgreSQL runs a query.

```sql
EXPLAIN ANALYZE
SELECT *
FROM books
WHERE genre = 'Programming';
```

Use before and after adding an index:

```sql
EXPLAIN ANALYZE
SELECT *
FROM books
WHERE author_id = 1;
```

Then:

```sql
CREATE INDEX idx_books_author_id
ON books (author_id);
```

Run again:

```sql
EXPLAIN ANALYZE
SELECT *
FROM books
WHERE author_id = 1;
```

Look for:

```text
sequential scan
index scan
execution time
```

[[#Navigation|⬆ Back to Navigation]]

---

# 56. Index Tips

```text
Always consider indexing foreign keys.
Index common search/filter columns.
Index columns used in joins.
Use unique indexes for unique business values.
Do not add indexes blindly.
Use EXPLAIN ANALYZE to compare.
On tiny tables, indexes may not show much improvement.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 57. What Normalization Is

Normalization is the process of organizing database tables to reduce duplication and avoid data problems.

Goals:

```text
store each fact once
avoid repeated data
avoid update anomalies
avoid insertion anomalies
avoid deletion anomalies
keep relationships clean
```

Key idea:

```text
If the same information is repeated in many rows, it probably belongs in another table.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 58. Unnormalized Design Problem

Bad design:

```sql
CREATE TABLE books_bad (
    id SERIAL PRIMARY KEY,
    title TEXT,
    author_name TEXT,
    author_country TEXT,
    author_birth INT,
    genre TEXT,
    year INT
);
```

Problems:

```text
author_name repeated for every book
author_country repeated for every book
changing author info requires many updates
cannot store author without a book
deleting last book deletes author info
wastes storage
```

These are called:

```text
update anomalies
insertion anomalies
deletion anomalies
```

[[#Navigation|⬆ Back to Navigation]]

---

# 59. Normalized Design Example

Good design:

```sql
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(150) NOT NULL,
    nationality VARCHAR(100),
    birth_year INT
);
```

```sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    genre VARCHAR(80),
    year INT,
    available BOOLEAN DEFAULT TRUE,
    author_id INT REFERENCES authors(id)
);
```

Benefits:

```text
author data stored once
books link to author through author_id
can store author before books exist
deleting a book does not delete author info
less redundancy
```

[[#Navigation|⬆ Back to Navigation]]

---

# 60. 1NF, 2NF, and 3NF

## First Normal Form

1NF means:

```text
Each column holds one value.
No comma-separated lists.
No arrays for relational records.
```

Bad:

```text
grades = '90, 85, 92'
```

Good:

```sql
CREATE TABLE student_grades (
    id SERIAL PRIMARY KEY,
    student_id INT REFERENCES students(id),
    grade INT CHECK (grade BETWEEN 0 AND 100)
);
```

## Second Normal Form

2NF means:

```text
Every non-key column depends on the whole primary key.
```

This matters most in tables with composite primary keys.

Example join table:

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    enrolled_at TIMESTAMPTZ,
    PRIMARY KEY (student_id, course_id)
);
```

`enrolled_at` describes the student-course relationship.

## Third Normal Form

3NF means:

```text
No non-key column should depend on another non-key column.
```

Better design:

```sql
CREATE TABLE programs (
    id SERIAL PRIMARY KEY,
    program_name VARCHAR(150) UNIQUE NOT NULL
);

CREATE TABLE sections (
    id SERIAL PRIMARY KEY,
    code VARCHAR(50) UNIQUE NOT NULL,
    program_id INT REFERENCES programs(id)
);
```

Key rule:

```text
For bootcamp, aim for 3NF.
If information repeats, consider another table.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 61. Normalization Tips

```text
One table per entity type.
Do not store comma-separated values.
Do not store arrays for data that needs querying.
Separate repeated information.
Use foreign keys instead of copied text.
Use junction tables for many-to-many relationships.
Store grades in student_grades, not in students as a list.
Store programs separately from sections.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 62. Subqueries

A subquery is a SELECT inside another query.

Example:

```sql
SELECT title, year
FROM books
WHERE author_id IN (
    SELECT id
    FROM authors
    WHERE nationality = 'British'
);
```

Meaning:

```text
Find authors who are British.
Use their ids to find books.
```

Pattern:

```sql
SELECT columns
FROM table
WHERE column IN (
    SELECT column
    FROM other_table
    WHERE condition
);
```

[[#Navigation|⬆ Back to Navigation]]

---

# 63. Scalar Subqueries and EXISTS

A scalar subquery returns one value.

```sql
SELECT
    title,
    year,
    (SELECT AVG(year) FROM books) AS avg_year,
    year - (SELECT AVG(year) FROM books) AS diff_from_avg
FROM books
ORDER BY diff_from_avg DESC;
```

EXISTS checks if a subquery returns any rows.

```sql
SELECT a.full_name
FROM authors AS a
WHERE EXISTS (
    SELECT 1
    FROM books AS b
    WHERE b.author_id = a.id
    AND b.available = TRUE
);
```

Meaning:

```text
Return authors who have at least one available book.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 64. CTEs Common Table Expressions

A CTE is a named temporary result set.

Syntax:

```sql
WITH available_books AS (
    SELECT *
    FROM books
    WHERE available = TRUE
)
SELECT
    ab.title,
    a.full_name AS author
FROM available_books AS ab
INNER JOIN authors AS a ON ab.author_id = a.id;
```

Use CTEs for:

```text
readability
breaking complex queries into steps
reusing a temporary result
```

Multiple CTEs:

```sql
WITH
programming_books AS (
    SELECT *
    FROM books
    WHERE genre = 'Programming'
),
british_authors AS (
    SELECT *
    FROM authors
    WHERE nationality = 'British'
)
SELECT
    pb.title,
    ba.full_name AS author
FROM programming_books AS pb
INNER JOIN british_authors AS ba
ON pb.author_id = ba.id;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 65. CTE vs Subquery

| Use Case | Better Option |
|---|---|
| simple one-time filtering | subquery |
| complex logic | CTE |
| query over 10 lines | CTE |
| reused temporary result | CTE |
| quick nested lookup | subquery |

Memory:

```text
Subquery = quick nested SELECT
CTE = named step-by-step query
```

[[#Navigation|⬆ Back to Navigation]]

---

# 66. Subquery and CTE Tips

```text
Use CTEs to make long SQL readable.
Use subqueries for simple nested conditions.
Use meaningful CTE names.
Check each CTE separately while debugging.
Avoid making a query clever if a CTE can make it clear.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 67. Library Schema Lab

Create:

```text
authors
books
loans
```

Required tables:

```sql
CREATE TABLE authors (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(150) NOT NULL,
    nationality VARCHAR(100),
    birth_year INT CHECK (birth_year > 1800)
);
```

```sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    genre VARCHAR(80),
    year INT CHECK (year BETWEEN 1000 AND 2030),
    available BOOLEAN NOT NULL DEFAULT TRUE,
    author_id INT REFERENCES authors(id) ON DELETE SET NULL
);
```

```sql
CREATE TABLE loans (
    id SERIAL PRIMARY KEY,
    book_id INT NOT NULL REFERENCES books(id),
    member_name VARCHAR(150) NOT NULL,
    loaned_at TIMESTAMPTZ DEFAULT NOW(),
    returned_at TIMESTAMPTZ
);
```

Verify:

```sql
SELECT * FROM authors;
SELECT * FROM books;
SELECT COUNT(*) FROM books;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 68. SQL Query Lab

Practice queries:

```sql
SELECT *
FROM books
WHERE available = TRUE;
```

```sql
SELECT *
FROM books
WHERE year > 2000
ORDER BY year DESC;
```

```sql
SELECT *
FROM books
WHERE title ILIKE '%code%';
```

```sql
SELECT *
FROM loans
WHERE returned_at IS NULL;
```

```sql
SELECT
    b.title,
    b.genre,
    a.full_name AS author
FROM books AS b
INNER JOIN authors AS a ON b.author_id = a.id;
```

```sql
SELECT
    genre,
    COUNT(*) AS total
FROM books
GROUP BY genre;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 69. Student Enrollment Database Lab

Required tables:

```text
students
programs
sections
student_sections
student_grades
```

Requirements:

```text
students have first_name, last_name, year, gender, enrolled, created_at
programs are separated into their own table
sections reference programs
student_sections is a junction table
student_grades stores multiple grades per student
use primary keys, foreign keys, unique, default, and check constraints
aim for 3NF
```

[[#Navigation|⬆ Back to Navigation]]

---

# 70. Student Enrollment Schema Solution Guide

Programs:

```sql
CREATE TABLE programs (
    id SERIAL PRIMARY KEY,
    program_name VARCHAR(150) NOT NULL UNIQUE
);
```

Students:

```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    year INT NOT NULL CHECK (year BETWEEN 1 AND 4),
    gender VARCHAR(30),
    enrolled BOOLEAN NOT NULL DEFAULT TRUE,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

Sections:

```sql
CREATE TABLE sections (
    id SERIAL PRIMARY KEY,
    code VARCHAR(50) NOT NULL UNIQUE,
    year INT NOT NULL CHECK (year BETWEEN 1 AND 4),
    program_id INT NOT NULL REFERENCES programs(id) ON DELETE RESTRICT
);
```

Student sections:

```sql
CREATE TABLE student_sections (
    id SERIAL PRIMARY KEY,
    student_id INT NOT NULL REFERENCES students(id) ON DELETE CASCADE,
    section_id INT NOT NULL REFERENCES sections(id) ON DELETE CASCADE,
    enrolled_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    UNIQUE (student_id, section_id)
);
```

Student grades:

```sql
CREATE TABLE student_grades (
    id SERIAL PRIMARY KEY,
    student_id INT NOT NULL REFERENCES students(id) ON DELETE CASCADE,
    grade NUMERIC(5,2) NOT NULL CHECK (grade >= 0 AND grade <= 100)
);
```

Design notes:

```text
programs is separate to avoid repeated program names
sections links to programs through program_id
student_sections handles student-to-section assignment
student_grades stores multiple grades as rows, not arrays
UNIQUE(student_id, section_id) prevents duplicate assignment
```

[[#Navigation|⬆ Back to Navigation]]

---

# 71. Student Enrollment Query Examples

All students with section code and program:

```sql
SELECT
    s.id,
    s.first_name,
    s.last_name,
    sec.code AS section_code,
    p.program_name
FROM students AS s
LEFT JOIN student_sections AS ss ON ss.student_id = s.id
LEFT JOIN sections AS sec ON ss.section_id = sec.id
LEFT JOIN programs AS p ON sec.program_id = p.id
ORDER BY s.last_name;
```

Currently enrolled students:

```sql
SELECT *
FROM students
WHERE enrolled = TRUE;
```

Students per section:

```sql
SELECT
    sec.code,
    COUNT(ss.student_id) AS total_students
FROM sections AS sec
LEFT JOIN student_sections AS ss ON ss.section_id = sec.id
GROUP BY sec.id, sec.code
ORDER BY total_students DESC;
```

Students per program:

```sql
SELECT
    p.program_name,
    COUNT(ss.student_id) AS total_students
FROM programs AS p
LEFT JOIN sections AS sec ON sec.program_id = p.id
LEFT JOIN student_sections AS ss ON ss.section_id = sec.id
GROUP BY p.id, p.program_name
ORDER BY total_students DESC;
```

Average grade per student:

```sql
SELECT
    s.id,
    s.first_name,
    s.last_name,
    ROUND(AVG(g.grade), 2) AS average_grade
FROM students AS s
LEFT JOIN student_grades AS g ON g.student_id = s.id
GROUP BY s.id, s.first_name, s.last_name
ORDER BY average_grade DESC;
```

Students not assigned to any section:

```sql
SELECT
    s.id,
    s.first_name,
    s.last_name
FROM students AS s
LEFT JOIN student_sections AS ss ON ss.student_id = s.id
WHERE ss.id IS NULL;
```

Sections with no students:

```sql
SELECT
    sec.id,
    sec.code
FROM sections AS sec
LEFT JOIN student_sections AS ss ON ss.section_id = sec.id
WHERE ss.id IS NULL;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 72. Index and EXPLAIN ANALYZE Lab

Create indexes:

```sql
CREATE INDEX idx_sections_program_id
ON sections(program_id);
```

```sql
CREATE INDEX idx_student_sections_student_id
ON student_sections(student_id);
```

```sql
CREATE INDEX idx_student_sections_section_id
ON student_sections(section_id);
```

```sql
CREATE INDEX idx_student_grades_student_id
ON student_grades(student_id);
```

Use EXPLAIN ANALYZE:

```sql
EXPLAIN ANALYZE
SELECT
    s.first_name,
    s.last_name,
    sec.code
FROM students AS s
INNER JOIN student_sections AS ss ON ss.student_id = s.id
INNER JOIN sections AS sec ON ss.section_id = sec.id;
```

Compare:

```text
before indexes
after indexes
```

Look at:

```text
execution time
sequential scan vs index scan
```

[[#Navigation|⬆ Back to Navigation]]

---

# 73. SQL Command Cheat Sheet

```sql
CREATE DATABASE librarydb;
```

```sql
CREATE TABLE books (...);
```

```sql
INSERT INTO books (...) VALUES (...);
```

```sql
SELECT columns FROM table;
```

```sql
UPDATE table SET column = value WHERE condition;
```

```sql
DELETE FROM table WHERE condition;
```

```sql
CREATE INDEX index_name ON table(column);
```

```sql
ALTER TABLE table ADD CONSTRAINT constraint_name UNIQUE(column);
```

[[#Navigation|⬆ Back to Navigation]]

---

# 74. Clause Order Cheat Sheet

SQL clause order:

```sql
SELECT
FROM
JOIN
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT
OFFSET
```

Example:

```sql
SELECT
    genre,
    COUNT(*) AS total
FROM books
WHERE available = TRUE
GROUP BY genre
HAVING COUNT(*) > 1
ORDER BY total DESC
LIMIT 5;
```

Execution idea:

```text
FROM/JOIN builds source data
WHERE filters rows
GROUP BY groups rows
HAVING filters groups
SELECT chooses output
ORDER BY sorts output
LIMIT/OFFSET trims output
```

[[#Navigation|⬆ Back to Navigation]]

---

# 75. Common SQL Mistakes

```text
forgetting semicolon
using = NULL instead of IS NULL
using WHERE with aggregate functions instead of HAVING
forgetting WHERE in UPDATE or DELETE
creating child table before parent table
forgetting foreign key constraints
storing repeated data instead of normalizing
using SELECT * too much
using INNER JOIN when LEFT JOIN is needed
forgetting GROUP BY when using aggregates with normal columns
adding indexes blindly without checking query patterns
```

[[#Navigation|⬆ Back to Navigation]]

---

# 76. PostgreSQL Tips and Tricks

```text
Use RETURNING after INSERT to get generated IDs.
Use ILIKE for case-insensitive search.
Use LIMIT and OFFSET for pagination.
Use LEFT JOIN to find missing relationships.
Use WHERE returned_at IS NULL for active loans.
Use COUNT(column) when you want non-null values only.
Use CHECK constraints for valid ranges.
Use DEFAULT NOW() for created timestamps.
Use TIMESTAMPTZ for created_at and loaned_at.
Use EXPLAIN ANALYZE to inspect performance.
Use CTEs to make long queries readable.
```

Safe workflow for destructive commands:

```text
1. Write SELECT with the target WHERE.
2. Verify affected rows.
3. Convert to UPDATE or DELETE.
4. Keep the WHERE clause.
5. Use RETURNING to verify changes.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 77. Final Key Takeaways

```text
A database solves the limitations of static in-memory lists.
PostgreSQL stores data persistently.
Tables are like CSharp class definitions.
Rows are like object instances.
Columns are like properties.
Primary keys uniquely identify rows.
Foreign keys connect related tables.
Constraints protect data integrity.
CREATE TABLE defines structure.
INSERT adds rows.
SELECT reads rows.
WHERE filters rows.
ORDER BY sorts rows.
UPDATE modifies rows.
DELETE removes rows.
JOIN connects tables.
GROUP BY summarizes data.
HAVING filters grouped results.
Indexes improve query performance.
Normalization reduces duplicate data.
Subqueries let one query use another query's result.
CTEs make complex queries readable.
Use pgAdmin or psql to test SQL queries.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 78. Final Review Checklist

```text
[ ] I can explain why static lists are not enough.
[ ] I can explain what PostgreSQL is.
[ ] I can explain table, row, column, and schema.
[ ] I can explain primary key and foreign key.
[ ] I can create a database.
[ ] I can connect using psql.
[ ] I can use pgAdmin Query Tool.
[ ] I can choose common PostgreSQL data types.
[ ] I can create tables with constraints.
[ ] I can insert one row.
[ ] I can insert multiple rows.
[ ] I can use RETURNING.
[ ] I can select specific columns.
[ ] I can filter with WHERE.
[ ] I can search with ILIKE.
[ ] I can check NULL with IS NULL.
[ ] I can sort with ORDER BY.
[ ] I can safely update rows.
[ ] I can safely delete rows.
[ ] I can write INNER JOIN queries.
[ ] I can write LEFT JOIN queries.
[ ] I can use COUNT, AVG, MIN, and MAX.
[ ] I can use GROUP BY.
[ ] I can use HAVING.
[ ] I can explain indexes.
[ ] I can create indexes on foreign keys.
[ ] I can explain normalization.
[ ] I can identify unnormalized repeated data.
[ ] I can write subqueries.
[ ] I can write CTEs.
[ ] I can design the student enrollment schema.
[ ] I can query students, sections, programs, and grades with JOINs.
```

[[#Navigation|⬆ Back to Navigation]]
