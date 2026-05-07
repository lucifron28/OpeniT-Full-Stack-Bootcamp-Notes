# ASP.NET Core Web API Reviewer — From Minimal APIs to Modular Structure

Tags: #aspnet #dotnet #webapi #minimal-api #controllers #dto #services #dependency-injection #middleware #csharp #obsidian

---

# Navigation

## A. Study Path and Big Picture

- [[#0. Suggested Study Path|0. Suggested Study Path]]
- [[#1. What This Reviewer Covers|1. What This Reviewer Covers]]
- [[#2. Web API Mental Model|2. Web API Mental Model]]
- [[#3. CSharp to ASP.NET Core Bridge|3. CSharp to ASP.NET Core Bridge]]
- [[#4. DRF to ASP.NET Core Translation Map|4. DRF to ASP.NET Core Translation Map]]

## B. Minimal APIs First

- [[#5. Why Start with Minimal APIs|5. Why Start with Minimal APIs]]
- [[#6. Minimal API Hello World|6. Minimal API Hello World]]
- [[#7. Minimal API Request and Response Basics|7. Minimal API Request and Response Basics]]
- [[#8. Minimal API Route Parameters|8. Minimal API Route Parameters]]
- [[#9. Minimal API Query Parameters|9. Minimal API Query Parameters]]
- [[#10. Minimal API Request Body|10. Minimal API Request Body]]
- [[#11. Minimal API CRUD Example|11. Minimal API CRUD Example]]
- [[#12. Minimal API Limitations|12. Minimal API Limitations]]

## C. Transition to Modular Web API

- [[#13. Why Move from Minimal APIs to Controllers|13. Why Move from Minimal APIs to Controllers]]
- [[#14. Minimal API to Controller Mapping|14. Minimal API to Controller Mapping]]
- [[#15. Modular Project Structure|15. Modular Project Structure]]
- [[#16. Layer Responsibilities|16. Layer Responsibilities]]
- [[#17. Beginner Version vs Organized Version vs Professional Version|17. Beginner Version vs Organized Version vs Professional Version]]

## D. CSharp Fundamentals Used in ASP.NET Core

- [[#18. Namespaces and Using Statements|18. Namespaces and Using Statements]]
- [[#19. File-Scoped Namespace|19. File-Scoped Namespace]]
- [[#20. Classes and Objects in Web APIs|20. Classes and Objects in Web APIs]]
- [[#21. Properties, Getters, and Setters in Models and DTOs|21. Properties, Getters, and Setters in Models and DTOs]]
- [[#22. Nullable Types in APIs|22. Nullable Types in APIs]]
- [[#23. Interfaces as Service Contracts|23. Interfaces as Service Contracts]]
- [[#24. Records vs Classes for DTOs|24. Records vs Classes for DTOs]]
- [[#25. Lists, Dictionaries, and HashSets in APIs|25. Lists, Dictionaries, and HashSets in APIs]]
- [[#26. LINQ in Services|26. LINQ in Services]]
- [[#27. Async, Task, and Await Preview|27. Async, Task, and Await Preview]]

## E. Program.cs and App Startup

- [[#28. Program.cs Mental Model|28. Program.cs Mental Model]]
- [[#29. Service Registration|29. Service Registration]]
- [[#30. Request Pipeline|30. Request Pipeline]]
- [[#31. Common Program.cs Templates|31. Common Program.cs Templates]]

## F. Controllers and Routing

- [[#32. What Controllers Are|32. What Controllers Are]]
- [[#33. ControllerBase and ApiController|33. ControllerBase and ApiController]]
- [[#34. Attribute Routing|34. Attribute Routing]]
- [[#35. api controller Route Token|35. api controller Route Token]]
- [[#36. HTTP Method Attributes|36. HTTP Method Attributes]]
- [[#37. Route Parameters|37. Route Parameters]]
- [[#38. Query Parameters|38. Query Parameters]]
- [[#39. Request Body and FromBody|39. Request Body and FromBody]]
- [[#40. Class-Level Routes vs Method-Level Routes|40. Class-Level Routes vs Method-Level Routes]]

## G. Return Types and HTTP Responses

- [[#41. IActionResult|41. IActionResult]]
- [[#42. ActionResult of T|42. ActionResult of T]]
- [[#43. Common Response Helpers|43. Common Response Helpers]]
- [[#44. HTTP Status Codes|44. HTTP Status Codes]]
- [[#45. CreatedAtAction|45. CreatedAtAction]]

## H. Models, DTOs, Validation, and Mapping

- [[#46. Models vs DTOs|46. Models vs DTOs]]
- [[#47. DTOs as DRF Serializer Equivalent|47. DTOs as DRF Serializer Equivalent]]
- [[#48. Create DTO, Update DTO, Patch DTO, Response DTO|48. Create DTO, Update DTO, Patch DTO, Response DTO]]
- [[#49. Data Annotations|49. Data Annotations]]
- [[#50. Automatic Validation with ApiController|50. Automatic Validation with ApiController]]
- [[#51. Manual Mapping Between DTOs and Models|51. Manual Mapping Between DTOs and Models]]
- [[#52. Common Mapping Helpers|52. Common Mapping Helpers]]

## I. Services, Interfaces, and Dependency Injection

- [[#53. Why Use Services|53. Why Use Services]]
- [[#54. Thin Controller Pattern|54. Thin Controller Pattern]]
- [[#55. Service Class Example|55. Service Class Example]]
- [[#56. Interface Example|56. Interface Example]]
- [[#57. Dependency Injection Basics|57. Dependency Injection Basics]]
- [[#58. Service Lifetimes|58. Service Lifetimes]]
- [[#59. Singleton vs Scoped vs Transient|59. Singleton vs Scoped vs Transient]]
- [[#60. DI and Database Mental Model|60. DI and Database Mental Model]]

## J. CRUD API Patterns

- [[#61. GET All Pattern|61. GET All Pattern]]
- [[#62. GET By Id Pattern|62. GET By Id Pattern]]
- [[#63. POST Create Pattern|63. POST Create Pattern]]
- [[#64. PUT Full Update Pattern|64. PUT Full Update Pattern]]
- [[#65. PATCH Partial Update Pattern|65. PATCH Partial Update Pattern]]
- [[#66. DELETE Pattern|66. DELETE Pattern]]
- [[#67. Search, Filter, Sort, and Pagination Pattern|67. Search, Filter, Sort, and Pagination Pattern]]
- [[#68. Stats Endpoint Pattern|68. Stats Endpoint Pattern]]
- [[#69. Nested Resource Pattern|69. Nested Resource Pattern]]

## K. Middleware and Pipeline

- [[#70. What Middleware Is|70. What Middleware Is]]
- [[#71. Built-In Middleware|71. Built-In Middleware]]
- [[#72. Custom Inline Middleware|72. Custom Inline Middleware]]
- [[#73. Custom Middleware Class|73. Custom Middleware Class]]
- [[#74. Middleware Extension Method|74. Middleware Extension Method]]
- [[#75. Middleware Order Matters|75. Middleware Order Matters]]
- [[#76. Middleware vs Controller vs Service|76. Middleware vs Controller vs Service]]
- [[#77. Request Body Middleware Preview|77. Request Body Middleware Preview]]

## L. Data Storage for Bootcamp Stage

- [[#78. In-Memory Data Store|78. In-Memory Data Store]]
- [[#79. Static Data vs Singleton Store|79. Static Data vs Singleton Store]]
- [[#80. List, Dictionary, HashSet in Web APIs|80. List, Dictionary, HashSet in Web APIs]]
- [[#81. Keeping Dictionary Lookup in Sync|81. Keeping Dictionary Lookup in Sync]]
- [[#82. EF Core Preview|82. EF Core Preview]]

## M. Testing and Debugging

- [[#83. Running the API|83. Running the API]]
- [[#84. Postman Testing Guide|84. Postman Testing Guide]]
- [[#85. Sample Request Bodies|85. Sample Request Bodies]]
- [[#86. Reading Responses|86. Reading Responses]]
- [[#87. Common Errors and Fixes|87. Common Errors and Fixes]]

## N. Complete Reference Example

- [[#88. Complete Minimal API Student Example|88. Complete Minimal API Student Example]]
- [[#89. Complete Modular Student API Example|89. Complete Modular Student API Example]]
- [[#90. Endpoint Design Checklist|90. Endpoint Design Checklist]]
- [[#91. Beginner Mistakes to Avoid|91. Beginner Mistakes to Avoid]]
- [[#92. Quick Memorization Tables|92. Quick Memorization Tables]]
- [[#93. Final Review Checklist|93. Final Review Checklist]]

---

# 0. Suggested Study Path

## 30-Minute Review

```text
5 min  - Web API mental model
5 min  - Minimal APIs
5 min  - Why modular structure exists
5 min  - Controllers and routing
5 min  - DTOs, services, DI
5 min  - Middleware and status codes
```

Recommended sections:

```text
2, 5, 6, 12, 13, 15, 32, 46, 53, 57, 70, 92
```

## 1-Hour Review

```text
10 min - Minimal APIs
10 min - Transition to controllers
10 min - CSharp bridge concepts
10 min - Program.cs and pipeline
10 min - CRUD patterns
10 min - Common errors
```

Recommended sections:

```text
5 to 17
18 to 27
28 to 31
61 to 69
83 to 87
```

## 2-Hour Deep Review

```text
20 min - Minimal API basics
20 min - Modular architecture
20 min - Controllers and routing
20 min - DTOs, validation, mapping
20 min - Services and DI
20 min - Middleware and debugging
```

Recommended sections:

```text
All sections from 1 to 93
```

[[#Navigation|⬆ Back to Navigation]]

---

# 1. What This Reviewer Covers

This reviewer starts from the simplest ASP.NET Core API style and gradually moves into the cleaner modular structure.

Progression:

```text
Minimal API
↓
Controller-based API
↓
DTOs
↓
Models
↓
Services
↓
Interfaces
↓
Dependency Injection
↓
Middleware
↓
Data storage
↓
CRUD patterns
```

The main goal:

```text
Understand why ASP.NET Core projects are structured the way they are.
```

Key idea:

```text
Minimal APIs are useful for learning the request/response basics.
Controllers, DTOs, services, and data folders are used when the API grows.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 2. Web API Mental Model

A Web API receives HTTP requests and returns HTTP responses.

Example requests:

```http
GET /api/students
GET /api/students/1
POST /api/students
PUT /api/students/1
PATCH /api/students/1
DELETE /api/students/1
```

Example responses:

```text
200 OK
201 Created
204 No Content
400 Bad Request
404 Not Found
409 Conflict
500 Internal Server Error
```

Main pieces:

| Concept | Job |
|---|---|
| `Program.cs` | app setup, service registration, pipeline |
| Minimal API endpoint | small endpoint written directly in `Program.cs` |
| Controller | organized HTTP endpoint class |
| Action method | endpoint method inside controller |
| DTO | request/response shape |
| Model | internal data shape |
| Service | business logic |
| Interface | service contract |
| Data store | in-memory storage or database |
| Middleware | code before/after endpoint |

General request flow:

```text
Client
↓
ASP.NET Core pipeline
↓
Endpoint
↓
Business logic
↓
Data
↓
Response
```

[[#Navigation|⬆ Back to Navigation]]

---

# 3. CSharp to ASP.NET Core Bridge

ASP.NET Core Web API is still C#.

Most Web API concepts are just C# fundamentals used in a framework.

| CSharp Concept | ASP.NET Core Use |
|---|---|
| Class | controller, model, DTO, service |
| Object | request DTO instance, model instance |
| Property | JSON fields, model fields |
| Method | controller action, service operation |
| Interface | service contract |
| Constructor | dependency injection |
| Namespace | organize folders/classes |
| Nullable `?` | optional values and not-found results |
| List | in-memory collection of records |
| Dictionary | fast lookup by key |
| HashSet | unique values |
| LINQ | search, filter, sort, map |
| Lambda | LINQ conditions |
| `async Task` | async endpoints/database calls |
| `static` | shared in-memory data or helper class |
| Extension method | middleware registration helpers |

Example bridge:

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public int Age { get; set; }
}
```

This is just a C# class with properties.

ASP.NET uses it as a request body shape:

```csharp
[HttpPost]
public IActionResult Create([FromBody] StudentCreateDto dto)
{
    return Ok(dto);
}
```

Key takeaway:

```text
ASP.NET Core adds HTTP behavior around normal C# classes, methods, objects, and interfaces.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 4. DRF to ASP.NET Core Translation Map

If you know Django REST Framework:

| DRF | ASP.NET Core |
|---|---|
| `urls.py` | route attributes |
| APIView / ViewSet | Controller |
| `get`, `post`, `put` methods | action methods |
| Serializer | DTO plus DataAnnotations |
| Django model | Model / Entity |
| QuerySet | LINQ / EF Core query |
| `request.data` | `[FromBody] dto` |
| `request.query_params` | `[FromQuery]` |
| path parameter | route parameter |
| `Response(data, status=200)` | `Ok(data)` |
| `Response(status=404)` | `NotFound()` |
| Django ORM | EF Core later |
| settings.py | `appsettings.json` plus `Program.cs` |

Important difference:

```text
DRF serializers often handle input, output, validation, and transformation.

ASP.NET commonly separates:
DTOs = input/output shape
DataAnnotations = validation
Services = business logic
Manual mapping = DTO to Model and Model to DTO
```

[[#Navigation|⬆ Back to Navigation]]

---

# 5. Why Start with Minimal APIs

Minimal APIs are the simplest way to see how ASP.NET Core receives requests and returns responses.

Minimal API example:

```csharp
app.MapGet("/hello", () =>
{
    return "Hello API";
});
```

Request:

```http
GET /hello
```

Response:

```text
Hello API
```

Minimal APIs are useful because they show:

```text
routes
HTTP methods
request parameters
JSON responses
body binding
status codes
```

without adding:

```text
controllers
DTO folders
service folders
interfaces
extra files
```

Best use cases:

```text
small APIs
microservices
quick demos
health checks
simple endpoints
learning fundamentals
```

Key takeaway:

```text
Minimal APIs are a good starting point because they show the API concept directly.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 6. Minimal API Hello World

Basic project:

```csharp
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

app.MapGet("/", () =>
{
    return "Hello World";
});

app.Run();
```

Request:

```http
GET /
```

Response:

```text
Hello World
```

Return JSON object:

```csharp
app.MapGet("/api/info", () =>
{
    return new
    {
        App = "Student API",
        Version = "1.0"
    };
});
```

Response:

```json
{
  "app": "Student API",
  "version": "1.0"
}
```

Key takeaway:

```text
app.MapGet maps a GET request to a C# function.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 7. Minimal API Request and Response Basics

Common Minimal API methods:

```csharp
app.MapGet("/api/students", () => {});
app.MapPost("/api/students", () => {});
app.MapPut("/api/students/{id}", () => {});
app.MapPatch("/api/students/{id}", () => {});
app.MapDelete("/api/students/{id}", () => {});
```

Return helpers:

```csharp
return Results.Ok(data);
return Results.Created($"/api/students/{student.Id}", student);
return Results.NoContent();
return Results.BadRequest("Invalid input.");
return Results.NotFound();
return Results.Conflict("Duplicate record.");
```

Example:

```csharp
app.MapGet("/api/students", () =>
{
    return Results.Ok(new[] { "Ana", "Ben", "Carlo" });
});
```

Key takeaway:

```text
Minimal APIs use Results helpers instead of ControllerBase helpers like Ok().
```

[[#Navigation|⬆ Back to Navigation]]

---

# 8. Minimal API Route Parameters

Route parameter:

```csharp
app.MapGet("/api/students/{id:int}", (int id) =>
{
    return Results.Ok(new
    {
        Id = id
    });
});
```

Request:

```http
GET /api/students/5
```

Response:

```json
{
  "id": 5
}
```

Multiple route parameters:

```csharp
app.MapGet("/api/sections/{sectionCode}/students/{studentId:int}",
    (string sectionCode, int studentId) =>
    {
        return Results.Ok(new
        {
            SectionCode = sectionCode,
            StudentId = studentId
        });
    });
```

Request:

```http
GET /api/sections/MB02/students/3
```

Key takeaway:

```text
Route parameters are read from the URL path.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 9. Minimal API Query Parameters

Query parameter:

```csharp
app.MapGet("/api/students/search", (string? name, int? age) =>
{
    return Results.Ok(new
    {
        Name = name,
        Age = age
    });
});
```

Request:

```http
GET /api/students/search?name=ana&age=20
```

Response:

```json
{
  "name": "ana",
  "age": 20
}
```

Use query parameters for:

```text
search
filter
sort
pagination
optional values
```

Example:

```csharp
app.MapGet("/api/students", (
    string? name,
    string? gender,
    int page = 1,
    int pageSize = 10) =>
{
    return Results.Ok();
});
```

Key takeaway:

```text
Route parameters identify resources.
Query parameters filter or modify collection results.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 10. Minimal API Request Body

DTO:

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public int Age { get; set; }
}
```

Minimal API POST:

```csharp
app.MapPost("/api/students", (StudentCreateDto dto) =>
{
    return Results.Ok(dto);
});
```

Request:

```http
POST /api/students
Content-Type: application/json
```

Body:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "age": 20
}
```

ASP.NET automatically binds the JSON body to `StudentCreateDto`.

Key takeaway:

```text
Minimal APIs can bind JSON body directly into DTO parameters.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 11. Minimal API CRUD Example

Model:

```csharp
public class Student
{
    public int Id { get; set; }
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
}
```

DTO:

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
}
```

Minimal CRUD:

```csharp
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

List<Student> students = new();

app.MapGet("/api/students", () =>
{
    return Results.Ok(students);
});

app.MapGet("/api/students/{id:int}", (int id) =>
{
    var student = students.FirstOrDefault(s => s.Id == id);

    return student is null
        ? Results.NotFound()
        : Results.Ok(student);
});

app.MapPost("/api/students", (StudentCreateDto dto) =>
{
    var student = new Student
    {
        Id = students.Count == 0 ? 1 : students.Max(s => s.Id) + 1,
        FirstName = dto.FirstName.Trim(),
        LastName = dto.LastName.Trim()
    };

    students.Add(student);

    return Results.Created($"/api/students/{student.Id}", student);
});

app.MapDelete("/api/students/{id:int}", (int id) =>
{
    var student = students.FirstOrDefault(s => s.Id == id);

    if (student is null)
    {
        return Results.NotFound();
    }

    students.Remove(student);

    return Results.NoContent();
});

app.Run();
```

Key takeaway:

```text
A full API can be built with Minimal APIs, but Program.cs gets crowded as the project grows.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 12. Minimal API Limitations

Minimal APIs can become hard to manage when there are many endpoints.

Problems:

```text
Program.cs becomes too long.
Business logic mixes with route setup.
DTOs and models may be scattered.
Harder to group large resource logic.
Harder for beginners to see layers.
Repeated code grows quickly.
```

Example messy direction:

```csharp
app.MapGet("/api/students", ...);
app.MapGet("/api/students/{id}", ...);
app.MapPost("/api/students", ...);
app.MapPut("/api/students/{id}", ...);
app.MapPatch("/api/students/{id}", ...);
app.MapDelete("/api/students/{id}", ...);

app.MapGet("/api/sections", ...);
app.MapGet("/api/sections/{id}", ...);
app.MapPost("/api/sections", ...);
app.MapPut("/api/sections/{id}", ...);
```

This is why larger bootcamp projects usually move to:

```text
Controllers
DTOs
Models
Services
Data
Middleware
```

Key takeaway:

```text
Minimal APIs are simple, but modular structure is better when the API grows.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 13. Why Move from Minimal APIs to Controllers

Controller-based APIs organize endpoints into classes.

Instead of:

```csharp
app.MapGet("/api/students", () => {});
app.MapPost("/api/students", () => {});
```

Use:

```csharp
[ApiController]
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok();
    }

    [HttpPost]
    public IActionResult Create([FromBody] StudentCreateDto dto)
    {
        return Ok(dto);
    }
}
```

Benefits:

```text
Groups related endpoints.
Keeps Program.cs cleaner.
Supports clear route attributes.
Works well with DTOs and services.
Better for large CRUD projects.
```

Key takeaway:

```text
Minimal API teaches endpoint basics.
Controllers organize endpoints when the project grows.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 14. Minimal API to Controller Mapping

| Minimal API | Controller API |
|---|---|
| `app.MapGet("/api/students", ...)` | `[HttpGet]` inside `StudentsController` |
| `app.MapPost("/api/students", ...)` | `[HttpPost]` |
| `Results.Ok(data)` | `Ok(data)` |
| `Results.NotFound()` | `NotFound()` |
| `Results.Created(...)` | `CreatedAtAction(...)` |
| function parameter `(int id)` | action parameter `int id` |
| DTO parameter `(StudentCreateDto dto)` | `[FromBody] StudentCreateDto dto` |
| route string in Program.cs | `[Route(...)]` and `[Http...]` attributes |

Minimal API:

```csharp
app.MapGet("/api/students/{id:int}", (int id) =>
{
    var student = service.GetById(id);

    return student is null
        ? Results.NotFound()
        : Results.Ok(student);
});
```

Controller equivalent:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    var student = _studentService.GetById(id);

    if (student is null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

Key takeaway:

```text
Controllers do the same endpoint job, but organized inside classes.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 15. Modular Project Structure

Recommended beginner structure:

```text
StudentEnrollmentApi/
├── Controllers/
│   └── StudentsController.cs
├── Models/
│   └── Student.cs
├── DTOs/
│   ├── StudentCreateDto.cs
│   ├── StudentUpdateDto.cs
│   ├── StudentPatchDto.cs
│   └── StudentResponseDto.cs
├── Services/
│   ├── IStudentService.cs
│   └── StudentService.cs
├── Data/
│   └── InMemoryDataStore.cs
├── Middleware/
│   └── RequestLoggingMiddleware.cs
├── Program.cs
└── appsettings.json
```

For enrollment system:

```text
EnrollmentSystemApi/
├── Controllers/
│   ├── SectionsController.cs
│   └── StudentsController.cs
├── Models/
│   ├── Section.cs
│   └── Student.cs
├── DTOs/
│   ├── Sections/
│   └── Students/
├── Services/
│   ├── Sections/
│   └── Students/
├── Data/
└── Middleware/
```

Key takeaway:

```text
Folder structure exists to separate responsibilities.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 16. Layer Responsibilities

| Layer | Responsibility |
|---|---|
| `Program.cs` | register services and configure middleware |
| `Controllers` | receive HTTP requests and return HTTP responses |
| `DTOs` | define request and response shapes |
| `Models` | define internal stored data shape |
| `Services` | business logic and LINQ |
| `Interfaces` | service contracts |
| `Data` | in-memory storage or database context |
| `Middleware` | cross-cutting request pipeline logic |

Rule:

```text
Controller = HTTP layer
Service = business logic layer
Data = storage layer
DTO = API contract
Model = internal data
Middleware = request pipeline
```

[[#Navigation|⬆ Back to Navigation]]

---

# 17. Beginner Version vs Organized Version vs Professional Version

## Beginner Version

```text
Minimal API
List stored in Program.cs
All logic inside endpoint
```

Good for:

```text
learning
very small demos
```

## Organized Version

```text
Controllers
DTOs
Models
Services
In-memory Data Store
Dependency Injection
```

Good for:

```text
bootcamp CRUD projects
larger assignments
cleaner structure
```

## Professional Version

```text
Controllers or Minimal APIs
DTOs
Services
Repositories or DbContext
EF Core
Database
Authentication
Middleware
Logging
Validation
Error handling
```

Good for:

```text
real applications
team projects
production APIs
```

Key takeaway:

```text
Start simple to understand the flow, then modularize to manage complexity.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 18. Namespaces and Using Statements

A namespace organizes classes.

Example file:

```csharp
namespace StudentEnrollmentApi.Models;

public class Student
{
    public int Id { get; set; }
}
```

Another file:

```csharp
using StudentEnrollmentApi.Models;

namespace StudentEnrollmentApi.Services;

public class StudentService
{
    private List<Student> _students = new();
}
```

Meaning:

```text
Student is inside StudentEnrollmentApi.Models.
StudentService uses that namespace to access Student.
```

Folder and namespace often match:

```text
Models/Student.cs
namespace StudentEnrollmentApi.Models;

Services/StudentService.cs
namespace StudentEnrollmentApi.Services;
```

Common `using` statements:

```csharp
using Microsoft.AspNetCore.Mvc;
using System.ComponentModel.DataAnnotations;
using StudentEnrollmentApi.DTOs;
using StudentEnrollmentApi.Models;
using StudentEnrollmentApi.Services;
```

Key takeaway:

```text
Namespaces organize code. using imports namespaces so you can use their classes.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 19. File-Scoped Namespace

Modern C# commonly uses file-scoped namespaces.

File-scoped:

```csharp
namespace StudentEnrollmentApi.Models;

public class Student
{
    public int Id { get; set; }
}
```

Old block style:

```csharp
namespace StudentEnrollmentApi.Models
{
    public class Student
    {
        public int Id { get; set; }
    }
}
```

Both work.

File-scoped is shorter and common in modern .NET projects.

Key takeaway:

```text
File-scoped namespace reduces indentation and keeps files cleaner.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 20. Classes and Objects in Web APIs

Models, DTOs, controllers, and services are all C# classes.

Model class:

```csharp
public class Student
{
    public int Id { get; set; }
    public string FirstName { get; set; } = string.Empty;
}
```

Object instance:

```csharp
var student = new Student
{
    Id = 1,
    FirstName = "Ana"
};
```

DTO class:

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
}
```

Controller class:

```csharp
public class StudentsController : ControllerBase
{
}
```

Service class:

```csharp
public class StudentService : IStudentService
{
}
```

Key takeaway:

```text
ASP.NET Core architecture is built from normal C# classes with specific framework roles.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 21. Properties, Getters, and Setters in Models and DTOs

ASP.NET uses public properties for model binding and JSON serialization.

DTO:

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public int Age { get; set; }
}
```

Model binding needs setters:

```text
set allows ASP.NET to assign values from JSON.
```

Response serialization uses getters:

```text
get allows ASP.NET to read values and convert them to JSON.
```

Computed property:

```csharp
public string FullName => $"{FirstName} {LastName}";
```

This can appear in JSON responses if returned directly or mapped to response DTO.

Key takeaway:

```text
Public get/set properties are how ASP.NET reads and writes object data.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 22. Nullable Types in APIs

Nullable reference:

```csharp
public string? MiddleName { get; set; }
```

Nullable value type:

```csharp
public int? Grade { get; set; }
```

Use nullable in PATCH DTOs:

```csharp
public class StudentPatchDto
{
    public string? FirstName { get; set; }
    public int? Age { get; set; }
}
```

Meaning:

```text
null means not provided.
```

Use nullable return when record might not exist:

```csharp
public StudentResponseDto? GetById(int id)
{
    var student = _students.FirstOrDefault(s => s.Id == id);

    return student is null ? null : ToResponseDto(student);
}
```

Controller handles null:

```csharp
if (student is null)
{
    return NotFound();
}
```

Key takeaway:

```text
Nullable types are important for optional input and not-found results.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 23. Interfaces as Service Contracts

Interface:

```csharp
public interface IStudentService
{
    List<StudentResponseDto> GetAll();
    StudentResponseDto? GetById(int id);
    StudentResponseDto Create(StudentCreateDto dto);
}
```

Implementation:

```csharp
public class StudentService : IStudentService
{
    public List<StudentResponseDto> GetAll()
    {
        return new();
    }

    public StudentResponseDto? GetById(int id)
    {
        return null;
    }

    public StudentResponseDto Create(StudentCreateDto dto)
    {
        return new StudentResponseDto();
    }
}
```

Register:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Inject:

```csharp
public StudentsController(IStudentService studentService)
{
    _studentService = studentService;
}
```

Key takeaway:

```text
Controller depends on the interface. DI decides the actual class.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 24. Records vs Classes for DTOs

Class DTO:

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
}
```

Record DTO:

```csharp
public record StudentCreateDto(string FirstName, string LastName);
```

Records are concise and value-based.

Class DTOs are beginner-friendly because:

```text
They look like models.
They work clearly with DataAnnotations.
They are easier to modify while learning.
```

Example record response:

```csharp
public record StudentResponseDto(
    int Id,
    string FullName,
    int Age
);
```

Key takeaway:

```text
Use classes while learning. Records are useful later for simple immutable DTOs.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 25. Lists, Dictionaries, and HashSets in APIs

## List

Used for record storage and querying:

```csharp
List<Student> Students = new();
```

Good for:

```text
Get all
Search
Filter
Sort
Pagination
```

## Dictionary

Used for fast lookup:

```csharp
Dictionary<int, Student> StudentLookup = new();
```

Good for:

```text
Get by ID quickly
Check if ID exists
```

## HashSet

Used for unique allowed values:

```csharp
HashSet<string> ValidSections = new()
{
    "MB02",
    "CS101"
};
```

Good for:

```text
checking valid values
preventing duplicates
unique categories
```

Key takeaway:

```text
List is most common for bootcamp CRUD. Dictionary and HashSet are useful optimization or validation tools.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 26. LINQ in Services

LINQ is commonly used inside services.

Find one:

```csharp
var student = _students.FirstOrDefault(s => s.Id == id);
```

Filter:

```csharp
var result = _students
    .Where(s => s.Age >= 18)
    .ToList();
```

Search text:

```csharp
var result = _students
    .Where(s =>
        s.FirstName.Contains(name, StringComparison.OrdinalIgnoreCase) ||
        s.LastName.Contains(name, StringComparison.OrdinalIgnoreCase))
    .ToList();
```

Sort:

```csharp
var result = _students
    .OrderBy(s => s.LastName)
    .ToList();
```

Map to DTO:

```csharp
var response = _students
    .Select(s => new StudentResponseDto
    {
        Id = s.Id,
        FullName = $"{s.FirstName} {s.LastName}",
        Age = s.Age
    })
    .ToList();
```

Pagination:

```csharp
var pageResult = _students
    .Skip((page - 1) * pageSize)
    .Take(pageSize)
    .ToList();
```

Key takeaway:

```text
LINQ is the main way services search, filter, sort, and map data.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 27. Async, Task, and Await Preview

Many Web API methods use async later, especially with databases.

Synchronous:

```csharp
public IActionResult GetAll()
{
    var students = _studentService.GetAll();

    return Ok(students);
}
```

Async pattern:

```csharp
public async Task<IActionResult> GetAll()
{
    var students = await _studentService.GetAllAsync();

    return Ok(students);
}
```

Service async pattern:

```csharp
public async Task<List<StudentResponseDto>> GetAllAsync()
{
    return await _context.Students
        .Select(s => new StudentResponseDto
        {
            Id = s.Id,
            FullName = s.FirstName + " " + s.LastName
        })
        .ToListAsync();
}
```

Key idea:

```text
Task means work that finishes later.
await waits without blocking the thread.
```

For in-memory bootcamp lists, async is usually not needed.

For EF Core/database, async is common.

[[#Navigation|⬆ Back to Navigation]]

---

# 28. Program.cs Mental Model

`Program.cs` has two main responsibilities:

```text
1. Register services
2. Build the middleware/request pipeline
```

Example:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddScoped<IStudentService, StudentService>();

var app = builder.Build();

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

Service registration:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Pipeline:

```csharp
app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();
```

Start app:

```csharp
app.Run();
```

Key takeaway:

```text
builder.Services = what the app can use.
app.Use / app.Map = what each request passes through.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 29. Service Registration

Register controller support:

```csharp
builder.Services.AddControllers();
```

Register OpenAPI/Swagger:

```csharp
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
```

Register app services:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Register singleton store:

```csharp
builder.Services.AddSingleton<InMemoryDataStore>();
```

Meaning:

```text
When something asks for IStudentService, provide StudentService.
When something asks for InMemoryDataStore, provide the same shared store instance.
```

Key takeaway:

```text
DI registration tells ASP.NET how to create and provide objects.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 30. Request Pipeline

The request pipeline is the ordered chain that processes requests.

Example:

```csharp
var app = builder.Build();

app.UseHttpsRedirection();

app.UseMiddleware<RequestLoggingMiddleware>();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Flow:

```text
Request
↓
HTTPS middleware
↓
Logging middleware
↓
Authorization middleware
↓
Controller endpoint
↓
Response
```

Key takeaway:

```text
Order matters because requests move through middleware in order.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 31. Common Program.cs Templates

## Minimal API Template

```csharp
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

app.MapGet("/", () => "Hello API");

app.Run();
```

## Controller API Template

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

## Modular API Template

```csharp
using StudentEnrollmentApi.Services;
using StudentEnrollmentApi.Data;
using StudentEnrollmentApi.Middleware;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

builder.Services.AddSingleton<InMemoryDataStore>();
builder.Services.AddScoped<IStudentService, StudentService>();

var app = builder.Build();

app.UseHttpsRedirection();

app.UseMiddleware<RequestLoggingMiddleware>();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 32. What Controllers Are

A controller is a class that groups related HTTP endpoints.

Example:

```csharp
[ApiController]
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok();
    }
}
```

This handles:

```http
GET /api/students
```

Responsibilities:

```text
Read route parameters.
Read query parameters.
Read body DTO.
Call service.
Return HTTP response.
```

Avoid:

```text
Putting all search, creation, validation, and data manipulation logic in the controller.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 33. ControllerBase and ApiController

`ControllerBase` gives response helpers:

```csharp
Ok()
NotFound()
BadRequest()
CreatedAtAction()
NoContent()
Conflict()
Unauthorized()
Forbid()
```

`[ApiController]` gives API-specific behavior:

```text
automatic model validation
better parameter binding
automatic 400 for invalid DTOs
```

Example:

```csharp
[ApiController]
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
}
```

Key takeaway:

```text
ControllerBase gives HTTP helpers. ApiController improves Web API behavior.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 34. Attribute Routing

Routing connects URLs to controller actions.

Controller route:

```csharp
[Route("api/[controller]")]
```

Method route:

```csharp
[HttpGet("{id:int}")]
```

Full route:

```http
GET /api/students/1
```

Named route segment:

```csharp
[HttpGet("search")]
```

Full route:

```http
GET /api/students/search
```

Key takeaway:

```text
Class-level route plus method-level route equals the full endpoint.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 35. api controller Route Token

`[controller]` is replaced by the controller class name without the word `Controller`.

Example:

```csharp
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
}
```

Result:

```text
/api/students
```

Examples:

| Controller Class | Route |
|---|---|
| `StudentsController` | `/api/students` |
| `BooksController` | `/api/books` |
| `SectionController` | `/api/section` |
| `SectionsController` | `/api/sections` |

Key takeaway:

```text
[controller] avoids hardcoding the controller name in the route.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 36. HTTP Method Attributes

| Attribute | Verb | Use |
|---|---|---|
| `[HttpGet]` | GET | read |
| `[HttpPost]` | POST | create |
| `[HttpPut]` | PUT | full update |
| `[HttpPatch]` | PATCH | partial update |
| `[HttpDelete]` | DELETE | remove |

Examples:

```csharp
[HttpGet]
public IActionResult GetAll()
{
    return Ok();
}
```

```csharp
[HttpPost]
public IActionResult Create([FromBody] StudentCreateDto dto)
{
    return Ok(dto);
}
```

```csharp
[HttpDelete("{id:int}")]
public IActionResult Delete(int id)
{
    return NoContent();
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 37. Route Parameters

Route parameter:

```http
GET /api/students/5
```

Action:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    return Ok(id);
}
```

`{id:int}` means:

```text
id comes from the route.
id must be an integer.
```

Nested route:

```csharp
[HttpGet("{sectionCode}/students/{studentId:int}")]
public IActionResult GetStudent(string sectionCode, int studentId)
{
    return Ok();
}
```

Request:

```http
GET /api/sections/MB02/students/3
```

[[#Navigation|⬆ Back to Navigation]]

---

# 38. Query Parameters

Query parameter:

```http
GET /api/students/search?name=ana&age=20
```

Action:

```csharp
[HttpGet("search")]
public IActionResult Search(
    [FromQuery] string? name,
    [FromQuery] int? age)
{
    return Ok();
}
```

Use query parameters for:

```text
search
filter
sort
pagination
optional modifiers
```

Rule:

```text
Route parameter = identify resource.
Query parameter = filter or modify result.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 39. Request Body and FromBody

POST/PUT/PATCH usually receive JSON body.

Body:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "age": 20
}
```

Action:

```csharp
[HttpPost]
public IActionResult Create([FromBody] StudentCreateDto dto)
{
    return Ok(dto);
}
```

`[FromBody]` means:

```text
Read JSON body and bind it to this DTO.
```

Key takeaway:

```text
[FromBody] is like DRF request.data.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 40. Class-Level Routes vs Method-Level Routes

Class-level:

```csharp
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
}
```

Base route:

```text
/api/students
```

Method-level:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    return Ok();
}
```

Full route:

```http
GET /api/students/1
```

Summary:

```text
Class route = common base path.
Method route = specific endpoint.
Full route = class route + method route.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 41. IActionResult

`IActionResult` is a return type that allows different HTTP responses.

Example:

```csharp
public IActionResult GetById(int id)
{
    var student = _studentService.GetById(id);

    if (student is null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

This method can return:

```text
404 NotFound
200 Ok
```

Both fit under:

```csharp
IActionResult
```

Key takeaway:

```text
IActionResult lets one action return different HTTP response types.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 42. ActionResult of T

Example:

```csharp
public ActionResult<StudentResponseDto> GetById(int id)
{
    var student = _studentService.GetById(id);

    if (student is null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

Meaning:

```text
This usually returns StudentResponseDto, but can also return HTTP errors.
```

Use:

```text
IActionResult = simple and flexible
ActionResult<T> = more explicit
```

[[#Navigation|⬆ Back to Navigation]]

---

# 43. Common Response Helpers

| Helper | Status |
|---|---|
| `Ok(data)` | 200 |
| `CreatedAtAction(...)` | 201 |
| `NoContent()` | 204 |
| `BadRequest()` | 400 |
| `Unauthorized()` | 401 |
| `Forbid()` | 403 |
| `NotFound()` | 404 |
| `Conflict()` | 409 |
| `Problem()` | 500 style error |

Examples:

```csharp
return Ok(student);
return NotFound();
return BadRequest("Invalid input.");
return Conflict("Duplicate student.");
return NoContent();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 44. HTTP Status Codes

| Status | Meaning | Use |
|---|---|---|
| 200 | OK | successful GET/PUT/PATCH |
| 201 | Created | successful POST |
| 204 | No Content | successful DELETE |
| 400 | Bad Request | invalid input |
| 401 | Unauthorized | not logged in |
| 403 | Forbidden | not allowed |
| 404 | Not Found | missing record |
| 409 | Conflict | duplicate or state conflict |
| 500 | Server Error | unhandled exception |

Beginner rules:

```text
GET success = 200
POST success = 201
DELETE success = 204
Not found = 404
Bad input = 400
Duplicate = 409
```

[[#Navigation|⬆ Back to Navigation]]

---

# 45. CreatedAtAction

Used after successful POST.

```csharp
return CreatedAtAction(
    nameof(GetById),
    new { id = student.Id },
    student
);
```

Meaning:

```text
Return 201 Created.
Return the created object.
Add a Location header for where to get it.
```

If `GetById` route is:

```http
GET /api/students/7
```

Then the created response points to that route.

[[#Navigation|⬆ Back to Navigation]]

---

# 46. Models vs DTOs

Model:

```csharp
public class Student
{
    public int Id { get; set; }
    public string FirstName { get; set; } = string.Empty;
    public DateTime CreatedAt { get; set; }
}
```

DTO:

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
}
```

Difference:

```text
Model = internal stored data
DTO = API input/output shape
```

Why separate:

```text
Client should not set Id.
Client should not set CreatedAt.
Response should not expose internal fields.
Different endpoints need different shapes.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 47. DTOs as DRF Serializer Equivalent

DRF serializer:

```python
class StudentSerializer(serializers.Serializer):
    first_name = serializers.CharField()
```

ASP.NET DTO:

```csharp
public class StudentCreateDto
{
    [Required]
    public string FirstName { get; set; } = string.Empty;
}
```

Mental model:

```text
DRF Serializer
≈
ASP.NET DTO + DataAnnotations + manual mapping
```

[[#Navigation|⬆ Back to Navigation]]

---

# 48. Create DTO, Update DTO, Patch DTO, Response DTO

Create DTO:

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
}
```

Update DTO:

```csharp
public class StudentUpdateDto
{
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public bool IsActive { get; set; }
}
```

Patch DTO:

```csharp
public class StudentPatchDto
{
    public string? FirstName { get; set; }
    public string? LastName { get; set; }
    public bool? IsActive { get; set; }
}
```

Response DTO:

```csharp
public class StudentResponseDto
{
    public int Id { get; set; }
    public string FullName { get; set; } = string.Empty;
    public bool IsActive { get; set; }
}
```

Rule:

```text
POST = Create DTO
PUT = Update DTO
PATCH = Patch DTO with nullable properties
GET response = Response DTO
```

[[#Navigation|⬆ Back to Navigation]]

---

# 49. Data Annotations

Import:

```csharp
using System.ComponentModel.DataAnnotations;
```

Common attributes:

```csharp
[Required]
[StringLength(100)]
[MinLength(2)]
[MaxLength(100)]
[Range(1, 4)]
[EmailAddress]
[Url]
[RegularExpression("pattern")]
```

Example:

```csharp
public class StudentCreateDto
{
    [Required]
    [StringLength(100, MinimumLength = 2)]
    public string FirstName { get; set; } = string.Empty;

    [Range(1, 4)]
    public int YearLevel { get; set; }
}
```

Key takeaway:

```text
DataAnnotations validate DTO input.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 50. Automatic Validation with ApiController

With `[ApiController]`, invalid DTOs can automatically return 400.

Controller:

```csharp
[ApiController]
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
    [HttpPost]
    public IActionResult Create([FromBody] StudentCreateDto dto)
    {
        return Ok(dto);
    }
}
```

If DTO validation fails:

```text
ASP.NET returns 400 Bad Request before the method logic continues.
```

Without `[ApiController]`, you often manually check:

```csharp
if (!ModelState.IsValid)
{
    return BadRequest(ModelState);
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 51. Manual Mapping Between DTOs and Models

Create DTO to model:

```csharp
var student = new Student
{
    Id = nextId,
    FirstName = dto.FirstName.Trim(),
    LastName = dto.LastName.Trim(),
    CreatedAt = DateTime.UtcNow
};
```

Model to response DTO:

```csharp
var response = new StudentResponseDto
{
    Id = student.Id,
    FullName = $"{student.FirstName} {student.LastName}"
};
```

Why mapping matters:

```text
Cleans input.
Hides internal fields.
Controls response shape.
Prevents over-posting.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 52. Common Mapping Helpers

Private helper method inside service:

```csharp
private StudentResponseDto ToResponseDto(Student student)
{
    return new StudentResponseDto
    {
        Id = student.Id,
        FullName = $"{student.FirstName} {student.LastName}",
        Age = student.Age
    };
}
```

Use:

```csharp
return ToResponseDto(student);
```

Map list:

```csharp
return _students
    .Select(ToResponseDto)
    .ToList();
```

Create model helper:

```csharp
private Student ToStudent(StudentCreateDto dto, int id)
{
    return new Student
    {
        Id = id,
        FirstName = dto.FirstName.Trim(),
        LastName = dto.LastName.Trim()
    };
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 53. Why Use Services

Services contain business logic.

Controller should not do everything.

Controller:

```csharp
[HttpPost]
public IActionResult Create([FromBody] StudentCreateDto dto)
{
    var student = _studentService.Create(dto);

    return CreatedAtAction(nameof(GetById), new { id = student.Id }, student);
}
```

Service:

```csharp
public StudentResponseDto Create(StudentCreateDto dto)
{
    // create ID
    // clean data
    // check duplicate
    // add to list
    // map to response DTO
}
```

Key takeaway:

```text
Controller handles HTTP.
Service handles actual app logic.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 54. Thin Controller Pattern

Thin controller example:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    var student = _studentService.GetById(id);

    if (student is null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

Controller does:

```text
receive id
call service
return status code
```

Service does:

```text
find record
map record
apply business rules
```

[[#Navigation|⬆ Back to Navigation]]

---

# 55. Service Class Example

```csharp
public class StudentService : IStudentService
{
    private readonly InMemoryDataStore _store;

    public StudentService(InMemoryDataStore store)
    {
        _store = store;
    }

    public List<StudentResponseDto> GetAll()
    {
        return _store.Students
            .Select(ToResponseDto)
            .ToList();
    }

    public StudentResponseDto? GetById(int id)
    {
        var student = _store.Students.FirstOrDefault(s => s.Id == id);

        return student is null ? null : ToResponseDto(student);
    }

    private StudentResponseDto ToResponseDto(Student student)
    {
        return new StudentResponseDto
        {
            Id = student.Id,
            FullName = $"{student.FirstName} {student.LastName}"
        };
    }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 56. Interface Example

```csharp
public interface IStudentService
{
    List<StudentResponseDto> GetAll();
    StudentResponseDto? GetById(int id);
    StudentResponseDto Create(StudentCreateDto dto);
}
```

Implementation:

```csharp
public class StudentService : IStudentService
{
    public List<StudentResponseDto> GetAll()
    {
        return new();
    }

    public StudentResponseDto? GetById(int id)
    {
        return null;
    }

    public StudentResponseDto Create(StudentCreateDto dto)
    {
        return new StudentResponseDto();
    }
}
```

Key takeaway:

```text
Interface says what methods exist.
Class provides how those methods work.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 57. Dependency Injection Basics

Register service:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Inject service:

```csharp
private readonly IStudentService _studentService;

public StudentsController(IStudentService studentService)
{
    _studentService = studentService;
}
```

Use service:

```csharp
var students = _studentService.GetAll();
```

Without DI:

```csharp
_studentService = new StudentService();
```

With DI:

```text
ASP.NET creates the service and gives it to the controller.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 58. Service Lifetimes

```csharp
builder.Services.AddTransient<IStudentService, StudentService>();
builder.Services.AddScoped<IStudentService, StudentService>();
builder.Services.AddSingleton<IStudentService, StudentService>();
```

| Lifetime | Meaning |
|---|---|
| Transient | new instance every time requested |
| Scoped | one instance per HTTP request |
| Singleton | one instance for whole app |

Default for Web APIs:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 59. Singleton vs Scoped vs Transient

## Singleton

```text
One instance for the entire app.
```

Good for:

```text
shared in-memory store
configuration/cache
```

Be careful with:

```text
mutable shared data
thread safety
user-specific data
```

## Scoped

```text
One instance per HTTP request.
```

Good for:

```text
normal services
EF Core DbContext
request-specific work
```

## Transient

```text
New instance every time requested.
```

Good for:

```text
small stateless helpers
```

Memory trick:

```text
Transient = always new
Scoped = once per request
Singleton = once per app
```

[[#Navigation|⬆ Back to Navigation]]

---

# 60. DI and Database Mental Model

With in-memory store:

```text
Controller
↓
Service
↓
List<Student>
```

With database later:

```text
Controller
↓
Service
↓
DbContext
↓
PostgreSQL
```

EF Core later:

```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseNpgsql(connectionString));
```

Usually:

```text
DbContext = scoped
Services using DbContext = scoped
```

Do not use Singleton for services that directly depend on DbContext.

[[#Navigation|⬆ Back to Navigation]]

---

# 61. GET All Pattern

```csharp
[HttpGet]
public IActionResult GetAll()
{
    var students = _studentService.GetAll();

    return Ok(students);
}
```

Service:

```csharp
public List<StudentResponseDto> GetAll()
{
    return _students
        .Select(ToResponseDto)
        .ToList();
}
```

Status:

```text
200 OK
```

[[#Navigation|⬆ Back to Navigation]]

---

# 62. GET By Id Pattern

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    var student = _studentService.GetById(id);

    if (student is null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

Status:

```text
200 OK if found
404 Not Found if missing
```

[[#Navigation|⬆ Back to Navigation]]

---

# 63. POST Create Pattern

```csharp
[HttpPost]
public IActionResult Create([FromBody] StudentCreateDto dto)
{
    var student = _studentService.Create(dto);

    return CreatedAtAction(
        nameof(GetById),
        new { id = student.Id },
        student
    );
}
```

Status:

```text
201 Created
```

[[#Navigation|⬆ Back to Navigation]]

---

# 64. PUT Full Update Pattern

```csharp
[HttpPut("{id:int}")]
public IActionResult Update(int id, [FromBody] StudentUpdateDto dto)
{
    var updated = _studentService.Update(id, dto);

    if (updated is null)
    {
        return NotFound();
    }

    return Ok(updated);
}
```

PUT means:

```text
Replace/update the full resource.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 65. PATCH Partial Update Pattern

```csharp
[HttpPatch("{id:int}")]
public IActionResult Patch(int id, [FromBody] StudentPatchDto dto)
{
    var patched = _studentService.Patch(id, dto);

    if (patched is null)
    {
        return NotFound();
    }

    return Ok(patched);
}
```

Patch DTO:

```csharp
public class StudentPatchDto
{
    public string? FirstName { get; set; }
    public int? Age { get; set; }
}
```

Service:

```csharp
if (!string.IsNullOrWhiteSpace(dto.FirstName))
{
    student.FirstName = dto.FirstName.Trim();
}

if (dto.Age.HasValue)
{
    student.Age = dto.Age.Value;
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 66. DELETE Pattern

```csharp
[HttpDelete("{id:int}")]
public IActionResult Delete(int id)
{
    bool deleted = _studentService.Delete(id);

    if (!deleted)
    {
        return NotFound();
    }

    return NoContent();
}
```

Status:

```text
204 No Content if deleted
404 Not Found if missing
```

[[#Navigation|⬆ Back to Navigation]]

---

# 67. Search, Filter, Sort, and Pagination Pattern

Controller:

```csharp
[HttpGet("search")]
public IActionResult Search(
    [FromQuery] string? name,
    [FromQuery] string? gender,
    [FromQuery] int page = 1,
    [FromQuery] int pageSize = 10)
{
    var result = _studentService.Search(name, gender, page, pageSize);

    return Ok(result);
}
```

Service:

```csharp
public List<StudentResponseDto> Search(
    string? name,
    string? gender,
    int page,
    int pageSize)
{
    var query = _students.AsEnumerable();

    if (!string.IsNullOrWhiteSpace(name))
    {
        query = query.Where(s =>
            s.FirstName.Contains(name, StringComparison.OrdinalIgnoreCase) ||
            s.LastName.Contains(name, StringComparison.OrdinalIgnoreCase));
    }

    if (!string.IsNullOrWhiteSpace(gender))
    {
        query = query.Where(s =>
            s.Gender.Equals(gender, StringComparison.OrdinalIgnoreCase));
    }

    return query
        .OrderBy(s => s.LastName)
        .Skip((page - 1) * pageSize)
        .Take(pageSize)
        .Select(ToResponseDto)
        .ToList();
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 68. Stats Endpoint Pattern

Controller:

```csharp
[HttpGet("stats/by-gender")]
public IActionResult GetStatsByGender()
{
    var stats = _studentService.GetStatsByGender();

    return Ok(stats);
}
```

Service:

```csharp
public List<object> GetStatsByGender()
{
    return _students
        .GroupBy(s => s.Gender)
        .Select(g => new
        {
            Gender = g.Key,
            Count = g.Count()
        })
        .Cast<object>()
        .ToList();
}
```

Better with DTO:

```csharp
public class GenderStatsDto
{
    public string Gender { get; set; } = string.Empty;
    public int Count { get; set; }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 69. Nested Resource Pattern

Example:

```http
POST /api/sections/MB02/students
GET /api/sections/MB02/students
GET /api/sections/MB02/students/3
```

Controller route:

```csharp
[ApiController]
[Route("api/sections")]
public class SectionsController : ControllerBase
{
    [HttpPost("{sectionCode}/students")]
    public IActionResult CreateStudent(
        string sectionCode,
        [FromBody] StudentCreateDto dto)
    {
        return Ok();
    }
}
```

Meaning:

```text
Student resource is nested under a section.
sectionCode identifies the parent section.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 70. What Middleware Is

Middleware runs during the request pipeline.

It can:

```text
log requests
handle errors
check authorization
modify request
modify response
short-circuit request
```

Pattern:

```csharp
app.Use(async (context, next) =>
{
    // before endpoint

    await next();

    // after endpoint
});
```

[[#Navigation|⬆ Back to Navigation]]

---

# 71. Built-In Middleware

Common middleware:

```csharp
app.UseHttpsRedirection();
app.UseAuthentication();
app.UseAuthorization();
app.UseCors();
app.UseExceptionHandler();
app.MapControllers();
```

Order usually:

```text
Exception handling
HTTPS redirection
CORS
Authentication
Authorization
MapControllers
```

[[#Navigation|⬆ Back to Navigation]]

---

# 72. Custom Inline Middleware

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine($"{context.Request.Method} {context.Request.Path}");

    await next();

    Console.WriteLine(context.Response.StatusCode);
});
```

Good for quick tests.

[[#Navigation|⬆ Back to Navigation]]

---

# 73. Custom Middleware Class

```csharp
public class RequestLoggingMiddleware
{
    private readonly RequestDelegate _next;

    public RequestLoggingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        Console.WriteLine($"{context.Request.Method} {context.Request.Path}");

        await _next(context);

        Console.WriteLine(context.Response.StatusCode);
    }
}
```

Register:

```csharp
app.UseMiddleware<RequestLoggingMiddleware>();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 74. Middleware Extension Method

```csharp
public static class RequestLoggingMiddlewareExtensions
{
    public static IApplicationBuilder UseRequestLogging(this IApplicationBuilder app)
    {
        return app.UseMiddleware<RequestLoggingMiddleware>();
    }
}
```

Use:

```csharp
app.UseRequestLogging();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 75. Middleware Order Matters

Bad:

```csharp
app.MapControllers();
app.UseAuthorization();
```

Better:

```csharp
app.UseAuthorization();
app.MapControllers();
```

Authentication before authorization:

```csharp
app.UseAuthentication();
app.UseAuthorization();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 76. Middleware vs Controller vs Service

| Task | Best Place |
|---|---|
| Log every request | Middleware |
| Read route ID and return 404 | Controller |
| Search students | Service |
| Validate required field | DTO |
| Store student data | Model/Data |
| Calculate grade stats | Service |

Rule:

```text
Many/all requests = middleware
Specific endpoint HTTP response = controller
Business/data logic = service
```

[[#Navigation|⬆ Back to Navigation]]

---

# 77. Request Body Middleware Preview

Request body is a stream:

```csharp
context.Request.Body
```

To read it:

```csharp
context.Request.EnableBuffering();

using var reader = new StreamReader(
    context.Request.Body,
    Encoding.UTF8,
    leaveOpen: true
);

string body = await reader.ReadToEndAsync();

context.Request.Body.Position = 0;
```

To replace it:

```csharp
byte[] bytes = Encoding.UTF8.GetBytes(modifiedBody);

context.Request.Body = new MemoryStream(bytes);
context.Request.ContentLength = bytes.Length;
context.Request.Body.Position = 0;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 78. In-Memory Data Store

```csharp
public class InMemoryDataStore
{
    public List<Student> Students { get; } = new()
    {
        new Student
        {
            Id = 1,
            FirstName = "Ana",
            LastName = "Reyes"
        }
    };
}
```

Register:

```csharp
builder.Services.AddSingleton<InMemoryDataStore>();
```

Use in service:

```csharp
public class StudentService
{
    private readonly InMemoryDataStore _store;

    public StudentService(InMemoryDataStore store)
    {
        _store = store;
    }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 79. Static Data vs Singleton Store

Static list:

```csharp
private static List<Student> _students = new();
```

Singleton store:

```csharp
builder.Services.AddSingleton<InMemoryDataStore>();
```

Comparison:

| Approach | Meaning |
|---|---|
| static list | belongs to class |
| singleton store | one object managed by DI |

Both:

```text
survive while app runs
disappear when app restarts
are not real database persistence
```

[[#Navigation|⬆ Back to Navigation]]

---

# 80. List, Dictionary, HashSet in Web APIs

List:

```csharp
List<Student> Students = new();
```

Dictionary:

```csharp
Dictionary<int, Student> StudentLookup = new();
```

HashSet:

```csharp
HashSet<string> ValidSectionCodes = new();
```

Use:

```text
List = main data collection
Dictionary = fast key lookup
HashSet = unique allowed values
```

[[#Navigation|⬆ Back to Navigation]]

---

# 81. Keeping Dictionary Lookup in Sync

Create:

```csharp
Students.Add(student);
StudentLookup[student.Id] = student;
```

Delete:

```csharp
Students.Remove(student);
StudentLookup.Remove(student.Id);
```

Update reference object:

```csharp
student.FirstName = dto.FirstName;
```

If replacing object:

```csharp
StudentLookup[id] = updatedStudent;
```

[[#Navigation|⬆ Back to Navigation]]

---

# 82. EF Core Preview

In-memory LINQ:

```csharp
_students.Where(s => s.Age >= 18).ToList();
```

EF Core LINQ later:

```csharp
_context.Students.Where(s => s.Age >= 18).ToList();
```

The syntax looks similar.

Difference:

```text
In-memory LINQ runs on C# objects.
EF Core LINQ translates to SQL and runs on database.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 83. Running the API

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

Build:

```bash
dotnet build
```

Look for:

```text
Now listening on: https://localhost:xxxx
```

[[#Navigation|⬆ Back to Navigation]]

---

# 84. Postman Testing Guide

Steps:

```text
1. Run API.
2. Copy localhost URL.
3. Open Postman.
4. Choose method.
5. Enter URL.
6. For POST/PUT/PATCH, set Body → raw → JSON.
7. Send.
8. Check status code.
9. Check response body.
```

Headers for JSON:

```text
Content-Type: application/json
```

[[#Navigation|⬆ Back to Navigation]]

---

# 85. Sample Request Bodies

POST student:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "age": 20,
  "gender": "Female"
}
```

PUT student:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "age": 21,
  "gender": "Female",
  "isActive": true
}
```

PATCH student:

```json
{
  "age": 21
}
```

POST section:

```json
{
  "code": "MB02",
  "program": "BSIT",
  "yearLevel": 2
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 86. Reading Responses

Check:

```text
Status code
Response body
Headers
Response time
```

POST success:

```text
201 Created
Location header
Created object in body
```

DELETE success:

```text
204 No Content
No response body
```

Validation error:

```text
400 Bad Request
Validation details
```

Not found:

```text
404 Not Found
```

[[#Navigation|⬆ Back to Navigation]]

---

# 87. Common Errors and Fixes

## 404 Not Found

Check:

```text
URL
HTTP method
controller route
method route
port
/api prefix
```

## 400 Bad Request

Check:

```text
JSON syntax
required fields
wrong data type
validation annotations
```

## 415 Unsupported Media Type

Fix in Postman:

```text
Body → raw → JSON
Content-Type: application/json
```

## Service cannot be resolved

Error usually means missing DI registration.

Fix:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

## Controller endpoint not working

Check:

```csharp
builder.Services.AddControllers();
app.MapControllers();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 88. Complete Minimal API Student Example

```csharp
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

List<Student> students = new();

app.MapGet("/api/students", () =>
{
    return Results.Ok(students);
});

app.MapGet("/api/students/{id:int}", (int id) =>
{
    var student = students.FirstOrDefault(s => s.Id == id);

    return student is null
        ? Results.NotFound()
        : Results.Ok(student);
});

app.MapPost("/api/students", (StudentCreateDto dto) =>
{
    var student = new Student
    {
        Id = students.Count == 0 ? 1 : students.Max(s => s.Id) + 1,
        FirstName = dto.FirstName.Trim(),
        LastName = dto.LastName.Trim(),
        Age = dto.Age
    };

    students.Add(student);

    return Results.Created($"/api/students/{student.Id}", student);
});

app.MapDelete("/api/students/{id:int}", (int id) =>
{
    var student = students.FirstOrDefault(s => s.Id == id);

    if (student is null)
    {
        return Results.NotFound();
    }

    students.Remove(student);

    return Results.NoContent();
});

app.Run();

public class Student
{
    public int Id { get; set; }
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public int Age { get; set; }
}

public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public int Age { get; set; }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

# 89. Complete Modular Student API Example

## Model

```csharp
namespace StudentEnrollmentApi.Models;

public class Student
{
    public int Id { get; set; }
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public int Age { get; set; }

    public string FullName => $"{FirstName} {LastName}";
}
```

## DTOs

```csharp
namespace StudentEnrollmentApi.DTOs;

public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public int Age { get; set; }
}
```

```csharp
namespace StudentEnrollmentApi.DTOs;

public class StudentResponseDto
{
    public int Id { get; set; }
    public string FullName { get; set; } = string.Empty;
    public int Age { get; set; }
}
```

## Data Store

```csharp
using StudentEnrollmentApi.Models;

namespace StudentEnrollmentApi.Data;

public class InMemoryDataStore
{
    public List<Student> Students { get; } = new();
}
```

## Interface

```csharp
using StudentEnrollmentApi.DTOs;

namespace StudentEnrollmentApi.Services;

public interface IStudentService
{
    List<StudentResponseDto> GetAll();
    StudentResponseDto? GetById(int id);
    StudentResponseDto Create(StudentCreateDto dto);
    bool Delete(int id);
}
```

## Service

```csharp
using StudentEnrollmentApi.Data;
using StudentEnrollmentApi.DTOs;
using StudentEnrollmentApi.Models;

namespace StudentEnrollmentApi.Services;

public class StudentService : IStudentService
{
    private readonly InMemoryDataStore _store;

    public StudentService(InMemoryDataStore store)
    {
        _store = store;
    }

    public List<StudentResponseDto> GetAll()
    {
        return _store.Students
            .Select(ToResponseDto)
            .ToList();
    }

    public StudentResponseDto? GetById(int id)
    {
        var student = _store.Students.FirstOrDefault(s => s.Id == id);

        return student is null ? null : ToResponseDto(student);
    }

    public StudentResponseDto Create(StudentCreateDto dto)
    {
        var student = new Student
        {
            Id = _store.Students.Count == 0
                ? 1
                : _store.Students.Max(s => s.Id) + 1,
            FirstName = dto.FirstName.Trim(),
            LastName = dto.LastName.Trim(),
            Age = dto.Age
        };

        _store.Students.Add(student);

        return ToResponseDto(student);
    }

    public bool Delete(int id)
    {
        var student = _store.Students.FirstOrDefault(s => s.Id == id);

        if (student is null)
        {
            return false;
        }

        _store.Students.Remove(student);
        return true;
    }

    private static StudentResponseDto ToResponseDto(Student student)
    {
        return new StudentResponseDto
        {
            Id = student.Id,
            FullName = student.FullName,
            Age = student.Age
        };
    }
}
```

## Controller

```csharp
using Microsoft.AspNetCore.Mvc;
using StudentEnrollmentApi.DTOs;
using StudentEnrollmentApi.Services;

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
    public IActionResult GetAll()
    {
        return Ok(_studentService.GetAll());
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        var student = _studentService.GetById(id);

        if (student is null)
        {
            return NotFound();
        }

        return Ok(student);
    }

    [HttpPost]
    public IActionResult Create([FromBody] StudentCreateDto dto)
    {
        var student = _studentService.Create(dto);

        return CreatedAtAction(
            nameof(GetById),
            new { id = student.Id },
            student
        );
    }

    [HttpDelete("{id:int}")]
    public IActionResult Delete(int id)
    {
        bool deleted = _studentService.Delete(id);

        if (!deleted)
        {
            return NotFound();
        }

        return NoContent();
    }
}
```

## Program.cs

```csharp
using StudentEnrollmentApi.Data;
using StudentEnrollmentApi.Services;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

builder.Services.AddSingleton<InMemoryDataStore>();
builder.Services.AddScoped<IStudentService, StudentService>();

var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 90. Endpoint Design Checklist

Good:

```text
GET /api/students
GET /api/students/1
POST /api/students
PUT /api/students/1
PATCH /api/students/1
DELETE /api/students/1
```

Avoid:

```text
GET /api/getStudents
POST /api/createStudent
POST /api/deleteStudent
```

Checklist:

```text
Use plural nouns.
Use correct HTTP verb.
Use route params for specific resources.
Use query params for filters.
Use DTOs for request bodies.
Return correct status codes.
Keep controllers thin.
Put business logic in services.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 91. Beginner Mistakes to Avoid

```text
Putting all logic in Program.cs.
Keeping all endpoints as Minimal APIs when the project becomes large.
Putting business logic in controllers.
Using models directly for all request bodies.
Forgetting AddControllers.
Forgetting MapControllers.
Forgetting service registration.
Returning Ok(null) instead of NotFound().
Using POST for every operation.
Confusing route params and query params.
Not checking null from FirstOrDefault.
Forgetting ToList after LINQ query when a List is needed.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 92. Quick Memorization Tables

## Minimal API vs Controller

| Topic | Minimal API | Controller |
|---|---|---|
| Location | `Program.cs` | `Controllers/` |
| Routing | `app.MapGet` | `[HttpGet]` |
| Response | `Results.Ok()` | `Ok()` |
| Best for | small/simple APIs | organized CRUD APIs |
| Structure | low ceremony | more files/layers |

## CSharp to API

| CSharp | API Use |
|---|---|
| Class | DTO, model, service, controller |
| Property | JSON field |
| Method | endpoint/action/service function |
| Interface | DI contract |
| Constructor | dependency injection |
| List | in-memory data |
| LINQ | query/filter/map |
| Nullable | optional/missing value |
| Namespace | code organization |

## HTTP Verbs

| Verb | Use |
|---|---|
| GET | read |
| POST | create |
| PUT | full update |
| PATCH | partial update |
| DELETE | remove |

## Status Codes

| Status | Use |
|---|---|
| 200 | successful read/update |
| 201 | created |
| 204 | deleted/no body |
| 400 | bad input |
| 404 | not found |
| 409 | conflict/duplicate |
| 500 | server error |

## Layers

| Layer | Job |
|---|---|
| Controller | HTTP |
| DTO | API shape |
| Model | stored data |
| Service | business logic |
| Data | storage |
| Middleware | request pipeline |
| Program.cs | setup |

[[#Navigation|⬆ Back to Navigation]]

---

# 93. Final Review Checklist

```text
[ ] I can explain what a Web API is.
[ ] I can create a Minimal API endpoint.
[ ] I can explain why Minimal APIs can become messy.
[ ] I can convert a Minimal API endpoint into a controller action.
[ ] I understand Program.cs service registration.
[ ] I understand Program.cs middleware pipeline.
[ ] I understand namespaces and using statements.
[ ] I understand models vs DTOs.
[ ] I understand Create, Update, Patch, and Response DTOs.
[ ] I can use route parameters.
[ ] I can use query parameters.
[ ] I can use FromBody.
[ ] I understand IActionResult.
[ ] I can return Ok, NotFound, BadRequest, CreatedAtAction, and NoContent.
[ ] I can create a service interface.
[ ] I can inject a service into a controller.
[ ] I understand Singleton, Scoped, and Transient.
[ ] I can write basic CRUD endpoints.
[ ] I can use LINQ inside services.
[ ] I understand middleware basics.
[ ] I can explain middleware vs controller vs service.
```

Final mental model:

```text
Minimal API shows the simplest endpoint.
Controller organizes endpoints.
DTO defines API input/output.
Model defines internal data.
Service handles business logic.
Interface supports dependency injection.
Program.cs wires the app together.
Middleware surrounds the request.
LINQ handles data searching, filtering, sorting, and mapping.
```

[[#Navigation|⬆ Back to Navigation]]
