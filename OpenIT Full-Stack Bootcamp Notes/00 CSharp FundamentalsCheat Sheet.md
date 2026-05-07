# C# Fundamentals Cheat Sheet

## Navigation

### A. Core C# Fundamentals
- [[#1. How to Read CSharp Code|1. How to Read C# Code]]
- [[#2. Basic Program Structure|2. Basic Program Structure]]
- [[#3. Variables and Declarations|3. Variables and Declarations]]
- [[#4. Value Types vs Reference Types|4. Value Types vs Reference Types]]
- [[#5. Nullable, Question Mark, and Exclamation Mark|5. Nullable, Question Mark, and Exclamation Mark]]
- [[#6. Var, Const, Readonly, and Static|6. Var, Const, Readonly, and Static]]

### B. Strings, Characters, and Text Handling
- [[#7. String Basics|7. String Basics]]
- [[#8. Important String Methods|8. Important String Methods]]
- [[#9. String Comparison and User Input|9. String Comparison and User Input]]
- [[#10. String Splitting, Joining, and Formatting|10. String Splitting, Joining, and Formatting]]
- [[#11. Char Basics and Char Methods|11. Char Basics and Char Methods]]

### C. Numbers, Conversion, and Type Tricks
- [[#12. Integer and Decimal Number Types|12. Integer and Decimal Number Types]]
- [[#13. Number Conversion and Formatting|13. Number Conversion and Formatting]]
- [[#14. Math and Random Tricks|14. Math and Random Tricks]]

### D. Logic and Control Flow
- [[#15. Boolean Logic and Operators|15. Boolean Logic and Operators]]
- [[#16. If, Ternary, Switch, and Pattern Matching|16. If, Ternary, Switch, and Pattern Matching]]
- [[#17. Loops and Flow Control|17. Loops and Flow Control]]

### E. Methods and Functions
- [[#18. Methods|18. Methods]]
- [[#19. Out Parameters, Try Pattern, and Tuples|19. Out Parameters, Try Pattern, and Tuples]]

### F. Object-Oriented Programming
- [[#20. Classes and Objects|20. Classes and Objects]]
- [[#21. Fields, Properties, Getters, and Setters|21. Fields, Properties, Getters, and Setters]]
- [[#22. Constructors and Encapsulation|22. Constructors and Encapsulation]]
- [[#23. Access Modifiers and Naming|23. Access Modifiers and Naming]]
- [[#24. Inheritance, Abstract Classes, Interfaces, Records, and Enums|24. Inheritance, Abstract Classes, Interfaces, Records, and Enums]]

### G. Collections and Data Structures
- [[#25. Arrays|25. Arrays]]
- [[#26. Matrices and Jagged Arrays|26. Matrices and Jagged Arrays]]
- [[#27. List Collections|27. List Collections]]
- [[#28. Dictionary Collections|28. Dictionary Collections]]
- [[#29. HashSet, Queue, and Stack|29. HashSet, Queue, and Stack]]
- [[#30. Choosing the Right Collection|30. Choosing the Right Collection]]

### H. LINQ Deep Dive
- [[#31. LINQ Mental Model|31. LINQ Mental Model]]
- [[#32. Lambda Expressions|32. Lambda Expressions]]
- [[#33. LINQ with Arrays and Lists|33. LINQ with Arrays and Lists]]
- [[#34. LINQ with Dictionaries|34. LINQ with Dictionaries]]
- [[#35. LINQ with HashSet, Matrices, and Nested Collections|35. LINQ with HashSet, Matrices, and Nested Collections]]
- [[#36. Where, Select, and SelectMany|36. Where, Select, and SelectMany]]
- [[#37. Sorting, Finding, and Checking with LINQ|37. Sorting, Finding, and Checking with LINQ]]
- [[#38. Aggregates, GroupBy, Pagination, and Distinct|38. Aggregates, GroupBy, Pagination, and Distinct]]
- [[#39. LINQ Conversion and Common Mistakes|39. LINQ Conversion and Common Mistakes]]

### I. Practical Mini Patterns
- [[#40. Practice Student Model|40. Practice Student Model]]
- [[#41. Console Input and Menu Patterns|41. Console Input and Menu Patterns]]
- [[#42. Quick Memorization Tables|42. Quick Memorization Tables]]


## 1. How to Read CSharp Code

C# is **strongly typed**, so the type is clear when variables, properties, parameters, and methods are declared.

```csharp
string name = "Ana";
int age = 20;
double gpa = 3.75;
bool enrolled = true;
```

Read a declaration like this:

```text
type → variable name → value
```

Example:

```csharp
int score = 95;
```

Meaning:

```text
Create an integer variable named score and store 95.
```

Important C# habits:

```text
Use semicolons ;
Use curly braces { }
Use explicit boolean conditions
Use clear types
```

C# does **not** allow truthy/falsy checks like JavaScript or Python.

```csharp
string name = "Ana";

if (name) // Wrong in C#
{
}
```

Correct:

```csharp
if (!string.IsNullOrWhiteSpace(name))
{
    Console.WriteLine("Valid name");
}
```

[[#Navigation|⬆ Back to Navigation]]

---

## 2. Basic Program Structure

Modern C# console apps can use **top-level statements**:

```csharp
Console.WriteLine("Hello, World!");
```

Older/full structure:

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

Console output:

```csharp
Console.WriteLine("Print with new line");
Console.Write("Print without new line");
```

Console input:

```csharp
string? input = Console.ReadLine();
```

Safer input:

```csharp
string input = Console.ReadLine() ?? string.Empty;
```

Why? `Console.ReadLine()` can return `null`.

[[#Navigation|⬆ Back to Navigation]]

---

## 3. Variables and Declarations

Basic variables:

```csharp
string name = "Ana";
int age = 20;
double grade = 91.5;
bool isEnrolled = true;
char section = 'A';
```

Declaring without assigning is allowed:

```csharp
string name;
```

But this does **not** mean empty. It means **unassigned**.

```csharp
string name;
Console.WriteLine(name); // Error: use of unassigned local variable
```

Correct:

```csharp
string name = string.Empty;
```

Required text:

```csharp
string firstName = string.Empty;
```

Optional text:

```csharp
string? middleName = null;
```

Empty string vs null:

```text
""   = empty text
" "  = one space
null = no value
```

[[#Navigation|⬆ Back to Navigation]]

---

## 4. Value Types vs Reference Types

Value types store the actual value:

```csharp
int age = 20;
double gpa = 3.75;
bool enrolled = true;
char grade = 'A';
DateTime today = DateTime.Now;
```

Reference types store a reference to an object:

```csharp
string name = "Ana";
Student student = new Student();
List<int> scores = new List<int>();
```

Value types cannot normally be null:

```csharp
int age = null;  // Wrong
int? age = null; // Correct
```

Reference types can be nullable when marked with `?`:

```csharp
string name = "Ana";   // should not be null
string? name2 = null;  // can be null
```

| Type | Category | Typical default |
|---|---|---|
| `int` | value type | `0` |
| `double` | value type | `0.0` |
| `bool` | value type | `false` |
| `char` | value type | `'\0'` |
| `string` | reference type | `null` if not initialized as a field |
| class object | reference type | `null` if not initialized as a field |

[[#Navigation|⬆ Back to Navigation]]

---

## 5. Nullable, Question Mark, and Exclamation Mark

`?` after a type means **can be null**:

```csharp
string? middleName = null;
int? age = null;
double? grade = null;
bool? enrolled = null;
```

Read:

```text
string? = string or null
int?    = int or null
bool?   = true, false, or null
```

`!` before a boolean means **not**:

```csharp
bool isActive = false;

if (!isActive)
{
    Console.WriteLine("Inactive");
}
```

`!` after a variable is the **null-forgiving operator**:

```csharp
Student? student = students.FirstOrDefault(s => s.Id == 1);
Console.WriteLine(student!.Name);
```

This only removes the warning. It does **not** prevent a crash if `student` is actually null.

Better:

```csharp
Student? student = students.FirstOrDefault(s => s.Id == 1);

if (student == null)
{
    Console.WriteLine("Student not found");
}
else
{
    Console.WriteLine(student.Name);
}
```

`?.` means **access only if not null**:

```csharp
Console.WriteLine(student?.Name);
```

`??` means **fallback if null**:

```csharp
string? name = null;
string displayName = name ?? "Unknown";
```

`??=` means **assign only if null**:

```csharp
string? name = null;
name ??= "Default";
```

[[#Navigation|⬆ Back to Navigation]]

---

## 6. Var, Const, Readonly, and Static

`var` means the compiler infers the type.

```csharp
var name = "Ana";  // string
var age = 20;      // int
var price = 99.99; // double
```

But `var` is **not dynamic**:

```csharp
var x = 10;
x = "hello"; // Wrong
```

`const` is a fixed compile-time value:

```csharp
const int MaxScore = 100;
const string AppName = "Grade Tracker";
```

`readonly` is assigned once at runtime:

```csharp
private readonly string _connectionString;

public Repository(string connectionString)
{
    _connectionString = connectionString;
}
```

`static` belongs to the class, not one object:

```csharp
public static class MathHelper
{
    public static int Square(int number)
    {
        return number * number;
    }
}

int result = MathHelper.Square(5);
```

| Keyword | Meaning |
|---|---|
| `var` | infer type |
| `const` | fixed at compile time |
| `readonly` | assigned once at runtime |
| `static` | belongs to class |

[[#Navigation|⬆ Back to Navigation]]

---

## 7. String Basics

A `string` is text.

```csharp
string name = "Ana";
string empty = string.Empty;
string alsoEmpty = "";
string? optional = null;
```

Check for missing text:

```csharp
string.IsNullOrEmpty(name);
string.IsNullOrWhiteSpace(name);
```

| Value | `IsNullOrEmpty` | `IsNullOrWhiteSpace` |
|---|---:|---:|
| `null` | true | true |
| `""` | true | true |
| `" "` | false | true |
| `"Ana"` | false | false |

For user input, prefer:

```csharp
if (!string.IsNullOrWhiteSpace(name))
{
    Console.WriteLine("Valid");
}
```

Because `" "` should usually be treated as invalid input.

[[#Navigation|⬆ Back to Navigation]]

---

## 8. Important String Methods

Example:

```csharp
string text = "  Hello CSharp World  ";
```

### Length

```csharp
int length = text.Length;
```

### Trim

```csharp
string cleaned = text.Trim();
string left = text.TrimStart();
string right = text.TrimEnd();
```

### Case conversion

```csharp
string upper = text.ToUpper();
string lower = text.ToLower();
```

### Contains

```csharp
bool hasHello = text.Contains("Hello");
bool hasHelloIgnoreCase = text.Contains("hello", StringComparison.OrdinalIgnoreCase);
```

### StartsWith and EndsWith

```csharp
bool starts = text.StartsWith("Hello");
bool ends = text.EndsWith("World");
```

Case-insensitive:

```csharp
bool starts = text.StartsWith("hello", StringComparison.OrdinalIgnoreCase);
```

### IndexOf and LastIndexOf

```csharp
int index = text.IndexOf("CSharp");
int last = text.LastIndexOf("o");
```

If not found, result is `-1`.

### Substring

```csharp
string word = "Programming";

string part1 = word.Substring(0, 4); // "Prog"
string part2 = word.Substring(4);    // "ramming"
```

### Replace

```csharp
string result = text.Replace("CSharp", "C#");
```

### Insert

```csharp
string result = "Hello World".Insert(6, "C# ");
```

### Remove

```csharp
string result1 = "Hello World".Remove(5);    // "Hello"
string result2 = "Hello World".Remove(5, 1); // removes 1 char at index 5
```

### PadLeft and PadRight

```csharp
string code = "7";

Console.WriteLine(code.PadLeft(3, '0'));  // "007"
Console.WriteLine(code.PadRight(3, '-')); // "7--"
```

### Split

```csharp
string csv = "Ana,Ben,Carlo";
string[] names = csv.Split(',');
```

### Join

```csharp
string[] names = { "Ana", "Ben", "Carlo" };
string result = string.Join(", ", names);
```

### ToCharArray

```csharp
char[] letters = "Ana".ToCharArray();
```

### Equals

```csharp
bool same = name.Equals("Ana");
bool sameIgnoreCase = name.Equals("ana", StringComparison.OrdinalIgnoreCase);
```

[[#Navigation|⬆ Back to Navigation]]

---

## 9. String Comparison and User Input

C# string comparison is case-sensitive by default.

```csharp
string a = "Ana";
string b = "ana";

Console.WriteLine(a == b); // false
```

Case-insensitive comparison:

```csharp
bool same = a.Equals(b, StringComparison.OrdinalIgnoreCase);
```

Case-insensitive search:

```csharp
bool found = name.Contains("ana", StringComparison.OrdinalIgnoreCase);
```

Clean and validate input:

```csharp
Console.Write("Enter name: ");
string name = Console.ReadLine() ?? string.Empty;

name = name.Trim();

if (string.IsNullOrWhiteSpace(name))
{
    Console.WriteLine("Name is required.");
}
else
{
    Console.WriteLine($"Hello, {name}");
}
```

| Task                   | Use                                                 |
| ---------------------- | --------------------------------------------------- |
| exact comparison       | `a == b`                                            |
| ignore case comparison | `Equals(..., StringComparison.OrdinalIgnoreCase)`   |
| search inside text     | `Contains(..., StringComparison.OrdinalIgnoreCase)` |
| remove spaces          | `Trim()`                                            |
| validate user input    | `IsNullOrWhiteSpace()`                              |

[[#Navigation|⬆ Back to Navigation]]

---

## 10. String Splitting, Joining, and Formatting

Split CSV:

```csharp
string csv = "Ana,Ben,Carlo";
string[] names = csv.Split(',');
```

Split and trim:

```csharp
string input = " Ana, Ben, Carlo ";

List<string> names = input
    .Split(',')
    .Select(x => x.Trim())
    .ToList();
```

Remove empty entries:

```csharp
string input = "Ana,,Ben,,Carlo";

string[] names = input.Split(',', StringSplitOptions.RemoveEmptyEntries);
```

Join:

```csharp
List<string> names = new() { "Ana", "Ben", "Carlo" };

string text = string.Join(" | ", names);
```

String interpolation:

```csharp
string name = "Ana";
int age = 20;

string message = $"Name: {name}, Age: {age}";
```

Formatting numbers:

```csharp
double average = 91.837;

Console.WriteLine($"Average: {average:F2}"); // 91.84
```

Common formats:

```csharp
double value = 1234.567;

Console.WriteLine($"{value:F2}"); // 1234.57
Console.WriteLine($"{value:N2}"); // 1,234.57
Console.WriteLine($"{0.875:P1}"); // 87.5%
Console.WriteLine($"{7:D3}");     // 007
```

[[#Navigation|⬆ Back to Navigation]]

---

## 11. Char Basics and Char Methods

A `char` stores one character and uses single quotes.

```csharp
char letter = 'A';
char digit = '7';
char symbol = '#';
```

Wrong:

```csharp
char x = "A"; // Wrong, double quotes are for string
```

Common char methods:

```csharp
char.IsLetter('A');        // true
char.IsDigit('7');         // true
char.IsLetterOrDigit('A'); // true
char.IsWhiteSpace(' ');    // true
char.IsUpper('A');         // true
char.IsLower('a');         // true
char.IsPunctuation('.');   // true
char.IsSymbol('$');        // true
```

Convert case:

```csharp
char upper = char.ToUpper('a');
char lower = char.ToLower('A');
```

Loop through characters:

```csharp
string text = "CSharp123";

foreach (char c in text)
{
    if (char.IsDigit(c))
    {
        Console.WriteLine($"{c} is a digit");
    }
}
```

LINQ with chars:

```csharp
string password = "Hello123";

bool hasDigit = password.Any(c => char.IsDigit(c));
bool hasUpper = password.Any(c => char.IsUpper(c));
bool allDigits = "12345".All(c => char.IsDigit(c));
int digitCount = "Room 204".Count(c => char.IsDigit(c));
```

[[#Navigation|⬆ Back to Navigation]]

---

## 12. Integer and Decimal Number Types

Whole number types:

```csharp
byte b = 255;
short small = 100;
int age = 20;
long big = 9_000_000_000L;
```

Most of the time, use:

```csharp
int count = 10;
```

Use `long` for very large whole numbers:

```csharp
long views = 9_000_000_000L;
```

Decimal number types:

```csharp
double gpa = 3.85;
float temp = 36.6f;
decimal price = 99.99m;
```

Use:

| Type | Use for |
|---|---|
| `int` | normal whole numbers |
| `long` | very large whole numbers |
| `double` | normal decimal/scientific values |
| `float` | less precise decimal, rarely needed |
| `decimal` | money/exact decimal values |

Money:

```csharp
decimal total = 1500.50m;
```

`m` is required for decimal literals.

[[#Navigation|⬆ Back to Navigation]]

---

## 13. Number Conversion and Formatting

### String to number with Parse

Use when you are sure the text is valid:

```csharp
int age = int.Parse("20");
double grade = double.Parse("91.5");
decimal price = decimal.Parse("99.99");
bool active = bool.Parse("true");
```

This crashes if invalid:

```csharp
int age = int.Parse("abc"); // FormatException
```

### String to number with TryParse

Best for user input:

```csharp
Console.Write("Enter age: ");
string? input = Console.ReadLine();

if (int.TryParse(input, out int age))
{
    Console.WriteLine($"Age: {age}");
}
else
{
    Console.WriteLine("Invalid age");
}
```

TryParse with nullable fallback:

```csharp
int? age = int.TryParse(input, out int parsedAge)
    ? parsedAge
    : null;
```

Common TryParse methods:

```csharp
int.TryParse(input, out int number);
double.TryParse(input, out double gpa);
decimal.TryParse(input, out decimal price);
bool.TryParse(input, out bool isActive);
DateTime.TryParse(input, out DateTime date);
```

### Number to string

```csharp
int age = 20;
string text = age.ToString();
```

With interpolation:

```csharp
string message = $"Age: {age}";
```

With format:

```csharp
double grade = 91.837;
string formatted = grade.ToString("F2"); // "91.84"
```

### Cast vs Convert

```csharp
double x = 9.99;

int a = (int)x;              // 9, truncates
int b = Convert.ToInt32(x);  // 10, rounds
```

### Integer division warning

```csharp
int result = 5 / 2;
Console.WriteLine(result); // 2
```

Correct decimal result:

```csharp
double result = 5.0 / 2; // 2.5
```

Or:

```csharp
int a = 5;
int b = 2;

double result = (double)a / b;
```

[[#Navigation|⬆ Back to Navigation]]

---

## 14. Math and Random Tricks

Common `Math` methods:

```csharp
Math.Abs(-5);          // 5
Math.Max(10, 20);      // 20
Math.Min(10, 20);      // 10
Math.Pow(2, 3);        // 8
Math.Sqrt(25);         // 5
Math.Round(3.567, 2);  // 3.57
Math.Floor(3.9);       // 3
Math.Ceiling(3.1);     // 4
```

Clamp value inside a range:

```csharp
int score = 120;
score = Math.Clamp(score, 0, 100); // 100
```

Random number:

```csharp
Random random = new Random();

int number = random.Next(1, 101); // 1 to 100
```

Important:

```text
Next(min, max) includes min but excludes max.
```

Random decimal:

```csharp
double value = random.NextDouble(); // 0.0 to less than 1.0
```

Random item from list:

```csharp
List<string> names = new() { "Ana", "Ben", "Carlo" };

string randomName = names[random.Next(names.Count)];
```

[[#Navigation|⬆ Back to Navigation]]

---

## 15. Boolean Logic and Operators

A `bool` can only be:

```csharp
true
false
```

Operators:

| Operator | Meaning |
|---|---|
| `==` | equal |
| `!=` | not equal |
| `>` | greater than |
| `<` | less than |
| `>=` | greater than or equal |
| `<=` | less than or equal |
| `&&` | AND |
| `||` | OR |
| `!` | NOT |

AND:

```csharp
if (score >= 75 && attendance >= 80)
{
    Console.WriteLine("Passed");
}
```

OR:

```csharp
if (role == "Admin" || role == "Teacher")
{
    Console.WriteLine("Allowed");
}
```

NOT:

```csharp
if (!isEnrolled)
{
    Console.WriteLine("Not enrolled");
}
```

No truthy/falsy:

```csharp
if ("hello") // Wrong
{
}
```

Correct:

```csharp
if (!string.IsNullOrWhiteSpace(name))
{
}
```

[[#Navigation|⬆ Back to Navigation]]

---

## 16. If, Ternary, Switch, and Pattern Matching

### If/else

```csharp
int score = 85;

if (score >= 90)
{
    Console.WriteLine("Excellent");
}
else if (score >= 75)
{
    Console.WriteLine("Passed");
}
else
{
    Console.WriteLine("Failed");
}
```

Order matters. Put stricter conditions first.

### Ternary

```csharp
string result = score >= 75 ? "Passed" : "Failed";
```

Format:

```text
condition ? valueIfTrue : valueIfFalse
```

### Switch expression

```csharp
string grade = score switch
{
    >= 90 and <= 100 => "A",
    >= 80 and < 90 => "B",
    >= 75 and < 80 => "C",
    >= 0 and < 75 => "Failed",
    _ => "Invalid score"
};
```

`_` means default.

### Type pattern

```csharp
object value = "Hello";

if (value is string text)
{
    Console.WriteLine(text.ToUpper());
}
```

### Null pattern

```csharp
if (student is null)
{
    Console.WriteLine("Not found");
}

if (student is not null)
{
    Console.WriteLine(student.Name);
}
```

### Property pattern

```csharp
if (student is { GPA: >= 3.7 })
{
    Console.WriteLine("Honor student");
}
```

[[#Navigation|⬆ Back to Navigation]]

---

## 17. Loops and Flow Control

### For loop

Use when you need an index.

```csharp
for (int i = 0; i < scores.Length; i++)
{
    Console.WriteLine(scores[i]);
}
```

### Foreach loop

Use for clean iteration.

```csharp
foreach (int score in scores)
{
    Console.WriteLine(score);
}
```

### While loop

Use when you do not know how many repetitions are needed.

```csharp
int attempts = 0;

while (attempts < 3)
{
    Console.WriteLine("Try again");
    attempts++;
}
```

### Do while

Runs at least once.

```csharp
string? input;

do
{
    Console.Write("Enter name: ");
    input = Console.ReadLine();
}
while (string.IsNullOrWhiteSpace(input));
```

### Break

Stops the loop.

```csharp
foreach (int score in scores)
{
    if (score < 0)
    {
        break;
    }
}
```

### Continue

Skips current iteration.

```csharp
foreach (int score in scores)
{
    if (score < 75)
    {
        continue;
    }

    Console.WriteLine(score);
}
```

### Return

Exits the method.

```csharp
public string GetResult(int score)
{
    if (score < 0 || score > 100)
    {
        return "Invalid";
    }

    return score >= 75 ? "Passed" : "Failed";
}
```

[[#Navigation|⬆ Back to Navigation]]

---

## 18. Methods

A method is a named reusable block of code.

```csharp
public int Add(int a, int b)
{
    return a + b;
}
```

Parts:

```text
public → access modifier
int → return type
Add → method name
(int a, int b) → parameters
return a + b → returned value
```

Void method:

```csharp
public void PrintName(string name)
{
    Console.WriteLine(name);
}
```

Early return:

```csharp
public double GetAverage(List<double> grades)
{
    if (grades.Count == 0)
    {
        return 0;
    }

    return grades.Average();
}
```

Optional parameter:

```csharp
public string Greet(string name, string title = "Mr./Ms.")
{
    return $"Hello, {title} {name}";
}
```

Named argument:

```csharp
Greet(name: "Ana", title: "Dr.");
```

Expression-bodied method:

```csharp
public int Square(int number) => number * number;
```

[[#Navigation|⬆ Back to Navigation]]

---

## 19. Out Parameters, Try Pattern, and Tuples

`out` allows a method to output another value through a parameter.

Most common example:

```csharp
string input = "123";

if (int.TryParse(input, out int number))
{
    Console.WriteLine(number);
}
```

Custom Try method:

```csharp
public bool TryFindStudent(int id, out Student? student)
{
    student = students.FirstOrDefault(s => s.Id == id);
    return student != null;
}
```

Usage:

```csharp
if (TryFindStudent(1, out Student? student))
{
    Console.WriteLine(student.Name);
}
else
{
    Console.WriteLine("Not found");
}
```

Tuples return multiple values:

```csharp
public (bool Success, string Message) ValidateName(string name)
{
    if (string.IsNullOrWhiteSpace(name))
    {
        return (false, "Name is required");
    }

    return (true, "Valid");
}
```

Usage:

```csharp
var (success, message) = ValidateName("Ana");
```

Use tuples for small returns. Use classes/records for bigger structures.

[[#Navigation|⬆ Back to Navigation]]

---

## 20. Classes and Objects

A class is a blueprint.

```csharp
public class Student
{
    public string Name { get; set; } = string.Empty;
    public string Course { get; set; } = string.Empty;
}
```

An object is an instance.

```csharp
Student student = new Student();

student.Name = "Ana";
student.Course = "CS";
```

Object initializer:

```csharp
Student student = new Student
{
    Name = "Ana",
    Course = "CS"
};
```

Class with method:

```csharp
public class Student
{
    public string Name { get; set; } = string.Empty;
    public List<double> Grades { get; set; } = new();

    public double GetAverage()
    {
        return Grades.Count == 0 ? 0 : Grades.Average();
    }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

## 21. Fields, Properties, Getters, and Setters

A field is usually private internal storage:

```csharp
private int _count;
```

A property exposes data:

```csharp
public string Name { get; set; } = string.Empty;
```

Auto-property:

```csharp
public string Name { get; set; } = string.Empty;
```

Read-only from outside:

```csharp
public string Course { get; private set; } = string.Empty;
```

Custom getter/setter:

```csharp
private double _grade;

public double Grade
{
    get
    {
        return _grade;
    }
    set
    {
        if (value < 0 || value > 100)
        {
            throw new ArgumentException("Grade must be 0 to 100.");
        }

        _grade = value;
    }
}
```

Computed property:

```csharp
public string FullName => $"{FirstName} {LastName}";
```

Use properties for models:

```csharp
public int Id { get; set; }
public string FirstName { get; set; } = string.Empty;
public string? MiddleName { get; set; }
```

[[#Navigation|⬆ Back to Navigation]]

---

## 22. Constructors and Encapsulation

A constructor runs when an object is created.

```csharp
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; } = string.Empty;

    public Student(int id, string name)
    {
        Id = id;
        Name = name;
    }
}
```

Usage:

```csharp
Student student = new Student(1, "Ana");
```

Default constructor:

```csharp
public Student()
{
}
```

Constructor with validation:

```csharp
public Student(string name)
{
    if (string.IsNullOrWhiteSpace(name))
    {
        throw new ArgumentException("Name is required.");
    }

    Name = name;
}
```

Encapsulation means protect data and expose controlled actions.

Bad:

```csharp
public decimal Balance { get; set; }
```

Better:

```csharp
public class BankAccount
{
    public decimal Balance { get; private set; }

    public void Deposit(decimal amount)
    {
        if (amount <= 0)
        {
            throw new ArgumentException("Amount must be positive.");
        }

        Balance += amount;
    }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

## 23. Access Modifiers and Naming

Access modifiers:

| Modifier | Meaning |
|---|---|
| `public` | accessible anywhere |
| `private` | accessible only inside same class |
| `protected` | accessible inside class and child classes |
| `internal` | accessible inside same project/assembly |

Example:

```csharp
public class Student
{
    private int _id;

    public string Name { get; set; } = string.Empty;

    private void Log()
    {
        Console.WriteLine("Internal log");
    }
}
```

Naming conventions:

| Item | Style |
|---|---|
| Class | `StudentRecord` |
| Public property | `FirstName` |
| Public method | `GetAverage()` |
| Private field | `_students` |
| Local variable | `studentName` |
| Parameter | `studentId` |

[[#Navigation|⬆ Back to Navigation]]

---

## 24. Inheritance, Abstract Classes, Interfaces, Records, and Enums

### Inheritance

```csharp
public class Person
{
    public string Name { get; set; } = string.Empty;
}

public class Student : Person
{
    public string Course { get; set; } = string.Empty;
}
```

### Virtual and override

```csharp
public class Person
{
    public virtual string GetRole()
    {
        return "Person";
    }
}

public class Student : Person
{
    public override string GetRole()
    {
        return "Student";
    }
}
```

### Abstract class

```csharp
public abstract class Animal
{
    public abstract void Speak();
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Woof");
    }
}
```

### Interface

```csharp
public interface IPrintable
{
    void Print();
}

public class Report : IPrintable
{
    public void Print()
    {
        Console.WriteLine("Printing report...");
    }
}
```

### Record

```csharp
public record StudentDto(int Id, string Name, string Course);
```

Records compare by value.

### Enum

```csharp
public enum EnrollmentStatus
{
    Pending,
    Enrolled,
    Dropped,
    Graduated
}
```

Switch with enum:

```csharp
string label = status switch
{
    EnrollmentStatus.Pending => "Waiting",
    EnrollmentStatus.Enrolled => "Active",
    EnrollmentStatus.Dropped => "Inactive",
    EnrollmentStatus.Graduated => "Completed",
    _ => "Unknown"
};
```

[[#Navigation|⬆ Back to Navigation]]

---

## 25. Arrays

Array = fixed-size collection.

```csharp
int[] scores = { 90, 85, 92 };
string[] names = { "Ana", "Ben", "Carlo" };
```

Access by index:

```csharp
Console.WriteLine(scores[0]);
```

Change item:

```csharp
scores[1] = 88;
```

Length:

```csharp
int count = scores.Length;
```

Loop with index:

```csharp
for (int i = 0; i < scores.Length; i++)
{
    Console.WriteLine(scores[i]);
}
```

Foreach:

```csharp
foreach (int score in scores)
{
    Console.WriteLine(score);
}
```

Array helper methods:

```csharp
Array.Sort(scores);
Array.Reverse(scores);
int index = Array.IndexOf(scores, 90);
bool exists = Array.Exists(scores, s => s >= 90);
```

Convert:

```csharp
List<int> list = scores.ToList();
int[] array = list.ToArray();
```

[[#Navigation|⬆ Back to Navigation]]

---

## 26. Matrices and Jagged Arrays

### 2D array / matrix

```csharp
int[,] matrix = new int[2, 3]
{
    { 1, 2, 3 },
    { 4, 5, 6 }
};
```

Access:

```csharp
Console.WriteLine(matrix[0, 0]); // 1
Console.WriteLine(matrix[1, 2]); // 6
```

Rows and columns:

```csharp
int rows = matrix.GetLength(0);
int columns = matrix.GetLength(1);
```

Loop:

```csharp
for (int row = 0; row < matrix.GetLength(0); row++)
{
    for (int col = 0; col < matrix.GetLength(1); col++)
    {
        Console.Write(matrix[row, col] + " ");
    }

    Console.WriteLine();
}
```

### Jagged array

A jagged array is an array of arrays.

```csharp
int[][] jagged = new int[][]
{
    new int[] { 1, 2 },
    new int[] { 3, 4, 5 },
    new int[] { 6 }
};
```

Access:

```csharp
Console.WriteLine(jagged[1][2]); // 5
```

Loop:

```csharp
for (int row = 0; row < jagged.Length; row++)
{
    for (int col = 0; col < jagged[row].Length; col++)
    {
        Console.Write(jagged[row][col] + " ");
    }

    Console.WriteLine();
}
```

| Type | Shape |
|---|---|
| `int[,]` | rectangular grid |
| `int[][]` | rows can have different lengths |

[[#Navigation|⬆ Back to Navigation]]

---

## 27. List Collections

A list is a dynamic array.

```csharp
List<string> names = new();
```

Initialize:

```csharp
List<string> names = new() { "Ana", "Ben", "Carlo" };
```

Add:

```csharp
names.Add("Diana");
names.AddRange(new[] { "Eric", "Faye" });
```

Insert:

```csharp
names.Insert(0, "First");
```

Access:

```csharp
string first = names[0];
```

Count:

```csharp
int count = names.Count;
```

Remove:

```csharp
names.Remove("Ana");
names.RemoveAt(0);
names.RemoveAll(n => n.StartsWith("B"));
```

Contains:

```csharp
bool hasAna = names.Contains("Ana");
```

Find:

```csharp
string? result = names.FirstOrDefault(n => n == "Ana");
```

Sort:

```csharp
names.Sort();
```

Descending:

```csharp
names = names.OrderByDescending(n => n).ToList();
```

[[#Navigation|⬆ Back to Navigation]]

---

## 28. Dictionary Collections

A dictionary stores key-value pairs.

```csharp
Dictionary<int, string> students = new()
{
    { 1, "Ana" },
    { 2, "Ben" },
    { 3, "Carlo" }
};
```

Read it as:

```text
1 → Ana
2 → Ben
3 → Carlo
```

This:

```csharp
{ 1, "Ana" }
```

means:

```csharp
students.Add(1, "Ana");
```

Access by key:

```csharp
Console.WriteLine(students[1]); // Ana
```

This means **key 1**, not position/index 1.

Safe lookup:

```csharp
if (students.TryGetValue(1, out string? name))
{
    Console.WriteLine(name);
}
else
{
    Console.WriteLine("Not found");
}
```

Add or update:

```csharp
students[4] = "Diana";
```

Add only if key is new:

```csharp
students.Add(5, "Eric");
```

Check:

```csharp
students.ContainsKey(1);
students.ContainsValue("Ana");
```

Remove:

```csharp
students.Remove(2);
```

Iterate:

```csharp
foreach (var pair in students)
{
    Console.WriteLine($"Key: {pair.Key}, Value: {pair.Value}");
}
```

Dictionary with object value:

```csharp
Dictionary<int, Student> studentMap = new()
{
    { 1, new Student { Id = 1, Name = "Ana", Course = "CS", GPA = 3.9 } },
    { 2, new Student { Id = 2, Name = "Ben", Course = "IT", GPA = 3.2 } }
};
```

[[#Navigation|⬆ Back to Navigation]]

---

## 29. HashSet, Queue, and Stack

### HashSet

A `HashSet` stores unique values.

```csharp
HashSet<string> tags = new()
{
    "csharp",
    "dotnet",
    "linq"
};
```

Add duplicate:

```csharp
tags.Add("csharp"); // ignored because already exists
```

Common methods:

```csharp
tags.Add("webapi");
tags.Contains("linq");
tags.Remove("dotnet");
int count = tags.Count;
```

Set operations:

```csharp
HashSet<int> a = new() { 1, 2, 3, 4 };
HashSet<int> b = new() { 3, 4, 5, 6 };

var union = a.Union(b).ToHashSet();
var common = a.Intersect(b).ToHashSet();
var onlyA = a.Except(b).ToHashSet();
```

Use `HashSet` when you need:

```text
unique values
fast Contains checks
no index positions
```

### Queue

First in, first out.

```csharp
Queue<string> queue = new();

queue.Enqueue("Ana");
queue.Enqueue("Ben");

string first = queue.Dequeue(); // Ana
```

### Stack

Last in, first out.

```csharp
Stack<string> stack = new();

stack.Push("Page 1");
stack.Push("Page 2");

string last = stack.Pop(); // Page 2
```

[[#Navigation|⬆ Back to Navigation]]

---

## 30. Choosing the Right Collection

| Need | Use |
|---|---|
| Fixed-size collection | Array |
| Dynamic ordered collection | List |
| Key-value lookup | Dictionary |
| Unique values only | HashSet |
| First in, first out | Queue |
| Last in, first out | Stack |
| Rectangular table/grid | 2D array |
| Rows with different sizes | Jagged array |

Memory trick:

```text
List       = position → value
Dictionary = key → value
HashSet    = unique values
Queue      = first in, first out
Stack      = last in, first out
```

[[#Navigation|⬆ Back to Navigation]]

---

## 31. LINQ Mental Model

LINQ lets you query collections.

```csharp
var honorStudents = students
    .Where(s => s.GPA >= 3.7)
    .OrderByDescending(s => s.GPA)
    .Select(s => s.Name)
    .ToList();
```

Read it as:

```text
Start with students.
Keep only GPA >= 3.7.
Sort highest GPA first.
Return only names.
Convert to list.
```

Most important methods:

| Method | Meaning |
|---|---|
| `Where` | filter |
| `Select` | transform |
| `SelectMany` | flatten |
| `OrderBy` | sort ascending |
| `OrderByDescending` | sort descending |
| `ThenBy` | secondary sort |
| `FirstOrDefault` | find first or null/default |
| `Any` | at least one exists |
| `All` | all match |
| `Count` | count |
| `Sum` | total |
| `Average` | average |
| `Min` / `Max` | smallest/largest |
| `MinBy` / `MaxBy` | item with smallest/largest property |
| `GroupBy` | group categories |
| `Skip` / `Take` | pagination |
| `Distinct` | remove duplicates |
| `ToList` | convert to list |
| `ToDictionary` | convert to dictionary |
| `ToHashSet` | convert to set |

[[#Navigation|⬆ Back to Navigation]]

---

## 32. Lambda Expressions

A lambda is an inline function.

```csharp
s => s.GPA >= 3.7
```

Read:

```text
For each student s, return whether GPA >= 3.7.
```

One parameter:

```csharp
s => s.Name
```

Two parameters:

```csharp
(a, b) => a + b
```

No parameter:

```csharp
() => DateTime.Now
```

Multiple statements:

```csharp
s =>
{
    double average = s.Grades.Average();
    return average >= 90;
}
```

In LINQ:

```csharp
students.Where(s => s.Course == "CS");
students.Select(s => s.Name);
students.OrderByDescending(s => s.GPA);
```

Meaning:

```text
Where needs true/false.
Select needs transformed value.
OrderBy needs sorting key.
```

[[#Navigation|⬆ Back to Navigation]]

---

## 33. LINQ with Arrays and Lists

Array example:

```csharp
int[] scores = { 90, 85, 72, 95, 88 };
```

Filter:

```csharp
var passing = scores.Where(s => s >= 75).ToArray();
```

Sort:

```csharp
var ranked = scores.OrderByDescending(s => s).ToArray();
```

Average:

```csharp
double average = scores.Average();
```

Check:

```csharp
bool hasPerfect = scores.Any(s => s == 100);
bool allPassed = scores.All(s => s >= 75);
```

Transform:

```csharp
var labels = scores
    .Select(s => s >= 75 ? "Passed" : "Failed")
    .ToArray();
```

List example:

```csharp
List<Student> students = new()
{
    new Student { Id = 1, Name = "Ana", Course = "CS", GPA = 3.9 },
    new Student { Id = 2, Name = "Ben", Course = "IT", GPA = 3.2 },
    new Student { Id = 3, Name = "Carlo", Course = "CS", GPA = 3.7 }
};
```

Filter by course:

```csharp
List<Student> csStudents = students
    .Where(s => s.Course == "CS")
    .ToList();
```

Names only:

```csharp
List<string> names = students
    .Select(s => s.Name)
    .ToList();
```

DTO-style shape:

```csharp
var result = students
    .Select(s => new
    {
        s.Id,
        s.Name,
        IsHonor = s.GPA >= 3.7
    })
    .ToList();
```

[[#Navigation|⬆ Back to Navigation]]

---

## 34. LINQ with Dictionaries

Dictionary example:

```csharp
Dictionary<int, Student> students = new()
{
    { 1, new Student { Id = 1, Name = "Ana", Course = "CS", GPA = 3.9 } },
    { 2, new Student { Id = 2, Name = "Ben", Course = "IT", GPA = 3.2 } },
    { 3, new Student { Id = 3, Name = "Carlo", Course = "CS", GPA = 3.7 } }
};
```

Each item is a pair:

```csharp
pair.Key
pair.Value
```

Use `.Values` when you only need students:

```csharp
var csStudents = students
    .Values
    .Where(s => s.Course == "CS")
    .ToList();
```

Use dictionary itself when you need key and value:

```csharp
var result = students
    .Where(pair => pair.Key > 1 && pair.Value.Course == "CS")
    .Select(pair => pair.Value)
    .ToList();
```

Get keys:

```csharp
List<int> ids = students.Keys.ToList();
```

Get values:

```csharp
List<Student> allStudents = students.Values.ToList();
```

Convert filtered result back to dictionary:

```csharp
Dictionary<int, Student> honors = students
    .Where(pair => pair.Value.GPA >= 3.7)
    .ToDictionary(pair => pair.Key, pair => pair.Value);
```

Important rule:

```text
Find by key → TryGetValue
Filter/sort/group by value → LINQ
```

Best key lookup:

```csharp
if (students.TryGetValue(1, out Student? student))
{
    Console.WriteLine(student.Name);
}
```

[[#Navigation|⬆ Back to Navigation]]

---

## 35. LINQ with HashSet, Matrices, and Nested Collections

### HashSet

```csharp
HashSet<string> courses = new()
{
    "CS",
    "IT",
    "IS"
};
```

Filter:

```csharp
var result = courses
    .Where(c => c.StartsWith("I"))
    .ToHashSet();
```

Unique courses from students:

```csharp
HashSet<string> uniqueCourses = students
    .Select(s => s.Course)
    .ToHashSet();
```

Set operations:

```csharp
var union = a.Union(b).ToHashSet();
var common = a.Intersect(b).ToHashSet();
var onlyA = a.Except(b).ToHashSet();
```

### Jagged array

```csharp
int[][] scores =
{
    new[] { 90, 85 },
    new[] { 72, 95, 88 },
    new[] { 100 }
};
```

Flatten:

```csharp
var allScores = scores
    .SelectMany(row => row)
    .ToList();
```

Passing only:

```csharp
var passing = scores
    .SelectMany(row => row)
    .Where(score => score >= 75)
    .ToList();
```

Average all:

```csharp
double average = scores
    .SelectMany(row => row)
    .Average();
```

### 2D array

```csharp
int[,] matrix =
{
    { 1, 2, 3 },
    { 4, 5, 6 }
};
```

2D arrays are less LINQ-friendly, but you can use `Cast`:

```csharp
int sum = matrix.Cast<int>().Sum();
int max = matrix.Cast<int>().Max();
var even = matrix.Cast<int>().Where(n => n % 2 == 0).ToList();
```

[[#Navigation|⬆ Back to Navigation]]

---

## 36. Where, Select, and SelectMany

### Where

Keeps items that match.

```csharp
var result = students
    .Where(s => s.Course == "CS")
    .ToList();
```

Multiple conditions:

```csharp
var result = students
    .Where(s => s.Course == "CS" && s.GPA >= 3.7)
    .ToList();
```

Search:

```csharp
var result = students
    .Where(s => s.Name.Contains("an", StringComparison.OrdinalIgnoreCase))
    .ToList();
```

### Select

Transforms each item.

```csharp
var names = students
    .Select(s => s.Name)
    .ToList();
```

Formatted strings:

```csharp
var labels = students
    .Select(s => $"[{s.Id}] {s.Name} - {s.Course}")
    .ToList();
```

With index:

```csharp
var ranked = students
    .OrderByDescending(s => s.GPA)
    .Select((s, index) => new
    {
        Rank = index + 1,
        s.Name,
        s.GPA
    })
    .ToList();
```

### SelectMany

Flattens nested collections.

```csharp
var allGrades = students
    .SelectMany(s => s.Grades)
    .ToList();
```

Memory:

```text
Select = transform
SelectMany = transform + flatten
```

[[#Navigation|⬆ Back to Navigation]]

---

## 37. Sorting, Finding, and Checking with LINQ

### Sorting

Ascending:

```csharp
var result = students
    .OrderBy(s => s.Name)
    .ToList();
```

Descending:

```csharp
var result = students
    .OrderByDescending(s => s.GPA)
    .ToList();
```

Secondary sort:

```csharp
var result = students
    .OrderBy(s => s.Course)
    .ThenByDescending(s => s.GPA)
    .ToList();
```

### Finding

```csharp
Student? student = students.FirstOrDefault(s => s.Id == 1);
```

If not found, class/reference types return `null`.

Check:

```csharp
if (student == null)
{
    Console.WriteLine("Not found");
}
```

Other find methods:

```csharp
students.First();
students.FirstOrDefault();
students.SingleOrDefault();
students.LastOrDefault();
students.ElementAtOrDefault(2);
```

### Any and All

```csharp
bool hasHonor = students.Any(s => s.GPA >= 3.7);
bool allPassed = students.All(s => s.GPA >= 2.0);
```

No failing students:

```csharp
bool noFailing = !students.Any(s => s.GPA < 2.0);
```

[[#Navigation|⬆ Back to Navigation]]

---

## 38. Aggregates, GroupBy, Pagination, and Distinct

### Count

```csharp
int count = students.Count();
int csCount = students.Count(s => s.Course == "CS");
```

### Sum, Average, Min, Max

```csharp
double totalGpa = students.Sum(s => s.GPA);
double average = students.Average(s => s.GPA);
double highest = students.Max(s => s.GPA);
double lowest = students.Min(s => s.GPA);
```

Average on empty collection can crash. Safe version:

```csharp
double average = students.Any()
    ? students.Average(s => s.GPA)
    : 0;
```

### MaxBy and MinBy

```csharp
Student? topStudent = students.MaxBy(s => s.GPA);
Student? lowestStudent = students.MinBy(s => s.GPA);
```

### GroupBy

Count by course:

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

Average by course:

```csharp
var result = students
    .GroupBy(s => s.Course)
    .Select(g => new
    {
        Course = g.Key,
        AverageGpa = g.Average(s => s.GPA)
    })
    .ToList();
```

### Pagination

```csharp
int page = 1;
int pageSize = 10;

var result = students
    .OrderBy(s => s.Name)
    .Skip((page - 1) * pageSize)
    .Take(pageSize)
    .ToList();
```

### Distinct and set-like LINQ

```csharp
var uniqueCourses = students
    .Select(s => s.Course)
    .Distinct()
    .ToList();
```

```csharp
var union = a.Union(b).ToList();
var common = a.Intersect(b).ToList();
var onlyA = a.Except(b).ToList();
```

[[#Navigation|⬆ Back to Navigation]]

---

## 39. LINQ Conversion and Common Mistakes

### Convert results

```csharp
List<Student> list = students.Where(s => s.GPA >= 3.7).ToList();
Student[] array = students.Where(s => s.GPA >= 3.7).ToArray();

Dictionary<int, Student> map = students.ToDictionary(s => s.Id, s => s);

HashSet<string> courses = students.Select(s => s.Course).ToHashSet();
```

### Lazy execution

Without `ToList()`, many LINQ queries are not executed immediately.

```csharp
var query = students.Where(s => s.GPA >= 3.7);
```

It runs when you iterate:

```csharp
foreach (var student in query)
{
    Console.WriteLine(student.Name);
}
```

Execute now:

```csharp
var result = students
    .Where(s => s.GPA >= 3.7)
    .ToList();
```

### Common mistakes

Wrong: using `First` when not sure item exists.

```csharp
var student = students.First(s => s.Id == 99); // can throw
```

Better:

```csharp
var student = students.FirstOrDefault(s => s.Id == 99);
```

Wrong: not checking null.

```csharp
Console.WriteLine(student.Name); // can crash
```

Correct:

```csharp
if (student != null)
{
    Console.WriteLine(student.Name);
}
```

Wrong: using LINQ for dictionary key lookup.

```csharp
var student = studentMap.FirstOrDefault(x => x.Key == id).Value;
```

Better:

```csharp
if (studentMap.TryGetValue(id, out var student))
{
    Console.WriteLine(student.Name);
}
```

[[#Navigation|⬆ Back to Navigation]]

---

## 40. Practice Student Model

Use this model for practice:

```csharp
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; } = string.Empty;
    public string Course { get; set; } = string.Empty;
    public double GPA { get; set; }
    public bool Enrolled { get; set; }
    public List<double> Grades { get; set; } = new();

    public double GetAverage()
    {
        return Grades.Count == 0 ? 0 : Grades.Average();
    }

    public bool IsHonor()
    {
        return GetAverage() >= 90;
    }

    public override string ToString()
    {
        return $"[{Id}] {Name} ({Course}) - GPA: {GPA:F2}";
    }
}
```

Sample data:

```csharp
List<Student> students = new()
{
    new Student { Id = 1, Name = "Ana Reyes", Course = "CS", GPA = 3.9, Enrolled = true, Grades = new() { 92, 95, 90 } },
    new Student { Id = 2, Name = "Ben Santos", Course = "IT", GPA = 3.2, Enrolled = true, Grades = new() { 85, 82, 88 } },
    new Student { Id = 3, Name = "Carlo Cruz", Course = "CS", GPA = 3.7, Enrolled = false, Grades = new() { 89, 91, 90 } },
    new Student { Id = 4, Name = "Diana Lim", Course = "IS", GPA = 3.8, Enrolled = true, Grades = new() { 94, 93, 96 } }
};
```

Practice queries:

```csharp
var honors = students.Where(s => s.GPA >= 3.7).ToList();

var ranked = students.OrderByDescending(s => s.GPA).ToList();

var names = students.Select(s => s.Name).ToList();

var countByCourse = students
    .GroupBy(s => s.Course)
    .Select(g => new { Course = g.Key, Count = g.Count() })
    .ToList();

var top = students.MaxBy(s => s.GPA);
```

[[#Navigation|⬆ Back to Navigation]]

---

## 41. Console Input and Menu Patterns

### Validate text input

```csharp
Console.Write("Enter name: ");
string name = Console.ReadLine() ?? string.Empty;

if (string.IsNullOrWhiteSpace(name))
{
    Console.WriteLine("Name is required.");
}
else
{
    name = name.Trim();
    Console.WriteLine($"Hello, {name}");
}
```

### Validate number input

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

### Repeat until valid

```csharp
int age;

while (true)
{
    Console.Write("Enter age: ");
    string? input = Console.ReadLine();

    if (int.TryParse(input, out age) && age >= 0)
    {
        break;
    }

    Console.WriteLine("Invalid age. Try again.");
}
```

### Simple menu

```csharp
List<string> books = new();

while (true)
{
    Console.WriteLine();
    Console.WriteLine("1. Add book");
    Console.WriteLine("2. View books");
    Console.WriteLine("3. Search book");
    Console.WriteLine("4. Exit");
    Console.Write("Choose: ");

    string choice = Console.ReadLine() ?? string.Empty;

    switch (choice)
    {
        case "1":
            Console.Write("Title: ");
            string title = Console.ReadLine() ?? string.Empty;

            if (string.IsNullOrWhiteSpace(title))
            {
                Console.WriteLine("Title is required.");
                break;
            }

            books.Add(title.Trim());
            Console.WriteLine("Book added.");
            break;

        case "2":
            foreach (string book in books)
            {
                Console.WriteLine($"- {book}");
            }
            break;

        case "3":
            Console.Write("Search: ");
            string search = Console.ReadLine() ?? string.Empty;

            var results = books
                .Where(b => b.Contains(search, StringComparison.OrdinalIgnoreCase))
                .ToList();

            foreach (string book in results)
            {
                Console.WriteLine($"- {book}");
            }
            break;

        case "4":
            return;

        default:
            Console.WriteLine("Invalid choice.");
            break;
    }
}
```

[[#Navigation|⬆ Back to Navigation]]

---

## 42. Quick Memorization Tables

### String methods

| Method | Use |
|---|---|
| `Trim()` | remove leading/trailing spaces |
| `ToUpper()` | uppercase |
| `ToLower()` | lowercase |
| `Contains()` | search inside text |
| `StartsWith()` | check beginning |
| `EndsWith()` | check ending |
| `IndexOf()` | find position |
| `Substring()` | cut part of string |
| `Replace()` | replace text |
| `Split()` | string to array |
| `Join()` | array/list to string |
| `IsNullOrEmpty()` | null or `""` |
| `IsNullOrWhiteSpace()` | null, `""`, or spaces |

### Char methods

| Method | Use |
|---|---|
| `char.IsLetter(c)` | letter |
| `char.IsDigit(c)` | digit |
| `char.IsLetterOrDigit(c)` | letter or digit |
| `char.IsWhiteSpace(c)` | space/tab/newline |
| `char.IsUpper(c)` | uppercase |
| `char.IsLower(c)` | lowercase |
| `char.ToUpper(c)` | uppercase conversion |
| `char.ToLower(c)` | lowercase conversion |

### Number conversion

| Task | Use |
|---|---|
| string to int safely | `int.TryParse(input, out int n)` |
| string to int directly | `int.Parse("123")` |
| int to string | `number.ToString()` |
| 2 decimals | `value.ToString("F2")` |
| money | `decimal` |
| normal decimals | `double` |
| whole numbers | `int` |

### LINQ

| LINQ | Meaning |
|---|---|
| `Where` | keep/filter |
| `Select` | transform |
| `SelectMany` | flatten |
| `OrderBy` | sort ascending |
| `OrderByDescending` | sort descending |
| `FirstOrDefault` | find one safely |
| `Any` | at least one |
| `All` | every item |
| `Count` | count |
| `Average` | average |
| `GroupBy` | categorize |
| `Skip` + `Take` | pagination |
| `Distinct` | remove duplicates |
| `ToList` | execute as list |
| `ToDictionary` | make dictionary |
| `ToHashSet` | make set |

### Study order

1. Variables, null, `?`, `!`, `??`
2. Strings and chars
3. Number conversions with `TryParse`
4. If, switch, loops
5. Methods
6. Classes, properties, constructors
7. Lists and dictionaries
8. HashSet
9. LINQ: `Where`, `Select`, `FirstOrDefault`, `Any`, `GroupBy`

[[#Navigation|⬆ Back to Navigation]]

---

