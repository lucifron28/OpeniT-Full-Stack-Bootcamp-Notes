# ASP.NET Core Web API Cheat Sheet

## Navigation

### A. Big Picture
1. [[#1. ASP.NET Core Web API Mental Model|ASP.NET Core Web API Mental Model]]
2. [[#2. DRF to ASP.NET Core Translation Map|DRF to ASP.NET Core Translation Map]]
3. [[#3. Request Flow Overview|Request Flow Overview]]
4. [[#4. Common Project Structure|Common Project Structure]]

### B. Program.cs and Startup
5. [[#5. Program.cs Mental Model|Program.cs Mental Model]]
6. [[#6. Service Registration|Service Registration]]
7. [[#7. Request Pipeline|Request Pipeline]]
8. [[#8. Common Program.cs Template|Common Program.cs Template]]

### C. Controllers and Routing
9. [[#9. What Controllers Are|What Controllers Are]]
10. [[#10. ControllerBase and ApiController|ControllerBase and ApiController]]
11. [[#11. Attribute Routing|Attribute Routing]]
12. [[#12. HTTP Method Attributes|HTTP Method Attributes]]
13. [[#13. Route Parameters|Route Parameters]]
14. [[#14. Query Parameters|Query Parameters]]
15. [[#15. Request Body and FromBody|Request Body and FromBody]]

### D. Return Types and HTTP Responses
16. [[#16. IActionResult Explained|IActionResult Explained]]
17. [[#17. ActionResult of T|ActionResult of T]]
18. [[#18. Common Response Helpers|Common Response Helpers]]
19. [[#19. HTTP Status Code Cheat Sheet|HTTP Status Code Cheat Sheet]]
20. [[#20. CreatedAtAction Explained|CreatedAtAction Explained]]

### E. Models, DTOs, and Validation
21. [[#21. Models vs DTOs|Models vs DTOs]]
22. [[#22. DTOs as DRF Serializers|DTOs as DRF Serializers]]
23. [[#23. Create DTO, Update DTO, Patch DTO, Response DTO|Create DTO, Update DTO, Patch DTO, Response DTO]]
24. [[#24. Data Annotations|Data Annotations]]
25. [[#25. Automatic Validation with ApiController|Automatic Validation with ApiController]]
26. [[#26. Manual Mapping Between DTOs and Models|Manual Mapping Between DTOs and Models]]

### F. Services and Clean Layering
27. [[#27. Why Use Services|Why Use Services]]
28. [[#28. Thin Controller Pattern|Thin Controller Pattern]]
29. [[#29. Service Class Example|Service Class Example]]
30. [[#30. Interfaces for Services|Interfaces for Services]]
31. [[#31. Dependency Injection Basics|Dependency Injection Basics]]
32. [[#32. Service Lifetimes|Service Lifetimes]]

### G. CRUD API Patterns
33. [[#33. GET All Pattern|GET All Pattern]]
34. [[#34. GET By Id Pattern|GET By Id Pattern]]
35. [[#35. POST Create Pattern|POST Create Pattern]]
36. [[#36. PUT Full Update Pattern|PUT Full Update Pattern]]
37. [[#37. PATCH Partial Update Pattern|PATCH Partial Update Pattern]]
38. [[#38. DELETE Pattern|DELETE Pattern]]
39. [[#39. Search, Filter, Sort, and Pagination Pattern|Search, Filter, Sort, and Pagination Pattern]]
40. [[#40. Stats Endpoint Pattern|Stats Endpoint Pattern]]

### H. Middleware and Pipeline
41. [[#41. What Middleware Is|What Middleware Is]]
42. [[#42. Built-in Middleware|Built-in Middleware]]
43. [[#43. Custom Inline Middleware|Custom Inline Middleware]]
44. [[#44. Custom Middleware Class|Custom Middleware Class]]
45. [[#45. Middleware Order Matters|Middleware Order Matters]]
46. [[#46. Middleware vs Controller vs Service|Middleware vs Controller vs Service]]

### I. Data Storage for Bootcamp Stage
47. [[#47. In-Memory Data Store|In-Memory Data Store]]
48. [[#48. List, Dictionary, HashSet in Web APIs|List, Dictionary, HashSet in Web APIs]]
49. [[#49. Keeping Dictionary Lookup in Sync|Keeping Dictionary Lookup in Sync]]
50. [[#50. When This Becomes EF Core Later|When This Becomes EF Core Later]]

### J. Testing and Debugging
51. [[#51. Running the API|Running the API]]
52. [[#52. Postman Testing Guide|Postman Testing Guide]]
53. [[#53. Sample Request Bodies|Sample Request Bodies]]
54. [[#54. Reading Responses|Reading Responses]]
55. [[#55. Common Errors and Fixes|Common Errors and Fixes]]

### K. Practical Reference
56. [[#56. Complete Student API Mini Example|Complete Student API Mini Example]]
57. [[#57. Endpoint Design Checklist|Endpoint Design Checklist]]
58. [[#58. Beginner Mistakes to Avoid|Beginner Mistakes to Avoid]]
59. [[#59. Quick Memorization Tables|Quick Memorization Tables]]
60. [[#60. Study Order for Bootcamp|Study Order for Bootcamp]]

---

# A. Big Picture

## 1. ASP.NET Core Web API Mental Model

ASP.NET Core Web API is a framework for building HTTP APIs using C#.

A Web API receives HTTP requests like:

```text
GET /api/students
POST /api/students
PUT /api/students/1
DELETE /api/students/1
```

Then it returns HTTP responses like:

```text
200 OK
201 Created
204 No Content
400 Bad Request
404 Not Found
500 Internal Server Error
```

The main building blocks are:

| ASP.NET Core Concept | Job |
|---|---|
| `Program.cs` | Configures app startup, services, and middleware |
| Middleware | Code that runs before/after controllers |
| Controller | Receives HTTP requests and returns responses |
| Action method | A method inside a controller mapped to an endpoint |
| Model | Internal data/entity shape |
| DTO | Request/response data shape |
| Service | Business logic layer |
| Data store | Where records are stored; in-memory now, database later |

Simple flow:

```text
HTTP Request
↓
Middleware
↓
Routing
↓
Controller Action
↓
Service
↓
Data Store
↓
Response
```

[[#Navigation|Back to Navigation]]

---

## 2. DRF to ASP.NET Core Translation Map

If you know Django REST Framework, this map helps:

| Django REST Framework | ASP.NET Core Web API |
|---|---|
| `urls.py` | Route attributes like `[Route("api/students")]` |
| `APIView` / `ViewSet` | Controller |
| View method like `get`, `post` | Controller action method |
| `Serializer` | DTO plus DataAnnotations |
| Django Model | Model / Entity |
| QuerySet | LINQ / EF Core query |
| `request.data` | `[FromBody] SomeDto dto` |
| `request.query_params` | `[FromQuery] string? name` |
| URL path parameter | Route parameter like `{id:int}` |
| `Response(data, status=200)` | `Ok(data)` |
| `Response(status=404)` | `NotFound()` |
| Middleware | Middleware |
| `settings.py` | `appsettings.json` plus `Program.cs` |
| Django ORM | EF Core later |

Important difference:

```text
DRF Serializer does many jobs:
- validation
- input shape
- output shape
- model conversion

ASP.NET usually separates these:
- DTOs define input/output shape
- DataAnnotations define validation
- Services/controllers map DTOs to Models
```

[[#Navigation|Back to Navigation]]

---

## 3. Request Flow Overview

A request does not immediately go to a controller.

It passes through the ASP.NET Core request pipeline.

```text
Postman / Browser / Frontend
↓
Kestrel Web Server
↓
Middleware 1
↓
Middleware 2
↓
Routing
↓
Controller Action
↓
Service Logic
↓
Data Store
↓
Controller Response
↓
Middleware after-response logic
↓
Client receives JSON + status code
```

Example:

```text
POST /api/students
↓
Request logging middleware logs request
↓
HTTPS redirection middleware checks HTTPS
↓
Routing finds StudentsController.Create
↓
ASP.NET reads JSON body into StudentCreateDto
↓
Validation checks DTO annotations
↓
Controller calls StudentService.Create
↓
Service adds student to in-memory list
↓
Controller returns 201 Created
↓
Logging middleware logs status code
```

[[#Navigation|Back to Navigation]]

---

## 4. Common Project Structure

A clean beginner Web API structure:

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

Each folder has one main responsibility:

| Folder | Responsibility |
|---|---|
| `Controllers` | HTTP endpoints |
| `Models` | Internal data objects |
| `DTOs` | API input/output shapes |
| `Services` | Business logic |
| `Data` | In-memory lists or database context |
| `Middleware` | Request pipeline logic |

Rule:

```text
Controllers should not contain all business logic.
Controllers should call services.
Services should handle data operations and LINQ.
```

[[#Navigation|Back to Navigation]]

---

# B. Program.cs and Startup

## 5. Program.cs Mental Model

`Program.cs` is the startup file.

It has two major parts:

```text
1. Register services
2. Configure request pipeline
```

Service registration:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddScoped<IStudentService, StudentService>();
```

This answers:

```text
What classes/features should my app be able to use?
```

Request pipeline:

```csharp
var app = builder.Build();

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

This answers:

```text
What should happen to every HTTP request?
```

Memory trick:

```text
builder.Services = register dependencies/tools
app.Use... = request pipeline steps
app.MapControllers = connect routes to controllers
app.Run = start the server
```

[[#Navigation|Back to Navigation]]

---

## 6. Service Registration

ASP.NET Core has a built-in dependency injection container.

When you write:

```csharp
builder.Services.AddControllers();
```

You are telling ASP.NET:

```text
This app uses controller-based APIs.
Find controller classes and make them available for routing.
```

When you write:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

You are telling ASP.NET:

```text
When a class asks for IStudentService,
give it a StudentService object.
```

Example controller constructor:

```csharp
private readonly IStudentService _studentService;

public StudentsController(IStudentService studentService)
{
    _studentService = studentService;
}
```

You do not manually write:

```csharp
_studentService = new StudentService();
```

ASP.NET creates it for you.

[[#Navigation|Back to Navigation]]

---

## 7. Request Pipeline

The request pipeline is the ordered list of middleware that processes requests.

Example:

```csharp
var app = builder.Build();

app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Requests pass through the pipeline in order.

```text
UseHttpsRedirection
↓
UseAuthorization
↓
MapControllers
```

Important:

```text
Order matters.
```

For example, authentication should normally happen before authorization.

A custom logging middleware should usually be placed before `MapControllers()` so it can log controller requests.

[[#Navigation|Back to Navigation]]

---

## 8. Common Program.cs Template

A beginner-friendly `Program.cs`:

```csharp
using StudentEnrollmentApi.Middleware;
using StudentEnrollmentApi.Services;

var builder = WebApplication.CreateBuilder(args);

// Registers controller support.
// Without this, ASP.NET will not know how to use controller classes.
builder.Services.AddControllers();

// Registers services for dependency injection.
// This means controllers can request IStudentService in their constructors.
builder.Services.AddScoped<IStudentService, StudentService>();

// Optional: helps API documentation tools discover endpoints.
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Enables Swagger UI in development so you can test endpoints in the browser.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

// Redirects HTTP requests to HTTPS.
app.UseHttpsRedirection();

// Custom middleware example.
// Logs request method/path and response status code.
app.UseMiddleware<RequestLoggingMiddleware>();

// Authorization middleware.
// Later, this matters when JWT/auth is added.
app.UseAuthorization();

// Maps controller routes like /api/students.
app.MapControllers();

// Starts the application.
app.Run();
```

If Swagger package is missing, create the project with:

```text
dotnet new webapi -n StudentEnrollmentApi
```

Modern templates usually include Swagger support.

[[#Navigation|Back to Navigation]]

---

# C. Controllers and Routing

## 9. What Controllers Are

A controller is like a DRF `APIView` or `ViewSet`.

It receives HTTP requests and returns HTTP responses.

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

This controller handles:

```text
GET /api/students
```

Why?

```text
StudentsController → students
[Route("api/[controller]")] → /api/students
[HttpGet] → GET /api/students
```

Controller responsibilities:

```text
Read route/query/body values
Call service methods
Return HTTP response codes
Avoid putting too much business logic inside
```

[[#Navigation|Back to Navigation]]

---

## 10. ControllerBase and ApiController

A Web API controller usually inherits from `ControllerBase`:

```csharp
public class StudentsController : ControllerBase
{
}
```

`ControllerBase` provides helper methods:

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

`[ApiController]` enables Web API behavior:

```csharp
[ApiController]
public class StudentsController : ControllerBase
{
}
```

Important features of `[ApiController]`:

```text
Automatic model validation
Better parameter binding behavior
Attribute routing requirement
Automatic 400 Bad Request for invalid DTOs
```

Example:

```csharp
public class StudentCreateDto
{
    [Required]
    public string FirstName { get; set; } = string.Empty;
}
```

If the client sends missing/invalid `FirstName`, `[ApiController]` can automatically return:

```text
400 Bad Request
```

before your action method runs.

[[#Navigation|Back to Navigation]]

---

## 11. Attribute Routing

Routing connects URLs to controller methods.

Controller route:

```csharp
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
}
```

`[controller]` is replaced by the controller name without `Controller`.

```text
StudentsController → students
CoursesController → courses
EnrollmentsController → enrollments
```

Action route:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
}
```

Full route:

```text
GET /api/students/1
```

Named sub-route:

```csharp
[HttpGet("search")]
public IActionResult Search()
{
}
```

Full route:

```text
GET /api/students/search
```

[[#Navigation|Back to Navigation]]

---

## 12. HTTP Method Attributes

Each action method usually has an HTTP method attribute.

| Attribute | HTTP Verb | Common Use |
|---|---|---|
| `[HttpGet]` | GET | read data |
| `[HttpPost]` | POST | create new data |
| `[HttpPut]` | PUT | full update |
| `[HttpPatch]` | PATCH | partial update |
| `[HttpDelete]` | DELETE | remove data |

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
    return CreatedAtAction(...);
}
```

```csharp
[HttpDelete("{id:int}")]
public IActionResult Delete(int id)
{
    return NoContent();
}
```

[[#Navigation|Back to Navigation]]

---

## 13. Route Parameters

Route parameters are part of the URL path.

```text
GET /api/students/5
```

Controller action:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    return Ok(id);
}
```

`{id:int}` means:

```text
There is a route parameter named id.
It must be an integer.
```

So this matches:

```text
/api/students/5
```

This does not match:

```text
/api/students/abc
```

because `abc` is not an integer.

Multiple route parameters:

```csharp
[HttpGet("{studentId:int}/courses/{courseId:int}")]
public IActionResult GetStudentCourse(int studentId, int courseId)
{
    return Ok();
}
```

Route:

```text
GET /api/students/1/courses/2
```

[[#Navigation|Back to Navigation]]

---

## 14. Query Parameters

Query parameters come after `?`.

```text
GET /api/students/search?department=CS&activeOnly=true&name=ana
```

Controller action:

```csharp
[HttpGet("search")]
public IActionResult Search(
    [FromQuery] string? department,
    [FromQuery] bool? activeOnly,
    [FromQuery] string? name)
{
    return Ok();
}
```

Use query parameters for:

```text
filtering
searching
sorting
pagination
optional modifiers
```

Examples:

```text
/api/students?department=CS
/api/students?activeOnly=true
/api/students?sortBy=name
/api/students?page=1&pageSize=10
```

Rule:

```text
Route params identify a specific resource.
Query params modify how you retrieve a collection.
```

Examples:

```text
/api/students/5 → specific student
/api/students?department=CS → filtered list
```

[[#Navigation|Back to Navigation]]

---

## 15. Request Body and FromBody

For POST, PUT, and PATCH, data usually comes from the JSON request body.

Example request:

```http
POST /api/students
Content-Type: application/json
```

Body:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "department": "CS",
  "yearLevel": 2
}
```

Controller action:

```csharp
[HttpPost]
public IActionResult Create([FromBody] StudentCreateDto dto)
{
    return Ok(dto);
}
```

`[FromBody]` means:

```text
Read the JSON body.
Convert it into a StudentCreateDto object.
```

DRF comparison:

```text
DRF request.data
≈
ASP.NET [FromBody] dto
```

Usually:

| HTTP Verb | Has Body? |
|---|---|
| GET | usually no |
| POST | yes |
| PUT | yes |
| PATCH | yes |
| DELETE | usually no |

[[#Navigation|Back to Navigation]]

---

# D. Return Types and HTTP Responses

## 16. IActionResult Explained

`IActionResult` is an interface used as a method return type.

```csharp
public IActionResult GetById(int id)
{
    var student = _studentService.GetById(id);

    if (student == null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

Why use `IActionResult`?

Because the method can return different HTTP result types:

```csharp
return Ok(student);    // 200
return NotFound();     // 404
return BadRequest();   // 400
return NoContent();    // 204
```

All of those fit under `IActionResult`.

Breakdown:

```csharp
public IActionResult GetById(int id)
```

```text
public = access modifier
IActionResult = return type
GetById = method name
int id = parameter
```

`IActionResult` is not part of the function name.

[[#Navigation|Back to Navigation]]

---

## 17. ActionResult of T

You may also see:

```csharp
public ActionResult<StudentResponseDto> GetById(int id)
{
    var student = _studentService.GetById(id);

    if (student == null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

`ActionResult<StudentResponseDto>` means:

```text
This action usually returns a StudentResponseDto,
but it can also return HTTP errors like NotFound.
```

Common beginner choice:

```csharp
IActionResult
```

More explicit/documentation-friendly choice:

```csharp
ActionResult<StudentResponseDto>
```

For bootcamp, `IActionResult` is okay and easier to understand.

[[#Navigation|Back to Navigation]]

---

## 18. Common Response Helpers

ControllerBase gives response helper methods.

```csharp
return Ok(data);
```

Returns:

```text
200 OK
```

```csharp
return CreatedAtAction(nameof(GetById), new { id = student.Id }, student);
```

Returns:

```text
201 Created
Location header pointing to the new resource
```

```csharp
return NoContent();
```

Returns:

```text
204 No Content
```

```csharp
return NotFound();
```

Returns:

```text
404 Not Found
```

```csharp
return BadRequest("Invalid department.");
```

Returns:

```text
400 Bad Request
```

```csharp
return Conflict("Course code already exists.");
```

Returns:

```text
409 Conflict
```

[[#Navigation|Back to Navigation]]

---

## 19. HTTP Status Code Cheat Sheet

| Status | Meaning | Common Use |
|---|---|---|
| `200 OK` | request succeeded | GET, PUT, PATCH |
| `201 Created` | new resource created | POST |
| `204 No Content` | success, no body | DELETE |
| `400 Bad Request` | invalid request | validation or bad input |
| `401 Unauthorized` | not logged in / missing token | auth later |
| `403 Forbidden` | logged in but not allowed | permissions later |
| `404 Not Found` | resource does not exist | missing ID |
| `405 Method Not Allowed` | wrong HTTP method | route exists but verb wrong |
| `409 Conflict` | duplicate or state conflict | duplicate code/email |
| `422 Unprocessable Entity` | semantically invalid data | optional advanced validation |
| `500 Internal Server Error` | server crashed | unhandled exception |

Beginner rules:

```text
GET success → 200
POST success → 201
PUT/PATCH success → 200
DELETE success → 204
Missing record → 404
Invalid input → 400
Duplicate unique value → 409
```

[[#Navigation|Back to Navigation]]

---

## 20. CreatedAtAction Explained

`CreatedAtAction` is commonly used after POST.

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
Tell the client where to find the newly created student.
Return the created student in the response body.
```

If `GetById` maps to:

```text
GET /api/students/{id}
```

Then after creating student ID 7, ASP.NET can generate:

```text
Location: /api/students/7
```

Why not just `Ok(student)`?

Because POST creation should ideally return:

```text
201 Created
```

not just:

```text
200 OK
```

[[#Navigation|Back to Navigation]]

---

# E. Models, DTOs, and Validation

## 21. Models vs DTOs

A model is your internal data shape.

```csharp
public class Student
{
    public int Id { get; set; }
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public string Department { get; set; } = string.Empty;
    public int YearLevel { get; set; }
    public DateTime CreatedAt { get; set; }
}
```

A DTO is your API input/output shape.

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public string Department { get; set; } = string.Empty;
    public int YearLevel { get; set; }
}
```

Why separate them?

The model may contain fields that the client should not control:

```text
Id
CreatedAt
InternalStatus
PasswordHash
Audit fields
```

For example, the client should not send:

```json
{
  "id": 999,
  "createdAt": "2020-01-01"
}
```

The server should generate those.

Rule:

```text
Model = internal/database entity
DTO = what the API accepts or returns
```

[[#Navigation|Back to Navigation]]

---

## 22. DTOs as DRF Serializers

In DRF, serializers define input/output and validation.

In ASP.NET, DTOs plus DataAnnotations do a similar job.

DRF serializer idea:

```python
class StudentSerializer(serializers.Serializer):
    first_name = serializers.CharField(max_length=100)
    year_level = serializers.IntegerField(min_value=1, max_value=4)
```

ASP.NET DTO idea:

```csharp
public class StudentCreateDto
{
    [Required]
    [StringLength(100)]
    public string FirstName { get; set; } = string.Empty;

    [Range(1, 4)]
    public int YearLevel { get; set; }
}
```

Mental model:

```text
DRF Serializer
≈
ASP.NET DTO + DataAnnotations
```

But DTOs do not automatically save to a database. You manually map them to models or use tools later like AutoMapper.

[[#Navigation|Back to Navigation]]

---

## 23. Create DTO, Update DTO, Patch DTO, Response DTO

Different operations need different data shapes.

### Create DTO

Used for POST.

```csharp
public class StudentCreateDto
{
    [Required]
    public string FirstName { get; set; } = string.Empty;

    [Required]
    public string LastName { get; set; } = string.Empty;

    [Required]
    public string Department { get; set; } = string.Empty;

    [Range(1, 4)]
    public int YearLevel { get; set; }
}
```

No `Id` because the server generates it.

### Update DTO

Used for PUT full update.

```csharp
public class StudentUpdateDto
{
    [Required]
    public string FirstName { get; set; } = string.Empty;

    [Required]
    public string LastName { get; set; } = string.Empty;

    [Required]
    public string Department { get; set; } = string.Empty;

    [Range(1, 4)]
    public int YearLevel { get; set; }

    public bool IsActive { get; set; }
}
```

PUT expects the full object data.

### Patch DTO

Used for PATCH partial update.

```csharp
public class StudentPatchDto
{
    public string? FirstName { get; set; }
    public string? LastName { get; set; }
    public string? Department { get; set; }
    public int? YearLevel { get; set; }
    public bool? IsActive { get; set; }
}
```

Notice the nullable `?`.

Why?

```text
In PATCH, a missing field means "do not change this field."
```

### Response DTO

Used for what the API returns.

```csharp
public class StudentResponseDto
{
    public int Id { get; set; }
    public string FullName { get; set; } = string.Empty;
    public string Department { get; set; } = string.Empty;
    public int YearLevel { get; set; }
    public bool IsActive { get; set; }
}
```

Response DTOs can combine or hide fields.

[[#Navigation|Back to Navigation]]

---

## 24. Data Annotations

Data Annotations are validation attributes.

Import:

```csharp
using System.ComponentModel.DataAnnotations;
```

Common annotations:

```csharp
[Required]
[StringLength(100)]
[Range(1, 4)]
[EmailAddress]
[Url]
[RegularExpression("pattern")]
[MinLength(2)]
[MaxLength(50)]
```

Example:

```csharp
public class StudentCreateDto
{
    [Required(ErrorMessage = "First name is required.")]
    [StringLength(100, MinimumLength = 2)]
    public string FirstName { get; set; } = string.Empty;

    [Required]
    [StringLength(100)]
    public string LastName { get; set; } = string.Empty;

    [Range(1, 4, ErrorMessage = "Year level must be from 1 to 4.")]
    public int YearLevel { get; set; }
}
```

Meaning:

```text
FirstName must exist.
FirstName must be 2 to 100 characters.
YearLevel must be between 1 and 4.
```

[[#Navigation|Back to Navigation]]

---

## 25. Automatic Validation with ApiController

With `[ApiController]`, invalid DTOs can automatically return:

```text
400 Bad Request
```

Example:

```csharp
[ApiController]
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
    [HttpPost]
    public IActionResult Create([FromBody] StudentCreateDto dto)
    {
        // If dto is invalid, this method may not even run.
        return Ok();
    }
}
```

If request body is:

```json
{
  "firstName": "",
  "yearLevel": 10
}
```

ASP.NET can return validation errors automatically.

Without `[ApiController]`, you often need:

```csharp
if (!ModelState.IsValid)
{
    return BadRequest(ModelState);
}
```

With `[ApiController]`, this is usually automatic.

[[#Navigation|Back to Navigation]]

---

## 26. Manual Mapping Between DTOs and Models

Mapping means converting one object shape to another.

Create DTO to model:

```csharp
var student = new Student
{
    Id = nextId,
    FirstName = dto.FirstName.Trim(),
    LastName = dto.LastName.Trim(),
    Department = dto.Department.Trim().ToUpper(),
    YearLevel = dto.YearLevel,
    IsActive = true,
    CreatedAt = DateTime.UtcNow
};
```

Model to response DTO:

```csharp
var response = new StudentResponseDto
{
    Id = student.Id,
    FullName = $"{student.FirstName} {student.LastName}",
    Department = student.Department,
    YearLevel = student.YearLevel,
    IsActive = student.IsActive
};
```

Why map manually?

```text
You control exactly what enters your model.
You control exactly what leaves your API.
You can normalize/clean data.
You avoid exposing internal fields.
```

Later, libraries like AutoMapper can reduce repetitive mapping, but manual mapping is better while learning.

[[#Navigation|Back to Navigation]]

---

# F. Services and Clean Layering

## 27. Why Use Services

A service contains business logic.

Controller should handle HTTP.

Service should handle operations like:

```text
find student
create student
update student
delete student
search/filter/sort
calculate statistics
check duplicate records
```

Bad controller:

```csharp
[HttpPost]
public IActionResult Create(StudentCreateDto dto)
{
    // validation, ID generation, duplicate checking,
    // list adding, mapping, and response all mixed here
}
```

Better:

```csharp
[HttpPost]
public IActionResult Create(StudentCreateDto dto)
{
    var student = _studentService.Create(dto);

    return CreatedAtAction(nameof(GetById), new { id = student.Id }, student);
}
```

Controller stays focused on HTTP response.

[[#Navigation|Back to Navigation]]

---

## 28. Thin Controller Pattern

Thin controller means the controller is small and delegates logic to services.

Example:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    var student = _studentService.GetById(id);

    if (student == null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

Controller responsibilities here:

```text
Accept id from route
Call service
Return 404 if null
Return 200 if found
```

Service responsibility:

```text
Actually search for the student
```

This is clean layering.

[[#Navigation|Back to Navigation]]

---

## 29. Service Class Example

```csharp
public class StudentService
{
    private readonly List<Student> _students;

    public StudentService()
    {
        _students = InMemoryDataStore.Students;
    }

    public List<StudentResponseDto> GetAll()
    {
        return _students
            .OrderBy(s => s.LastName)
            .Select(s => ToResponseDto(s))
            .ToList();
    }

    public StudentResponseDto? GetById(int id)
    {
        var student = _students.FirstOrDefault(s => s.Id == id);

        if (student == null)
        {
            return null;
        }

        return ToResponseDto(student);
    }

    private StudentResponseDto ToResponseDto(Student student)
    {
        return new StudentResponseDto
        {
            Id = student.Id,
            FullName = $"{student.FirstName} {student.LastName}",
            Department = student.Department,
            YearLevel = student.YearLevel,
            IsActive = student.IsActive
        };
    }
}
```

LINQ explanation:

```text
OrderBy sorts students by last name.
Select converts each Student model into a StudentResponseDto.
ToList executes the query and returns a List.
FirstOrDefault finds one item or returns null.
```

[[#Navigation|Back to Navigation]]

---

## 30. Interfaces for Services

An interface defines what a service must provide.

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
        return new List<StudentResponseDto>();
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

This means:

```text
StudentService promises to implement IStudentService.
```

Register in Program.cs:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Use in controller:

```csharp
private readonly IStudentService _studentService;

public StudentsController(IStudentService studentService)
{
    _studentService = studentService;
}
```

[[#Navigation|Back to Navigation]]

---

## 31. Dependency Injection Basics

Dependency Injection means ASP.NET gives classes their dependencies instead of you manually creating them.

Instead of:

```csharp
private StudentService _studentService = new StudentService();
```

Use:

```csharp
private readonly IStudentService _studentService;

public StudentsController(IStudentService studentService)
{
    _studentService = studentService;
}
```

ASP.NET sees the constructor and provides the service.

This works because you registered it:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Why this is useful:

```text
Cleaner code
Easier testing
Less manual object creation
Better separation of concerns
```

[[#Navigation|Back to Navigation]]

---

## 32. Service Lifetimes

When registering services, you choose a lifetime.

```csharp
builder.Services.AddTransient<IStudentService, StudentService>();
builder.Services.AddScoped<IStudentService, StudentService>();
builder.Services.AddSingleton<IStudentService, StudentService>();
```

| Lifetime | Meaning | Use |
|---|---|---|
| Transient | new instance every time requested | lightweight stateless service |
| Scoped | one instance per HTTP request | common for web apps and EF Core |
| Singleton | one instance for entire app lifetime | shared config/cache, careful with state |

For most Web API services:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Use `Scoped` as your default for services in ASP.NET Core.

[[#Navigation|Back to Navigation]]

---

# G. CRUD API Patterns

## 33. GET All Pattern

Endpoint:

```text
GET /api/students
```

Controller:

```csharp
[HttpGet]
public IActionResult GetAll()
{
    var students = _studentService.GetAll();

    return Ok(students);
}
```

Meaning:

```text
Call service to get all students.
Return 200 OK with JSON array.
```

Service:

```csharp
public List<StudentResponseDto> GetAll()
{
    return _students
        .OrderBy(s => s.LastName)
        .Select(s => ToResponseDto(s))
        .ToList();
}
```

[[#Navigation|Back to Navigation]]

---

## 34. GET By Id Pattern

Endpoint:

```text
GET /api/students/1
```

Controller:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    var student = _studentService.GetById(id);

    if (student == null)
    {
        return NotFound();
    }

    return Ok(student);
}
```

Meaning:

```text
If service returns null, record does not exist.
Return 404 Not Found.
Otherwise return 200 OK.
```

Service:

```csharp
public StudentResponseDto? GetById(int id)
{
    var student = _students.FirstOrDefault(s => s.Id == id);

    return student == null ? null : ToResponseDto(student);
}
```

[[#Navigation|Back to Navigation]]

---

## 35. POST Create Pattern

Endpoint:

```text
POST /api/students
```

Request body:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "department": "CS",
  "yearLevel": 2
}
```

Controller:

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

Service:

```csharp
public StudentResponseDto Create(StudentCreateDto dto)
{
    var student = new Student
    {
        Id = _students.Count == 0 ? 1 : _students.Max(s => s.Id) + 1,
        FirstName = dto.FirstName.Trim(),
        LastName = dto.LastName.Trim(),
        Department = dto.Department.Trim().ToUpper(),
        YearLevel = dto.YearLevel,
        IsActive = true,
        CreatedAt = DateTime.UtcNow
    };

    _students.Add(student);

    return ToResponseDto(student);
}
```

POST success should return:

```text
201 Created
```

[[#Navigation|Back to Navigation]]

---

## 36. PUT Full Update Pattern

PUT means full replacement/update.

Endpoint:

```text
PUT /api/students/1
```

Body should include all update fields:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "department": "IT",
  "yearLevel": 3,
  "isActive": true
}
```

Controller:

```csharp
[HttpPut("{id:int}")]
public IActionResult Update(int id, [FromBody] StudentUpdateDto dto)
{
    var updated = _studentService.Update(id, dto);

    if (updated == null)
    {
        return NotFound();
    }

    return Ok(updated);
}
```

Service:

```csharp
public StudentResponseDto? Update(int id, StudentUpdateDto dto)
{
    var student = _students.FirstOrDefault(s => s.Id == id);

    if (student == null)
    {
        return null;
    }

    student.FirstName = dto.FirstName.Trim();
    student.LastName = dto.LastName.Trim();
    student.Department = dto.Department.Trim().ToUpper();
    student.YearLevel = dto.YearLevel;
    student.IsActive = dto.IsActive;

    return ToResponseDto(student);
}
```

[[#Navigation|Back to Navigation]]

---

## 37. PATCH Partial Update Pattern

PATCH means update only provided fields.

Endpoint:

```text
PATCH /api/students/1
```

Body:

```json
{
  "yearLevel": 4
}
```

Patch DTO uses nullable properties:

```csharp
public class StudentPatchDto
{
    public string? FirstName { get; set; }
    public string? LastName { get; set; }
    public string? Department { get; set; }
    public int? YearLevel { get; set; }
    public bool? IsActive { get; set; }
}
```

Service:

```csharp
public StudentResponseDto? Patch(int id, StudentPatchDto dto)
{
    var student = _students.FirstOrDefault(s => s.Id == id);

    if (student == null)
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

    if (!string.IsNullOrWhiteSpace(dto.Department))
    {
        student.Department = dto.Department.Trim().ToUpper();
    }

    if (dto.YearLevel.HasValue)
    {
        student.YearLevel = dto.YearLevel.Value;
    }

    if (dto.IsActive.HasValue)
    {
        student.IsActive = dto.IsActive.Value;
    }

    return ToResponseDto(student);
}
```

Important:

```text
null means "not provided, do not change."
```

[[#Navigation|Back to Navigation]]

---

## 38. DELETE Pattern

Endpoint:

```text
DELETE /api/students/1
```

Controller:

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

Service:

```csharp
public bool Delete(int id)
{
    var student = _students.FirstOrDefault(s => s.Id == id);

    if (student == null)
    {
        return false;
    }

    _students.Remove(student);
    return true;
}
```

Success response:

```text
204 No Content
```

Why no body?

```text
The resource is deleted.
There is nothing important to return.
```

[[#Navigation|Back to Navigation]]

---

## 39. Search, Filter, Sort, and Pagination Pattern

Endpoint:

```text
GET /api/students/search?department=CS&activeOnly=true&name=ana&page=1&pageSize=5
```

Controller:

```csharp
[HttpGet("search")]
public IActionResult Search(
    [FromQuery] string? department,
    [FromQuery] bool? activeOnly,
    [FromQuery] string? name,
    [FromQuery] int page = 1,
    [FromQuery] int pageSize = 10)
{
    var result = _studentService.Search(department, activeOnly, name, page, pageSize);

    return Ok(result);
}
```

Service:

```csharp
public List<StudentResponseDto> Search(
    string? department,
    bool? activeOnly,
    string? name,
    int page,
    int pageSize)
{
    var query = _students.AsEnumerable();

    if (!string.IsNullOrWhiteSpace(department))
    {
        query = query.Where(s =>
            s.Department.Equals(department, StringComparison.OrdinalIgnoreCase));
    }

    if (activeOnly == true)
    {
        query = query.Where(s => s.IsActive);
    }

    if (!string.IsNullOrWhiteSpace(name))
    {
        query = query.Where(s =>
            s.FirstName.Contains(name, StringComparison.OrdinalIgnoreCase) ||
            s.LastName.Contains(name, StringComparison.OrdinalIgnoreCase));
    }

    return query
        .OrderBy(s => s.LastName)
        .Skip((page - 1) * pageSize)
        .Take(pageSize)
        .Select(s => ToResponseDto(s))
        .ToList();
}
```

LINQ meaning:

```text
Where filters.
OrderBy sorts.
Skip and Take paginate.
Select maps model to response DTO.
ToList returns the final list.
```

[[#Navigation|Back to Navigation]]

---

## 40. Stats Endpoint Pattern

Stats endpoints often use `GroupBy`.

Endpoint:

```text
GET /api/students/stats/departments
```

Service:

```csharp
public List<DepartmentStatsDto> GetStatsByDepartment()
{
    return _students
        .GroupBy(s => s.Department)
        .Select(g => new DepartmentStatsDto
        {
            Department = g.Key,
            Count = g.Count(),
            ActiveCount = g.Count(s => s.IsActive)
        })
        .ToList();
}
```

Stats DTO:

```csharp
public class DepartmentStatsDto
{
    public string Department { get; set; } = string.Empty;
    public int Count { get; set; }
    public int ActiveCount { get; set; }
}
```

`g.Key` means the group name, such as `"CS"` or `"IT"`.

[[#Navigation|Back to Navigation]]

---

# H. Middleware and Pipeline

## 41. What Middleware Is

Middleware is code that runs during the request/response pipeline.

It can run:

```text
before the controller
after the controller
or stop the request before it reaches the controller
```

Examples of middleware jobs:

```text
request logging
error handling
authentication
authorization
CORS
HTTPS redirection
static files
rate limiting
```

Middleware mental model:

```text
Request enters
↓
Middleware does something before
↓
Calls next middleware/controller
↓
Response comes back
↓
Middleware does something after
```

[[#Navigation|Back to Navigation]]

---

## 42. Built-in Middleware

Common built-in middleware:

```csharp
app.UseHttpsRedirection();
app.UseAuthentication();
app.UseAuthorization();
app.UseCors();
app.MapControllers();
```

Meaning:

| Middleware | Purpose |
|---|---|
| `UseHttpsRedirection` | redirects HTTP to HTTPS |
| `UseAuthentication` | identifies who the user is |
| `UseAuthorization` | checks what the user can access |
| `UseCors` | allows frontend apps from other origins |
| `MapControllers` | maps routes to controller actions |

`MapControllers()` is technically endpoint mapping, but it is part of configuring how requests reach controllers.

[[#Navigation|Back to Navigation]]

---

## 43. Custom Inline Middleware

Inline middleware goes directly in `Program.cs`.

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");

    await next();

    Console.WriteLine($"Response: {context.Response.StatusCode}");
});
```

Explanation:

```text
context contains the HTTP request and response.
next represents the next middleware in the pipeline.
Code before await next runs before the controller.
Code after await next runs after the controller.
```

If you do not call:

```csharp
await next();
```

the request stops there and never reaches the controller.

[[#Navigation|Back to Navigation]]

---

## 44. Custom Middleware Class

Middleware class:

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
        var start = DateTime.UtcNow;

        Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");

        await _next(context);

        var elapsed = DateTime.UtcNow - start;

        Console.WriteLine(
            $"Response: {context.Response.StatusCode} in {elapsed.TotalMilliseconds:F0}ms");
    }
}
```

Register in `Program.cs`:

```csharp
app.UseMiddleware<RequestLoggingMiddleware>();
```

Key parts:

```text
RequestDelegate _next = the next step in the pipeline
HttpContext = request and response information
await _next(context) = continue to next middleware/controller
```

[[#Navigation|Back to Navigation]]

---

## 45. Middleware Order Matters

Example order:

```csharp
app.UseHttpsRedirection();

app.UseMiddleware<RequestLoggingMiddleware>();

app.UseAuthentication();

app.UseAuthorization();

app.MapControllers();
```

Why order matters:

```text
HTTPS redirection should happen early.
Authentication should run before authorization.
Controllers should be mapped after middleware setup.
Logging can wrap around controller execution.
```

Bad order example:

```csharp
app.MapControllers();

app.UseAuthorization();
```

This can be wrong because requests may reach controllers before authorization is applied properly.

Beginner default order:

```text
Exception handling/logging
HTTPS redirection
CORS
Authentication
Authorization
MapControllers
```

[[#Navigation|Back to Navigation]]

---

## 46. Middleware vs Controller vs Service

| Layer | Job |
|---|---|
| Middleware | Cross-cutting request pipeline logic |
| Controller | HTTP endpoint handling |
| Service | Business logic |
| Model | Internal data |
| DTO | API input/output shape |

Examples:

| Task | Best Place |
|---|---|
| Log every request | Middleware |
| Return 404 for missing student | Controller |
| Search students by name | Service |
| Validate required input fields | DTO DataAnnotations |
| Store student properties | Model |
| Calculate average grade | Service |

Rule:

```text
If it applies to all/many requests, middleware.
If it is about HTTP response, controller.
If it is about business/data logic, service.
```

[[#Navigation|Back to Navigation]]

---

# I. Data Storage for Bootcamp Stage

## 47. In-Memory Data Store

Before database/EF Core, bootcamps often use in-memory collections.

```csharp
public static class InMemoryDataStore
{
    public static List<Student> Students { get; } = new()
    {
        new Student
        {
            Id = 1,
            FirstName = "Ana",
            LastName = "Reyes",
            Department = "CS",
            YearLevel = 2,
            IsActive = true,
            CreatedAt = DateTime.UtcNow
        }
    };

    public static HashSet<string> ValidDepartments { get; } = new()
    {
        "CS",
        "IT",
        "IS",
        "BUSINESS",
        "ENGINEERING"
    };
}
```

Important:

```text
In-memory data resets when the app restarts.
It is good for learning CRUD and LINQ.
It is not permanent storage.
```

[[#Navigation|Back to Navigation]]

---

## 48. List, Dictionary, HashSet in Web APIs

### List

Good for ordered records and LINQ:

```csharp
List<Student> Students = new();
```

Use for:

```text
Get all
Search/filter
Sort
GroupBy stats
```

### Dictionary

Good for fast lookup by ID:

```csharp
Dictionary<int, Student> StudentLookup = new();
```

Use for:

```text
Get by ID quickly
Check if ID exists
```

### HashSet

Good for unique allowed values:

```csharp
HashSet<string> ValidDepartments = new()
{
    "CS",
    "IT",
    "IS"
};
```

Use for:

```text
checking valid department
preventing duplicates
distinct values
```

### Array

Good for fixed values:

```csharp
string[] DefaultDepartments =
{
    "CS",
    "IT",
    "IS"
};
```

[[#Navigation|Back to Navigation]]

---

## 49. Keeping Dictionary Lookup in Sync

If you use both list and dictionary, keep them synchronized.

Create:

```csharp
_students.Add(student);
_studentLookup[student.Id] = student;
```

Delete:

```csharp
_students.Remove(student);
_studentLookup.Remove(student.Id);
```

Update usually does not need replacement if the object reference is the same:

```csharp
student.FirstName = dto.FirstName;
```

But if you replace the whole object:

```csharp
_studentLookup[id] = updatedStudent;
```

Warning:

```text
Using both List and Dictionary can teach data structures,
but it adds sync responsibility.
```

For bootcamp, this is okay if documented clearly.

[[#Navigation|Back to Navigation]]

---

## 50. When This Becomes EF Core Later

In-memory now:

```csharp
_students.FirstOrDefault(s => s.Id == id);
_students.Where(s => s.Department == "CS").ToList();
```

EF Core later:

```csharp
_context.Students.FirstOrDefault(s => s.Id == id);
_context.Students.Where(s => s.Department == "CS").ToList();
```

The LINQ syntax looks similar.

Difference:

```text
In-memory LINQ runs against C# objects.
EF Core LINQ is translated to SQL and runs against a database.
```

That is why LINQ is important for ASP.NET.

[[#Navigation|Back to Navigation]]

---

# J. Testing and Debugging

## 51. Running the API

Create project:

```text
dotnet new webapi -n StudentEnrollmentApi
cd StudentEnrollmentApi
code .
```

Run:

```text
dotnet run
```

Hot reload:

```text
dotnet watch
```

Build only:

```text
dotnet build
```

Look for terminal output like:

```text
Now listening on: https://localhost:5001
```

Your actual port may be different.

[[#Navigation|Back to Navigation]]

---

## 52. Postman Testing Guide

Basic steps:

```text
1. Run API with dotnet run.
2. Copy localhost URL from terminal.
3. Open Postman.
4. Create new request.
5. Choose HTTP method.
6. Enter URL.
7. For POST/PUT/PATCH, go to Body → raw → JSON.
8. Send request.
9. Check status code first.
10. Check response body and headers.
```

Example GET:

```text
GET https://localhost:5001/api/students
```

Example POST:

```text
POST https://localhost:5001/api/students
```

Headers:

```text
Content-Type: application/json
```

Body:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "department": "CS",
  "yearLevel": 2
}
```

Expected:

```text
201 Created
```

[[#Navigation|Back to Navigation]]

---

## 53. Sample Request Bodies

### POST student

```json
{
  "firstName": "Maria",
  "lastName": "Santos",
  "department": "CS",
  "yearLevel": 2
}
```

### PUT student

```json
{
  "firstName": "Maria",
  "lastName": "Santos",
  "department": "IT",
  "yearLevel": 3,
  "isActive": true
}
```

### PATCH student

```json
{
  "yearLevel": 4
}
```

### POST course

```json
{
  "code": "CS101",
  "title": "Introduction to Programming",
  "department": "CS",
  "units": 3
}
```

### PATCH enrollment grade

```json
{
  "grade": 92.5,
  "isCompleted": true
}
```

[[#Navigation|Back to Navigation]]

---

## 54. Reading Responses

In Postman, always check:

```text
Status code
Response body
Response headers
Response time
```

For POST create, check:

```text
201 Created
Location header
Response body has generated ID
```

For DELETE, check:

```text
204 No Content
No response body
```

For invalid DTO, check:

```text
400 Bad Request
Validation error details
```

For missing ID, check:

```text
404 Not Found
```

[[#Navigation|Back to Navigation]]

---

## 55. Common Errors and Fixes

### 404 Not Found

Possible causes:

```text
Wrong URL
Wrong route attribute
Wrong controller name
Missing /api
Wrong HTTP method
```

Check:

```csharp
[Route("api/[controller]")]
[HttpGet("{id:int}")]
```

### 400 Bad Request

Possible causes:

```text
Invalid JSON
Missing required field
Wrong data type
Validation failed
```

Example invalid:

```json
{
  "yearLevel": "two"
}
```

If `YearLevel` is int, this fails.

### 415 Unsupported Media Type

Cause:

```text
Missing Content-Type: application/json
```

In Postman, choose:

```text
Body → raw → JSON
```

### CORS error

Usually happens from browser/frontend, not Postman.

Fix later with:

```csharp
builder.Services.AddCors(...);
app.UseCors(...);
```

### App does not start

Try:

```text
dotnet build
```

Read compiler errors from top to bottom.

[[#Navigation|Back to Navigation]]

---

# K. Practical Reference

## 56. Complete Student API Mini Example

### Model

```csharp
namespace StudentEnrollmentApi.Models;

public class Student
{
    public int Id { get; set; }
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public string Department { get; set; } = string.Empty;
    public int YearLevel { get; set; }
    public bool IsActive { get; set; } = true;
    public DateTime CreatedAt { get; set; } = DateTime.UtcNow;

    public string FullName => $"{FirstName} {LastName}";
}
```

Explanation:

```text
This is the internal data shape.
FullName is a computed property.
CreatedAt is generated by the server.
```

### DTO

```csharp
using System.ComponentModel.DataAnnotations;

namespace StudentEnrollmentApi.DTOs;

public class StudentCreateDto
{
    [Required]
    [StringLength(100)]
    public string FirstName { get; set; } = string.Empty;

    [Required]
    [StringLength(100)]
    public string LastName { get; set; } = string.Empty;

    [Required]
    public string Department { get; set; } = string.Empty;

    [Range(1, 4)]
    public int YearLevel { get; set; }
}
```

Explanation:

```text
This is the POST request shape.
Validation is placed here because this is what the client sends.
```

### Controller

```csharp
using Microsoft.AspNetCore.Mvc;
using StudentEnrollmentApi.DTOs;
using StudentEnrollmentApi.Models;

namespace StudentEnrollmentApi.Controllers;

[ApiController]
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
    private static List<Student> _students = new();

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

    [HttpPost]
    public IActionResult Create([FromBody] StudentCreateDto dto)
    {
        var student = new Student
        {
            Id = _students.Count == 0 ? 1 : _students.Max(s => s.Id) + 1,
            FirstName = dto.FirstName.Trim(),
            LastName = dto.LastName.Trim(),
            Department = dto.Department.Trim().ToUpper(),
            YearLevel = dto.YearLevel
        };

        _students.Add(student);

        return CreatedAtAction(nameof(GetById), new { id = student.Id }, student);
    }
}
```

Explanation:

```text
GetAll returns all records with 200 OK.
GetById returns 404 if the student does not exist.
Create reads JSON into StudentCreateDto.
Create maps the DTO to a Student model.
CreatedAtAction returns 201 Created and a Location header.
```

[[#Navigation|Back to Navigation]]

---

## 57. Endpoint Design Checklist

Good REST endpoint names use nouns, not verbs.

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
Use plural nouns for collections.
Use route parameter for specific resource ID.
Use query parameters for filtering/searching.
Use correct HTTP method.
Return correct status code.
Use DTOs for request bodies.
Validate input.
Return 404 for missing records.
```

[[#Navigation|Back to Navigation]]

---

## 58. Beginner Mistakes to Avoid

### Putting all logic in controllers

Avoid huge controllers. Move logic to services.

### Using models directly for all requests

It works early, but DTOs are cleaner and safer.

### Returning 200 with null

Bad:

```csharp
return Ok(student);
```

when `student` is null.

Better:

```csharp
if (student == null)
{
    return NotFound();
}
```

### Forgetting FromBody

For complex DTOs, ASP.NET often infers body binding, but being explicit helps beginners:

```csharp
public IActionResult Create([FromBody] StudentCreateDto dto)
```

### Confusing route params and query params

```text
/api/students/1 → route param, specific student
/api/students?department=CS → query param, filter list
```

### Using POST for everything

Use the correct verbs:

```text
GET read
POST create
PUT full update
PATCH partial update
DELETE remove
```

[[#Navigation|Back to Navigation]]

---

## 59. Quick Memorization Tables

### ASP.NET Core Parts

| Concept | Meaning |
|---|---|
| `Program.cs` | app setup and pipeline |
| Controller | handles HTTP endpoints |
| Action method | endpoint method |
| DTO | request/response shape |
| Model | internal data shape |
| Service | business logic |
| Middleware | request pipeline logic |
| DataAnnotations | validation rules |

### Common Attributes

| Attribute | Use |
|---|---|
| `[ApiController]` | Web API behavior and validation |
| `[Route("api/[controller]")]` | controller route |
| `[HttpGet]` | GET endpoint |
| `[HttpPost]` | POST endpoint |
| `[HttpPut]` | PUT endpoint |
| `[HttpPatch]` | PATCH endpoint |
| `[HttpDelete]` | DELETE endpoint |
| `[FromBody]` | bind JSON body |
| `[FromQuery]` | bind query string |
| `[Required]` | required field |
| `[StringLength]` | string length validation |
| `[Range]` | number range validation |

### Response Helpers

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

### DRF to ASP.NET

| DRF | ASP.NET |
|---|---|
| ViewSet/APIView | Controller |
| Serializer | DTO plus DataAnnotations |
| request.data | FromBody DTO |
| query_params | FromQuery |
| Response | IActionResult helpers |
| QuerySet | LINQ |
| Django model | Model/entity |
| urls.py | route attributes |

[[#Navigation|Back to Navigation]]

---

## 60. Study Order for Bootcamp

Use this study order:

```text
1. Understand Program.cs
2. Understand request pipeline
3. Understand controllers and action methods
4. Understand route params and query params
5. Understand FromBody DTOs
6. Understand IActionResult and status codes
7. Understand Models vs DTOs
8. Understand DataAnnotations validation
9. Understand Services and dependency injection
10. Practice CRUD endpoints
11. Practice middleware logging
12. Practice Postman testing
13. Practice LINQ inside services
```

Minimum survival set for Day 3:

```text
Program.cs
Middleware
Controllers
Routing
DTOs
Services
IActionResult
Ok / NotFound / BadRequest / CreatedAtAction / NoContent
```

Final mental model:

```text
DTO receives request data.
Controller receives HTTP request.
Service handles logic.
Model stores internal data.
Middleware surrounds the request.
Program.cs wires everything together.
```

[[#Navigation|Back to Navigation]]
