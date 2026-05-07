# C# + LINQ + Web API Cheat Sheet
Tags: #csharp #dotnet #linq #webapi #bootcamp

> Purpose: quick reviewer from C# fundamentals up to ASP.NET Core Web APIs, with extra focus on collections, iteration, and LINQ.
# Navigation
## 1. Overview

- [[#0. Big Picture|0. Big Picture]]
## 2. CSharp Fundamentals

- [[#1. CSharp Basics|1. C# Basics]]
  - [[#Variables|Variables]]
  - [[#var Keyword|var Keyword]]
  - [[#Nullable Types|Nullable Types]]
- [[#2. Console Input and Output|2. Console Input and Output]]
- [[#3. Conditions|3. Conditions]]
  - [[#Ternary|Ternary]]
  - [[#Switch Expression|Switch Expression]]
- [[#4. Methods|4. Methods]]
  - [[#Basic Method|Basic Method]]
  - [[#Void Method|Void Method]]
  - [[#Expression-Bodied Method|Expression-Bodied Method]]
  - [[#Method With Nullable Return|Method With Nullable Return]]
- [[#5. Classes and Objects|5. Classes and Objects]]
  - [[#Model Example|Model Example]]
  - [[#Object Creation|Object Creation]]

## 3. Collections

- [[#6. Collections: Which One Should I Use?|6. Collections: Which One Should I Use?]]
- [[#7. List Collections|7. List Collections]]
  - [[#Create a List|Create a List]]
  - [[#Common Operations|Common Operations]]
  - [[#Iterate a List|Iterate a List]]
- [[#8. Dictionary Collections|8. Dictionary Collections]]
  - [[#Safe Lookup|Safe Lookup]]
  - [[#Iterate Dictionary|Iterate Dictionary]]
- [[#9. HashSet Collections|9. HashSet Collections]]

## 4. LINQ Foundations

- [[#10. Lambda Expressions|10. Lambda Expressions]]
- [[#11. LINQ Mental Model|11. LINQ Mental Model]]
- [[#12. The LINQ Ladder|12. The LINQ Ladder]]
- [[#13. LINQ Core Methods|13. LINQ Core Methods]]
  - [[#Where — Filter Many Items|Where — Filter Many Items]]
  - [[#FirstOrDefault — Find One Item|FirstOrDefault — Find One Item]]
  - [[#Any — Check If Something Exists|Any — Check If Something Exists]]
  - [[#OrderBy / OrderByDescending — Sort|OrderBy / OrderByDescending — Sort]]
  - [[#Select — Transform Shape|Select — Transform Shape]]
  - [[#Count — Count Items|Count — Count Items]]
  - [[#Average, Max, Min, Sum|Average, Max, Min, Sum]]
  - [[#Skip and Take — Pagination|Skip and Take — Pagination]]
  - [[#GroupBy — Grouping and Stats|GroupBy — Grouping and Stats]]

## 5. LINQ Recipes and Mistakes

- [[#14. LINQ: Common Recipes|14. LINQ: Common Recipes]]
  - [[#Get All CS Students|Get All CS Students]]
  - [[#Get Honor Students Sorted Highest First|Get Honor Students Sorted Highest First]]
  - [[#Get Top Student|Get Top Student]]
  - [[#Get Top 3 Students|Get Top 3 Students]]
  - [[#Search by Name|Search by Name]]
  - [[#Filter by Optional Query Params|Filter by Optional Query Params]]
  - [[#Count Students Per Course|Count Students Per Course]]
  - [[#Get Students Per Course With Names|Get Students Per Course With Names]]
  - [[#Convert List to Dictionary|Convert List to Dictionary]]
- [[#15. LINQ Mistakes to Avoid|15. LINQ Mistakes to Avoid]]
  - [[#Mistake 1: Forgetting .ToList()|Mistake 1: Forgetting .ToList()]]
  - [[#Mistake 2: Using First() When Item Might Not Exist|Mistake 2: Using First() When Item Might Not Exist]]
  - [[#Mistake 3: Calling Average on an Empty List|Mistake 3: Calling Average on an Empty List]]
  - [[#Mistake 4: Case-Sensitive String Comparison|Mistake 4: Case-Sensitive String Comparison]]
  - [[#Mistake 5: Confusing Select and Where|Mistake 5: Confusing Select and Where]]

## 6. Web API Basics

- [[#16. Web API Basics|16. Web API Basics]]
  - [[#Program.cs|Program.cs]]
- [[#17. Controller Template|17. Controller Template]]
- [[#18. Route Params vs Query Params|18. Route Params vs Query Params]]
  - [[#Route Parameter|Route Parameter]]
  - [[#Query Parameter|Query Parameter]]
- [[#19. CRUD Endpoint Cheat Sheet|19. CRUD Endpoint Cheat Sheet]]
- [[#20. Full CRUD Mini Template|20. Full CRUD Mini Template]]
- [[#21. Data Annotations|21. Data Annotations]]
- [[#22. DTOs|22. DTOs]]
  - [[#Model|Model]]
  - [[#Create DTO|Create DTO]]
  - [[#Response DTO|Response DTO]]
  - [[#Manual Mapping|Manual Mapping]]
- [[#23. IActionResult Helpers|23. IActionResult Helpers]]

## 7. Middleware and Day 3 Prep

- [[#24. Middleware Preview for Day 3|24. Middleware Preview for Day 3]]
- [[#28. Final Day 3 Prep|28. Final Day 3 Prep]]

## 8. Must-Memorize Patterns and Practice

- [[#25. Most Important Patterns to Memorize|25. Most Important Patterns to Memorize]]
  - [[#Find by ID|Find by ID]]
  - [[#Filter Optional Query Params|Filter Optional Query Params]]
  - [[#Create New ID|Create New ID]]
  - [[#Stats Endpoint|Stats Endpoint]]
  - [[#Pagination|Pagination]]
- [[#26. LINQ Quick Translation Table|26. LINQ Quick Translation Table]]
- [[#27. Practice Drills|27. Practice Drills]]

---

# 0. Big Picture

[[#Navigation|⬆ Back to Navigation]]


```text
C# syntax
→ variables, methods, classes
→ collections: List, Dictionary, HashSet
→ LINQ: filter, sort, transform, group
→ Web API: controllers, routes, status codes
→ middleware: request pipeline
```

For Web APIs, most beginner code follows this flow:

```text
Postman request
→ middleware
→ route matching
→ controller action
→ collection / service / database
→ IActionResult response
```

---

# 1. CSharp Basics

[[#Navigation|⬆ Back to Navigation]]


## Variables

```csharp
string name = "Ana";
int age = 20;
double gpa = 3.75;
decimal price = 99.99m; // use decimal for money
bool enrolled = true;
char grade = 'A';
```

## var Keyword

`var` means the compiler infers the type. It is **not dynamic**.

```csharp
var name = "Ana";   // string forever
var age = 20;       // int forever
var gpa = 3.75;     // double forever
```

This is invalid:

```csharp
var age = 20;
age = "twenty"; // error
```

## Nullable Types

```csharp
string? middleName = null;
int? optionalAge = null;
bool? maybeEnrolled = null;
```

Use `?` when a value is allowed to be null.

---

# 2. Console Input and Output

[[#Navigation|⬆ Back to Navigation]]


```csharp
Console.Write("Enter name: ");
string? name = Console.ReadLine();

Console.Write("Enter age: ");
int age = int.Parse(Console.ReadLine()!);

Console.WriteLine($"Hello {name}, age {age}");
```

Safer number input:

```csharp
Console.Write("Enter age: ");
string? input = Console.ReadLine();

if (int.TryParse(input, out int age))
{
    Console.WriteLine($"Age: {age}");
}
else
{
    Console.WriteLine("Invalid number.");
}
```

---

# 3. Conditions

[[#Navigation|⬆ Back to Navigation]]


```csharp
if (age >= 18)
{
    Console.WriteLine("Adult");
}
else
{
    Console.WriteLine("Minor");
}
```

C# has **no truthy/falsy** like JavaScript.

```csharp
// Wrong
if (name) { }

// Correct
if (!string.IsNullOrEmpty(name))
{
    Console.WriteLine(name);
}
```

## Ternary

```csharp
string label = age >= 18 ? "Adult" : "Minor";
```

## Switch Expression

```csharp
string level = score switch
{
    >= 90 => "Excellent",
    >= 75 => "Passed",
    _ => "Failed"
};
```

---

# 4. Methods

[[#Navigation|⬆ Back to Navigation]]


## Basic Method

```csharp
static int Add(int a, int b)
{
    return a + b;
}
```

## Void Method

```csharp
static void PrintName(string name)
{
    Console.WriteLine(name);
}
```

## Expression-Bodied Method

```csharp
static double GetAverage(List<double> grades) =>
    grades.Count == 0 ? 0 : grades.Average();
```

## Method With Nullable Return

```csharp
static Student? FindStudentById(List<Student> students, int id)
{
    return students.FirstOrDefault(s => s.Id == id);
}
```

---

# 5. Classes and Objects

[[#Navigation|⬆ Back to Navigation]]


## Model Example

```csharp
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; } = string.Empty;
    public string Course { get; set; } = string.Empty;
    public List<double> Grades { get; set; } = new();

    public double GetAverage()
    {
        return Grades.Count == 0 ? 0 : Grades.Average();
    }

    public bool IsHonor()
    {
        return GetAverage() >= 87;
    }

    public override string ToString()
    {
        return $"[{Id}] {Name} ({Course}) - Avg: {GetAverage():F2}";
    }
}
```

## Object Creation

```csharp
var student = new Student
{
    Id = 1,
    Name = "Ana Reyes",
    Course = "CS",
    Grades = new List<double> { 90, 92, 95 }
};
```

---

# 6. Collections: Which One Should I Use?

[[#Navigation|⬆ Back to Navigation]]


| Collection | Use When | Example |
|---|---|---|
| `List<T>` | You need an ordered list of items | list of students |
| `Dictionary<K,V>` | You need fast lookup by key | student by ID |
| `HashSet<T>` | You need unique values | unique tags/categories |
| Array `T[]` | Fixed-size list | grades from a file |

---

# 7. List Collections

[[#Navigation|⬆ Back to Navigation]]


## Create a List

```csharp
List<string> books = new List<string>();

books.Add("Clean Code");
books.Add("C# in Depth");
books.Add("Dune");
```

Shorter:

```csharp
var books = new List<string> { "Clean Code", "C# in Depth", "Dune" };
```

## Common Operations

```csharp
books.Add("Sapiens");       // add
books.Remove("Dune");       // remove by value
books.RemoveAt(0);          // remove by index
books.Count;                // number of items
books[0];                   // first item
books.Contains("Dune");     // true/false
```

## Iterate a List

Use `foreach` most of the time.

```csharp
foreach (var book in books)
{
    Console.WriteLine(book);
}
```

Use `for` when you need the index.

```csharp
for (int i = 0; i < books.Count; i++)
{
    Console.WriteLine($"{i + 1}. {books[i]}");
}
```

---

# 8. Dictionary Collections

[[#Navigation|⬆ Back to Navigation]]


A dictionary stores key-value pairs.

```csharp
var studentsById = new Dictionary<int, Student>();

studentsById[1] = new Student { Id = 1, Name = "Ana", Course = "CS" };
studentsById[2] = new Student { Id = 2, Name = "Ben", Course = "IT" };
```

## Safe Lookup

Use `TryGetValue`.

```csharp
if (studentsById.TryGetValue(1, out Student? student))
{
    Console.WriteLine(student.Name);
}
else
{
    Console.WriteLine("Student not found.");
}
```

Avoid this unless you are sure the key exists:

```csharp
var student = studentsById[99]; // throws error if key is missing
```

## Iterate Dictionary

```csharp
foreach (var pair in studentsById)
{
    Console.WriteLine($"ID: {pair.Key}, Name: {pair.Value.Name}");
}
```

Keys only:

```csharp
foreach (var id in studentsById.Keys)
{
    Console.WriteLine(id);
}
```

Values only:

```csharp
foreach (var student in studentsById.Values)
{
    Console.WriteLine(student.Name);
}
```

---

# 9. HashSet Collections

[[#Navigation|⬆ Back to Navigation]]


A `HashSet<T>` stores unique items.

```csharp
var courses = new HashSet<string>();

courses.Add("CS");
courses.Add("IT");
courses.Add("CS"); // ignored, duplicate

Console.WriteLine(courses.Count); // 2
```

Good for checking uniqueness:

```csharp
if (courses.Contains("CS"))
{
    Console.WriteLine("CS exists");
}
```

---

# 10. Lambda Expressions

[[#Navigation|⬆ Back to Navigation]]


A lambda is an inline function.

```csharp
s => s.Course == "CS"
```

Read it as:

```text
For each student s, return true if s.Course is CS.
```

More examples:

```csharp
s => s.Name
s => s.GPA >= 3.7
b => b.Available == true
x => x * 2
```

With two parameters:

```csharp
(a, b) => a + b
```

Block lambda:

```csharp
s =>
{
    double avg = s.GetAverage();
    return avg >= 87;
}
```

---

# 11. LINQ Mental Model

[[#Navigation|⬆ Back to Navigation]]


LINQ is how you query collections.

SQL idea:

```sql
SELECT Name
FROM Students
WHERE Course = 'CS'
ORDER BY GPA DESC
```

C# LINQ version:

```csharp
var result = students
    .Where(s => s.Course == "CS")
    .OrderByDescending(s => s.GPA)
    .Select(s => s.Name)
    .ToList();
```

Read it out loud:

```text
Start with students
Keep only CS students
Sort by GPA highest first
Get only their names
Execute and turn into a List
```

---

# 12. The LINQ Ladder

[[#Navigation|⬆ Back to Navigation]]


Learn LINQ in this order:

1. `Where` — filter
2. `FirstOrDefault` — find one
3. `Any` — check existence
4. `OrderBy` / `OrderByDescending` — sort
5. `Select` — transform
6. `Count` — count
7. `Average`, `Max`, `Min`, `Sum` — compute
8. `Skip` / `Take` — pagination
9. `GroupBy` — grouping/statistics

---

# 13. LINQ Core Methods

[[#Navigation|⬆ Back to Navigation]]


## Where — Filter Many Items

```csharp
var csStudents = students
    .Where(s => s.Course == "CS")
    .ToList();
```

Meaning:

```text
Keep only students where Course is CS.
```

More examples:

```csharp
var honors = students.Where(s => s.GPA >= 3.7).ToList();

var availableBooks = books.Where(b => b.Available).ToList();

var recentBooks = books.Where(b => b.Year >= 2020).ToList();
```

---

## FirstOrDefault — Find One Item

```csharp
var student = students.FirstOrDefault(s => s.Id == 1);
```

Always check for null:

```csharp
if (student == null)
{
    Console.WriteLine("Not found");
}
else
{
    Console.WriteLine(student.Name);
}
```

For Web API:

```csharp
var student = _students.FirstOrDefault(s => s.Id == id);

return student == null ? NotFound() : Ok(student);
```

---

## Any — Check If Something Exists

```csharp
bool hasHonor = students.Any(s => s.GPA >= 3.7);
```

Examples:

```csharp
bool hasCS = students.Any(s => s.Course == "CS");

bool bookExists = books.Any(b => b.Id == id);

bool duplicateTitle = books.Any(b => b.Title == newBook.Title);
```

For duplicate checking:

```csharp
if (_books.Any(b => b.Title == book.Title))
{
    return Conflict("Book title already exists.");
}
```

---

## OrderBy / OrderByDescending — Sort

```csharp
var sortedByName = students
    .OrderBy(s => s.Name)
    .ToList();
```

```csharp
var highestFirst = students
    .OrderByDescending(s => s.GPA)
    .ToList();
```

Multiple sorting:

```csharp
var sorted = students
    .OrderBy(s => s.Course)
    .ThenByDescending(s => s.GPA)
    .ToList();
```

Meaning:

```text
Sort by course A-Z.
If same course, sort by GPA highest first.
```

---

## Select — Transform Shape

`Select` changes what each item looks like.

```csharp
var names = students
    .Select(s => s.Name)
    .ToList();
```

Output:

```text
List<string>
```

Create custom response shape:

```csharp
var result = students
    .Select(s => new
    {
        s.Id,
        s.Name,
        s.Course,
        Average = s.GetAverage(),
        IsHonor = s.GetAverage() >= 87
    })
    .ToList();
```

Useful in Web APIs:

```csharp
return Ok(result);
```

---

## Count — Count Items

```csharp
int total = students.Count;
```

With condition:

```csharp
int csCount = students.Count(s => s.Course == "CS");
int honorCount = students.Count(s => s.GPA >= 3.7);
```

---

## Average, Max, Min, Sum

```csharp
double averageGpa = students.Average(s => s.GPA);
double highestGpa = students.Max(s => s.GPA);
double lowestGpa = students.Min(s => s.GPA);
double totalGpa = students.Sum(s => s.GPA);
```

Avoid crash on empty list:

```csharp
double average = students.Any()
    ? students.Average(s => s.GPA)
    : 0;
```

---

## Skip and Take — Pagination

```csharp
int page = 1;
int size = 10;

var result = students
    .Skip((page - 1) * size)
    .Take(size)
    .ToList();
```

Examples:

```text
page 1, size 10 → skip 0, take 10
page 2, size 10 → skip 10, take 10
page 3, size 10 → skip 20, take 10
```

Web API example:

```csharp
[HttpGet]
public IActionResult GetAll([FromQuery] int page = 1, [FromQuery] int size = 10)
{
    var result = _students
        .Skip((page - 1) * size)
        .Take(size)
        .ToList();

    return Ok(result);
}
```

---

## GroupBy — Grouping and Stats

Group students by course:

```csharp
var grouped = students
    .GroupBy(s => s.Course)
    .ToList();
```

Usually, you combine `GroupBy` with `Select`.

```csharp
var stats = students
    .GroupBy(s => s.Course)
    .Select(group => new
    {
        Course = group.Key,
        Count = group.Count(),
        AverageGpa = group.Average(s => s.GPA)
    })
    .ToList();
```

Read it:

```text
Group students by Course.
For each group, return:
- the course name
- the number of students
- the average GPA
```

Web API stats endpoint:

```csharp
[HttpGet("stats")]
public IActionResult GetStats()
{
    var stats = _students
        .GroupBy(s => s.Course)
        .Select(g => new
        {
            Course = g.Key,
            Count = g.Count(),
            AverageGpa = g.Average(s => s.GPA)
        })
        .ToList();

    return Ok(stats);
}
```

---

# 14. LINQ: Common Recipes

[[#Navigation|⬆ Back to Navigation]]


## Get All CS Students

```csharp
var result = students
    .Where(s => s.Course == "CS")
    .ToList();
```

## Get Honor Students Sorted Highest First

```csharp
var result = students
    .Where(s => s.GetAverage() >= 87)
    .OrderByDescending(s => s.GetAverage())
    .ToList();
```

## Get Top Student

```csharp
var top = students
    .OrderByDescending(s => s.GetAverage())
    .FirstOrDefault();
```

## Get Top 3 Students

```csharp
var top3 = students
    .OrderByDescending(s => s.GetAverage())
    .Take(3)
    .ToList();
```

## Search by Name

```csharp
var result = students
    .Where(s => s.Name.Contains(search, StringComparison.OrdinalIgnoreCase))
    .ToList();
```

## Filter by Optional Query Params

```csharp
var result = students.AsEnumerable();

if (!string.IsNullOrEmpty(course))
{
    result = result.Where(s => s.Course == course);
}

if (honorOnly == true)
{
    result = result.Where(s => s.GetAverage() >= 87);
}

return Ok(result.ToList());
```

## Count Students Per Course

```csharp
var result = students
    .GroupBy(s => s.Course)
    .Select(g => new
    {
        Course = g.Key,
        Count = g.Count()
    })
    .ToList();
```

## Get Students Per Course With Names

```csharp
var result = students
    .GroupBy(s => s.Course)
    .Select(g => new
    {
        Course = g.Key,
        Students = g.Select(s => s.Name).ToList()
    })
    .ToList();
```

## Convert List to Dictionary

```csharp
var dictionary = students.ToDictionary(s => s.Id);
```

Then:

```csharp
var student = dictionary[1];
```

Safer:

```csharp
if (dictionary.TryGetValue(1, out var student))
{
    Console.WriteLine(student.Name);
}
```

---

# 15. LINQ Mistakes to Avoid

[[#Navigation|⬆ Back to Navigation]]


## Mistake 1: Forgetting `.ToList()`

```csharp
var result = students.Where(s => s.Course == "CS");
```

This is not a `List<Student>` yet. It is a lazy query.

Usually for beginner work:

```csharp
var result = students.Where(s => s.Course == "CS").ToList();
```

## Mistake 2: Using `First()` When Item Might Not Exist

```csharp
var student = students.First(s => s.Id == 99); // can crash
```

Safer:

```csharp
var student = students.FirstOrDefault(s => s.Id == 99);
```

## Mistake 3: Calling Average on an Empty List

```csharp
double avg = grades.Average(); // crashes if empty
```

Safer:

```csharp
double avg = grades.Count == 0 ? 0 : grades.Average();
```

## Mistake 4: Case-Sensitive String Comparison

```csharp
s.Course == "cs" // may fail if stored as "CS"
```

Safer:

```csharp
s.Course.Equals(course, StringComparison.OrdinalIgnoreCase)
```

## Mistake 5: Confusing `Select` and `Where`

```text
Where = filters items
Select = changes item shape
```

Example:

```csharp
students.Where(s => s.Course == "CS") // still Student objects
students.Select(s => s.Name)          // now strings
```

---

# 16. Web API Basics

[[#Navigation|⬆ Back to Navigation]]


## Program.cs

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Important:

```text
builder.Services = register services
app.Use... = middleware/request pipeline
app.MapControllers = connect controller routes
```

---

# 17. Controller Template

[[#Navigation|⬆ Back to Navigation]]


```csharp
using Microsoft.AspNetCore.Mvc;

namespace StudentApi.Controllers;

[ApiController]
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
    private static List<Student> _students = new()
    {
        new Student { Id = 1, Name = "Ana", Course = "CS", GPA = 3.9 },
        new Student { Id = 2, Name = "Ben", Course = "IT", GPA = 3.2 }
    };

    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok(_students);
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        var student = _students.FirstOrDefault(s => s.Id == id);

        if (student == null)
        {
            return NotFound();
        }

        return Ok(student);
    }
}
```

---

# 18. Route Params vs Query Params

[[#Navigation|⬆ Back to Navigation]]


## Route Parameter

```http
GET /api/students/1
```

Controller:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
```

Use when identifying one specific resource.

## Query Parameter

```http
GET /api/students/search?course=CS&honorOnly=true
```

Controller:

```csharp
[HttpGet("search")]
public IActionResult Search([FromQuery] string? course, [FromQuery] bool? honorOnly)
```

Use for filtering, searching, sorting, and pagination.

---

# 19. CRUD Endpoint Cheat Sheet

[[#Navigation|⬆ Back to Navigation]]


| Action | HTTP Verb | Route | Status |
|---|---|---|---|
| Get all | GET | `/api/books` | `200 OK` |
| Get one | GET | `/api/books/{id}` | `200 OK` or `404 Not Found` |
| Create | POST | `/api/books` | `201 Created` |
| Full update | PUT | `/api/books/{id}` | `200 OK` or `404 Not Found` |
| Partial update | PATCH | `/api/books/{id}` | `200 OK` or `404 Not Found` |
| Delete | DELETE | `/api/books/{id}` | `204 No Content` or `404 Not Found` |

---

# 20. Full CRUD Mini Template

[[#Navigation|⬆ Back to Navigation]]


```csharp
[ApiController]
[Route("api/[controller]")]
public class BooksController : ControllerBase
{
    private static List<Book> _books = new();

    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok(_books);
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        var book = _books.FirstOrDefault(b => b.Id == id);
        return book == null ? NotFound() : Ok(book);
    }

    [HttpPost]
    public IActionResult Create([FromBody] Book book)
    {
        book.Id = _books.Count == 0 ? 1 : _books.Max(b => b.Id) + 1;
        _books.Add(book);

        return CreatedAtAction(nameof(GetById), new { id = book.Id }, book);
    }

    [HttpPut("{id:int}")]
    public IActionResult Update(int id, [FromBody] Book updated)
    {
        var book = _books.FirstOrDefault(b => b.Id == id);

        if (book == null)
        {
            return NotFound();
        }

        book.Title = updated.Title;
        book.Author = updated.Author;
        book.Genre = updated.Genre;
        book.Year = updated.Year;
        book.Available = updated.Available;

        return Ok(book);
    }

    [HttpPatch("{id:int}")]
    public IActionResult Patch(int id, [FromBody] BookPatchDto patch)
    {
        var book = _books.FirstOrDefault(b => b.Id == id);

        if (book == null)
        {
            return NotFound();
        }

        if (patch.Title != null)
        {
            book.Title = patch.Title;
        }

        if (patch.Available != null)
        {
            book.Available = patch.Available.Value;
        }

        return Ok(book);
    }

    [HttpDelete("{id:int}")]
    public IActionResult Delete(int id)
    {
        var book = _books.FirstOrDefault(b => b.Id == id);

        if (book == null)
        {
            return NotFound();
        }

        _books.Remove(book);

        return NoContent();
    }
}
```

---

# 21. Data Annotations

[[#Navigation|⬆ Back to Navigation]]


```csharp
using System.ComponentModel.DataAnnotations;

public class Student
{
    public int Id { get; set; }

    [Required]
    [StringLength(100, MinimumLength = 2)]
    public string Name { get; set; } = string.Empty;

    [Required]
    public string Course { get; set; } = string.Empty;

    [Range(0.0, 4.0)]
    public double GPA { get; set; }
}
```

With `[ApiController]`, invalid input automatically returns:

```text
400 Bad Request
```

---

# 22. DTOs

[[#Navigation|⬆ Back to Navigation]]


## Model

```csharp
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; } = string.Empty;
    public string Course { get; set; } = string.Empty;
    public double GPA { get; set; }
}
```

## Create DTO

```csharp
public class StudentCreateDto
{
    public string Name { get; set; } = string.Empty;
    public string Course { get; set; } = string.Empty;
    public double GPA { get; set; }
}
```

## Response DTO

```csharp
public class StudentResponseDto
{
    public int Id { get; set; }
    public string Name { get; set; } = string.Empty;
    public bool IsHonor { get; set; }
}
```

## Manual Mapping

```csharp
var response = new StudentResponseDto
{
    Id = student.Id,
    Name = student.Name,
    IsHonor = student.GPA >= 3.7
};
```

Using LINQ:

```csharp
var response = students
    .Select(s => new StudentResponseDto
    {
        Id = s.Id,
        Name = s.Name,
        IsHonor = s.GPA >= 3.7
    })
    .ToList();
```

---

# 23. IActionResult Helpers

[[#Navigation|⬆ Back to Navigation]]


| Method | Status | Use |
|---|---:|---|
| `Ok(data)` | 200 | Successful GET/PUT/PATCH |
| `CreatedAtAction(...)` | 201 | Successful POST |
| `NoContent()` | 204 | Successful DELETE |
| `BadRequest()` | 400 | Invalid request |
| `Unauthorized()` | 401 | Not logged in |
| `Forbid()` | 403 | Logged in but not allowed |
| `NotFound()` | 404 | Missing resource |
| `Conflict()` | 409 | Duplicate/state conflict |
| `StatusCode(500)` | 500 | Server error |

---

# 24. Middleware Preview for Day 3

[[#Navigation|⬆ Back to Navigation]]


Middleware is code that runs before/after controllers.

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");

    await next();

    Console.WriteLine($"Response: {context.Response.StatusCode}");
});
```

Order matters:

```csharp
var app = builder.Build();

app.UseHttpsRedirection();

app.Use(async (context, next) =>
{
    Console.WriteLine("Before controller");
    await next();
    Console.WriteLine("After controller");
});

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Mental model:

```text
Request enters
→ middleware
→ routing
→ controller
→ response goes back through middleware
```

---

# 25. Most Important Patterns to Memorize

[[#Navigation|⬆ Back to Navigation]]


## Find by ID

```csharp
var item = items.FirstOrDefault(x => x.Id == id);
return item == null ? NotFound() : Ok(item);
```

## Filter Optional Query Params

```csharp
var result = items.AsEnumerable();

if (!string.IsNullOrEmpty(search))
{
    result = result.Where(x => x.Name.Contains(search, StringComparison.OrdinalIgnoreCase));
}

if (available.HasValue)
{
    result = result.Where(x => x.Available == available.Value);
}

return Ok(result.ToList());
```

## Create New ID

```csharp
item.Id = items.Count == 0 ? 1 : items.Max(x => x.Id) + 1;
items.Add(item);
return CreatedAtAction(nameof(GetById), new { id = item.Id }, item);
```

## Stats Endpoint

```csharp
var stats = items
    .GroupBy(x => x.Category)
    .Select(g => new
    {
        Category = g.Key,
        Count = g.Count()
    })
    .ToList();

return Ok(stats);
```

## Pagination

```csharp
var pageItems = items
    .Skip((page - 1) * size)
    .Take(size)
    .ToList();

return Ok(pageItems);
```

---

# 26. LINQ Quick Translation Table

[[#Navigation|⬆ Back to Navigation]]


| You want to... | Use |
|---|---|
| Filter items | `.Where(...)` |
| Find one item | `.FirstOrDefault(...)` |
| Check if exists | `.Any(...)` |
| Sort A-Z / low-high | `.OrderBy(...)` |
| Sort high-low | `.OrderByDescending(...)` |
| Transform output | `.Select(...)` |
| Count items | `.Count()` or `.Count(...)` |
| Average values | `.Average(...)` |
| Highest value | `.Max(...)` |
| Lowest value | `.Min(...)` |
| Add values | `.Sum(...)` |
| Page results | `.Skip(...).Take(...)` |
| Group items | `.GroupBy(...)` |
| Execute as list | `.ToList()` |

---

# 27. Practice Drills

[[#Navigation|⬆ Back to Navigation]]


Use this sample list:

```csharp
var students = new List<Student>
{
    new Student { Id = 1, Name = "Ana", Course = "CS", GPA = 3.9 },
    new Student { Id = 2, Name = "Ben", Course = "IT", GPA = 3.2 },
    new Student { Id = 3, Name = "Carlo", Course = "CS", GPA = 3.6 },
    new Student { Id = 4, Name = "Diana", Course = "IT", GPA = 3.8 }
};
```

Practice writing:

```csharp
// 1. All CS students
var cs = students.Where(s => s.Course == "CS").ToList();

// 2. Student with Id 3
var id3 = students.FirstOrDefault(s => s.Id == 3);

// 3. Honor students GPA >= 3.7
var honors = students.Where(s => s.GPA >= 3.7).ToList();

// 4. Students sorted by GPA high to low
var ranked = students.OrderByDescending(s => s.GPA).ToList();

// 5. Names only
var names = students.Select(s => s.Name).ToList();

// 6. Count per course
var countPerCourse = students
    .GroupBy(s => s.Course)
    .Select(g => new
    {
        Course = g.Key,
        Count = g.Count()
    })
    .ToList();
```

---

# 28. Final Day 3 Prep

[[#Navigation|⬆ Back to Navigation]]


Before middleware, be comfortable with this:

```text
1. Controller receives request
2. Route parameters identify resources
3. Query parameters filter collections
4. LINQ filters/searches/sorts the in-memory list
5. Controller returns IActionResult
6. Middleware runs before/after the controller
```

Minimum LINQ to survive tomorrow:

```csharp
.Where(...)
.FirstOrDefault(...)
.Any(...)
.OrderByDescending(...)
.Select(...)
.GroupBy(...)
.ToList()
```
