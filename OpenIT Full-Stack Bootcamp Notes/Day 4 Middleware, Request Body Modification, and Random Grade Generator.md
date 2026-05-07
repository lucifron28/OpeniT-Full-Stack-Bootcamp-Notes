# Day 4 Reviewer — ASP.NET Core Middleware, Request Pipeline, and Request Body Handling

Tags: #openit-bootcamp #aspnet #dotnet #webapi #middleware #request-pipeline #httpcontext #streams #obsidian

---

# Navigation

## Study Plan

- [[#0. Suggested Study Plan|0. Suggested Study Plan]]
- [[#1. Day 4 Overview|1. Day 4 Overview]]

## Middleware Fundamentals

- [[#2. Middleware Mental Model|2. Middleware Mental Model]]
- [[#3. Request Pipeline|3. Request Pipeline]]
- [[#4. Program.cs Structure|4. Program.cs Structure]]
- [[#5. Middleware Order|5. Middleware Order]]
- [[#6. Use vs Run vs Map|6. Use vs Run vs Map]]
- [[#7. Short-Circuiting Requests|7. Short-Circuiting Requests]]

## HttpContext and Request/Response

- [[#8. HttpContext|8. HttpContext]]
- [[#9. context.Request|9. context.Request]]
- [[#10. context.Response|10. context.Response]]
- [[#11. context.Items|11. context.Items]]
- [[#12. context.RequestServices|12. context.RequestServices]]

## Custom Middleware

- [[#13. Inline Middleware|13. Inline Middleware]]
- [[#14. Middleware Class|14. Middleware Class]]
- [[#15. InvokeAsync|15. InvokeAsync]]
- [[#16. RequestDelegate|16. RequestDelegate]]
- [[#17. Middleware Extension Method|17. Middleware Extension Method]]
- [[#18. Three Middleware Implementation Styles|18. Three Middleware Implementation Styles]]

## Error Handling

- [[#19. Error Handling with Try-Catch Middleware|19. Error Handling with Try-Catch Middleware]]
- [[#20. app.UseExceptionHandler|20. app.UseExceptionHandler]]
- [[#21. Returning JSON Error Responses|21. Returning JSON Error Responses]]

## Dependency Injection in Middleware

- [[#22. Dependency Injection in Middleware|22. Dependency Injection in Middleware]]
- [[#23. Constructor Injection vs InvokeAsync Injection|23. Constructor Injection vs InvokeAsync Injection]]
- [[#24. Middleware with ILogger|24. Middleware with ILogger]]
- [[#25. Middleware with Scoped Services|25. Middleware with Scoped Services]]

## Minimal APIs, Controllers, and Endpoints

- [[#26. Minimal APIs vs Controllers|26. Minimal APIs vs Controllers]]
- [[#27. Are Controllers Middleware?|27. Are Controllers Middleware?]]
- [[#28. app.MapControllers|28. app.MapControllers]]

## Extension Methods

- [[#29. Custom Extension Methods|29. Custom Extension Methods]]
- [[#30. Extension Methods for Middleware Registration|30. Extension Methods for Middleware Registration]]
- [[#31. Extension Methods for Data Cleaning|31. Extension Methods for Data Cleaning]]

## Streams and Low-Level Body Handling

- [[#32. Why Request.Body Is Not a String|32. Why Request.Body Is Not a String]]
- [[#33. byte[]|33. byte[]]]
- [[#34. Stream|34. Stream]]
- [[#35. Buffer|35. Buffer]]
- [[#36. Encoding|36. Encoding]]
- [[#37. MemoryStream|37. MemoryStream]]
- [[#38. Reading Request.Body as String|38. Reading Request.Body as String]]
- [[#39. Modifying Request.Body|39. Modifying Request.Body]]
- [[#40. EnableBuffering and Resetting Position|40. EnableBuffering and Resetting Position]]

## Practical Middleware Patterns

- [[#41. Request Logging Middleware|41. Request Logging Middleware]]
- [[#42. Request Timer Middleware|42. Request Timer Middleware]]
- [[#43. Request Counter Middleware|43. Request Counter Middleware]]
- [[#44. Data Cleaner Middleware|44. Data Cleaner Middleware]]
- [[#45. Body Modifier Middleware|45. Body Modifier Middleware]]
- [[#46. API Key Guard Middleware|46. API Key Guard Middleware]]
- [[#47. Random Grade Middleware Activity|47. Random Grade Middleware Activity]]

## DTO vs Raw Body

- [[#48. With DTO Approach|48. With DTO Approach]]
- [[#49. Without DTO Approach|49. Without DTO Approach]]
- [[#50. With DTO vs Without DTO Comparison|50. With DTO vs Without DTO Comparison]]

## Review

- [[#51. Common Mistakes and Fixes|51. Common Mistakes and Fixes]]
- [[#52. Quick Reference Tables|52. Quick Reference Tables]]
- [[#53. Practice Tasks|53. Practice Tasks]]
- [[#54. Final Key Takeaways|54. Final Key Takeaways]]

---

# 0. Suggested Study Plan

Use this reviewer in layers.

## 30-Minute Quick Review

```text
5 min  - Middleware mental model
5 min  - Request pipeline and middleware order
5 min  - HttpContext, Request, Response
5 min  - InvokeAsync, RequestDelegate, next()
5 min  - Request.Body, Stream, MemoryStream
5 min  - Common mistakes
```

Recommended sections:

```text
2, 3, 5, 8, 15, 16, 32, 37, 39, 51
```

## 1-Hour Practical Review

```text
10 min - Middleware fundamentals
10 min - Inline middleware vs middleware class vs extension method
10 min - Error handling
10 min - Streams and body reading
10 min - Body modification
10 min - Random grade middleware activity
```

Recommended sections:

```text
2 to 7
13 to 18
19 to 21
32 to 40
47 to 50
```

## 2-Hour Deep Review

```text
20 min - Pipeline and middleware order
20 min - HttpContext and request/response
20 min - Custom middleware class pattern
20 min - DI in middleware
20 min - Streams, buffers, byte arrays
20 min - Body modifier and random grade examples
```

Recommended sections:

```text
All sections from 1 to 54
```

[[#Navigation|⬆ Back to Navigation]]

---

# 1. Day 4 Overview

Day 4 focuses on ASP.NET Core middleware and how HTTP requests move through an API.

Main topics:

```text
Middleware
Request pipeline
HttpContext
context.Request
context.Response
RequestDelegate
InvokeAsync
Short-circuiting
Error handling
Extension methods
Minimal APIs vs Controllers
Reading request bodies
Modifying request bodies
Streams and buffers
DTO vs raw request body handling
```

Big picture flow:

```text
Client / Postman
↓
Middleware pipeline
↓
Controller or Minimal API endpoint
↓
Service
↓
Data store / database
↓
Response returns through middleware
↓
Client receives response
```

Key takeaway:

```text
Middleware is code that runs around the endpoint.
It can inspect, modify, allow, block, or log requests and responses.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 2. Middleware Mental Model

Middleware is code that runs while a request is being processed.

It can run:

```text
before the controller
after the controller
both before and after the controller
instead of the controller if it short-circuits
```

Basic middleware pattern:

```csharp
app.Use(async (context, next) =>
{
    // Runs before the next middleware or controller

    await next();

    // Runs after the next middleware or controller
});
```

Example:

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine("Before endpoint");

    await next();

    Console.WriteLine("After endpoint");
});
```

Flow:

```text
Request enters middleware
↓
"Before endpoint"
↓
await next()
↓
Controller/action runs
↓
"After endpoint"
↓
Response returns
```

Key takeaway:

```text
Middleware surrounds the endpoint.
Code before next() runs on the way in.
Code after next() runs on the way out.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 3. Request Pipeline

The request pipeline is the ordered chain of middleware.

Example:

```csharp
app.UseHttpsRedirection();

app.UseAuthentication();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Request goes top to bottom:

```text
Request
↓
UseHttpsRedirection
↓
UseAuthentication
↓
UseAuthorization
↓
MapControllers
↓
Controller action
```

Response goes bottom to top:

```text
Controller response
↑
Authorization middleware
↑
Authentication middleware
↑
HTTPS middleware
↑
Client
```

Key takeaway:

```text
Middleware order matters because each middleware decides what happens before the request reaches the endpoint.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 4. Program.cs Structure

A normal Web API `Program.cs` has two main parts:

```text
1. Service registration
2. Middleware pipeline configuration
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

Middleware registration:

```csharp
app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();
```

Key takeaway:

```text
builder.Services registers dependencies.
app.Use... builds the request pipeline.
app.MapControllers maps controller endpoints.
app.Run starts the application.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 5. Middleware Order

Middleware order affects behavior.

Correct authentication/authorization order:

```csharp
app.UseAuthentication();
app.UseAuthorization();
```

Wrong order:

```csharp
app.UseAuthorization();
app.UseAuthentication();
```

Why?

```text
Authentication identifies who the user is.
Authorization checks what the user is allowed to do.
```

Typical API order:

```csharp
app.UseExceptionHandler("/error");

app.UseHttpsRedirection();

app.UseCors("AllowFrontend");

app.UseAuthentication();

app.UseAuthorization();

app.MapControllers();
```

For simple bootcamp APIs:

```csharp
app.UseHttpsRedirection();

app.UseMiddleware<CustomMiddleware>();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Key takeaway:

```text
Place global error handling early.
Place authentication before authorization.
Place endpoint mapping near the end.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 6. Use vs Run vs Map

ASP.NET Core has different methods for adding behavior to the pipeline.

## app.Use

`Use` can run logic before and after the next middleware.

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine("Before");

    await next();

    Console.WriteLine("After");
});
```

Use when:

```text
You want the request to continue to the next middleware.
```

## app.Run

`Run` ends the pipeline.

```csharp
app.Run(async context =>
{
    await context.Response.WriteAsync("Hello from Run");
});
```

Use when:

```text
You want to handle the request and stop there.
```

## app.Map

`Map` branches the pipeline based on path.

```csharp
app.Map("/health", healthApp =>
{
    healthApp.Run(async context =>
    {
        await context.Response.WriteAsync("Healthy");
    });
});
```

Request:

```http
GET /health
```

Response:

```text
Healthy
```

Key takeaway:

```text
Use = continue-capable middleware
Run = terminal middleware
Map = branch the pipeline by path
```

[[#Navigation|⬆ Back to Navigation]]

---

# 7. Short-Circuiting Requests

Short-circuiting means stopping a request before it reaches the controller.

Example:

```csharp
app.Use(async (context, next) =>
{
    if (!context.Request.Headers.ContainsKey("X-API-KEY"))
    {
        context.Response.StatusCode = 401;
        await context.Response.WriteAsync("Missing API key.");
        return;
    }

    await next();
});
```

If the header is missing:

```text
Request enters middleware
↓
Middleware returns 401
↓
Controller does not run
```

If the header exists:

```text
Request enters middleware
↓
await next()
↓
Controller runs
```

Common use cases:

```text
API key checking
maintenance mode
blocking invalid requests
rate limiting
early validation
```

Key takeaway:

```text
Calling next() continues the pipeline.
Not calling next() short-circuits the request.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 8. HttpContext

`HttpContext` represents the current HTTP request and response.

In inline middleware:

```csharp
app.Use(async (context, next) =>
{
    await next();
});
```

In middleware class:

```csharp
public async Task InvokeAsync(HttpContext context)
{
    await _next(context);
}
```

Important properties:

```csharp
context.Request
context.Response
context.User
context.Items
context.RequestServices
```

Key takeaway:

```text
HttpContext is the main object used by middleware to access the request and response.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 9. context.Request

`context.Request` represents the incoming HTTP request.

Common properties:

```csharp
context.Request.Method
context.Request.Path
context.Request.QueryString
context.Request.Headers
context.Request.Cookies
context.Request.Body
context.Request.ContentType
context.Request.ContentLength
```

Example:

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine(context.Request.Method);
    Console.WriteLine(context.Request.Path);

    await next();
});
```

Example output:

```text
POST
/api/sections/MB02/students
```

Check method:

```csharp
if (context.Request.Method == HttpMethods.Post)
{
    Console.WriteLine("POST request");
}
```

Check path:

```csharp
if (context.Request.Path.StartsWithSegments("/api/sections"))
{
    Console.WriteLine("Section endpoint");
}
```

Check header:

```csharp
if (context.Request.Headers.ContainsKey("X-API-KEY"))
{
    Console.WriteLine("Has API key");
}
```

Check cookie:

```csharp
if (context.Request.Cookies.ContainsKey("sessionId"))
{
    Console.WriteLine("Has session cookie");
}
```

Key takeaway:

```text
context.Request is used to inspect incoming request data before it reaches the controller.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 10. context.Response

`context.Response` represents the outgoing HTTP response.

Common properties:

```csharp
context.Response.StatusCode
context.Response.ContentType
context.Response.Headers
context.Response.Body
```

Set status code:

```csharp
context.Response.StatusCode = 400;
```

Write plain text:

```csharp
await context.Response.WriteAsync("Invalid request.");
```

Write JSON:

```csharp
await context.Response.WriteAsJsonAsync(new
{
    error = "Invalid request."
});
```

Short-circuit with JSON:

```csharp
app.Use(async (context, next) =>
{
    if (context.Request.Path == "/blocked")
    {
        context.Response.StatusCode = 403;
        context.Response.ContentType = "application/json";

        await context.Response.WriteAsJsonAsync(new
        {
            message = "This route is blocked."
        });

        return;
    }

    await next();
});
```

Key takeaway:

```text
context.Response is used to control what gets sent back to the client.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 11. context.Items

`context.Items` stores temporary data during one request.

Middleware:

```csharp
app.Use(async (context, next) =>
{
    context.Items["RequestId"] = Guid.NewGuid().ToString();

    await next();
});
```

Controller:

```csharp
[HttpGet]
public IActionResult Get()
{
    var requestId = HttpContext.Items["RequestId"];

    return Ok(new
    {
        RequestId = requestId
    });
}
```

Use cases:

```text
request ID
temporary flags
middleware-to-controller data
per-request calculated data
```

Key takeaway:

```text
context.Items is temporary storage for the current request only.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 12. context.RequestServices

`context.RequestServices` is the request-level service provider.

Manual service resolution:

```csharp
var studentService = context.RequestServices.GetRequiredService<IStudentService>();
```

Example:

```csharp
app.Use(async (context, next) =>
{
    var service = context.RequestServices.GetRequiredService<IStudentService>();

    var students = service.GetAllStudents();

    Console.WriteLine($"Students: {students.Count}");

    await next();
});
```

Better option for middleware class:

```csharp
public async Task InvokeAsync(HttpContext context, IStudentService studentService)
{
    var students = studentService.GetAllStudents();

    await _next(context);
}
```

Key takeaway:

```text
context.RequestServices can manually resolve services, but constructor injection or InvokeAsync injection is usually cleaner.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 13. Inline Middleware

Inline middleware is written directly in `Program.cs`.

Example:

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");

    await next();

    Console.WriteLine($"Response: {context.Response.StatusCode}");
});
```

Good for:

```text
quick testing
small logging
small guards
learning
```

Not ideal for:

```text
large logic
request body modification
reusable middleware
clean architecture
```

Key takeaway:

```text
Inline middleware is fast to write but can make Program.cs messy.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 14. Middleware Class

A middleware class stores middleware logic in a separate file.

Example:

```csharp
public class RequestLoggerMiddleware
{
    private readonly RequestDelegate _next;

    public RequestLoggerMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");

        await _next(context);

        Console.WriteLine($"Response: {context.Response.StatusCode}");
    }
}
```

Register:

```csharp
app.UseMiddleware<RequestLoggerMiddleware>();
```

Advantages:

```text
cleaner Program.cs
easier to read
reusable
more obvious responsibility
better for longer middleware
```

Key takeaway:

```text
Middleware class is the recommended structure for custom middleware with real logic.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 15. InvokeAsync

`InvokeAsync` is the method called when a middleware class runs.

Pattern:

```csharp
public async Task InvokeAsync(HttpContext context)
{
    await _next(context);
}
```

Full example:

```csharp
public class SampleMiddleware
{
    private readonly RequestDelegate _next;

    public SampleMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        Console.WriteLine("Middleware started");

        await _next(context);

        Console.WriteLine("Middleware ended");
    }
}
```

Important:

```text
InvokeAsync receives HttpContext.
It can inspect or modify request/response.
It calls _next(context) to continue.
```

Key takeaway:

```text
InvokeAsync is the main method of a custom middleware class.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 16. RequestDelegate

`RequestDelegate` represents the next middleware or endpoint.

Conceptually:

```csharp
public delegate Task RequestDelegate(HttpContext context);
```

In middleware:

```csharp
private readonly RequestDelegate _next;

public CustomMiddleware(RequestDelegate next)
{
    _next = next;
}
```

Continue the pipeline:

```csharp
await _next(context);
```

Pipeline example:

```csharp
app.UseMiddleware<MiddlewareA>();
app.UseMiddleware<MiddlewareB>();
app.MapControllers();
```

Flow:

```text
Request
↓
MiddlewareA
↓
MiddlewareB
↓
Controller
↓
MiddlewareB after code
↓
MiddlewareA after code
↓
Response
```

In `MiddlewareA`, `_next` points to `MiddlewareB`.

In `MiddlewareB`, `_next` points to the controller endpoint.

Key takeaway:

```text
RequestDelegate is the stored reference to the next step in the pipeline.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 17. Middleware Extension Method

A middleware extension method creates cleaner registration syntax.

Middleware class:

```csharp
public class RequestLoggerMiddleware
{
    private readonly RequestDelegate _next;

    public RequestLoggerMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        Console.WriteLine("Logging request");

        await _next(context);
    }
}
```

Extension method:

```csharp
public static class RequestLoggerMiddlewareExtensions
{
    public static IApplicationBuilder UseRequestLogger(this IApplicationBuilder app)
    {
        return app.UseMiddleware<RequestLoggerMiddleware>();
    }
}
```

Usage:

```csharp
app.UseRequestLogger();
```

Instead of:

```csharp
app.UseMiddleware<RequestLoggerMiddleware>();
```

Key takeaway:

```text
Extension methods hide setup details and keep Program.cs simple.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 18. Three Middleware Implementation Styles

## 1. Inline

```csharp
app.Use(async (context, next) =>
{
    await next();
});
```

## 2. Middleware class

```csharp
app.UseMiddleware<CustomMiddleware>();
```

## 3. Extension method

```csharp
app.UseCustomMiddleware();
```

Comparison:

| Style | Best For | Example |
|---|---|---|
| Inline | quick tests | `app.Use(async...)` |
| Class | real custom middleware | `app.UseMiddleware<T>()` |
| Extension | clean registration | `app.UseSomething()` |

Key takeaway:

```text
Use inline for learning.
Use class for real middleware logic.
Use extension methods to make Program.cs clean.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 19. Error Handling with Try-Catch Middleware

Error handling middleware catches exceptions globally.

Inline example:

```csharp
app.Use(async (context, next) =>
{
    try
    {
        await next();
    }
    catch (Exception)
    {
        context.Response.StatusCode = 500;
        context.Response.ContentType = "application/json";

        await context.Response.WriteAsJsonAsync(new
        {
            error = "An unexpected error occurred."
        });
    }
});
```

Middleware class:

```csharp
public class ErrorHandlingMiddleware
{
    private readonly RequestDelegate _next;

    public ErrorHandlingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (ArgumentException ex)
        {
            context.Response.StatusCode = 400;

            await context.Response.WriteAsJsonAsync(new
            {
                error = ex.Message
            });
        }
        catch (InvalidOperationException ex)
        {
            context.Response.StatusCode = 409;

            await context.Response.WriteAsJsonAsync(new
            {
                error = ex.Message
            });
        }
        catch (Exception)
        {
            context.Response.StatusCode = 500;

            await context.Response.WriteAsJsonAsync(new
            {
                error = "Internal server error."
            });
        }
    }
}
```

Register early:

```csharp
app.UseMiddleware<ErrorHandlingMiddleware>();
```

Key takeaway:

```text
Exception handling middleware should be early so it can catch errors from later middleware and controllers.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 20. app.UseExceptionHandler

`UseExceptionHandler` is built-in exception handling middleware.

Example:

```csharp
app.UseExceptionHandler(errorApp =>
{
    errorApp.Run(async context =>
    {
        context.Response.StatusCode = 500;
        context.Response.ContentType = "application/json";

        await context.Response.WriteAsJsonAsync(new
        {
            error = "An unexpected error occurred."
        });
    });
});
```

Alternative:

```csharp
app.UseExceptionHandler("/error");
```

Controller:

```csharp
[ApiController]
public class ErrorController : ControllerBase
{
    [Route("/error")]
    public IActionResult Error()
    {
        return Problem("An unexpected error occurred.");
    }
}
```

Key takeaway:

```text
UseExceptionHandler is the built-in way to handle unhandled exceptions globally.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 21. Returning JSON Error Responses

Set status code:

```csharp
context.Response.StatusCode = 400;
```

Set content type:

```csharp
context.Response.ContentType = "application/json";
```

Write JSON:

```csharp
await context.Response.WriteAsJsonAsync(new
{
    error = "Invalid request."
});
```

Full example:

```csharp
app.Use(async (context, next) =>
{
    if (context.Request.Path == "/blocked")
    {
        context.Response.StatusCode = 403;
        context.Response.ContentType = "application/json";

        await context.Response.WriteAsJsonAsync(new
        {
            error = "This route is blocked."
        });

        return;
    }

    await next();
});
```

Key takeaway:

```text
context.Response controls status code, headers, content type, and response body.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 22. Dependency Injection in Middleware

Middleware can receive services through dependency injection.

Constructor injection:

```csharp
public class RequestLoggerMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<RequestLoggerMiddleware> _logger;

    public RequestLoggerMiddleware(
        RequestDelegate next,
        ILogger<RequestLoggerMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }
}
```

InvokeAsync injection:

```csharp
public async Task InvokeAsync(HttpContext context, IStudentService studentService)
{
    await _next(context);
}
```

Manual resolution:

```csharp
var service = context.RequestServices.GetRequiredService<IStudentService>();
```

Key takeaway:

```text
Middleware supports DI, but scoped services should usually be injected into InvokeAsync.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 23. Constructor Injection vs InvokeAsync Injection

## Constructor Injection

Use for:

```text
RequestDelegate
ILogger
IConfiguration
Singleton services
```

Example:

```csharp
public RequestLoggerMiddleware(
    RequestDelegate next,
    ILogger<RequestLoggerMiddleware> logger)
{
    _next = next;
    _logger = logger;
}
```

## InvokeAsync Injection

Use for:

```text
Scoped services
DbContext
services that depend on DbContext
request-specific dependencies
```

Example:

```csharp
public async Task InvokeAsync(HttpContext context, IStudentService studentService)
{
    var students = studentService.GetAllStudents();

    await _next(context);
}
```

Why?

```text
Middleware instances can live longer than one request.
Scoped services live only for one request.
InvokeAsync runs per request.
```

Key takeaway:

```text
Constructor = app-level dependencies.
InvokeAsync = request-level dependencies.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 24. Middleware with ILogger

Example:

```csharp
public class RequestLoggerMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<RequestLoggerMiddleware> _logger;

    public RequestLoggerMiddleware(
        RequestDelegate next,
        ILogger<RequestLoggerMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        _logger.LogInformation(
            "Incoming request: {Method} {Path}",
            context.Request.Method,
            context.Request.Path
        );

        await _next(context);

        _logger.LogInformation(
            "Outgoing response: {StatusCode}",
            context.Response.StatusCode
        );
    }
}
```

Register:

```csharp
app.UseMiddleware<RequestLoggerMiddleware>();
```

Key takeaway:

```text
ILogger is better than Console.WriteLine for real application logging.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 25. Middleware with Scoped Services

Service registration:

```csharp
builder.Services.AddScoped<IStudentService, StudentService>();
```

Middleware:

```csharp
public class StudentCountMiddleware
{
    private readonly RequestDelegate _next;

    public StudentCountMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context, IStudentService studentService)
    {
        var students = studentService.GetAllStudents();

        Console.WriteLine($"Student count: {students.Count}");

        await _next(context);
    }
}
```

Register:

```csharp
app.UseMiddleware<StudentCountMiddleware>();
```

Key takeaway:

```text
Scoped services should be injected into InvokeAsync so the correct request scope is used.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 26. Minimal APIs vs Controllers

## Minimal API

```csharp
app.MapGet("/api/books", () =>
{
    return Results.Ok(new[] { "Book A", "Book B" });
});
```

Good for:

```text
small APIs
microservices
simple endpoints
quick prototypes
small codebases
```

## Controller

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
}
```

Good for:

```text
larger APIs
many endpoints
DTO-heavy APIs
organized actions
service-based applications
validation-heavy projects
```

Key takeaway:

```text
Minimal API is direct.
Controller is structured.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 27. Are Controllers Middleware?

Controllers are not ordinary middleware.

Better mental model:

```text
Controllers are endpoint handlers mapped near the end of the pipeline.
```

The pipeline reaches controllers through:

```csharp
app.MapControllers();
```

Example:

```csharp
app.UseHttpsRedirection();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Key takeaway:

```text
Middleware runs around endpoints.
Controllers are endpoints, not normal app.Use middleware.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 28. app.MapControllers

`MapControllers` maps attribute-routed controllers.

Example controller:

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

Required in `Program.cs`:

```csharp
app.MapControllers();
```

Without it:

```text
Controller routes will not be available.
```

Key takeaway:

```text
MapControllers connects controller attributes to the request pipeline.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 29. Custom Extension Methods

Extension methods add methods to existing types.

Example:

```csharp
public static class StringExtensions
{
    public static string CleanName(this string value)
    {
        return value.Trim();
    }
}
```

Usage:

```csharp
string name = "  Ana  ";
string cleaned = name.CleanName();
```

Result:

```text
Ana
```

Rules:

```text
Class must be static.
Method must be static.
First parameter uses this.
```

Example:

```csharp
public static bool IsLongName(this string value)
{
    return value.Length > 10;
}
```

Usage:

```csharp
bool result = "Christopher".IsLongName();
```

Key takeaway:

```text
Extension methods are helper methods that make existing types feel like they have new methods.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 30. Extension Methods for Middleware Registration

Middleware class:

```csharp
public class RequestTimerMiddleware
{
    private readonly RequestDelegate _next;

    public RequestTimerMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        var start = DateTime.UtcNow;

        await _next(context);

        var elapsed = DateTime.UtcNow - start;

        Console.WriteLine($"{context.Request.Path} took {elapsed.TotalMilliseconds} ms");
    }
}
```

Extension:

```csharp
public static class RequestTimerMiddlewareExtensions
{
    public static IApplicationBuilder UseRequestTimer(this IApplicationBuilder app)
    {
        return app.UseMiddleware<RequestTimerMiddleware>();
    }
}
```

Usage:

```csharp
app.UseRequestTimer();
```

Key takeaway:

```text
Use extension methods to keep Program.cs readable.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 31. Extension Methods for Data Cleaning

Example string cleaner:

```csharp
public static class StringExtensions
{
    public static string CleanInput(this string value)
    {
        return value.Trim();
    }
}
```

Usage:

```csharp
student.FirstName = dto.FirstName.CleanInput();
```

Normalize student number:

```csharp
public static class StringExtensions
{
    public static string NormalizeStudentNumber(this string value)
    {
        return value.Trim().ToUpper();
    }
}
```

Usage:

```csharp
dto.StudentNumber.NormalizeStudentNumber();
```

Null-safe version:

```csharp
public static class StringExtensions
{
    public static string CleanOrEmpty(this string? value)
    {
        return string.IsNullOrWhiteSpace(value)
            ? string.Empty
            : value.Trim();
    }
}
```

Usage:

```csharp
string cleanName = dto.FirstName.CleanOrEmpty();
```

Key takeaway:

```text
Extension methods can abstract repeated data cleaning logic.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 32. Why Request.Body Is Not a String

`Request.Body` can contain:

```text
JSON
files
images
form data
large uploads
binary data
```

So ASP.NET exposes it as:

```csharp
Stream
```

not:

```csharp
string
```

This allows data to be read gradually instead of forcing everything into memory immediately.

Key takeaway:

```text
Request.Body is a stream of bytes, not a ready-made string.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 33. byte[]

`byte[]` is an array of bytes.

Example:

```csharp
byte[] data = Encoding.UTF8.GetBytes("Hello");
```

Used for:

```text
raw request body
files
images
binary data
encoded strings
network data
```

Convert string to bytes:

```csharp
string text = "Hello";
byte[] bytes = Encoding.UTF8.GetBytes(text);
```

Convert bytes to string:

```csharp
string result = Encoding.UTF8.GetString(bytes);
```

Key takeaway:

```text
byte[] is the raw data form of text or files.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 34. Stream

A stream is a flow of data.

Example:

```csharp
context.Request.Body
```

is a stream.

Analogy:

```text
byte[] = bucket of water
Stream = hose where water flows
```

Common streams:

```text
FileStream
MemoryStream
NetworkStream
Request.Body
Response.Body
```

Read a stream as text:

```csharp
using var reader = new StreamReader(context.Request.Body);

string body = await reader.ReadToEndAsync();
```

Key takeaway:

```text
A stream lets data be read or written gradually.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 35. Buffer

A buffer is temporary storage used while reading or writing data.

Example:

```csharp
byte[] buffer = new byte[1024];
```

Meaning:

```text
Create temporary storage for 1024 bytes.
```

Used when reading streams in chunks:

```csharp
byte[] buffer = new byte[1024];

int bytesRead = await stream.ReadAsync(buffer, 0, buffer.Length);
```

For beginner ASP.NET work, `StreamReader` often handles buffering internally.

Key takeaway:

```text
A buffer is temporary memory used while moving data.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 36. Encoding

Encoding converts text to bytes and bytes to text.

Most APIs use UTF-8.

String to bytes:

```csharp
string text = "Hello";
byte[] bytes = Encoding.UTF8.GetBytes(text);
```

Bytes to string:

```csharp
string textAgain = Encoding.UTF8.GetString(bytes);
```

Why needed:

```text
Computers send bytes.
Humans read text.
Encoding translates between them.
```

Key takeaway:

```text
Encoding.UTF8 is commonly used for JSON request/response bodies.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 37. MemoryStream

`MemoryStream` is a stream stored in memory.

Create from bytes:

```csharp
byte[] bytes = Encoding.UTF8.GetBytes("Hello");

var stream = new MemoryStream(bytes);
```

Replace request body:

```csharp
context.Request.Body = new MemoryStream(bytes);
```

Used when:

```text
You modified request body text.
You converted it to bytes.
You need to give ASP.NET a new Stream.
```

Key takeaway:

```text
MemoryStream is the easiest way to replace Request.Body after modifying it.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 38. Reading Request.Body as String

Pattern:

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

Explanation:

```text
EnableBuffering allows rereading.
StreamReader converts stream to text.
ReadToEndAsync reads the whole body.
Position = 0 resets the stream.
```

Full middleware example:

```csharp
app.Use(async (context, next) =>
{
    context.Request.EnableBuffering();

    using var reader = new StreamReader(
        context.Request.Body,
        Encoding.UTF8,
        leaveOpen: true
    );

    string body = await reader.ReadToEndAsync();

    context.Request.Body.Position = 0;

    Console.WriteLine(body);

    await next();
});
```

Key takeaway:

```text
If middleware reads the body, reset it so the controller can still read it.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 39. Modifying Request.Body

Steps:

```text
1. Enable buffering
2. Read body as string
3. Parse or modify string
4. Convert modified string to byte[]
5. Create MemoryStream from byte[]
6. Assign MemoryStream to Request.Body
7. Update ContentLength
8. Reset stream position
9. Continue pipeline
```

Example:

```csharp
app.Use(async (context, next) =>
{
    context.Request.EnableBuffering();

    using var reader = new StreamReader(
        context.Request.Body,
        Encoding.UTF8,
        leaveOpen: true
    );

    string body = await reader.ReadToEndAsync();

    if (!string.IsNullOrWhiteSpace(body))
    {
        string modifiedBody = body.Trim();

        byte[] bytes = Encoding.UTF8.GetBytes(modifiedBody);

        context.Request.Body = new MemoryStream(bytes);

        context.Request.ContentLength = bytes.Length;

        context.Request.Body.Position = 0;
    }

    await next();
});
```

Key takeaway:

```text
To modify Request.Body, replace it with a new Stream.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 40. EnableBuffering and Resetting Position

When a stream is read, its position moves.

Example:

```text
Before reading:
Position = 0

After ReadToEndAsync:
Position = end of stream
```

If controller tries to read after that:

```text
It may receive an empty body.
```

Fix:

```csharp
context.Request.EnableBuffering();

string body = await reader.ReadToEndAsync();

context.Request.Body.Position = 0;
```

After replacing body:

```csharp
context.Request.Body = new MemoryStream(bytes);
context.Request.Body.Position = 0;
```

Key takeaway:

```text
Reset Request.Body.Position to 0 so the next reader starts from the beginning.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 41. Request Logging Middleware

Inline version:

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");

    await next();

    Console.WriteLine($"Response: {context.Response.StatusCode}");
});
```

Class version:

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
        Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");

        await _next(context);

        Console.WriteLine($"Response: {context.Response.StatusCode}");
    }
}
```

Register:

```csharp
app.UseMiddleware<RequestLoggingMiddleware>();
```

Key takeaway:

```text
Logging middleware is one of the simplest ways to understand before/after request flow.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 42. Request Timer Middleware

```csharp
public class RequestTimerMiddleware
{
    private readonly RequestDelegate _next;

    public RequestTimerMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        var start = DateTime.UtcNow;

        await _next(context);

        var elapsed = DateTime.UtcNow - start;

        Console.WriteLine(
            $"{context.Request.Method} {context.Request.Path} took {elapsed.TotalMilliseconds:F0} ms"
        );
    }
}
```

Register:

```csharp
app.UseMiddleware<RequestTimerMiddleware>();
```

Example output:

```text
GET /api/sections took 18 ms
POST /api/sections/MB02/students took 31 ms
```

Key takeaway:

```text
Middleware can measure how long an endpoint takes.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 43. Request Counter Middleware

```csharp
public class RequestCounterMiddleware
{
    private readonly RequestDelegate _next;
    private static int _requestCount = 0;

    public RequestCounterMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        _requestCount++;

        Console.WriteLine($"Request count: {_requestCount}");

        await _next(context);
    }
}
```

Register:

```csharp
app.UseMiddleware<RequestCounterMiddleware>();
```

Note:

```text
This uses static memory.
Good for learning.
For production, use logging/metrics tools.
```

Key takeaway:

```text
Static fields can maintain temporary app-wide state while the app is running.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 44. Data Cleaner Middleware

Example: reject empty JSON body for POST, PUT, PATCH.

```csharp
public class EmptyBodyGuardMiddleware
{
    private readonly RequestDelegate _next;

    public EmptyBodyGuardMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        bool methodNeedsBody =
            context.Request.Method == HttpMethods.Post ||
            context.Request.Method == HttpMethods.Put ||
            context.Request.Method == HttpMethods.Patch;

        if (methodNeedsBody && context.Request.ContentLength == 0)
        {
            context.Response.StatusCode = 400;

            await context.Response.WriteAsJsonAsync(new
            {
                error = "Request body is required."
            });

            return;
        }

        await _next(context);
    }
}
```

Register:

```csharp
app.UseMiddleware<EmptyBodyGuardMiddleware>();
```

Key takeaway:

```text
Middleware can validate broad request rules before the controller runs.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 45. Body Modifier Middleware

Example: trim raw request body.

```csharp
public class BodyModifierMiddleware
{
    private readonly RequestDelegate _next;

    public BodyModifierMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        context.Request.EnableBuffering();

        using var reader = new StreamReader(
            context.Request.Body,
            Encoding.UTF8,
            leaveOpen: true
        );

        string body = await reader.ReadToEndAsync();

        if (!string.IsNullOrWhiteSpace(body))
        {
            string cleanedBody = body.Trim();

            byte[] bytes = Encoding.UTF8.GetBytes(cleanedBody);

            context.Request.Body = new MemoryStream(bytes);
            context.Request.ContentLength = bytes.Length;
            context.Request.Body.Position = 0;
        }
        else
        {
            context.Request.Body.Position = 0;
        }

        await _next(context);
    }
}
```

Register:

```csharp
app.UseMiddleware<BodyModifierMiddleware>();
```

Key takeaway:

```text
Body modification is advanced and should be used carefully.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 46. API Key Guard Middleware

```csharp
public class ApiKeyMiddleware
{
    private readonly RequestDelegate _next;
    private const string ApiKeyHeaderName = "X-API-KEY";

    public ApiKeyMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        if (!context.Request.Headers.TryGetValue(ApiKeyHeaderName, out var apiKey))
        {
            context.Response.StatusCode = 401;

            await context.Response.WriteAsJsonAsync(new
            {
                error = "Missing API key."
            });

            return;
        }

        if (apiKey != "secret-key")
        {
            context.Response.StatusCode = 403;

            await context.Response.WriteAsJsonAsync(new
            {
                error = "Invalid API key."
            });

            return;
        }

        await _next(context);
    }
}
```

Register:

```csharp
app.UseMiddleware<ApiKeyMiddleware>();
```

Key takeaway:

```text
Middleware can block unauthorized requests before they reach controllers.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 47. Random Grade Middleware Activity

Goal:

```text
Automatically generate a random grade when creating a student.
```

Target:

```http
POST /api/sections/{sectionCode}/students
```

Expected body from client:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "age": 20,
  "gender": "Female"
}
```

Modified body after middleware:

```json
{
  "firstName": "Ana",
  "lastName": "Reyes",
  "age": 20,
  "gender": "Female",
  "grade": 88
}
```

Middleware class:

```csharp
using System.Text;
using System.Text.Json;

public class RandomGradeGeneratorMiddleware
{
    private readonly RequestDelegate _next;

    public RandomGradeGeneratorMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        string path = context.Request.Path.Value ?? string.Empty;

        bool isAddStudentRequest =
            context.Request.Method == HttpMethods.Post &&
            path.StartsWith("/api/sections/", StringComparison.OrdinalIgnoreCase) &&
            path.EndsWith("/students", StringComparison.OrdinalIgnoreCase) &&
            context.Request.ContentType?.Contains("application/json") == true &&
            context.Request.ContentLength > 0;

        if (isAddStudentRequest)
        {
            context.Request.EnableBuffering();

            using var reader = new StreamReader(
                context.Request.Body,
                Encoding.UTF8,
                leaveOpen: true
            );

            string body = await reader.ReadToEndAsync();

            var jsonObject = JsonSerializer.Deserialize<Dictionary<string, object>>(body);

            if (jsonObject != null)
            {
                jsonObject["Grade"] = Random.Shared.Next(75, 101);

                string modifiedBody = JsonSerializer.Serialize(jsonObject);

                byte[] byteArray = Encoding.UTF8.GetBytes(modifiedBody);

                context.Request.Body = new MemoryStream(byteArray);
                context.Request.ContentLength = byteArray.Length;
                context.Request.Body.Position = 0;
            }
        }

        await _next(context);
    }
}
```

Register directly:

```csharp
app.UseMiddleware<RandomGradeGeneratorMiddleware>();
```

Extension method:

```csharp
public static class RandomGradeGeneratorMiddlewareExtensions
{
    public static IApplicationBuilder UseRandomGradeGenerator(this IApplicationBuilder app)
    {
        return app.UseMiddleware<RandomGradeGeneratorMiddleware>();
    }
}
```

Register with extension:

```csharp
app.UseRandomGradeGenerator();
```

Key takeaway:

```text
Middleware can modify a JSON request body before model binding happens.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 48. With DTO Approach

Controller:

```csharp
[HttpPost("{sectionCode}/students")]
public IActionResult CreateStudent(
    string sectionCode,
    [FromBody] StudentCreateDto dto)
{
    var student = studentService.CreateInSection(sectionCode, dto);

    if (student == null)
    {
        return NotFound();
    }

    return CreatedAtAction(
        nameof(GetStudentById),
        new { sectionCode, studentId = student.Id },
        student
    );
}
```

DTO:

```csharp
public class StudentCreateDto
{
    public string FirstName { get; set; } = string.Empty;
    public string LastName { get; set; } = string.Empty;
    public int Age { get; set; }
    public string Gender { get; set; } = string.Empty;
    public int? Grade { get; set; }
}
```

Flow:

```text
Client sends JSON
↓
Middleware adds Grade
↓
ASP.NET binds modified JSON to DTO
↓
Controller receives DTO
↓
Service saves DTO data
```

Advantages:

```text
cleaner
structured
works with validation
normal Web API approach
```

Key takeaway:

```text
With DTO, ASP.NET handles JSON-to-object conversion after middleware modifies the body.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 49. Without DTO Approach

Raw controller method:

```csharp
[HttpPost("{sectionCode}/students-raw")]
public async Task<IActionResult> CreateStudentRaw(string sectionCode)
{
    using var reader = new StreamReader(Request.Body, Encoding.UTF8);

    string body = await reader.ReadToEndAsync();

    if (string.IsNullOrWhiteSpace(body))
    {
        return BadRequest("Request body is required.");
    }

    var jsonObject = JsonSerializer.Deserialize<Dictionary<string, object>>(body);

    if (jsonObject == null)
    {
        return BadRequest("Invalid JSON.");
    }

    string firstName = jsonObject["firstName"].ToString() ?? string.Empty;
    string lastName = jsonObject["lastName"].ToString() ?? string.Empty;
    int grade = Convert.ToInt32(jsonObject["Grade"].ToString());

    return Ok(new
    {
        firstName,
        lastName,
        grade
    });
}
```

Flow:

```text
Client sends JSON
↓
Middleware adds Grade
↓
Controller manually reads Request.Body
↓
Controller manually parses JSON
↓
Controller manually extracts values
```

Advantages:

```text
good for learning low-level body handling
shows how streams work
more control
```

Disadvantages:

```text
more manual
more error-prone
less clean for CRUD APIs
harder validation
```

Key takeaway:

```text
Without DTO means manually reading and parsing the raw request body.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 50. With DTO vs Without DTO Comparison

| Topic | With DTO | Without DTO |
|---|---|---|
| Body reading | Automatic | Manual |
| JSON parsing | ASP.NET model binding | You parse it |
| Validation | Easier | Manual |
| Clean code | Better | More verbose |
| Learning streams | Less visible | More visible |
| Recommended for CRUD | Yes | No |
| Good for low-level practice | Somewhat | Yes |

Best rule:

```text
Use DTOs for normal API development.
Use raw body reading only for low-level middleware/body experiments.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 51. Common Mistakes and Fixes

## Mistake 1: Middleware does not call next()

Bad:

```csharp
app.Use(async (context, next) =>
{
    if (context.Request.ContentLength > 0)
    {
        await next();
    }
});
```

Problem:

```text
Requests with no body never continue.
```

Fix:

```csharp
app.Use(async (context, next) =>
{
    if (context.Request.ContentLength > 0)
    {
        // do work
    }

    await next();
});
```

## Mistake 2: Controller receives empty body

Cause:

```text
Middleware read the stream and did not reset Position.
```

Fix:

```csharp
context.Request.Body.Position = 0;
```

## Mistake 3: Assigning string directly to Request.Body

Bad:

```csharp
context.Request.Body = modifiedBody;
```

Fix:

```csharp
byte[] bytes = Encoding.UTF8.GetBytes(modifiedBody);
context.Request.Body = new MemoryStream(bytes);
```

## Mistake 4: Middleware runs twice

Cause:

```csharp
app.UseMiddleware<RandomGradeGeneratorMiddleware>();
app.UseRandomGradeGenerator();
```

Fix:

```text
Use only one registration method at a time.
```

## Mistake 5: Modifying every JSON request

Bad:

```csharp
if (context.Request.ContentType?.Contains("application/json") == true)
{
    // modify all JSON bodies
}
```

Better:

```csharp
bool isAddStudentRequest =
    context.Request.Method == HttpMethods.Post &&
    path.StartsWith("/api/sections/", StringComparison.OrdinalIgnoreCase) &&
    path.EndsWith("/students", StringComparison.OrdinalIgnoreCase);
```

## Mistake 6: Using new Random repeatedly

Acceptable for learning:

```csharp
var random = new Random();
```

Better:

```csharp
Random.Shared.Next(75, 101);
```

Key takeaway:

```text
Most middleware bugs come from forgetting next(), not resetting body position, or modifying too many requests.
```

[[#Navigation|⬆ Back to Navigation]]

---

# 52. Quick Reference Tables

## Middleware Terms

| Term | Meaning |
|---|---|
| Middleware | Code that runs during request/response pipeline |
| Pipeline | Ordered chain of middleware |
| HttpContext | Current request and response |
| RequestDelegate | Next middleware or endpoint |
| InvokeAsync | Method called when middleware runs |
| next() | Continue pipeline |
| Short-circuit | Stop request by not calling next() |
| Request.Body | Stream containing request body |
| MemoryStream | Stream stored in memory |
| Encoding | Converts string to bytes and bytes to string |

## Middleware Styles

| Style | Syntax | Best For |
|---|---|---|
| Inline | `app.Use(async...)` | quick test |
| Class | `app.UseMiddleware<T>()` | real middleware |
| Extension | `app.UseSomething()` | clean Program.cs |

## Pipeline Methods

| Method | Meaning |
|---|---|
| `Use` | Can continue to next |
| `Run` | Terminal middleware |
| `Map` | Branch pipeline |
| `MapControllers` | Map controller endpoints |

## Request Body Modification

| Step | Code |
|---|---|
| Enable reread | `EnableBuffering()` |
| Read body | `ReadToEndAsync()` |
| String to bytes | `Encoding.UTF8.GetBytes()` |
| Bytes to stream | `new MemoryStream(bytes)` |
| Replace body | `context.Request.Body = stream` |
| Reset | `Position = 0` |

[[#Navigation|⬆ Back to Navigation]]

---

# 53. Practice Tasks

## Task 1: Request Logger

Create middleware that logs:

```text
HTTP method
Path
Status code
```

Expected output:

```text
GET /api/sections → 200
POST /api/sections/MB02/students → 201
```

## Task 2: Request Timer

Create middleware that logs:

```text
GET /api/sections took 15 ms
```

## Task 3: API Key Guard

Block requests without:

```text
X-API-KEY
```

Return:

```http
401 Unauthorized
```

## Task 4: Empty Body Guard

For POST/PUT/PATCH, return 400 if body is empty.

## Task 5: Random Grade Generator

For:

```http
POST /api/sections/{sectionCode}/students
```

Add:

```json
{
  "Grade": 88
}
```

before the controller receives the body.

## Task 6: Middleware Extension

Create:

```csharp
app.UseRandomGradeGenerator();
```

instead of:

```csharp
app.UseMiddleware<RandomGradeGeneratorMiddleware>();
```

## Task 7: Raw Body Controller

Create one endpoint that manually reads `Request.Body`.

## Task 8: DTO Controller

Create one endpoint that uses `[FromBody] StudentCreateDto`.

[[#Navigation|⬆ Back to Navigation]]

---

# 54. Final Key Takeaways

```text
Middleware runs before and/or after endpoints.

The request pipeline is ordered.

app.Use can continue the request.

app.Run ends the pipeline.

app.Map branches the pipeline.

HttpContext contains Request and Response.

context.Request is for incoming data.

context.Response is for outgoing data.

RequestDelegate represents the next middleware or endpoint.

InvokeAsync is the main method of middleware classes.

Calling next() continues the pipeline.

Not calling next() short-circuits the request.

Middleware classes are cleaner than long inline middleware.

Extension methods keep Program.cs clean.

Request.Body is a Stream, not a string.

To modify Request.Body, read it, modify it, convert to bytes, wrap in MemoryStream, then replace the stream.

Use EnableBuffering when middleware needs to read the body before the controller.

Reset Request.Body.Position to 0 after reading.

Use DTOs for normal Web API work.

Use raw body reading only for low-level learning or special cases.

Error handling middleware should be early in the pipeline.

UseExceptionHandler is the built-in global exception handling middleware.

Middleware order matters.
```

Final mental model:

```text
Request
↓
Middleware checks/modifies/logs
↓
Controller receives request
↓
Service performs logic
↓
Response returns
↓
Middleware checks/modifies/logs response
↓
Client
```

[[#Navigation|⬆ Back to Navigation]]
