# PostgreSQL to EF Core in ASP.NET Core Web API — Transition Reviewer, Guide, and Cheat Sheet

Tags: #aspnet #dotnet #webapi #postgresql #efcore #npgsql #database #sql #migrations #dbcontext #crud #obsidian

---

# Purpose

This is a **transition reviewer** from:

```text
ASP.NET Core Web API with in-memory lists
```

to:

```text
ASP.NET Core Web API with PostgreSQL + EF Core
```

It is written as:

```text
reviewer
+ cheat sheet
+ tutorial guide
+ reference material
```

Main goal:

```text
Understand how your API moves from temporary RAM data to a real PostgreSQL database using EF Core.
```

---

# Navigation

## A. Learning Path

- [[#0. How to Use This Reviewer|0. How to Use This Reviewer]]
- [[#1. Big Picture Transition|1. Big Picture Transition]]
- [[#2. What Changes from In-Memory to Database|2. What Changes from In-Memory to Database]]
- [[#3. Full Request Flow Before and After EF Core|3. Full Request Flow Before and After EF Core]]
- [[#4. Mental Model Summary|4. Mental Model Summary]]

## B. PostgreSQL Foundation Before EF Core

- [[#5. Why PostgreSQL Is Needed|5. Why PostgreSQL Is Needed]]
- [[#6. Relational Model Review|6. Relational Model Review]]
- [[#7. Table, Row, Column, Schema|7. Table, Row, Column, Schema]]
- [[#8. Primary Keys and Foreign Keys|8. Primary Keys and Foreign Keys]]
- [[#9. Relationships|9. Relationships]]
- [[#10. PostgreSQL Data Types|10. PostgreSQL Data Types]]
- [[#11. Constraints|11. Constraints]]
- [[#12. SQL CRUD Review|12. SQL CRUD Review]]
- [[#13. JOINs Review|13. JOINs Review]]
- [[#14. Aggregates and GROUP BY Review|14. Aggregates and GROUP BY Review]]
- [[#15. Indexes Review|15. Indexes Review]]
- [[#16. Normalization Review|16. Normalization Review]]
- [[#17. ACID and Transactions|17. ACID and Transactions]]

## C. EF Core Foundation

- [[#18. What EF Core Is|18. What EF Core Is]]
- [[#19. What Npgsql Is|19. What Npgsql Is]]
- [[#20. EF Core vs Raw SQL|20. EF Core vs Raw SQL]]
- [[#21. Entity, DbContext, DbSet|21. Entity, DbContext, DbSet]]
- [[#22. Entity Mapping Mental Model|22. Entity Mapping Mental Model]]
- [[#23. Change Tracking|23. Change Tracking]]
- [[#24. SaveChanges and SaveChangesAsync|24. SaveChanges and SaveChangesAsync]]
- [[#25. LINQ to SQL Translation|25. LINQ to SQL Translation]]
- [[#26. IQueryable vs IEnumerable|26. IQueryable vs IEnumerable]]

## D. Setup from Scratch

- [[#27. Create the ASP.NET Core Web API Project|27. Create the ASP.NET Core Web API Project]]
- [[#28. Install Required Packages|28. Install Required Packages]]
- [[#29. Create PostgreSQL Database|29. Create PostgreSQL Database]]
- [[#30. Add Connection String|30. Add Connection String]]
- [[#31. Create AppDbContext|31. Create AppDbContext]]
- [[#32. Register DbContext in Program.cs|32. Register DbContext in Program.cs]]
- [[#33. Recommended Project Folder Structure|33. Recommended Project Folder Structure]]
- [[#34. Safe Handling of Database Passwords|34. Safe Handling of Database Passwords]]

## E. Designing the Database with CSharp Entities

- [[#35. In-Memory Model vs EF Core Entity|35. In-Memory Model vs EF Core Entity]]
- [[#36. Student Entity|36. Student Entity]]
- [[#37. Program Entity|37. Program Entity]]
- [[#38. Section Entity|38. Section Entity]]
- [[#39. StudentSection Entity Junction Table|39. StudentSection Entity Junction Table]]
- [[#40. StudentGrade Entity|40. StudentGrade Entity]]
- [[#41. Entity Relationship Summary|41. Entity Relationship Summary]]
- [[#42. Navigation Properties vs Foreign Key Properties|42. Navigation Properties vs Foreign Key Properties]]
- [[#43. DataAnnotations vs Fluent API|43. DataAnnotations vs Fluent API]]
- [[#44. Fluent API Relationship Configuration|44. Fluent API Relationship Configuration]]

## F. Migrations

- [[#45. What Migrations Are|45. What Migrations Are]]
- [[#46. Add First Migration|46. Add First Migration]]
- [[#47. Apply Migration to PostgreSQL|47. Apply Migration to PostgreSQL]]
- [[#48. Migration Files Explained|48. Migration Files Explained]]
- [[#49. Common Migration Workflow|49. Common Migration Workflow]]
- [[#50. Undo, Remove, or Reset Migrations|50. Undo, Remove, or Reset Migrations]]
- [[#51. When to Use Migrations vs Manual SQL|51. When to Use Migrations vs Manual SQL]]

## G. DTOs Still Matter

- [[#52. Why DTOs Still Matter with EF Core|52. Why DTOs Still Matter with EF Core]]
- [[#53. Create DTO|53. Create DTO]]
- [[#54. Update DTO|54. Update DTO]]
- [[#55. Patch DTO|55. Patch DTO]]
- [[#56. Response DTO|56. Response DTO]]
- [[#57. DTO vs Entity Examples|57. DTO vs Entity Examples]]
- [[#58. Mapping Entity to DTO|58. Mapping Entity to DTO]]

## H. Service Layer with EF Core

- [[#59. Why DbContext Should Usually Be Used in Services|59. Why DbContext Should Usually Be Used in Services]]
- [[#60. Service Interface with Async Methods|60. Service Interface with Async Methods]]
- [[#61. Injecting DbContext into a Service|61. Injecting DbContext into a Service]]
- [[#62. Service Lifetime with DbContext|62. Service Lifetime with DbContext]]
- [[#63. Replacing In-Memory List Logic|63. Replacing In-Memory List Logic]]
- [[#64. Common Service Helper Methods|64. Common Service Helper Methods]]

## I. CRUD Tutorial — In-Memory to EF Core

- [[#65. GET All Transition|65. GET All Transition]]
- [[#66. GET By Id Transition|66. GET By Id Transition]]
- [[#67. POST Create Transition|67. POST Create Transition]]
- [[#68. PUT Full Update Transition|68. PUT Full Update Transition]]
- [[#69. PATCH Partial Update Transition|69. PATCH Partial Update Transition]]
- [[#70. DELETE Transition|70. DELETE Transition]]
- [[#71. Search, Filter, Sort, Pagination Transition|71. Search, Filter, Sort, Pagination Transition]]
- [[#72. Duplicate Checking Transition|72. Duplicate Checking Transition]]

## J. Relationships with EF Core

- [[#73. Loading Related Data|73. Loading Related Data]]
- [[#74. Include|74. Include]]
- [[#75. ThenInclude|75. ThenInclude]]
- [[#76. Projection Instead of Include|76. Projection Instead of Include]]
- [[#77. Create Student Under Section|77. Create Student Under Section]]
- [[#78. Query Students with Program and Section|78. Query Students with Program and Section]]
- [[#79. Query Average Grades|79. Query Average Grades]]
- [[#80. Find Unassigned Students or Empty Sections|80. Find Unassigned Students or Empty Sections]]

## K. Complete Tutorial Build

- [[#81. Step 1 Create Project|81. Step 1 Create Project]]
- [[#82. Step 2 Install Packages|82. Step 2 Install Packages]]
- [[#83. Step 3 Configure appsettings.json|83. Step 3 Configure appsettings.json]]
- [[#84. Step 4 Create Entities|84. Step 4 Create Entities]]
- [[#85. Step 5 Create AppDbContext|85. Step 5 Create AppDbContext]]
- [[#86. Step 6 Register DbContext and Services|86. Step 6 Register DbContext and Services]]
- [[#87. Step 7 Create DTOs|87. Step 7 Create DTOs]]
- [[#88. Step 8 Create Service Interface|88. Step 8 Create Service Interface]]
- [[#89. Step 9 Create Service Implementation|89. Step 9 Create Service Implementation]]
- [[#90. Step 10 Create Controller|90. Step 10 Create Controller]]
- [[#91. Step 11 Add Migration and Update Database|91. Step 11 Add Migration and Update Database]]
- [[#92. Step 12 Test in Postman|92. Step 12 Test in Postman]]

## L. Commands and Cheat Sheets

- [[#93. PostgreSQL psql Commands|93. PostgreSQL psql Commands]]
- [[#94. SQL Command Cheat Sheet|94. SQL Command Cheat Sheet]]
- [[#95. dotnet ef Command Cheat Sheet|95. dotnet ef Command Cheat Sheet]]
- [[#96. EF Core Method Cheat Sheet|96. EF Core Method Cheat Sheet]]
- [[#97. SQL to EF Core Translation Table|97. SQL to EF Core Translation Table]]
- [[#98. HTTP to SQL to EF Core Mapping|98. HTTP to SQL to EF Core Mapping]]
- [[#99. PostgreSQL Type to CSharp Type Cheat Sheet|99. PostgreSQL Type to CSharp Type Cheat Sheet]]

## M. Advanced but Important Concepts

- [[#100. Transactions in EF Core|100. Transactions in EF Core]]
- [[#101. Concurrency Preview|101. Concurrency Preview]]
- [[#102. Raw SQL with EF Core|102. Raw SQL with EF Core]]
- [[#103. Seeding Data|103. Seeding Data]]
- [[#104. Indexes in EF Core|104. Indexes in EF Core]]
- [[#105. Soft Delete with EF Core|105. Soft Delete with EF Core]]

## N. Debugging and Common Errors

- [[#106. Common Connection Errors|106. Common Connection Errors]]
- [[#107. Common Migration Errors|107. Common Migration Errors]]
- [[#108. Common Query Errors|108. Common Query Errors]]
- [[#109. Common API Errors After Switching to Database|109. Common API Errors After Switching to Database]]
- [[#110. Debugging Checklist|110. Debugging Checklist]]

## O. Final Review

- [[#111. Tips and Tricks|111. Tips and Tricks]]
- [[#112. Best Practices|112. Best Practices]]
- [[#113. Final Transition Summary|113. Final Transition Summary]]
- [[#114. Final Review Checklist|114. Final Review Checklist]]

---

# 0. How to Use This Reviewer

Use this file in three ways:

## As a guide

Follow sections 81 to 92 to build a working database-backed ASP.NET Core Web API.

## As a reviewer

Use the navigation to revisit PostgreSQL, EF Core, DbContext, migrations, DTOs, services, and CRUD.

## As a cheat sheet

Use sections 93 to 99 for commands and quick translation tables.

Best study order:

```text
1. Understand why the static list must be replaced.
2. Review PostgreSQL tables and SQL.
3. Learn EF Core concepts.
4. Set up DbContext and connection string.
5. Create entities.
6. Add migrations.
7. Replace in-memory service code with DbContext code.
8. Test all endpoints in Postman.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 1. Big Picture Transition

Before database:

```text
ASP.NET Core Web API
↓
Controller
↓
Service
↓
static List<T> / in-memory store
```

After database:

```text
ASP.NET Core Web API
↓
Controller
↓
Service
↓
EF Core DbContext
↓
PostgreSQL database
```

The endpoint may stay the same:

```http
GET /api/students
POST /api/students
GET /api/students/1
PUT /api/students/1
PATCH /api/students/1
DELETE /api/students/1
```

But the storage changes.

Before:

```csharp
private static List<Student> _students = new();
```

After:

```csharp
private readonly AppDbContext _context;
```

Main takeaway:

```text
The API contract can stay the same.
The storage implementation changes from RAM to PostgreSQL.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 2. What Changes from In-Memory to Database

| Area | In-Memory Version | Database Version |
|---|---|---|
| Storage | `List<T>` | PostgreSQL table |
| Persistence | disappears on restart | survives restart |
| Querying | LINQ to objects | LINQ translated to SQL |
| Relationships | nested objects or strings | foreign keys and join tables |
| IDs | manually generated | database generated |
| Validation | mostly C# only | C# + database constraints |
| Performance | fine for tiny data | scalable with indexes |
| Multi-user | weak | designed for shared access |
| App restart | resets data | keeps data |

Important mindset:

```text
EF Core does not remove the need to understand SQL.
EF Core is a bridge between C# and SQL.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 3. Full Request Flow Before and After EF Core

## Before EF Core

```text
Client sends request
↓
Controller receives request
↓
Controller calls service
↓
Service reads/writes List<T>
↓
Service returns DTO
↓
Controller returns JSON
```

## After EF Core

```text
Client sends request
↓
Controller receives request
↓
Controller calls service
↓
Service uses AppDbContext
↓
EF Core translates LINQ/change tracking to SQL
↓
PostgreSQL executes SQL
↓
EF Core materializes C# objects
↓
Service maps entities to DTOs
↓
Controller returns JSON
```

Key idea:

```text
Controllers should not need to care whether the service uses List<T> or PostgreSQL.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 4. Mental Model Summary

```text
PostgreSQL = actual database
SQL = language used by the database
EF Core = C# library that talks to the database
Npgsql = PostgreSQL provider for EF Core
DbContext = database session in C#
DbSet<T> = table-like property in C#
Entity = C# class mapped to a table
Migration = generated schema change
DTO = API input/output shape
Service = business/data logic layer
Controller = HTTP layer
```

C# to PostgreSQL mapping:

```text
Entity class       → table
Entity object      → row
Entity property    → column
Primary key        → unique row identifier
Foreign key        → relationship link
DbSet<Student>     → students table access
DbContext          → database session
```

[[#Navigation|⬆ Back to Navigation]]

---

# 5. Why PostgreSQL Is Needed

In-memory data has limits:

```text
data disappears after restart
data cannot scale across multiple API instances
querying large data is slow
relationships are manual or messy
constraints are not enforced by a database
multi-user behavior can become unsafe
```

PostgreSQL solves this by providing:

```text
persistent disk storage
structured relational tables
SQL querying
constraints
foreign keys
indexes
transactions
multi-user database engine
```

Example limitation:

```csharp
private static List<Book> _books = new();
```

If the app restarts:

```text
_books returns to original seed data.
POSTed books disappear.
```

Database version:

```sql
INSERT INTO books (title)
VALUES ('Clean Code');
```

After app restart:

```text
The row is still in PostgreSQL.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 6. Relational Model Review

The relational model stores data in related tables.

Instead of one huge table:

```text
books_bad
- title
- author_name
- author_country
- author_birth_year
```

Use separate related tables:

```text
authors
- id
- full_name
- nationality

books
- id
- title
- author_id
```

Relationship:

```text
books.author_id references authors.id
```

Reason:

```text
Author data is stored once.
Books link to the author.
Repeated data is avoided.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 7. Table, Row, Column, Schema

| Database Concept | Meaning | C# Equivalent |
|---|---|---|
| Table | structure containing records | class/list collection |
| Row | one record | object instance |
| Column | field in the table | property |
| Schema | database structure | project model structure |
| Constraint | database rule | validation/rule |
| Primary key | unique row ID | `Id` property |
| Foreign key | link to another table | reference ID |

SQL:

```sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    available BOOLEAN NOT NULL DEFAULT TRUE
);
```

C#:

```csharp
public class Book
{
    public int Id { get; set; }
    public string Title { get; set; } = string.Empty;
    public bool Available { get; set; } = true;
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 8. Primary Keys and Foreign Keys

## Primary key

A primary key uniquely identifies a row.

```sql
id SERIAL PRIMARY KEY
```

Properties:

```text
unique
not null
stable identity
usually indexed automatically
```

## Foreign key

A foreign key references another table's primary key.

```sql
author_id INT REFERENCES authors(id)
```

Meaning:

```text
A book's author_id must point to an existing author.
```

EF Core equivalent:

```csharp
public int AuthorId { get; set; }
public Author? Author { get; set; }
```

[[#Navigation|⬆ Back to Navigation]]

---

# 9. Relationships

## One-to-many

One author has many books.

```text
authors 1 → many books
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

EF Core:

```csharp
public class Author
{
    public int Id { get; set; }
    public List<Book> Books { get; set; } = new();
}

public class Book
{
    public int Id { get; set; }
    public int? AuthorId { get; set; }
    public Author? Author { get; set; }
}
```

## Many-to-many

Students and sections can be many-to-many.

Use a junction table:

```sql
CREATE TABLE student_sections (
    id SERIAL PRIMARY KEY,
    student_id INT REFERENCES students(id),
    section_id INT REFERENCES sections(id)
);
```

EF Core explicit join entity:

```csharp
public class StudentSection
{
    public int Id { get; set; }

    public int StudentId { get; set; }
    public Student? Student { get; set; }

    public int SectionId { get; set; }
    public Section? Section { get; set; }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 10. PostgreSQL Data Types

Common types:

| PostgreSQL | Use | C# |
|---|---|---|
| `INT` | normal whole numbers | `int` |
| `BIGINT` | large whole numbers | `long` |
| `SERIAL` | auto-increment int | `int` |
| `BIGSERIAL` | auto-increment long | `long` |
| `NUMERIC(p,s)` | exact decimal | `decimal` |
| `BOOLEAN` | true/false | `bool` |
| `VARCHAR(n)` | limited text | `string` |
| `TEXT` | unrestricted text | `string` |
| `TIMESTAMP` | date + time | `DateTime` |
| `TIMESTAMPTZ` | timestamp with timezone handling | `DateTime` |
| `UUID` | globally unique ID | `Guid` |
| `JSONB` | queryable JSON | string/object depending setup |

Tips:

```text
Use SERIAL for beginner primary keys.
Use NUMERIC/DECIMAL for money.
Use BOOLEAN for true/false.
Use TIMESTAMPTZ for created_at.
Use TEXT unless there is a real max length rule.
Use VARCHAR(n) when length itself matters.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 11. Constraints

Constraints are database rules.

| Constraint | Meaning |
|---|---|
| `PRIMARY KEY` | unique row identifier |
| `NOT NULL` | value is required |
| `UNIQUE` | no duplicate values |
| `CHECK` | custom rule |
| `DEFAULT` | value if none supplied |
| `REFERENCES` | foreign key |

Example:

```sql
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    student_number VARCHAR(50) NOT NULL UNIQUE,
    first_name VARCHAR(100) NOT NULL,
    year INT NOT NULL CHECK (year BETWEEN 1 AND 4),
    enrolled BOOLEAN NOT NULL DEFAULT TRUE,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

EF Core equivalent:

```csharp
modelBuilder.Entity<Student>()
    .HasIndex(s => s.StudentNumber)
    .IsUnique();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 12. SQL CRUD Review

## SELECT

```sql
SELECT id, first_name, last_name
FROM students;
```

## INSERT

```sql
INSERT INTO students (student_number, first_name, last_name, year)
VALUES ('2024-0001', 'Ana', 'Reyes', 2)
RETURNING id;
```

## UPDATE

```sql
UPDATE students
SET year = 3
WHERE id = 1
RETURNING id, first_name, year;
```

## DELETE

```sql
DELETE FROM students
WHERE id = 1;
```

Safety rule:

```text
Always use WHERE with UPDATE and DELETE unless you intentionally want to affect all rows.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 13. JOINs Review

JOIN connects related tables.

Example:

```sql
SELECT
    s.first_name,
    s.last_name,
    sec.code AS section_code
FROM students AS s
INNER JOIN student_sections AS ss ON ss.student_id = s.id
INNER JOIN sections AS sec ON ss.section_id = sec.id;
```

## INNER JOIN

```text
Only rows with matches on both sides.
```

## LEFT JOIN

```text
All rows from the left table, even if the right side has no match.
```

Find students with no section:

```sql
SELECT
    s.id,
    s.first_name,
    s.last_name
FROM students AS s
LEFT JOIN student_sections AS ss ON ss.student_id = s.id
WHERE ss.id IS NULL;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 14. Aggregates and GROUP BY Review

Aggregate functions:

```text
COUNT
SUM
AVG
MIN
MAX
```

Count students per section:

```sql
SELECT
    sec.code,
    COUNT(ss.student_id) AS total_students
FROM sections AS sec
LEFT JOIN student_sections AS ss ON ss.section_id = sec.id
GROUP BY sec.id, sec.code
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
GROUP BY s.id, s.first_name, s.last_name;
```

Rule:

```text
WHERE filters rows before grouping.
HAVING filters groups after grouping.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 15. Indexes Review

Indexes improve query performance.

SQL:

```sql
CREATE INDEX idx_student_sections_student_id
ON student_sections(student_id);
```

Common columns to index:

```text
foreign keys
frequently searched columns
columns used in JOIN
columns used in ORDER BY
unique business keys
```

Tradeoff:

```text
Indexes speed up reads.
Indexes add cost to writes.
```

Check performance:

```sql
EXPLAIN ANALYZE
SELECT *
FROM student_sections
WHERE student_id = 1;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 16. Normalization Review

Normalization reduces duplicate data.

Bad:

```text
students table contains program_name and program_department repeatedly
```

Better:

```text
programs table stores program details
sections table references programs
students relate to sections
```

3NF beginner rule:

```text
Each fact should be stored once.
If data repeats, consider another table.
```

Example:

```sql
CREATE TABLE programs (
    id SERIAL PRIMARY KEY,
    program_name VARCHAR(150) NOT NULL UNIQUE
);
```

```sql
CREATE TABLE sections (
    id SERIAL PRIMARY KEY,
    code VARCHAR(50) NOT NULL UNIQUE,
    program_id INT NOT NULL REFERENCES programs(id)
);
```

[[#Navigation|⬆ Back to Navigation]]

---

# 17. ACID and Transactions

ACID describes reliable database transactions.

| Letter | Meaning | Simple Memory |
|---|---|---|
| A | Atomicity | all or nothing |
| C | Consistency | database rules stay valid |
| I | Isolation | transactions do not interfere incorrectly |
| D | Durability | committed data stays saved |

Example transaction:

```sql
BEGIN;

INSERT INTO students (first_name, last_name, year)
VALUES ('Ana', 'Reyes', 2);

INSERT INTO student_grades (student_id, grade)
VALUES (1, 95);

COMMIT;
```

If something fails:

```sql
ROLLBACK;
```

EF Core usually wraps one `SaveChangesAsync()` in a transaction.

```csharp
_context.Students.Add(student);
_context.StudentGrades.Add(grade);

await _context.SaveChangesAsync();
```

For multiple save operations:

```csharp
using var transaction = await _context.Database.BeginTransactionAsync();

try
{
    _context.Students.Add(student);
    await _context.SaveChangesAsync();

    _context.StudentGrades.Add(grade);
    await _context.SaveChangesAsync();

    await transaction.CommitAsync();
}
catch
{
    await transaction.RollbackAsync();
    throw;
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 18. What EF Core Is

EF Core means:

```text
Entity Framework Core
```

It is an Object-Relational Mapper.

Meaning:

```text
C# objects
↔
database rows
```

Instead of manually writing SQL for everything:

```sql
SELECT *
FROM students
WHERE id = 1;
```

you write C#:

```csharp
var student = await _context.Students
    .FirstOrDefaultAsync(s => s.Id == 1);
```

EF Core translates many LINQ queries into SQL.

[[#Navigation|⬆ Back to Navigation]]

---

# 19. What Npgsql Is

Npgsql is the PostgreSQL provider/driver used by .NET and EF Core.

In this stack:

```text
ASP.NET Core
↓
EF Core
↓
Npgsql EF Core provider
↓
PostgreSQL
```

Package:

```bash
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL
```

Use in Program.cs:

```csharp
options.UseNpgsql(connectionString)
```

[[#Navigation|⬆ Back to Navigation]]

---

# 20. EF Core vs Raw SQL

Raw SQL:

```sql
SELECT *
FROM students
WHERE year = 2;
```

EF Core:

```csharp
var students = await _context.Students
    .Where(s => s.Year == 2)
    .ToListAsync();
```

Raw SQL strengths:

```text
full SQL control
advanced query tuning
database-specific features
```

EF Core strengths:

```text
C# LINQ queries
change tracking
migrations
strong typing
integration with dependency injection
less repetitive CRUD SQL
```

Best mindset:

```text
Know SQL.
Use EF Core for application code.
Use raw SQL when EF Core is not the best tool for a specific query.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 21. Entity, DbContext, DbSet

## Entity

C# class that maps to a database table.

```csharp
public class Student
{
    public int Id { get; set; }
    public string FirstName { get; set; } = string.Empty;
}
```

## DbContext

Database session object.

```csharp
public class AppDbContext : DbContext
{
}
```

## DbSet

Table-like access point.

```csharp
public DbSet<Student> Students { get; set; }
```

Mental mapping:

```text
Student entity → students table
Student object → one row
Student property → one column
DbSet<Student> → query/modify students table
AppDbContext → database session
```

[[#Navigation|⬆ Back to Navigation]]

---

# 22. Entity Mapping Mental Model

EF Core conventions:

```text
Id property becomes primary key.
DbSet<Student> Students becomes a table.
String properties become text/varchar-like columns depending config.
Navigation properties define relationships.
Foreign key properties connect relationships.
```

Example:

```csharp
public int SectionId { get; set; }
public Section? Section { get; set; }
```

This means:

```text
Student has a foreign key to Section.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 23. Change Tracking

EF Core tracks entities loaded from the database.

Example:

```csharp
var student = await _context.Students.FindAsync(id);

student.FirstName = "Maria";

await _context.SaveChangesAsync();
```

EF Core detects:

```text
student existed in database
FirstName changed
UPDATE should be sent
```

Entity states:

```text
Added
Modified
Deleted
Unchanged
Detached
```

[[#Navigation|⬆ Back to Navigation]]

---

# 24. SaveChanges and SaveChangesAsync

`Add()` only prepares an insert.

```csharp
_context.Students.Add(student);
```

`SaveChangesAsync()` commits it.

```csharp
await _context.SaveChangesAsync();
```

Update pattern:

```csharp
student.FirstName = dto.FirstName.Trim();
await _context.SaveChangesAsync();
```

Delete pattern:

```csharp
_context.Students.Remove(student);
await _context.SaveChangesAsync();
```

Key rule:

```text
No SaveChangesAsync means no database write.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 25. LINQ to SQL Translation

LINQ query:

```csharp
var students = await _context.Students
    .Where(s => s.Year == 2)
    .OrderBy(s => s.LastName)
    .ToListAsync();
```

SQL idea:

```sql
SELECT *
FROM students
WHERE year = 2
ORDER BY last_name;
```

Projection:

```csharp
var result = await _context.Students
    .Select(s => new StudentResponseDto
    {
        Id = s.Id,
        FullName = s.FirstName + " " + s.LastName
    })
    .ToListAsync();
```

SQL idea:

```sql
SELECT id, first_name, last_name
FROM students;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 26. IQueryable vs IEnumerable

`IQueryable`:

```text
query not executed yet
can still become SQL
```

Example:

```csharp
IQueryable<Student> query = _context.Students;

query = query.Where(s => s.Year == 2);
query = query.OrderBy(s => s.LastName);

var result = await query.ToListAsync();
```

`IEnumerable`:

```text
already in memory or treated as C# sequence
LINQ runs in C# memory
```

Best EF Core habit:

```text
Build query as IQueryable.
Execute once at the end with ToListAsync, FirstOrDefaultAsync, AnyAsync, etc.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 27. Create the ASP.NET Core Web API Project

Create project:

```bash
dotnet new webapi -n StudentEnrollmentApi
cd StudentEnrollmentApi
code .
```

Run:

```bash
dotnet run
```

Hot reload:

```bash
dotnet watch
```

Expected:

```text
Now listening on: https://localhost:xxxx
```

[[#Navigation|⬆ Back to Navigation]]

---

# 28. Install Required Packages

Install EF Core PostgreSQL packages:

```bash
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.Design
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL
```

Install EF CLI tool:

```bash
dotnet tool install --global dotnet-ef
```

If already installed:

```bash
dotnet tool update --global dotnet-ef
```

Check:

```bash
dotnet ef
```

[[#Navigation|⬆ Back to Navigation]]

---

# 29. Create PostgreSQL Database

Using psql:

```bash
psql -U postgres
```

Create database:

```sql
CREATE DATABASE student_enrollment_db;
```

Connect:

```sql
\c student_enrollment_db
```

List tables:

```sql
\dt
```

Exit:

```sql
\q
```

Tip:

```text
Make sure your connection string uses this exact database name.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 30. Add Connection String

`appsettings.json`:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Database=student_enrollment_db;Username=postgres;Password=yourpassword"
  }
}
```

Parts:

```text
Host = PostgreSQL server
Port = usually 5432
Database = target database
Username = PostgreSQL user
Password = PostgreSQL password
```

Read it:

```csharp
builder.Configuration.GetConnectionString("DefaultConnection")
```

[[#Navigation|⬆ Back to Navigation]]

---

# 31. Create AppDbContext

Create:

```text
Data/AppDbContext.cs
```

Code:

```csharp
using Microsoft.EntityFrameworkCore;
using StudentEnrollmentApi.Models;

namespace StudentEnrollmentApi.Data;

public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options)
        : base(options)
    {
    }

    public DbSet<Student> Students { get; set; }

    public DbSet<ProgramEntity> Programs { get; set; }

    public DbSet<Section> Sections { get; set; }

    public DbSet<StudentSection> StudentSections { get; set; }

    public DbSet<StudentGrade> StudentGrades { get; set; }
}
```

Note:

```text
ProgramEntity is used instead of Program because Program is commonly associated with Program.cs.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 32. Register DbContext in Program.cs

```csharp
using Microsoft.EntityFrameworkCore;
using StudentEnrollmentApi.Data;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseNpgsql(
        builder.Configuration.GetConnectionString("DefaultConnection")
    ));

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Meaning:

```text
AddDbContext registers AppDbContext in dependency injection.
UseNpgsql tells EF Core to use PostgreSQL.
The connection string tells EF Core where the database is.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 33. Recommended Project Folder Structure

```text
StudentEnrollmentApi/
├── Controllers/
│   ├── StudentsController.cs
│   ├── SectionsController.cs
│   └── ProgramsController.cs
├── Data/
│   └── AppDbContext.cs
├── DTOs/
│   ├── Students/
│   ├── Sections/
│   └── Programs/
├── Models/
│   ├── Student.cs
│   ├── ProgramEntity.cs
│   ├── Section.cs
│   ├── StudentSection.cs
│   └── StudentGrade.cs
├── Services/
│   ├── Students/
│   ├── Sections/
│   └── Programs/
├── Migrations/
├── Program.cs
└── appsettings.json
```

[[#Navigation|⬆ Back to Navigation]]

---

# 34. Safe Handling of Database Passwords

For local bootcamp work, appsettings may be acceptable.

But avoid committing real passwords to public GitHub.

Better options:

```text
dotnet user-secrets
environment variables
deployment provider secrets
```

User secrets:

```bash
dotnet user-secrets init
dotnet user-secrets set "ConnectionStrings:DefaultConnection" "Host=localhost;Port=5432;Database=student_enrollment_db;Username=postgres;Password=yourpassword"
```

[[#Navigation|⬆ Back to Navigation]]

---

# 35. In-Memory Model vs EF Core Entity

In-memory model:

```csharp
public class Student
{
    public int Id { get; set; }
    public string FirstName { get; set; } = string.Empty;
}
```

EF Core entity may include:

```text
primary key
foreign keys
navigation properties
created_at
updated_at
database constraints
```

Example:

```csharp
public class Student
{
    public int Id { get; set; }

    public string StudentNumber { get; set; } = string.Empty;

    public string FirstName { get; set; } = string.Empty;

    public string LastName { get; set; } = string.Empty;

    public int Year { get; set; }

    public bool Enrolled { get; set; } = true;

    public DateTime CreatedAt { get; set; } = DateTime.UtcNow;

    public List<StudentSection> StudentSections { get; set; } = new();

    public List<StudentGrade> Grades { get; set; } = new();
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 36. Student Entity

```csharp
namespace StudentEnrollmentApi.Models;

public class Student
{
    public int Id { get; set; }

    public string StudentNumber { get; set; } = string.Empty;

    public string FirstName { get; set; } = string.Empty;

    public string LastName { get; set; } = string.Empty;

    public int Year { get; set; }

    public string? Gender { get; set; }

    public bool Enrolled { get; set; } = true;

    public DateTime CreatedAt { get; set; } = DateTime.UtcNow;

    public List<StudentSection> StudentSections { get; set; } = new();

    public List<StudentGrade> Grades { get; set; } = new();
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 37. Program Entity

```csharp
namespace StudentEnrollmentApi.Models;

public class ProgramEntity
{
    public int Id { get; set; }

    public string ProgramName { get; set; } = string.Empty;

    public List<Section> Sections { get; set; } = new();
}
```

Why separate programs?

```text
Program names repeat across many sections.
Separate table prevents duplication.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 38. Section Entity

```csharp
namespace StudentEnrollmentApi.Models;

public class Section
{
    public int Id { get; set; }

    public string Code { get; set; } = string.Empty;

    public int Year { get; set; }

    public int ProgramEntityId { get; set; }

    public ProgramEntity? Program { get; set; }

    public List<StudentSection> StudentSections { get; set; } = new();
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 39. StudentSection Entity Junction Table

```csharp
namespace StudentEnrollmentApi.Models;

public class StudentSection
{
    public int Id { get; set; }

    public int StudentId { get; set; }

    public Student? Student { get; set; }

    public int SectionId { get; set; }

    public Section? Section { get; set; }

    public DateTime EnrolledAt { get; set; } = DateTime.UtcNow;
}
```

Purpose:

```text
Represents student assignment to a section.
Allows many-to-many style relationship.
Prevents storing section lists inside students.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 40. StudentGrade Entity

```csharp
namespace StudentEnrollmentApi.Models;

public class StudentGrade
{
    public int Id { get; set; }

    public int StudentId { get; set; }

    public Student? Student { get; set; }

    public decimal Grade { get; set; }
}
```

Why not store grades as array/list column?

```text
Grades need filtering, averaging, counting, and joining.
Each grade should be a row.
This follows normalization.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 41. Entity Relationship Summary

```text
ProgramEntity
1 → many Sections

Section
many → many Students through StudentSection

Student
1 → many StudentGrades
```

Visual:

```text
programs
   ↓
sections
   ↓
student_sections
   ↓
students
   ↓
student_grades
```

[[#Navigation|⬆ Back to Navigation]]

---

# 42. Navigation Properties vs Foreign Key Properties

Foreign key:

```csharp
public int SectionId { get; set; }
```

Navigation:

```csharp
public Section? Section { get; set; }
```

Collection navigation:

```csharp
public List<StudentSection> StudentSections { get; set; } = new();
```

Difference:

```text
Foreign key stores the ID.
Navigation property lets EF Core access the related object.
Collection navigation represents many related rows.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 43. DataAnnotations vs Fluent API

DataAnnotations example:

```csharp
using System.ComponentModel.DataAnnotations;

public class Student
{
    [Key]
    public int Id { get; set; }

    [Required]
    [MaxLength(100)]
    public string FirstName { get; set; } = string.Empty;
}
```

Fluent API example:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Student>()
        .HasIndex(s => s.StudentNumber)
        .IsUnique();
}
```

Beginner rule:

```text
Use conventions first.
Use DataAnnotations for simple validation/mapping.
Use Fluent API for relationships, indexes, unique constraints, and advanced mapping.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 44. Fluent API Relationship Configuration

Inside `AppDbContext`:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Student>()
        .HasIndex(s => s.StudentNumber)
        .IsUnique();

    modelBuilder.Entity<ProgramEntity>()
        .HasIndex(p => p.ProgramName)
        .IsUnique();

    modelBuilder.Entity<Section>()
        .HasIndex(s => s.Code)
        .IsUnique();

    modelBuilder.Entity<StudentSection>()
        .HasIndex(ss => new { ss.StudentId, ss.SectionId })
        .IsUnique();

    modelBuilder.Entity<StudentGrade>()
        .Property(g => g.Grade)
        .HasPrecision(5, 2);

    modelBuilder.Entity<Student>()
        .Property(s => s.Year)
        .HasColumnName("year");
}
```

Note:

```text
HasIndex creates indexes.
IsUnique enforces uniqueness.
HasPrecision controls decimal precision.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 45. What Migrations Are

Migrations are EF Core's way of turning C# model changes into database schema changes.

Flow:

```text
Change entity classes
↓
Create migration
↓
EF Core generates migration file
↓
Apply migration
↓
PostgreSQL tables change
```

Example:

```bash
dotnet ef migrations add InitialCreate
dotnet ef database update
```

[[#Navigation|⬆ Back to Navigation]]

---

# 46. Add First Migration

Command:

```bash
dotnet ef migrations add InitialCreate
```

This creates:

```text
Migrations/
├── timestamp_InitialCreate.cs
├── timestamp_InitialCreate.Designer.cs
└── AppDbContextModelSnapshot.cs
```

Tip:

```text
Build the project before adding a migration.
```

```bash
dotnet build
```

[[#Navigation|⬆ Back to Navigation]]

---

# 47. Apply Migration to PostgreSQL

Command:

```bash
dotnet ef database update
```

Meaning:

```text
Apply pending migrations to the configured PostgreSQL database.
```

After this, check tables using psql:

```sql
\dt
```

or pgAdmin.

[[#Navigation|⬆ Back to Navigation]]

---

# 48. Migration Files Explained

Migration file has:

```csharp
protected override void Up(MigrationBuilder migrationBuilder)
{
    // changes to apply
}
```

and:

```csharp
protected override void Down(MigrationBuilder migrationBuilder)
{
    // changes to undo
}
```

Snapshot:

```text
EF Core's current memory of the model.
```

Tip:

```text
Read migrations before applying them.
They show what EF Core will do to the database.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 49. Common Migration Workflow

```bash
dotnet build
dotnet ef migrations add AddStudentTables
dotnet ef database update
dotnet run
```

After changing entities:

```text
1. Update entity class.
2. Build project.
3. Add migration.
4. Inspect migration.
5. Update database.
6. Test API.
```

Good migration names:

```text
InitialCreate
AddStudentGrades
AddProgramSections
MakeStudentNumberUnique
```

Bad names:

```text
Update1
Fix
NewMigration
asdf
```

[[#Navigation|⬆ Back to Navigation]]

---

# 50. Undo, Remove, or Reset Migrations

If migration was created but not applied:

```bash
dotnet ef migrations remove
```

If migration was already applied:

```bash
dotnet ef database update PreviousMigrationName
dotnet ef migrations remove
```

Drop database:

```bash
dotnet ef database drop
```

Warning:

```text
Dropping the database deletes data.
Only do this for local development if safe.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 51. When to Use Migrations vs Manual SQL

Use migrations when:

```text
EF Core owns the schema
you are building normal app tables
team needs versioned schema changes
deployment should apply schema changes
```

Use manual SQL when:

```text
learning SQL
testing queries in pgAdmin
writing reports
using database-specific advanced features
quick inspection/debugging
```

In this transition:

```text
Use SQL to understand PostgreSQL.
Use EF Core migrations to create/update schema from ASP.NET Core.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 52. Why DTOs Still Matter with EF Core

Even with a real database, do not use entities as your only request/response shape.

Entity:

```csharp
public class Student
{
    public int Id { get; set; }
    public string StudentNumber { get; set; } = string.Empty;
    public DateTime CreatedAt { get; set; }
}
```

Create DTO:

```csharp
public class StudentCreateDto
{
    public string StudentNumber { get; set; } = string.Empty;
}
```

Response DTO:

```csharp
public class StudentResponseDto
{
    public int Id { get; set; }
    public string StudentNumber { get; set; } = string.Empty;
    public DateTime CreatedAt { get; set; }
}
```

Key rule:

```text
Create DTO controls what client can send.
Response DTO controls what client receives.
Entity controls database shape.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 53. Create DTO

```csharp
namespace StudentEnrollmentApi.DTOs.Students;

public class StudentCreateDto
{
    public string StudentNumber { get; set; } = string.Empty;

    public string FirstName { get; set; } = string.Empty;

    public string LastName { get; set; } = string.Empty;

    public int Year { get; set; }

    public string? Gender { get; set; }
}
```

Client sends:

```json
{
  "studentNumber": "2024-0001",
  "firstName": "Ana",
  "lastName": "Reyes",
  "year": 2,
  "gender": "Female"
}
```

Client should not send:

```text
Id
CreatedAt
navigation properties
```

[[#Navigation|⬆ Back to Navigation]]

---

# 54. Update DTO

PUT/full update DTO:

```csharp
public class StudentUpdateDto
{
    public string StudentNumber { get; set; } = string.Empty;

    public string FirstName { get; set; } = string.Empty;

    public string LastName { get; set; } = string.Empty;

    public int Year { get; set; }

    public string? Gender { get; set; }

    public bool Enrolled { get; set; }
}
```

PUT means:

```text
Client sends complete replacement data.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 55. Patch DTO

PATCH/partial update DTO:

```csharp
public class StudentPatchDto
{
    public string? StudentNumber { get; set; }

    public string? FirstName { get; set; }

    public string? LastName { get; set; }

    public int? Year { get; set; }

    public string? Gender { get; set; }

    public bool? Enrolled { get; set; }
}
```

PATCH means:

```text
Client sends only fields to change.
Nullable properties allow "not provided" state.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 56. Response DTO

```csharp
public class StudentResponseDto
{
    public int Id { get; set; }

    public string StudentNumber { get; set; } = string.Empty;

    public string FullName { get; set; } = string.Empty;

    public int Year { get; set; }

    public string? Gender { get; set; }

    public bool Enrolled { get; set; }

    public DateTime CreatedAt { get; set; }
}
```

The frontend often needs:

```text
Id
CreatedAt
computed display fields
status fields
```

So include them intentionally in the response DTO.

[[#Navigation|⬆ Back to Navigation]]

---

# 57. DTO vs Entity Examples

Entity can have navigation properties:

```csharp
public List<StudentSection> StudentSections { get; set; } = new();
public List<StudentGrade> Grades { get; set; } = new();
```

Response DTO should usually avoid exposing full nested entity graphs by accident.

Better:

```csharp
public class StudentWithSectionDto
{
    public int Id { get; set; }

    public string FullName { get; set; } = string.Empty;

    public List<string> SectionCodes { get; set; } = new();

    public decimal? AverageGrade { get; set; }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 58. Mapping Entity to DTO

Helper:

```csharp
private static StudentResponseDto ToResponseDto(Student student)
{
    return new StudentResponseDto
    {
        Id = student.Id,
        StudentNumber = student.StudentNumber,
        FullName = student.FirstName + " " + student.LastName,
        Year = student.Year,
        Gender = student.Gender,
        Enrolled = student.Enrolled,
        CreatedAt = student.CreatedAt
    };
}
```

Projection:

```csharp
var students = await _context.Students
    .Select(s => new StudentResponseDto
    {
        Id = s.Id,
        StudentNumber = s.StudentNumber,
        FullName = s.FirstName + " " + s.LastName,
        Year = s.Year,
        Gender = s.Gender,
        Enrolled = s.Enrolled,
        CreatedAt = s.CreatedAt
    })
    .ToListAsync();
```

Tip:

```text
Projection is often more efficient because it selects only needed columns.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 59. Why DbContext Should Usually Be Used in Services

Avoid putting DbContext logic directly in controllers.

Controller should handle:

```text
route parameters
query parameters
request body
status codes
HTTP response
```

Service should handle:

```text
queries
business rules
duplicates
mapping
saving changes
database operations
```

Controller:

```csharp
[HttpGet("{id:int}")]
public async Task<IActionResult> GetById(int id)
{
    var student = await _studentService.GetByIdAsync(id);

    if (student is null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

Service:

```csharp
public async Task<StudentResponseDto?> GetByIdAsync(int id)
{
    var student = await _context.Students.FindAsync(id);

    return student is null ? null : ToResponseDto(student);
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 60. Service Interface with Async Methods

```csharp
public interface IStudentService
{
    Task<List<StudentResponseDto>> GetAllAsync();

    Task<StudentResponseDto?> GetByIdAsync(int id);

    Task<StudentResponseDto> CreateAsync(StudentCreateDto dto);

    Task<StudentResponseDto?> UpdateAsync(int id, StudentUpdateDto dto);

    Task<StudentResponseDto?> PatchAsync(int id, StudentPatchDto dto);

    Task<bool> DeleteAsync(int id);
}
```

Why async?

```text
Database calls involve waiting for I/O.
Async prevents blocking server threads while waiting.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 61. Injecting DbContext into a Service

```csharp
public class StudentService : IStudentService
{
    private readonly AppDbContext _context;

    public StudentService(AppDbContext context)
    {
        _context = context;
    }
}
```

Register service:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Register DbContext:

```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseNpgsql(connectionString));
```

[[#Navigation|⬆ Back to Navigation]]

---

# 62. Service Lifetime with DbContext

DbContext is usually scoped.

```text
one DbContext instance per HTTP request
```

Therefore services using DbContext should usually also be scoped.

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Avoid:

```text
Singleton service depending on DbContext
```

Why:

```text
Singleton lives for entire app.
DbContext is request-scoped.
That lifetime mismatch causes problems.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 63. Replacing In-Memory List Logic

## Get all

Before:

```csharp
return _students
    .Select(ToResponseDto)
    .ToList();
```

After:

```csharp
return await _context.Students
    .Select(s => new StudentResponseDto
    {
        Id = s.Id,
        FullName = s.FirstName + " " + s.LastName
    })
    .ToListAsync();
```

## Find by id

Before:

```csharp
var student = _students.FirstOrDefault(s => s.Id == id);
```

After:

```csharp
var student = await _context.Students.FirstOrDefaultAsync(s => s.Id == id);
```

## Add

Before:

```csharp
_students.Add(student);
```

After:

```csharp
_context.Students.Add(student);
await _context.SaveChangesAsync();
```

## Delete

Before:

```csharp
_students.Remove(student);
```

After:

```csharp
_context.Students.Remove(student);
await _context.SaveChangesAsync();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 64. Common Service Helper Methods

Normalize student number:

```csharp
private static string NormalizeStudentNumber(string value)
{
    return value.Trim().ToUpper();
}
```

Map entity to DTO:

```csharp
private static StudentResponseDto ToResponseDto(Student student)
{
    return new StudentResponseDto
    {
        Id = student.Id,
        StudentNumber = student.StudentNumber,
        FullName = student.FirstName + " " + student.LastName
    };
}
```

Generate full name:

```csharp
private static string GetFullName(Student student)
{
    return student.FirstName + " " + student.LastName;
}
```

Tip:

```text
If helper is used by many services, move it to Helpers or Extensions.
If helper is business logic, consider a service.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 65. GET All Transition

## In-memory

```csharp
public List<StudentResponseDto> GetAll()
{
    return _students
        .Select(ToResponseDto)
        .ToList();
}
```

## EF Core

```csharp
public async Task<List<StudentResponseDto>> GetAllAsync()
{
    return await _context.Students
        .OrderBy(s => s.LastName)
        .Select(s => new StudentResponseDto
        {
            Id = s.Id,
            StudentNumber = s.StudentNumber,
            FullName = s.FirstName + " " + s.LastName,
            Year = s.Year,
            Enrolled = s.Enrolled,
            CreatedAt = s.CreatedAt
        })
        .ToListAsync();
}
```

Controller:

```csharp
[HttpGet]
public async Task<IActionResult> GetAll()
{
    var students = await _studentService.GetAllAsync();

    return Ok(students);
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 66. GET By Id Transition

## In-memory

```csharp
var student = _students.FirstOrDefault(s => s.Id == id);
```

## EF Core

```csharp
var student = await _context.Students
    .FirstOrDefaultAsync(s => s.Id == id);
```

Full service:

```csharp
public async Task<StudentResponseDto?> GetByIdAsync(int id)
{
    var student = await _context.Students
        .FirstOrDefaultAsync(s => s.Id == id);

    return student is null ? null : ToResponseDto(student);
}
```

Controller:

```csharp
[HttpGet("{id:int}")]
public async Task<IActionResult> GetById(int id)
{
    var student = await _studentService.GetByIdAsync(id);

    if (student is null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 67. POST Create Transition

## In-memory

```csharp
var student = new Student
{
    Id = _students.Count == 0 ? 1 : _students.Max(s => s.Id) + 1,
    FirstName = dto.FirstName.Trim()
};

_students.Add(student);
```

## EF Core

```csharp
var student = new Student
{
    StudentNumber = dto.StudentNumber.Trim().ToUpper(),
    FirstName = dto.FirstName.Trim(),
    LastName = dto.LastName.Trim(),
    Year = dto.Year,
    Gender = dto.Gender,
    Enrolled = true,
    CreatedAt = DateTime.UtcNow
};

_context.Students.Add(student);

await _context.SaveChangesAsync();
```

Important:

```text
Database generates Id.
You usually do not manually compute Id anymore.
```

Controller:

```csharp
[HttpPost]
public async Task<IActionResult> Create([FromBody] StudentCreateDto dto)
{
    var student = await _studentService.CreateAsync(dto);

    return CreatedAtAction(
        nameof(GetById),
        new { id = student.Id },
        student
    );
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 68. PUT Full Update Transition

## In-memory

```csharp
var student = _students.FirstOrDefault(s => s.Id == id);

student.FirstName = dto.FirstName.Trim();
```

## EF Core

```csharp
var student = await _context.Students
    .FirstOrDefaultAsync(s => s.Id == id);

if (student is null)
{
    return null;
}

student.StudentNumber = dto.StudentNumber.Trim().ToUpper();
student.FirstName = dto.FirstName.Trim();
student.LastName = dto.LastName.Trim();
student.Year = dto.Year;
student.Gender = dto.Gender;
student.Enrolled = dto.Enrolled;

await _context.SaveChangesAsync();

return ToResponseDto(student);
```

Key idea:

```text
Load entity.
Change properties.
SaveChangesAsync.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 69. PATCH Partial Update Transition

Patch DTO:

```csharp
public class StudentPatchDto
{
    public string? FirstName { get; set; }

    public string? LastName { get; set; }

    public int? Year { get; set; }

    public bool? Enrolled { get; set; }
}
```

Service:

```csharp
public async Task<StudentResponseDto?> PatchAsync(int id, StudentPatchDto dto)
{
    var student = await _context.Students
        .FirstOrDefaultAsync(s => s.Id == id);

    if (student is null)
    {
        return null;
    }

    if (!string.IsNullOrWhiteSpace(dto.FirstName))
    {
        student.FirstName = dto.FirstName.Trim();
    }

    if (!string.IsNullOrWhiteSpace(dto.LastName))
    {
        student.LastName = dto.LastName.Trim();
    }

    if (dto.Year.HasValue)
    {
        student.Year = dto.Year.Value;
    }

    if (dto.Enrolled.HasValue)
    {
        student.Enrolled = dto.Enrolled.Value;
    }

    await _context.SaveChangesAsync();

    return ToResponseDto(student);
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 70. DELETE Transition

## In-memory

```csharp
_students.Remove(student);
```

## EF Core

```csharp
public async Task<bool> DeleteAsync(int id)
{
    var student = await _context.Students
        .FirstOrDefaultAsync(s => s.Id == id);

    if (student is null)
    {
        return false;
    }

    _context.Students.Remove(student);

    await _context.SaveChangesAsync();

    return true;
}
```

Controller:

```csharp
[HttpDelete("{id:int}")]
public async Task<IActionResult> Delete(int id)
{
    bool deleted = await _studentService.DeleteAsync(id);

    if (!deleted)
    {
        return NotFound();
    }

    return NoContent();
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 71. Search, Filter, Sort, Pagination Transition

```csharp
public async Task<List<StudentResponseDto>> SearchAsync(
    string? keyword,
    int? year,
    bool? enrolled,
    int page = 1,
    int pageSize = 10)
{
    var query = _context.Students.AsQueryable();

    if (!string.IsNullOrWhiteSpace(keyword))
    {
        query = query.Where(s =>
            s.FirstName.Contains(keyword) ||
            s.LastName.Contains(keyword) ||
            s.StudentNumber.Contains(keyword));
    }

    if (year.HasValue)
    {
        query = query.Where(s => s.Year == year.Value);
    }

    if (enrolled.HasValue)
    {
        query = query.Where(s => s.Enrolled == enrolled.Value);
    }

    return await query
        .OrderBy(s => s.LastName)
        .Skip((page - 1) * pageSize)
        .Take(pageSize)
        .Select(s => new StudentResponseDto
        {
            Id = s.Id,
            StudentNumber = s.StudentNumber,
            FullName = s.FirstName + " " + s.LastName,
            Year = s.Year,
            Enrolled = s.Enrolled,
            CreatedAt = s.CreatedAt
        })
        .ToListAsync();
}
```

SQL idea:

```sql
SELECT *
FROM students
WHERE ...
ORDER BY last_name
LIMIT pageSize
OFFSET (page - 1) * pageSize;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 72. Duplicate Checking Transition

In-memory:

```csharp
bool exists = _students.Any(s => s.StudentNumber == studentNumber);
```

EF Core:

```csharp
string studentNumber = dto.StudentNumber.Trim().ToUpper();

bool exists = await _context.Students
    .AnyAsync(s => s.StudentNumber == studentNumber);

if (exists)
{
    throw new InvalidOperationException("Student number already exists.");
}
```

Database-level unique constraint:

```csharp
modelBuilder.Entity<Student>()
    .HasIndex(s => s.StudentNumber)
    .IsUnique();
```

Controller can return:

```csharp
return Conflict("Student number already exists.");
```

[[#Navigation|⬆ Back to Navigation]]

---

# 73. Loading Related Data

Related data is not always automatically loaded.

Example:

```csharp
var student = await _context.Students
    .FirstOrDefaultAsync(s => s.Id == id);
```

This may not include:

```text
student.StudentSections
student.Grades
```

Use:

```text
Include
ThenInclude
Projection
```

[[#Navigation|⬆ Back to Navigation]]

---

# 74. Include

Load direct related data:

```csharp
var student = await _context.Students
    .Include(s => s.Grades)
    .FirstOrDefaultAsync(s => s.Id == id);
```

For section:

```csharp
var section = await _context.Sections
    .Include(s => s.StudentSections)
    .FirstOrDefaultAsync(s => s.Id == id);
```

[[#Navigation|⬆ Back to Navigation]]

---

# 75. ThenInclude

Load nested related data:

```csharp
var students = await _context.Students
    .Include(s => s.StudentSections)
        .ThenInclude(ss => ss.Section)
    .ToListAsync();
```

More nested:

```csharp
var students = await _context.Students
    .Include(s => s.StudentSections)
        .ThenInclude(ss => ss.Section)
            .ThenInclude(sec => sec.Program)
    .ToListAsync();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 76. Projection Instead of Include

Projection directly shapes query output.

```csharp
var students = await _context.Students
    .Select(s => new StudentWithSectionDto
    {
        Id = s.Id,
        FullName = s.FirstName + " " + s.LastName,
        SectionCodes = s.StudentSections
            .Select(ss => ss.Section!.Code)
            .ToList(),
        AverageGrade = s.Grades.Any()
            ? s.Grades.Average(g => g.Grade)
            : null
    })
    .ToListAsync();
```

Benefits:

```text
returns only needed fields
avoids exposing entities
often better for API responses
```

[[#Navigation|⬆ Back to Navigation]]

---

# 77. Create Student Under Section

```csharp
public async Task<StudentResponseDto?> CreateStudentInSectionAsync(
    string sectionCode,
    StudentCreateDto dto)
{
    var section = await _context.Sections
        .FirstOrDefaultAsync(s => s.Code == sectionCode);

    if (section is null)
    {
        return null;
    }

    var student = new Student
    {
        StudentNumber = dto.StudentNumber.Trim().ToUpper(),
        FirstName = dto.FirstName.Trim(),
        LastName = dto.LastName.Trim(),
        Year = dto.Year,
        Gender = dto.Gender,
        Enrolled = true,
        CreatedAt = DateTime.UtcNow
    };

    _context.Students.Add(student);

    await _context.SaveChangesAsync();

    var assignment = new StudentSection
    {
        StudentId = student.Id,
        SectionId = section.Id,
        EnrolledAt = DateTime.UtcNow
    };

    _context.StudentSections.Add(assignment);

    await _context.SaveChangesAsync();

    return ToResponseDto(student);
}
```

Better transaction version:

```text
Use explicit transaction if student creation and section assignment must succeed together.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 78. Query Students with Program and Section

```csharp
var students = await _context.Students
    .Select(s => new StudentWithSectionDto
    {
        Id = s.Id,
        FullName = s.FirstName + " " + s.LastName,
        SectionCodes = s.StudentSections
            .Select(ss => ss.Section!.Code)
            .ToList(),
        ProgramNames = s.StudentSections
            .Select(ss => ss.Section!.Program!.ProgramName)
            .Distinct()
            .ToList()
    })
    .ToListAsync();
```

SQL equivalent idea:

```sql
SELECT
    s.first_name,
    s.last_name,
    sec.code,
    p.program_name
FROM students AS s
LEFT JOIN student_sections AS ss ON ss.student_id = s.id
LEFT JOIN sections AS sec ON ss.section_id = sec.id
LEFT JOIN programs AS p ON sec.program_id = p.id;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 79. Query Average Grades

```csharp
var result = await _context.Students
    .Select(s => new StudentAverageDto
    {
        Id = s.Id,
        FullName = s.FirstName + " " + s.LastName,
        AverageGrade = s.Grades.Any()
            ? Math.Round(s.Grades.Average(g => g.Grade), 2)
            : null
    })
    .ToListAsync();
```

SQL idea:

```sql
SELECT
    s.id,
    s.first_name,
    s.last_name,
    ROUND(AVG(g.grade), 2) AS average_grade
FROM students AS s
LEFT JOIN student_grades AS g ON g.student_id = s.id
GROUP BY s.id, s.first_name, s.last_name;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 80. Find Unassigned Students or Empty Sections

Unassigned students:

```csharp
var students = await _context.Students
    .Where(s => !s.StudentSections.Any())
    .Select(s => new StudentResponseDto
    {
        Id = s.Id,
        FullName = s.FirstName + " " + s.LastName
    })
    .ToListAsync();
```

Sections with no students:

```csharp
var sections = await _context.Sections
    .Where(s => !s.StudentSections.Any())
    .Select(s => new SectionResponseDto
    {
        Id = s.Id,
        Code = s.Code
    })
    .ToListAsync();
```

SQL idea:

```sql
LEFT JOIN ... WHERE joined_table.id IS NULL
```

[[#Navigation|⬆ Back to Navigation]]

---

# 81. Step 1 Create Project

```bash
dotnet new webapi -n StudentEnrollmentApi
cd StudentEnrollmentApi
code .
```

Run:

```bash
dotnet run
```

Check:

```text
API starts successfully before adding database code.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 82. Step 2 Install Packages

```bash
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.Design
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL
```

Install/update CLI:

```bash
dotnet tool install --global dotnet-ef
```

or:

```bash
dotnet tool update --global dotnet-ef
```

[[#Navigation|⬆ Back to Navigation]]

---

# 83. Step 3 Configure appsettings.json

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Database=student_enrollment_db;Username=postgres;Password=yourpassword"
  }
}
```

Tip:

```text
Do not forget to create the database in PostgreSQL.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 84. Step 4 Create Entities

Create:

```text
Models/
├── Student.cs
├── ProgramEntity.cs
├── Section.cs
├── StudentSection.cs
└── StudentGrade.cs
```

Use the entity examples from sections 36 to 40.

[[#Navigation|⬆ Back to Navigation]]

---

# 85. Step 5 Create AppDbContext

```csharp
using Microsoft.EntityFrameworkCore;
using StudentEnrollmentApi.Models;

namespace StudentEnrollmentApi.Data;

public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options)
        : base(options)
    {
    }

    public DbSet<Student> Students { get; set; }

    public DbSet<ProgramEntity> Programs { get; set; }

    public DbSet<Section> Sections { get; set; }

    public DbSet<StudentSection> StudentSections { get; set; }

    public DbSet<StudentGrade> StudentGrades { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Student>()
            .HasIndex(s => s.StudentNumber)
            .IsUnique();

        modelBuilder.Entity<ProgramEntity>()
            .HasIndex(p => p.ProgramName)
            .IsUnique();

        modelBuilder.Entity<Section>()
            .HasIndex(s => s.Code)
            .IsUnique();

        modelBuilder.Entity<StudentSection>()
            .HasIndex(ss => new { ss.StudentId, ss.SectionId })
            .IsUnique();

        modelBuilder.Entity<StudentGrade>()
            .Property(g => g.Grade)
            .HasPrecision(5, 2);
    }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 86. Step 6 Register DbContext and Services

```csharp
using Microsoft.EntityFrameworkCore;
using StudentEnrollmentApi.Data;
using StudentEnrollmentApi.Services.Students;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseNpgsql(
        builder.Configuration.GetConnectionString("DefaultConnection")
    ));

builder.Services.AddScoped<IStudentService, StudentService>();

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 87. Step 7 Create DTOs

Create:

```text
DTOs/Students/
├── StudentCreateDto.cs
├── StudentUpdateDto.cs
├── StudentPatchDto.cs
└── StudentResponseDto.cs
```

Use sections 53 to 56.

[[#Navigation|⬆ Back to Navigation]]

---

# 88. Step 8 Create Service Interface

```csharp
using StudentEnrollmentApi.DTOs.Students;

namespace StudentEnrollmentApi.Services.Students;

public interface IStudentService
{
    Task<List<StudentResponseDto>> GetAllAsync();

    Task<StudentResponseDto?> GetByIdAsync(int id);

    Task<StudentResponseDto> CreateAsync(StudentCreateDto dto);

    Task<StudentResponseDto?> UpdateAsync(int id, StudentUpdateDto dto);

    Task<StudentResponseDto?> PatchAsync(int id, StudentPatchDto dto);

    Task<bool> DeleteAsync(int id);
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 89. Step 9 Create Service Implementation

```csharp
using Microsoft.EntityFrameworkCore;
using StudentEnrollmentApi.Data;
using StudentEnrollmentApi.DTOs.Students;
using StudentEnrollmentApi.Models;

namespace StudentEnrollmentApi.Services.Students;

public class StudentService : IStudentService
{
    private readonly AppDbContext _context;

    public StudentService(AppDbContext context)
    {
        _context = context;
    }

    public async Task<List<StudentResponseDto>> GetAllAsync()
    {
        return await _context.Students
            .OrderBy(s => s.LastName)
            .Select(s => new StudentResponseDto
            {
                Id = s.Id,
                StudentNumber = s.StudentNumber,
                FullName = s.FirstName + " " + s.LastName,
                Year = s.Year,
                Gender = s.Gender,
                Enrolled = s.Enrolled,
                CreatedAt = s.CreatedAt
            })
            .ToListAsync();
    }

    public async Task<StudentResponseDto?> GetByIdAsync(int id)
    {
        var student = await _context.Students
            .FirstOrDefaultAsync(s => s.Id == id);

        return student is null ? null : ToResponseDto(student);
    }

    public async Task<StudentResponseDto> CreateAsync(StudentCreateDto dto)
    {
        string studentNumber = dto.StudentNumber.Trim().ToUpper();

        bool exists = await _context.Students
            .AnyAsync(s => s.StudentNumber == studentNumber);

        if (exists)
        {
            throw new InvalidOperationException("Student number already exists.");
        }

        var student = new Student
        {
            StudentNumber = studentNumber,
            FirstName = dto.FirstName.Trim(),
            LastName = dto.LastName.Trim(),
            Year = dto.Year,
            Gender = dto.Gender,
            Enrolled = true,
            CreatedAt = DateTime.UtcNow
        };

        _context.Students.Add(student);

        await _context.SaveChangesAsync();

        return ToResponseDto(student);
    }

    public async Task<StudentResponseDto?> UpdateAsync(int id, StudentUpdateDto dto)
    {
        var student = await _context.Students
            .FirstOrDefaultAsync(s => s.Id == id);

        if (student is null)
        {
            return null;
        }

        student.StudentNumber = dto.StudentNumber.Trim().ToUpper();
        student.FirstName = dto.FirstName.Trim();
        student.LastName = dto.LastName.Trim();
        student.Year = dto.Year;
        student.Gender = dto.Gender;
        student.Enrolled = dto.Enrolled;

        await _context.SaveChangesAsync();

        return ToResponseDto(student);
    }

    public async Task<StudentResponseDto?> PatchAsync(int id, StudentPatchDto dto)
    {
        var student = await _context.Students
            .FirstOrDefaultAsync(s => s.Id == id);

        if (student is null)
        {
            return null;
        }

        if (!string.IsNullOrWhiteSpace(dto.StudentNumber))
        {
            student.StudentNumber = dto.StudentNumber.Trim().ToUpper();
        }

        if (!string.IsNullOrWhiteSpace(dto.FirstName))
        {
            student.FirstName = dto.FirstName.Trim();
        }

        if (!string.IsNullOrWhiteSpace(dto.LastName))
        {
            student.LastName = dto.LastName.Trim();
        }

        if (dto.Year.HasValue)
        {
            student.Year = dto.Year.Value;
        }

        if (dto.Gender is not null)
        {
            student.Gender = dto.Gender;
        }

        if (dto.Enrolled.HasValue)
        {
            student.Enrolled = dto.Enrolled.Value;
        }

        await _context.SaveChangesAsync();

        return ToResponseDto(student);
    }

    public async Task<bool> DeleteAsync(int id)
    {
        var student = await _context.Students
            .FirstOrDefaultAsync(s => s.Id == id);

        if (student is null)
        {
            return false;
        }

        _context.Students.Remove(student);

        await _context.SaveChangesAsync();

        return true;
    }

    private static StudentResponseDto ToResponseDto(Student student)
    {
        return new StudentResponseDto
        {
            Id = student.Id,
            StudentNumber = student.StudentNumber,
            FullName = student.FirstName + " " + student.LastName,
            Year = student.Year,
            Gender = student.Gender,
            Enrolled = student.Enrolled,
            CreatedAt = student.CreatedAt
        };
    }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 90. Step 10 Create Controller

```csharp
using Microsoft.AspNetCore.Mvc;
using StudentEnrollmentApi.DTOs.Students;
using StudentEnrollmentApi.Services.Students;

namespace StudentEnrollmentApi.Controllers;

[ApiController]
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
    private readonly IStudentService _studentService;

    public StudentsController(IStudentService studentService)
    {
        _studentService = studentService;
    }

    [HttpGet]
    public async Task<IActionResult> GetAll()
    {
        var students = await _studentService.GetAllAsync();

        return Ok(students);
    }

    [HttpGet("{id:int}")]
    public async Task<IActionResult> GetById(int id)
    {
        var student = await _studentService.GetByIdAsync(id);

        if (student is null)
        {
            return NotFound();
        }

        return Ok(student);
    }

    [HttpPost]
    public async Task<IActionResult> Create([FromBody] StudentCreateDto dto)
    {
        try
        {
            var student = await _studentService.CreateAsync(dto);

            return CreatedAtAction(
                nameof(GetById),
                new { id = student.Id },
                student
            );
        }
        catch (InvalidOperationException ex)
        {
            return Conflict(ex.Message);
        }
    }

    [HttpPut("{id:int}")]
    public async Task<IActionResult> Update(int id, [FromBody] StudentUpdateDto dto)
    {
        var updated = await _studentService.UpdateAsync(id, dto);

        if (updated is null)
        {
            return NotFound();
        }

        return Ok(updated);
    }

    [HttpPatch("{id:int}")]
    public async Task<IActionResult> Patch(int id, [FromBody] StudentPatchDto dto)
    {
        var patched = await _studentService.PatchAsync(id, dto);

        if (patched is null)
        {
            return NotFound();
        }

        return Ok(patched);
    }

    [HttpDelete("{id:int}")]
    public async Task<IActionResult> Delete(int id)
    {
        bool deleted = await _studentService.DeleteAsync(id);

        if (!deleted)
        {
            return NotFound();
        }

        return NoContent();
    }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 91. Step 11 Add Migration and Update Database

Build first:

```bash
dotnet build
```

Add migration:

```bash
dotnet ef migrations add InitialCreate
```

Apply:

```bash
dotnet ef database update
```

Check in PostgreSQL:

```sql
\c student_enrollment_db
\dt
```

or in pgAdmin:

```text
Databases
↓
student_enrollment_db
↓
Schemas
↓
public
↓
Tables
```

[[#Navigation|⬆ Back to Navigation]]

---

# 92. Step 12 Test in Postman

## Create student

```http
POST /api/students
Content-Type: application/json
```

Body:

```json
{
  "studentNumber": "2024-0001",
  "firstName": "Ana",
  "lastName": "Reyes",
  "year": 2,
  "gender": "Female"
}
```

Expected:

```text
201 Created
```

## Get all

```http
GET /api/students
```

Expected:

```text
200 OK
```

## Get one

```http
GET /api/students/1
```

Expected:

```text
200 OK or 404 Not Found
```

## Update

```http
PUT /api/students/1
```

## Patch

```http
PATCH /api/students/1
```

## Delete

```http
DELETE /api/students/1
```

Expected:

```text
204 No Content
```

[[#Navigation|⬆ Back to Navigation]]

---

# 93. PostgreSQL psql Commands

```bash
psql -U postgres
```

```sql
\l
```

List databases.

```sql
\c student_enrollment_db
```

Connect to database.

```sql
\dt
```

List tables.

```sql
\d students
```

Describe table.

```sql
SELECT * FROM students;
```

Read rows.

```sql
\q
```

Quit.

[[#Navigation|⬆ Back to Navigation]]

---

# 94. SQL Command Cheat Sheet

```sql
CREATE DATABASE database_name;
```

```sql
CREATE TABLE table_name (...);
```

```sql
INSERT INTO table_name (columns)
VALUES (values);
```

```sql
SELECT columns
FROM table_name;
```

```sql
UPDATE table_name
SET column = value
WHERE condition;
```

```sql
DELETE FROM table_name
WHERE condition;
```

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

[[#Navigation|⬆ Back to Navigation]]

---

# 95. dotnet ef Command Cheat Sheet

Install/update tool:

```bash
dotnet tool install --global dotnet-ef
dotnet tool update --global dotnet-ef
```

Add migration:

```bash
dotnet ef migrations add InitialCreate
```

Apply migrations:

```bash
dotnet ef database update
```

List migrations:

```bash
dotnet ef migrations list
```

Remove last migration:

```bash
dotnet ef migrations remove
```

Drop database:

```bash
dotnet ef database drop
```

Specify context:

```bash
dotnet ef migrations add InitialCreate --context AppDbContext
```

[[#Navigation|⬆ Back to Navigation]]

---

# 96. EF Core Method Cheat Sheet

| Method | Use |
|---|---|
| `Add` | insert new entity |
| `Remove` | delete entity |
| `Update` | mark entire entity as modified |
| `FindAsync` | find by primary key |
| `FirstOrDefaultAsync` | first match or null |
| `SingleOrDefaultAsync` | single match or null |
| `Where` | filter |
| `OrderBy` | sort ascending |
| `OrderByDescending` | sort descending |
| `Select` | project/map |
| `Include` | load related data |
| `ThenInclude` | load nested related data |
| `AnyAsync` | check if exists |
| `CountAsync` | count rows |
| `ToListAsync` | execute query to list |
| `SaveChangesAsync` | commit database changes |

[[#Navigation|⬆ Back to Navigation]]

---

# 97. SQL to EF Core Translation Table

| SQL | EF Core |
|---|---|
| `SELECT * FROM students` | `_context.Students.ToListAsync()` |
| `WHERE id = 1` | `.Where(s => s.Id == 1)` |
| `ORDER BY last_name` | `.OrderBy(s => s.LastName)` |
| `LIMIT 10` | `.Take(10)` |
| `OFFSET 10` | `.Skip(10)` |
| `INSERT` | `.Add(entity)` + `SaveChangesAsync()` |
| `UPDATE` | load entity, modify properties, `SaveChangesAsync()` |
| `DELETE` | `.Remove(entity)` + `SaveChangesAsync()` |
| `COUNT(*)` | `.CountAsync()` |
| `EXISTS` | `.AnyAsync()` |
| `JOIN` | `.Include()`, navigation query, or projection |

[[#Navigation|⬆ Back to Navigation]]

---

# 98. HTTP to SQL to EF Core Mapping

| HTTP | SQL | EF Core |
|---|---|---|
| GET all | SELECT | `ToListAsync()` |
| GET by ID | SELECT WHERE id | `FirstOrDefaultAsync()` / `FindAsync()` |
| POST | INSERT | `Add()` + `SaveChangesAsync()` |
| PUT | UPDATE all fields | load, assign all fields, save |
| PATCH | UPDATE some fields | load, assign provided fields, save |
| DELETE | DELETE | `Remove()` + `SaveChangesAsync()` |

[[#Navigation|⬆ Back to Navigation]]

---

# 99. PostgreSQL Type to CSharp Type Cheat Sheet

| PostgreSQL | CSharp |
|---|---|
| `INT` | `int` |
| `BIGINT` | `long` |
| `SERIAL` | `int` |
| `BIGSERIAL` | `long` |
| `NUMERIC` | `decimal` |
| `BOOLEAN` | `bool` |
| `TEXT` | `string` |
| `VARCHAR` | `string` |
| `TIMESTAMP` | `DateTime` |
| `TIMESTAMPTZ` | `DateTime` |
| `UUID` | `Guid` |

[[#Navigation|⬆ Back to Navigation]]

---

# 100. Transactions in EF Core

Simple `SaveChangesAsync()` is usually transactional.

For multiple save steps:

```csharp
using var transaction = await _context.Database.BeginTransactionAsync();

try
{
    _context.Students.Add(student);
    await _context.SaveChangesAsync();

    _context.StudentSections.Add(studentSection);
    await _context.SaveChangesAsync();

    await transaction.CommitAsync();
}
catch
{
    await transaction.RollbackAsync();
    throw;
}
```

Use explicit transactions when:

```text
multiple operations must succeed together
you call SaveChangesAsync more than once
you are modifying multiple related tables
partial save would be bad
```

[[#Navigation|⬆ Back to Navigation]]

---

# 101. Concurrency Preview

Concurrency means multiple users may update data at the same time.

Example:

```text
User A opens student record.
User B updates same student.
User A saves old version.
```

Potential problem:

```text
User A overwrites User B's changes.
```

Common solution later:

```text
row version / concurrency token
```

Beginner note:

```text
Understand that databases support many users.
EF Core has tools for concurrency, but basic CRUD usually introduces this later.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 102. Raw SQL with EF Core

For queries:

```csharp
var students = await _context.Students
    .FromSqlRaw("SELECT * FROM students WHERE enrolled = TRUE")
    .ToListAsync();
```

For commands:

```csharp
await _context.Database.ExecuteSqlRawAsync(
    "UPDATE students SET enrolled = FALSE WHERE id = {0}",
    id
);
```

Use raw SQL carefully.

Prefer LINQ for normal CRUD.

Use raw SQL when:

```text
query is easier in SQL
using PostgreSQL-specific feature
performance tuning requires custom SQL
```

[[#Navigation|⬆ Back to Navigation]]

---

# 103. Seeding Data

Simple seeding in `OnModelCreating`:

```csharp
modelBuilder.Entity<ProgramEntity>().HasData(
    new ProgramEntity { Id = 1, ProgramName = "BSIT" },
    new ProgramEntity { Id = 2, ProgramName = "BSCS" }
);
```

Important:

```text
Seed data IDs should be fixed.
Migrations include seed data changes.
```

For development-only seeding, some apps seed on startup, but this should be done carefully.

[[#Navigation|⬆ Back to Navigation]]

---

# 104. Indexes in EF Core

Unique index:

```csharp
modelBuilder.Entity<Student>()
    .HasIndex(s => s.StudentNumber)
    .IsUnique();
```

Normal index:

```csharp
modelBuilder.Entity<StudentSection>()
    .HasIndex(ss => ss.StudentId);
```

Composite unique index:

```csharp
modelBuilder.Entity<StudentSection>()
    .HasIndex(ss => new { ss.StudentId, ss.SectionId })
    .IsUnique();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 105. Soft Delete with EF Core

Entity:

```csharp
public DateTime? DeletedAt { get; set; }
```

Soft delete:

```csharp
student.DeletedAt = DateTime.UtcNow;

await _context.SaveChangesAsync();
```

Filter active records:

```csharp
var students = await _context.Students
    .Where(s => s.DeletedAt == null)
    .ToListAsync();
```

Why:

```text
keeps history
allows restore
avoids permanent deletion
```

[[#Navigation|⬆ Back to Navigation]]

---

# 106. Common Connection Errors

Checklist:

```text
PostgreSQL is running.
Database exists.
Connection string database name is correct.
Username is correct.
Password is correct.
Port is 5432 unless changed.
Npgsql package is installed.
DbContext is registered.
```

Common message:

```text
password authentication failed
```

Fix:

```text
Check postgres password in connection string.
```

Common message:

```text
database does not exist
```

Fix:

```sql
CREATE DATABASE student_enrollment_db;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 107. Common Migration Errors

## dotnet ef not found

```bash
dotnet tool install --global dotnet-ef
```

## Build failed

```bash
dotnet build
```

Fix C# errors first.

## No DbContext found

Check:

```text
AppDbContext class exists.
It inherits DbContext.
It has constructor with DbContextOptions.
Project builds.
```

## Provider not configured

Check:

```csharp
options.UseNpgsql(...)
```

[[#Navigation|⬆ Back to Navigation]]

---

# 108. Common Query Errors

## ToListAsync not found

Add:

```csharp
using Microsoft.EntityFrameworkCore;
```

## Navigation property is null

Use:

```csharp
.Include(...)
```

or projection with null checks.

## Duplicate key violation

Cause:

```text
Unique index/constraint violated.
```

Fix:

```text
Check duplicate with AnyAsync before inserting.
Return 409 Conflict.
```

## SaveChangesAsync does nothing

Check:

```text
Did you modify a tracked entity?
Did you call Add for new entity?
Did you call SaveChangesAsync?
Are you connected to the expected database?
```

[[#Navigation|⬆ Back to Navigation]]

---

# 109. Common API Errors After Switching to Database

## 400 Bad Request

Check:

```text
JSON shape
DTO property names
required fields
data types
validation annotations
```

## 404 Not Found

Check:

```text
route
record ID
database data
whether migration seeded data
```

## 409 Conflict

Use for:

```text
duplicate student number
duplicate section code
duplicate assignment
```

## 500 Internal Server Error

Common causes:

```text
database down
connection string wrong
migration not applied
null navigation property
unhandled duplicate key exception
```

[[#Navigation|⬆ Back to Navigation]]

---

# 110. Debugging Checklist

```text
[ ] Does dotnet build pass?
[ ] Is PostgreSQL running?
[ ] Does the database exist?
[ ] Is the connection string correct?
[ ] Is Npgsql installed?
[ ] Is AppDbContext registered?
[ ] Did you add migration?
[ ] Did you run database update?
[ ] Do tables exist in pgAdmin or psql?
[ ] Did you call SaveChangesAsync?
[ ] Did you import Microsoft.EntityFrameworkCore?
[ ] Are DTO names/properties correct?
[ ] Are controller routes correct?
[ ] Are services registered in Program.cs?
[ ] Are you querying the correct database?
```

[[#Navigation|⬆ Back to Navigation]]

---

# 111. Tips and Tricks

```text
Write SQL first to understand the data.
Then translate to EF Core LINQ.
Keep controllers thin.
Put DbContext logic in services.
Use DTOs even with EF Core.
Use projection for API responses.
Use Include only when you need related entities.
Use AnyAsync for duplicate checks.
Use CreatedAtAction after POST.
Use NoContent after DELETE.
Use Conflict for duplicates.
Use migrations with descriptive names.
Read generated migrations before applying.
Use psql or pgAdmin to verify database state.
```

Destructive SQL habit:

```text
SELECT first.
Verify rows.
Then UPDATE or DELETE.
Always keep WHERE.
Use RETURNING when possible.
```

EF Core habit:

```text
Build query.
Apply filters.
Apply sorting.
Project to DTO.
Execute with ToListAsync.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 112. Best Practices

```text
Use PostgreSQL constraints for data integrity.
Use EF Core validation/mapping for app-level rules.
Use database unique indexes for unique fields.
Use DTOs to control API input and output.
Use services to isolate business logic.
Use scoped lifetime for services that use DbContext.
Use async EF Core methods.
Avoid returning entities directly.
Avoid storing arrays for relational data.
Normalize schema to reduce duplication.
Index foreign keys and common search columns.
Avoid too many indexes without reason.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 113. Final Transition Summary

In-memory version:

```text
Students are stored in a List<Student>.
IDs are manually generated.
Data disappears on restart.
Relationships are manually represented.
Queries run in C# memory.
```

Database version:

```text
Students are stored in PostgreSQL tables.
IDs can be generated by database.
Data persists after restart.
Relationships use foreign keys and join tables.
Queries are translated to SQL.
Indexes improve performance.
Constraints protect integrity.
```

Final request flow:

```text
HTTP Request
↓
Controller
↓
Service
↓
AppDbContext
↓
EF Core
↓
Npgsql
↓
PostgreSQL
↓
DTO response
↓
JSON
```

[[#Navigation|⬆ Back to Navigation]]

---

# 114. Final Review Checklist

```text
[ ] I can explain why static lists are not enough.
[ ] I can explain PostgreSQL tables, rows, and columns.
[ ] I can explain primary keys and foreign keys.
[ ] I can write basic SELECT, INSERT, UPDATE, DELETE.
[ ] I can explain JOINs.
[ ] I can explain GROUP BY and aggregates.
[ ] I can explain indexes.
[ ] I can explain normalization.
[ ] I can explain ACID.
[ ] I can explain what EF Core does.
[ ] I can explain what Npgsql does.
[ ] I can create AppDbContext.
[ ] I can create DbSet properties.
[ ] I can register DbContext in Program.cs.
[ ] I can add a connection string.
[ ] I can create EF Core entities.
[ ] I can add migrations.
[ ] I can update the PostgreSQL database.
[ ] I can replace List<T> queries with DbContext queries.
[ ] I can write GET all using ToListAsync.
[ ] I can write GET by ID using FirstOrDefaultAsync.
[ ] I can write POST using Add and SaveChangesAsync.
[ ] I can write PUT by loading, modifying, and saving.
[ ] I can write PATCH with nullable DTO fields.
[ ] I can write DELETE using Remove and SaveChangesAsync.
[ ] I can use Include and projection for related data.
[ ] I can use AnyAsync for duplicate checks.
[ ] I can troubleshoot connection and migration errors.
```

[[#Navigation|⬆ Back to Navigation]]
