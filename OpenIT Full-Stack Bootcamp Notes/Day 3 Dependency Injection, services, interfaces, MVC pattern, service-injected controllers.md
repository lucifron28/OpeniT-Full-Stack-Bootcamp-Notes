Tags: #aspnet #dotnet #webapi #dependency-injection #services #mvc #bootcamp


> Corrected focus:
>
> - **Day 3:** Dependency Injection, services, interfaces, MVC pattern, service-injected controllers
> - **Day 4:** Middleware, request pipeline, clean layering, request/response flow

---

# Navigation

### A. Bootcamp Flow

- [[#0. Day 3 and Day 4 Flow|0. Corrected Day 3 and Day 4 Flow]]
- [[#1. Day 3 Big Picture|1. Day 3 Big Picture]]

### B. Clean Controller and Service Structure

- [[#2. No Business Logic in Controllers|2. No Business Logic in Controllers]]
  - [[#2.1 What Controllers Should Do|2.1 What Controllers Should Do]]
  - [[#2.2 What Controllers Should Not Do|2.2 What Controllers Should Not Do]]
  - [[#2.3 Controller vs Service Responsibility|2.3 Controller vs Service Responsibility]]

- [[#3. Service Layer|3. Service Layer]]
  - [[#3.1 What a Service Is|3.1 What a Service Is]]
  - [[#3.2 Service Method Examples|3.2 Service Method Examples]]
  - [[#3.3 Why Services Make Refactoring Easier|3.3 Why Services Make Refactoring Easier]]

### C. Interfaces and Dependency Injection

- [[#4. Interfaces and Why We Use Them|4. Interfaces and Why We Use Them]]
  - [[#4.1 Interface as a Contract|4.1 Interface as a Contract]]
  - [[#4.2 Implementation Class|4.2 Implementation Class]]
  - [[#4.3 Refactoring Example BookService to BookDBService|4.3 Refactoring Example: BookService to BookDBService]]

- [[#5. Dependency Injection|5. Dependency Injection]]
  - [[#5.1 What Dependency Injection Means|5.1 What Dependency Injection Means]]
  - [[#5.2 Without DI|5.2 Without DI]]
  - [[#5.3 With DI|5.3 With DI]]

- [[#6. Constructor Injection|6. Constructor Injection]]
- [[#7. Registering Services in Program.cs|7. Registering Services in Program.cs]]

### D. Lifetimes and Memory

- [[#8. DI Lifetimes Singleton vs Scoped vs Transient|8. DI Lifetimes: Singleton vs Scoped vs Transient]]
  - [[#8.1 Singleton|8.1 Singleton]]
  - [[#8.2 Scoped|8.2 Scoped]]
  - [[#8.3 Transient|8.3 Transient]]

- [[#9. Singleton vs Scoped Demonstration Using Guid|9. Singleton vs Scoped Demonstration Using Guid]]
- [[#10. Static Data and In-Memory Storage|10. Static Data and In-Memory Storage]]
- [[#11. DI and Memory Persistence|11. DI and Memory Persistence]]

### E. Lifecycle and Routing

- [[#12. Controller Lifecycle|12. Controller Lifecycle]]
- [[#13. HTTP Lifecycle Without Deep Middleware Yet|13. HTTP Lifecycle Without Deep Middleware Yet]]
- [[#14. MVC Pattern in ASP.NET Core Web API|14. MVC Pattern in ASP.NET Core Web API]]
- [[#15. Routes api controller|15. Routes: api/[controller]]]
- [[#16. Class-Level Routes vs Method-Level Routes|16. Class-Level Routes vs Method-Level Routes]]
- [[#17. Query Methods GetAll GetById Search|17. Query Methods: GetAll, GetById, Search]]

### F. Extra Day 3 Topics

- [[#18. Injecting Services Using IServiceProvider|18. Injecting Services Using IServiceProvider]]
- [[#19. Day 3 Mini Tutorial Service-Injected Book API|19. Day 3 Mini Tutorial: Service-Injected Book API]]
- [[#20. Day 3 Project Application Enrollment System API|20. Day 3 Project Application: Enrollment System API]]

### G. Day 4 Preview and Review

- [[#21. Day 4 Preview Middleware and Request Pipeline|21. Day 4 Preview: Middleware and Request Pipeline]]
- [[#22. Common Mistakes|22. Common Mistakes]]
- [[#23. Final Review Tables|23. Final Review Tables]]
- [[#24. Day 3 Practice Checklist|24. Day 3 Practice Checklist]]

---

# 0. Day 3 and Day 4 Flow

The bootcamp outline shows:

```text
Day 3: Web API Structure
Topics: Middleware, request pipeline, clean layering
Output: Multi-endpoint API project

Day 4: Dependency Injection + MVC
Topics: DI concepts, services, interfaces, MVC pattern
Output: Service-injected controller
```

But based on your current class flow, the topics appear to be swapped:

```text
Corrected Day 3:
Dependency Injection + MVC
DI concepts, services, interfaces, service-injected controller

Corrected Day 4:
Middleware
Request pipeline, middleware order, request/response lifecycle
```

For this note, the main focus is **Day 3: Dependency Injection, services, interfaces, controller lifecycle, MVC pattern, and routing**.

[[#Navigation|⬆ Back to Navigation]]

---

# 1. Day 3 Big Picture

Day 3 is about moving from this beginner pattern:

```text
Controller does everything.
```

to this cleaner pattern:

```text
Controller receives request
↓
Controller calls service
↓
Service performs business logic
↓
Controller returns HTTP response
```

Main idea:

```text
Controller = HTTP layer
Service = business logic layer
Interface = contract
Dependency Injection = gives services to controllers
```

By the end of Day 3, you should understand:

```text
- why business logic should not stay in controllers
- how services are created
- why interfaces are useful
- how DI injects services into controllers
- the difference between Singleton, Scoped, and Transient
- why static data stays in memory
- why DI is not the same as database persistence
- how class-level and method-level routes combine
```

[[#Navigation|⬆ Back to Navigation]]

---

# 2. No Business Logic in Controllers

## 2.1 What Controllers Should Do

Controllers should handle **HTTP-related work**.

A controller should do things like:

```text
- receive HTTP requests
- read route parameters
- read query parameters
- read request body DTOs
- call service methods
- return IActionResult responses
```

Examples of HTTP responses:

```csharp
return Ok(data);
return NotFound();
return BadRequest();
return CreatedAtAction(nameof(GetById), new { id = item.Id }, item);
return NoContent();
```

A controller is like the front desk of the API.

It receives the request, asks the correct service to do the work, then returns the response.

[[#Navigation|⬆ Back to Navigation]]

---

## 2.2 What Controllers Should Not Do

Controllers should not contain most of the business logic.

Avoid putting this logic directly in controllers:

```text
- searching records manually
- creating new IDs
- checking duplicate records
- updating many object properties
- deleting from lists
- calculating statistics
- complex LINQ queries
- business rules
```

Bad example:

```csharp
[HttpPost]
public IActionResult Create([FromBody] Book book)
{
    bool duplicate = _books.Any(b => b.Title == book.Title);

    if (duplicate)
    {
        return Conflict("Book already exists.");
    }

    book.Id = _books.Count == 0 ? 1 : _books.Max(b => b.Id) + 1;
    book.CreatedAt = DateTime.UtcNow;

    _books.Add(book);

    return CreatedAtAction(nameof(GetById), new { id = book.Id }, book);
}
```

This works, but the controller is doing too much.

Better:

```csharp
[HttpPost]
public IActionResult Create([FromBody] BookCreateDto dto)
{
    var result = _bookService.Create(dto);

    if (result == null)
    {
        return Conflict("Book already exists.");
    }

    return CreatedAtAction(nameof(GetById), new { id = result.Id }, result);
}
```

Here, the controller delegates the logic to the service.

[[#Navigation|⬆ Back to Navigation]]

---

## 2.3 Controller vs Service Responsibility

| Layer | Responsibility |
|---|---|
| Controller | HTTP request/response |
| Service | Business logic |
| Model | Internal data shape |
| DTO | Request/response shape |
| DataStore | Temporary in-memory storage |
| Program.cs | App configuration and DI registration |

Simple memory:

```text
Controller = "What HTTP response should I return?"
Service = "What should the system do?"
```

[[#Navigation|⬆ Back to Navigation]]

---

# 3. Service Layer

## 3.1 What a Service Is

A service is a class that contains the real operations of the application.

Examples:

```text
BookService
StudentService
SectionService
EnrollmentService
```

A service usually contains methods like:

```text
GetAll()
GetById()
Search()
Create()
Update()
Patch()
Delete()
GetStats()
```

Example:

```csharp
public class BookService
{
    private static List<Book> _books = new();

    public List<Book> GetAll()
    {
        return _books;
    }

    public Book? GetById(int id)
    {
        return _books.FirstOrDefault(b => b.Id == id);
    }
}
```

The service does not return `Ok()` or `NotFound()`.

Those are HTTP concerns and should stay in the controller.

[[#Navigation|⬆ Back to Navigation]]

---

## 3.2 Service Method Examples

For a book API:

```csharp
public interface IBookService
{
    List<Book> GetAll();
    Book? GetById(int id);
    List<Book> Search(string? keyword, bool? availableOnly);
    Book? Create(BookCreateDto dto);
    Book? Update(int id, BookUpdateDto dto);
    Book? Patch(int id, BookPatchDto dto);
    bool Delete(int id);
}
```

For an enrollment API:

```csharp
public interface ISectionService
{
    List<SectionResponseDto> GetAllSections();
    SectionResponseDto? GetSectionByCode(string sectionCode);
    SectionResponseDto CreateSection(SectionCreateDto dto);
    SectionResponseDto? UpdateSection(string sectionCode, SectionUpdateDto dto);
    bool DeleteSection(string sectionCode);

    List<StudentResponseDto>? GetStudentsBySection(string sectionCode);
    StudentResponseDto? AddStudent(string sectionCode, StudentCreateDto dto);
    StudentResponseDto? UpdateStudent(string sectionCode, Guid studentId, StudentUpdateDto dto);
    bool DeleteStudent(string sectionCode, Guid studentId);
}
```

The service is where you usually write your LINQ queries.

[[#Navigation|⬆ Back to Navigation]]

---

## 3.3 Why Services Make Refactoring Easier

Services make your app easier to change later.

Example:

At first, your API may use in-memory data:

```csharp
public class BookService : IBookService
{
    private static List<Book> _books = new();
}
```

Later, you can replace it with a database version:

```csharp
public class BookDBService : IBookService
{
    private readonly AppDbContext _context;

    public BookDBService(AppDbContext context)
    {
        _context = context;
    }
}
```

Because both implement `IBookService`, the controller does not need major changes.

Only one line in `Program.cs` changes:

```csharp
builder.Services.AddSingleton<IBookService, BookService>();
```

to:

```csharp
builder.Services.AddScoped<IBookService, BookDBService>();
```

This is one reason interfaces and DI are useful.

[[#Navigation|⬆ Back to Navigation]]

---

# 4. Interfaces and Why We Use Them

## 4.1 Interface as a Contract

An interface is a contract.

It says:

```text
Any class that implements me must provide these methods.
```

Example:

```csharp
public interface IBookService
{
    List<Book> GetAll();
    Book? GetById(int id);
    Book Create(BookCreateDto dto);
}
```

This does not contain the actual logic.

It only defines what methods must exist.

[[#Navigation|⬆ Back to Navigation]]

---

## 4.2 Implementation Class

A class implements the interface:

```csharp
public class BookService : IBookService
{
    private static List<Book> _books = new();

    public List<Book> GetAll()
    {
        return _books;
    }

    public Book? GetById(int id)
    {
        return _books.FirstOrDefault(b => b.Id == id);
    }

    public Book Create(BookCreateDto dto)
    {
        var book = new Book
        {
            Id = _books.Count == 0 ? 1 : _books.Max(b => b.Id) + 1,
            Title = dto.Title,
            Author = dto.Author,
            Available = true
        };

        _books.Add(book);

        return book;
    }
}
```

This means:

```text
BookService promises to provide everything listed in IBookService.
```

[[#Navigation|⬆ Back to Navigation]]

---

## 4.3 Refactoring Example BookService to BookDBService

Controller depends on the interface:

```csharp
private readonly IBookService _bookService;

public BooksController(IBookService bookService)
{
    _bookService = bookService;
}
```

The controller does not care whether the actual class is:

```text
BookService
BookDBService
MockBookService
CachedBookService
```

As long as the class implements `IBookService`, it can be injected.

Registration:

```csharp
builder.Services.AddSingleton<IBookService, BookService>();
```

Can be changed to:

```csharp
builder.Services.AddScoped<IBookService, BookDBService>();
```

without rewriting the controller.

That is why one of the main reasons for interfaces is **refactoring**.

[[#Navigation|⬆ Back to Navigation]]

---

# 5. Dependency Injection

## 5.1 What Dependency Injection Means

Dependency Injection means:

```text
Instead of a class creating what it needs,
ASP.NET gives that dependency to the class from the outside.
```

In Web API:

```text
Controller needs a service.
ASP.NET provides that service.
```

Simple analogy:

```text
Without DI:
Controller says, "I will create my own BookService."

With DI:
Controller says, "I need an IBookService."
ASP.NET says, "Here is a BookService."
```

[[#Navigation|⬆ Back to Navigation]]

---

## 5.2 Without DI

Without DI, the controller creates the service manually:

```csharp
public class BooksController : ControllerBase
{
    private readonly BookService _bookService;

    public BooksController()
    {
        _bookService = new BookService();
    }
}
```

This works, but it creates problems:

```text
- controller is tightly connected to BookService
- harder to replace with BookDBService later
- harder to test
- controller controls object creation
```

[[#Navigation|⬆ Back to Navigation]]

---

## 5.3 With DI

With DI, the controller asks for the service in the constructor:

```csharp
public class BooksController : ControllerBase
{
    private readonly IBookService _bookService;

    public BooksController(IBookService bookService)
    {
        _bookService = bookService;
    }
}
```

Then `Program.cs` defines what implementation to use:

```csharp
builder.Services.AddScoped<IBookService, BookService>();
```

Meaning:

```text
When something asks for IBookService,
give it a BookService.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 6. Constructor Injection

Constructor injection is the most common DI pattern in ASP.NET Core.

Example:

```csharp
private readonly IBookService _bookService;

public BooksController(IBookService bookService)
{
    _bookService = bookService;
}
```

Breakdown:

```text
private readonly IBookService _bookService;
```

This stores the injected service.

```text
public BooksController(IBookService bookService)
```

This asks ASP.NET for an `IBookService`.

```text
_bookService = bookService;
```

This saves the injected service into the private field.

Why `readonly`?

```text
After the service is injected, the controller should not replace it.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 7. Registering Services in Program.cs

DI will not work unless the service is registered.

Example:

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

builder.Services.AddScoped<IBookService, BookService>();

var app = builder.Build();

app.MapControllers();

app.Run();
```

This line is the key:

```csharp
builder.Services.AddScoped<IBookService, BookService>();
```

Meaning:

```text
Register IBookService.
When requested, use BookService.
Lifetime: Scoped.
```

Other examples:

```csharp
builder.Services.AddSingleton<IBookService, BookService>();
builder.Services.AddScoped<IBookService, BookService>();
builder.Services.AddTransient<IBookService, BookService>();
```

[[#Navigation|⬆ Back to Navigation]]

---

# 8. DI Lifetimes Singleton vs Scoped vs Transient

DI lifetimes control how service instances are created and reused.

```text
Singleton = one instance for the entire app
Scoped = one instance per HTTP request
Transient = new instance every time requested
```

[[#Navigation|⬆ Back to Navigation]]

---

## 8.1 Singleton

Registration:

```csharp
builder.Services.AddSingleton<IBookService, BookService>();
```

Meaning:

```text
Create one BookService instance.
Reuse the same instance for all requests while the app is running.
```

Flow:

```text
Request 1 → BookService instance A
Request 2 → BookService instance A
Request 3 → BookService instance A
```

Good for:

```text
- shared cache
- app-wide configuration services
- demo in-memory storage
```

Be careful:

```text
- shared across all users
- mutable data can cause concurrency issues
- can consume memory if it stores too much data
```

[[#Navigation|⬆ Back to Navigation]]

---

## 8.2 Scoped

Registration:

```csharp
builder.Services.AddScoped<IBookService, BookService>();
```

Meaning:

```text
Create one service instance per HTTP request.
```

Flow:

```text
Request 1 → BookService instance A
Request 2 → BookService instance B
Request 3 → BookService instance C
```

Good for:

```text
- normal Web API services
- services that use DbContext
- request-specific business logic
```

Scoped is the common default for Web APIs.

[[#Navigation|⬆ Back to Navigation]]

---

## 8.3 Transient

Registration:

```csharp
builder.Services.AddTransient<IBookService, BookService>();
```

Meaning:

```text
Create a new service instance every time it is requested.
```

Flow:

```text
Request 1:
- Controller asks for service → BookService A
- Another class asks for service → BookService B

Request 2:
- Controller asks for service → BookService C
```

Good for:

```text
- lightweight helpers
- stateless services
```

Not good for:

```text
- storing state
- temporary in-memory storage
```

[[#Navigation|⬆ Back to Navigation]]

---

# 9. Singleton vs Scoped Demonstration Using Guid

A common demo uses `Guid.NewGuid()` to prove whether the service instance is reused.

Service interface:

```csharp
public interface IBookService
{
    Guid GetInstanceId();
}
```

Service implementation:

```csharp
public class BookService : IBookService
{
    private readonly Guid _instanceId = Guid.NewGuid();

    public Guid GetInstanceId()
    {
        return _instanceId;
    }
}
```

Controller:

```csharp
[HttpGet("instance")]
public IActionResult GetInstance()
{
    return Ok(new
    {
        InstanceId = _bookService.GetInstanceId()
    });
}
```

If registered as Singleton:

```csharp
builder.Services.AddSingleton<IBookService, BookService>();
```

Result:

```text
Request 1 → same Guid
Request 2 → same Guid
Request 3 → same Guid
```

Meaning:

```text
The same service instance is reused.
```

If registered as Scoped:

```csharp
builder.Services.AddScoped<IBookService, BookService>();
```

Result:

```text
Request 1 → Guid A
Request 2 → Guid B
Request 3 → Guid C
```

Meaning:

```text
A new service instance is created for each request.
```

If registered as Transient, it can create a new instance even within the same request if requested multiple times.

[[#Navigation|⬆ Back to Navigation]]

---

# 10. Static Data and In-Memory Storage

`static` means the member belongs to the class itself, not to one object instance.

Example:

```csharp
public class BookService : IBookService
{
    private static List<Book> _books = new();
}
```

This means:

```text
_books belongs to the BookService class.
It is shared across all BookService instances.
```

Flow:

```text
Request 1 creates BookService instance A
→ uses static _books

Request 2 creates BookService instance B
→ still uses the same static _books
```

Why use static in bootcamp?

```text
It allows in-memory data to survive across requests while the app is running.
```

Warning:

```text
Static data is stored in memory.
Too many static objects can consume/flood memory.
Static data disappears when the app restarts.
Static data is not real database persistence.
```

Use static data for:

```text
- bootcamp demos
- temporary CRUD testing
- learning before database integration
```

Use a database for real apps.

[[#Navigation|⬆ Back to Navigation]]

---

# 11. DI and Memory Persistence

Important correction:

```text
Dependency Injection does not automatically mean memory persistence.
```

DI controls service instance lifetime.

Memory persistence depends on where the data is stored.

Compare:

| Setup | What Happens |
|---|---|
| Scoped service + normal list | list resets per request |
| Scoped service + static list | list survives while app runs |
| Singleton service + normal list | list survives while app runs |
| Database | data survives app restarts |

Example scoped service with normal list:

```csharp
public class BookService : IBookService
{
    private List<Book> _books = new();
}
```

If the service is scoped, this list is recreated for each request.

Example scoped service with static list:

```csharp
public class BookService : IBookService
{
    private static List<Book> _books = new();
}
```

This list is shared while the app runs.

Best note:

```text
DI manages object lifetimes.
Static fields or Singleton services can keep temporary in-memory data while the app runs.
Databases provide real persistence.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 12. Controller Lifecycle

Controllers are short-lived.

Typical flow:

```text
Request arrives
↓
ASP.NET matches route to controller/action
↓
ASP.NET creates controller instance
↓
ASP.NET injects dependencies
↓
Action method runs
↓
IActionResult is returned
↓
Controller instance is discarded
```

This means:

```text
Do not store long-term data in controller fields.
```

Bad example:

```csharp
public class BooksController : ControllerBase
{
    private List<Book> _books = new();
}
```

Why bad?

```text
Request 1 creates a controller with a new empty list.
Request 1 ends.
Controller is discarded.

Request 2 creates another controller with another new empty list.
Previous data is gone.
```

Better:

```text
Store logic in services.
Use static in-memory data only for demos.
Use database for real persistence.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 13. HTTP Lifecycle Without Deep Middleware Yet

Middleware is officially Day 4 in your corrected flow, but you still need the simple request lifecycle.

```text
HTTP request arrives
↓
ASP.NET routing finds endpoint
↓
Controller instance is created
↓
Services are injected
↓
Model binding reads route/query/body data
↓
Validation happens
↓
Controller action runs
↓
Service performs business logic
↓
Controller returns IActionResult
↓
ASP.NET converts it into HTTP response
```

Example:

```http
GET /api/books/1
```

Controller:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    var book = _bookService.GetById(id);

    if (book == null)
    {
        return NotFound();
    }

    return Ok(book);
}
```

Flow:

```text
Route gets id = 1
Controller calls _bookService.GetById(1)
Service searches for book
Controller returns 404 if null
Controller returns 200 if found
```

[[#Navigation|⬆ Back to Navigation]]

---

# 14. MVC Pattern in ASP.NET Core Web API

MVC means:

```text
Model
View
Controller
```

In Web APIs, there is usually no HTML View.

So Web API MVC is more like:

```text
Model = data
Controller = HTTP endpoint
DTO/JSON response = what client receives instead of a View
Service = business logic layer added for cleaner architecture
```

In your bootcamp context:

| MVC Concept | Web API Version |
|---|---|
| Model | `Book`, `Student`, `Section` |
| View | JSON response |
| Controller | `BooksController`, `SectionsController` |
| Extra layer | Service classes |

Example:

```text
Client/Postman
↓
BooksController
↓
BookService
↓
Book model/list/database
↓
JSON response
```

[[#Navigation|⬆ Back to Navigation]]

---

# 15. Routes api controller

`[controller]` is a route token.

It means:

```text
Use the controller class name without the word Controller.
```

Example:

```csharp
[ApiController]
[Route("api/[controller]")]
public class StudentsController : ControllerBase
{
}
```

`StudentsController` becomes:

```text
students
```

Full route:

```text
/api/students
```

More examples:

| Controller Class | Route |
|---|---|
| `BooksController` | `/api/books` |
| `StudentController` | `/api/student` |
| `StudentsController` | `/api/students` |
| `SectionsController` | `/api/sections` |

Why use `[controller]`?

```text
It avoids hardcoding the route.
It automatically uses the controller name.
```

You can also hardcode:

```csharp
[Route("api/books")]
```

But `[Route("api/[controller]")]` is common for beginners.

[[#Navigation|⬆ Back to Navigation]]

---

# 16. Class-Level Routes vs Method-Level Routes

Class-level route:

```csharp
[Route("api/[controller]")]
public class BooksController : ControllerBase
{
}
```

This defines the base path:

```text
/api/books
```

Method-level route:

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    return Ok();
}
```

This adds a specific path:

```text
/api/books/{id}
```

Together:

```text
Class route + Method route = Full endpoint
```

Example controller:

```csharp
[ApiController]
[Route("api/[controller]")]
public class BooksController : ControllerBase
{
    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok();
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        return Ok();
    }

    [HttpGet("search")]
    public IActionResult Search([FromQuery] string? keyword)
    {
        return Ok();
    }

    [HttpPost]
    public IActionResult Create([FromBody] BookCreateDto dto)
    {
        return Ok();
    }
}
```

Full endpoints:

| Attribute | Endpoint |
|---|---|
| `[HttpGet]` | `GET /api/books` |
| `[HttpGet("{id:int}")]` | `GET /api/books/1` |
| `[HttpGet("search")]` | `GET /api/books/search?keyword=clean` |
| `[HttpPost]` | `POST /api/books` |

[[#Navigation|⬆ Back to Navigation]]

---

# 17. Query Methods GetAll GetById Search

Common API query methods:

```text
GetAll()
GetById()
Search()
```

## GetAll

Gets all records.

```csharp
[HttpGet]
public IActionResult GetAll()
{
    var books = _bookService.GetAll();
    return Ok(books);
}
```

Route:

```http
GET /api/books
```

## GetById

Gets one record using route parameter.

```csharp
[HttpGet("{id:int}")]
public IActionResult GetById(int id)
{
    var book = _bookService.GetById(id);

    if (book == null)
    {
        return NotFound();
    }

    return Ok(book);
}
```

Route:

```http
GET /api/books/1
```

## Search

Filters records using query parameters.

```csharp
[HttpGet("search")]
public IActionResult Search([FromQuery] string? keyword, [FromQuery] bool? availableOnly)
{
    var books = _bookService.Search(keyword, availableOnly);
    return Ok(books);
}
```

Route:

```http
GET /api/books/search?keyword=clean&availableOnly=true
```

[[#Navigation|⬆ Back to Navigation]]

---

# 18. Injecting Services Using IServiceProvider

Constructor injection is preferred.

Preferred:

```csharp
public BooksController(IBookService bookService)
{
    _bookService = bookService;
}
```

But you may also see `IServiceProvider`.

Example:

```csharp
using var scope = app.Services.CreateScope();
var bookService = scope.ServiceProvider.GetRequiredService<IBookService>();
```

This manually asks the DI container for a service.

Use cases:

```text
- app startup tasks
- seeding data
- background services
- advanced cases
```

Beginner rule:

```text
Use constructor injection most of the time.
Use IServiceProvider only when you have a specific reason.
```

Avoid this pattern inside normal controller actions unless instructed:

```csharp
var service = HttpContext.RequestServices.GetRequiredService<IBookService>();
```

It works, but it hides dependencies. Constructor injection is clearer.

[[#Navigation|⬆ Back to Navigation]]

---

# 19. Day 3 Mini Tutorial Service-Injected Book API

This section shows the full Day 3 pattern.

## Step 1: Model

`Models/Book.cs`

```csharp
namespace BookApi.Models;

public class Book
{
    public int Id { get; set; }
    public string Title { get; set; } = string.Empty;
    public string Author { get; set; } = string.Empty;
    public bool Available { get; set; } = true;
}
```

Explanation:

```text
Book is the internal data structure.
It represents what the API stores in memory.
```

## Step 2: DTO

`DTOs/BookCreateDto.cs`

```csharp
namespace BookApi.DTOs;

public class BookCreateDto
{
    public string Title { get; set; } = string.Empty;
    public string Author { get; set; } = string.Empty;
}
```

Explanation:

```text
The create DTO represents what the client sends when creating a book.
The client does not send Id because the server creates it.
```

## Step 3: Interface

`Services/IBookService.cs`

```csharp
using BookApi.DTOs;
using BookApi.Models;

namespace BookApi.Services;

public interface IBookService
{
    List<Book> GetAll();
    Book? GetById(int id);
    List<Book> Search(string? keyword, bool? availableOnly);
    Book Create(BookCreateDto dto);
}
```

Explanation:

```text
The interface defines what the service can do.
The controller will depend on this interface.
```

## Step 4: Service Implementation

`Services/BookService.cs`

```csharp
using BookApi.DTOs;
using BookApi.Models;

namespace BookApi.Services;

public class BookService : IBookService
{
    private static List<Book> _books = new();

    public List<Book> GetAll()
    {
        return _books;
    }

    public Book? GetById(int id)
    {
        return _books.FirstOrDefault(b => b.Id == id);
    }

    public List<Book> Search(string? keyword, bool? availableOnly)
    {
        var query = _books.AsEnumerable();

        if (!string.IsNullOrWhiteSpace(keyword))
        {
            query = query.Where(b =>
                b.Title.Contains(keyword, StringComparison.OrdinalIgnoreCase) ||
                b.Author.Contains(keyword, StringComparison.OrdinalIgnoreCase));
        }

        if (availableOnly == true)
        {
            query = query.Where(b => b.Available);
        }

        return query.ToList();
    }

    public Book Create(BookCreateDto dto)
    {
        var book = new Book
        {
            Id = _books.Count == 0 ? 1 : _books.Max(b => b.Id) + 1,
            Title = dto.Title.Trim(),
            Author = dto.Author.Trim(),
            Available = true
        };

        _books.Add(book);

        return book;
    }
}
```

Explanation:

```text
The service contains the business logic.
It manages the in-memory static list.
It uses LINQ for searching and finding books.
```

## Step 5: Register Service

`Program.cs`

```csharp
using BookApi.Services;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

builder.Services.AddScoped<IBookService, BookService>();

var app = builder.Build();

app.MapControllers();

app.Run();
```

Explanation:

```text
AddScoped registers the service with the DI container.
When a controller asks for IBookService, ASP.NET provides BookService.
```

## Step 6: Controller

`Controllers/BooksController.cs`

```csharp
using BookApi.DTOs;
using BookApi.Services;
using Microsoft.AspNetCore.Mvc;

namespace BookApi.Controllers;

[ApiController]
[Route("api/[controller]")]
public class BooksController : ControllerBase
{
    private readonly IBookService _bookService;

    public BooksController(IBookService bookService)
    {
        _bookService = bookService;
    }

    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok(_bookService.GetAll());
    }

    [HttpGet("{id:int}")]
    public IActionResult GetById(int id)
    {
        var book = _bookService.GetById(id);

        if (book == null)
        {
            return NotFound();
        }

        return Ok(book);
    }

    [HttpGet("search")]
    public IActionResult Search([FromQuery] string? keyword, [FromQuery] bool? availableOnly)
    {
        var result = _bookService.Search(keyword, availableOnly);
        return Ok(result);
    }

    [HttpPost]
    public IActionResult Create([FromBody] BookCreateDto dto)
    {
        var book = _bookService.Create(dto);

        return CreatedAtAction(nameof(GetById), new { id = book.Id }, book);
    }
}
```

Explanation:

```text
The controller receives HTTP requests.
It does not manage the list directly.
It calls IBookService.
It returns HTTP responses.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 20. Day 3 Project Application Enrollment System API

Your project requirement:

```text
Create a full Web CRUD API for an enrollment system.

The API must support:
- add/search/update/delete sections
- add/search/update/delete students inside each section
```

Required nested route example:

```http
POST /api/sections/M2022/students
```

Meaning:

```text
Add a student to the section with code M2022.
```

Recommended structure:

```text
EnrollmentSystemApi/
├── Controllers/
│   ├── SectionsController.cs
│   └── SectionStudentsController.cs
├── Models/
│   ├── Section.cs
│   └── Student.cs
├── DTOs/
│   ├── Sections/
│   └── Students/
├── Services/
│   ├── ISectionService.cs
│   └── SectionService.cs
├── Data/
│   └── InMemoryDataStore.cs
└── Program.cs
```

Recommended service registration:

```csharp
builder.Services.AddScoped<ISectionService, SectionService>();
```

Main controller routes:

```csharp
[Route("api/[controller]")]
public class SectionsController : ControllerBase
{
}
```

For nested students:

```csharp
[Route("api/sections/{sectionCode}/students")]
public class SectionStudentsController : ControllerBase
{
}
```

Important endpoints:

```text
GET    /api/sections
GET    /api/sections/{sectionCode}
GET    /api/sections/search
POST   /api/sections
PUT    /api/sections/{sectionCode}
PATCH  /api/sections/{sectionCode}
DELETE /api/sections/{sectionCode}

GET    /api/sections/{sectionCode}/students
GET    /api/sections/{sectionCode}/students/{studentId}
GET    /api/sections/{sectionCode}/students/search
POST   /api/sections/{sectionCode}/students
PUT    /api/sections/{sectionCode}/students/{studentId}
PATCH  /api/sections/{sectionCode}/students/{studentId}
DELETE /api/sections/{sectionCode}/students/{studentId}
```

Day 3 concept applied:

```text
Controllers should only call ISectionService.
SectionService should contain the logic for managing sections and students.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 21. Day 4 Preview Middleware and Request Pipeline

Since Day 3 and Day 4 were swapped, middleware will be deeper in Day 4.

For now, remember:

```text
Middleware runs before and/or after controllers.
```

Example:

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine("Before controller");

    await next();

    Console.WriteLine("After controller");
});
```

Middleware is good for:

```text
- request logging
- error handling
- authentication
- authorization
- CORS
- rate limiting
```

Day 4 will focus on:

```text
Middleware
Request pipeline
Clean layering
How requests move through app.Use(...)
```

For now, do not confuse:

```text
DI = service creation and injection
Middleware = request pipeline behavior
```

[[#Navigation|⬆ Back to Navigation]]

---

# 22. Common Mistakes

## Mistake 1: Putting business logic in controller

Bad:

```csharp
_books.Add(book);
_books.Remove(book);
_books.Where(...);
```

Better:

```csharp
_bookService.Create(dto);
_bookService.Delete(id);
_bookService.Search(keyword);
```

## Mistake 2: Forgetting to register service

If you inject this:

```csharp
public BooksController(IBookService bookService)
```

but forget this:

```csharp
builder.Services.AddScoped<IBookService, BookService>();
```

ASP.NET will throw an error because it does not know how to create `IBookService`.

## Mistake 3: Thinking DI automatically saves data

DI only controls service instance lifetime.

It does not automatically save data permanently.

## Mistake 4: Using Singleton with DbContext later

Avoid:

```csharp
builder.Services.AddSingleton<IBookService, BookDBService>();
```

if `BookDBService` uses `DbContext`.

Use:

```csharp
builder.Services.AddScoped<IBookService, BookDBService>();
```

## Mistake 5: Confusing class route and method route

Remember:

```text
Class route + Method route = Full endpoint
```

[[#Navigation|⬆ Back to Navigation]]

---

# 23. Final Review Tables

## Controller vs Service

| Layer | Job |
|---|---|
| Controller | HTTP request and response |
| Service | Business logic |
| Interface | Contract for service |
| Model | Internal data |
| DTO | Request/response data |

## DI Lifetimes

| Lifetime | Instance Created | Shared Across Requests? | Best For |
|---|---|---:|---|
| Singleton | once for whole app | Yes | cache, config, demo memory |
| Scoped | once per request | No | normal Web API services, DbContext |
| Transient | every request for service | No | lightweight stateless helpers |

## Memory Persistence

| Storage | Survives Next Request? | Survives App Restart? |
|---|---:|---:|
| Controller instance field | No | No |
| Scoped service instance field | No | No |
| Static field | Yes | No |
| Singleton instance field | Yes | No |
| Database | Yes | Yes |

## Route Types

| Route Type | Example | Purpose |
|---|---|---|
| Class-level | `[Route("api/[controller]")]` | base route |
| Method-level | `[HttpGet("{id:int}")]` | specific route |
| Route parameter | `/api/books/1` | identify resource |
| Query parameter | `/api/books/search?keyword=clean` | filter/search |

[[#Navigation|⬆ Back to Navigation]]

---

# 24. Day 3 Practice Checklist

Before moving to Day 4 middleware, make sure you can explain:

```text
[ ] Why controllers should not contain business logic
[ ] What services are for
[ ] What interfaces are for
[ ] How constructor injection works
[ ] Where services are registered in Program.cs
[ ] What AddScoped means
[ ] Difference between Singleton, Scoped, and Transient
[ ] Why static data survives across requests
[ ] Why DI is not the same as database persistence
[ ] What api/[controller] means
[ ] Difference between class-level and method-level routes
[ ] How GetAll, GetById, and Search endpoints are structured
[ ] Why Day 4 middleware is separate from Day 3 DI
```

Final summary:

```text
Day 3 teaches how controllers receive services through Dependency Injection.

Controllers should stay clean.
Services contain business logic.
Interfaces make services replaceable.
DI lifetimes control how service instances are reused.
Static or Singleton can preserve temporary memory while the app runs.
Database is still needed for real persistence.
Middleware is the next topic for Day 4.
```

[[#Navigation|⬆ Back to Navigation]]
