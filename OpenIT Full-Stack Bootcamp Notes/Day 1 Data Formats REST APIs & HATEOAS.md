---
title: "Day 1A Reviewer: Data Formats, REST APIs & HATEOAS"
aliases:
  - Day 1A REST Reviewer
  - Data Formats REST HATEOAS Reviewer
  - JSON XML REST Notes
tags:
  - bootcamp
  - rest-api
  - json
  - xml
  - http
  - hateoas
  - reviewer
source: "Day1 DataFormats REST.pdf"
created: 2026-05-04
---

# Day 1A Reviewer: Data Formats, REST APIs & HATEOAS

> [!summary]
> This reviewer covers **Data Serialization**, **JSON**, **XML**, **Schemas**, **HTTP Requests and Responses**, **REST API principles**, **Richardson Maturity Model Levels 0–3**, **Resource-Based Routing**, **Path vs Query Parameters**, and **HATEOAS**.

## Quick Navigation

- [[#1. Data Serialization]]
- [[#2. JSON — JavaScript Object Notation]]
- [[#3. JSON Schema — Validating JSON Data]]
- [[#4. XML — eXtensible Markup Language]]
- [[#5. XML Schema XSD]]
- [[#6. JSON vs XML]]
- [[#7. REST API Core Principles]]
- [[#8. HTTP Verbs and Resource Design]]
- [[#9. HTTP Request Anatomy]]
- [[#10. HTTP Request Headers]]
- [[#11. HTTP Response Headers and Structure]]
- [[#12. Richardson Maturity Model]]
- [[#13. Level 0 and Level 1 REST Examples]]
- [[#14. Level 2 — HTTP Verbs and Status Codes]]
- [[#15. HTTP Status Codes Reference]]
- [[#16. Path Parameters vs Query Parameters]]
- [[#17. Query Parameters in Depth]]
- [[#18. Resource-Based Routing]]
- [[#19. Deep Dive: `/books/1/authors/2`]]
- [[#20. HATEOAS — Level 3 REST]]
- [[#21. HATEOAS Client Navigation Flow]]
- [[#22. Practice Activities]]
- [[#23. Hands-On Lab Reviewer]]
- [[#24. Common Mistakes to Avoid]]
- [[#25. Quick Quiz]]
- [[#26. Day 1 Recap]]

---

# 1. Data Serialization

## What is Data Serialization?

**Data serialization** is the process of converting objects or structured data into a format that can be stored, transmitted, and later reconstructed.

In simple terms:

```text
Object/Data Structure → Bytes or Text → Sent/Stored → Converted Back to Object
```

## Serialize vs Deserialize

| Term | Meaning | Example |
|---|---|---|
| **Serialize** | Encode an object into text/bytes | JavaScript object → JSON string |
| **Deserialize** | Decode text/bytes back into an object | JSON string → JavaScript object |

## Why Serialization Matters

Serialization is important because it allows systems to exchange data even if they are built with different programming languages or run on different machines.

Common uses:

- Sending data over **HTTP APIs**
- Storing configuration files on disk
- Inter-process communication
- Cross-language data exchange
- Database input/output

## Common Data Formats

| Format | Description | Best Used For |
|---|---|---|
| **JSON** | Lightweight, web-native text format | REST APIs, web apps, configs |
| **XML** | Verbose, schema-driven markup format | Enterprise systems, SOAP, B2B |
| **YAML** | Human-friendly config format | Config files, DevOps tools |
| **Protobuf** | Binary, very fast format | High-performance services |
| **MessagePack** | Compact binary format | Efficient data transmission |

## Key Concepts

| Concept | Meaning |
|---|---|
| **Schema** | A structural contract that defines what data should look like |
| **Validation** | Checking if data follows the schema |
| **Versioning** | Keeping new data formats backward compatible |

> [!tip]
> Think of a **schema** like a form template. It defines what fields are required and what type of values are allowed.

---

# 2. JSON — JavaScript Object Notation

## What is JSON?

**JSON** stands for **JavaScript Object Notation**. It is a lightweight data format commonly used in REST APIs.

JSON is popular because it is:

- Easy to read
- Easy to parse in JavaScript
- Compact compared to XML
- Supported by many programming languages
- Commonly used for request and response bodies in web APIs

## JSON Data Types

| JSON Type | Example | Meaning |
|---|---|---|
| **String** | `"Hello World"` | Text value |
| **Number** | `42`, `3.14`, `-7` | Integer or decimal number |
| **Boolean** | `true`, `false` | Logical true/false value |
| **Null** | `null` | No value |
| **Array** | `[1, "a", true]` | Ordered list of values |
| **Object** | `{ "key": "value" }` | Key-value pair collection |

## Example JSON

```json
{
  "student": {
    "id": 101,
    "name": "Maria Santos",
    "enrolled": true,
    "grades": [88, 92, 95],
    "address": null
  }
}
```

## JSON Rules

- Data is written as **key-value pairs**.
- Keys must be wrapped in **double quotes**.
- Strings must use **double quotes**.
- Objects use `{ }`.
- Arrays use `[ ]`.
- JSON does **not** support comments natively.
- JSON can represent strings, numbers, booleans, null, arrays, and objects.

## JSON Example: Library Book

```json
{
  "id": 101,
  "title": "Clean Code",
  "authors": ["Robert C. Martin"],
  "published_year": 2008,
  "available": true,
  "genres": ["programming", "best-practices"],
  "publisher": {
    "name": "Prentice Hall",
    "city": "Upper Saddle River"
  }
}
```

> [!note]
> JSON is usually the preferred format for REST APIs because it is compact and easy for frontend apps to consume.

---

# 3. JSON Schema — Validating JSON Data

## What is JSON Schema?

**JSON Schema** defines and enforces the structure of JSON data. It acts as a contract between the client and server.

It can specify:

- Required fields
- Allowed data types
- String length limits
- Numeric ranges
- Regex patterns
- Allowed values
- Reusable sub-schemas

## Common JSON Schema Keywords

| Keyword | Meaning | Example |
|---|---|---|
| `type` | Data type constraint | `"type": "string"` |
| `required` | Required fields list | `"required": ["id", "name"]` |
| `properties` | Field definitions | Define each object property |
| `minLength` / `maxLength` | String length limits | Name must be 1–100 chars |
| `minimum` / `maximum` | Numeric bounds | Age must be 0–120 |
| `pattern` | Regex validation | Email format pattern |
| `enum` | Allowed values only | `"enum": ["fiction", "tech"]` |
| `$ref` | Reference to another schema | Reuse schema definitions |

## Example JSON Schema

```json
{
  "$schema": "https://json-schema.org/draft-07/schema",
  "type": "object",
  "required": ["id", "name"],
  "properties": {
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string",
      "minLength": 1,
      "maxLength": 100
    },
    "age": {
      "type": "integer",
      "minimum": 0,
      "maximum": 120
    },
    "email": {
      "type": "string",
      "pattern": "^[^@]+@[^@]+$"
    }
  }
}
```

## JSON Schema for Library Book

```json
{
  "$schema": "https://json-schema.org/draft-07/schema",
  "type": "object",
  "required": ["id", "title", "authors", "available"],
  "properties": {
    "id": {
      "type": "integer"
    },
    "title": {
      "type": "string",
      "minLength": 1
    },
    "authors": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1
    },
    "published_year": {
      "type": "integer",
      "minimum": 0
    },
    "available": {
      "type": "boolean"
    },
    "genres": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 2
    },
    "publisher": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string"
        },
        "city": {
          "type": "string"
        }
      }
    }
  }
}
```

> [!important]
> JSON Schema does not store the actual data. It validates whether a JSON object follows the required structure.

---

# 4. XML — eXtensible Markup Language

## What is XML?

**XML** stands for **eXtensible Markup Language**. It is a structured, tag-based format used to represent data.

XML is commonly used in:

- Enterprise systems
- SOAP APIs
- B2B integrations
- Configuration files
- Systems that require strict structure and schemas

## XML Example

```xml
<?xml version="1.0" encoding="UTF-8"?>
<library xmlns="http://example.com/lib">
  <book id="101" genre="tech">
    <title>Clean Code</title>
    <author>Robert C. Martin</author>
    <year>2008</year>
    <price currency="USD">35.99</price>
    <available>true</available>
    <tags>
      <tag>programming</tag>
      <tag>best-practices</tag>
    </tags>
  </book>
</library>
```

## XML Core Concepts

| Concept | Example | Meaning |
|---|---|---|
| **Element** | `<title>Clean Code</title>` | Tag with content |
| **Attribute** | `id="101"` | Metadata inside opening tag |
| **Root Element** | `<library>...</library>` | One top-level element only |
| **Namespace** | `xmlns="http://example.com/lib"` | Avoids naming conflicts |
| **CDATA** | `<![CDATA[raw text]]>` | Raw text block |
| **Declaration** | `<?xml version="1.0"?>` | XML version and encoding info |
| **Comment** | `<!-- comment here -->` | XML comment |
| **Encoding** | `UTF-8`, `UTF-16` | Character encoding |

## Elements vs Attributes

### Element

```xml
<title>Clean Code</title>
```

Use elements for the actual data/content.

### Attribute

```xml
<book id="101" genre="tech">
```

Use attributes for metadata or identifiers related to an element.

> [!tip]
> A simple rule: use **elements** for data that may contain text or nested structure. Use **attributes** for small metadata values like IDs, categories, or flags.

## XML Version of the Library Book

```xml
<?xml version="1.0" encoding="UTF-8"?>
<library xmlns="http://example.com/lib">
  <!-- Library book document -->
  <book id="101">
    <title>Clean Code</title>
    <author>Robert C. Martin</author>
    <published_year>2008</published_year>
    <available>true</available>
    <genres>
      <genre>programming</genre>
      <genre>best-practices</genre>
    </genres>
    <publisher>
      <name>Prentice Hall</name>
      <city>Upper Saddle River</city>
    </publisher>
  </book>
</library>
```

---

# 5. XML Schema XSD

## What is XSD?

**XSD** stands for **XML Schema Definition**. It defines and validates the structure of an XML document.

It can specify:

- Allowed elements
- Required and optional elements
- Element data types
- Element order
- Attributes
- Cardinality, or how many times an element can appear

## XSD Example

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="book">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="title" type="xs:string" minOccurs="1"/>
        <xs:element name="author" type="xs:string" minOccurs="1" maxOccurs="unbounded"/>
        <xs:element name="year" type="xs:integer" minOccurs="0"/>
      </xs:sequence>
      <xs:attribute name="id" type="xs:integer" use="required"/>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

## XSD Keywords

| Keyword | Meaning |
|---|---|
| `xs:element` | Defines an XML element with a name and type |
| `xs:complexType` | Defines an element that contains child elements or attributes |
| `xs:sequence` | Child elements must appear in the defined order |
| `minOccurs` | Minimum number of times an element may appear |
| `maxOccurs` | Maximum number of times an element may appear |
| `unbounded` | Allows any number of occurrences |
| `xs:attribute` | Defines an attribute on the parent element |
| `use="required"` | Makes the attribute required |

## Minimal XSD for a Book

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="book">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="title" type="xs:string" minOccurs="1"/>
        <xs:element name="year" type="xs:integer" minOccurs="0"/>
      </xs:sequence>
      <xs:attribute name="id" type="xs:integer" use="required"/>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

> [!warning]
> In XML Schema, order matters when using `xs:sequence`. If the XML elements appear in the wrong order, validation can fail.

---

# 6. JSON vs XML

## Side-by-Side Comparison

| Feature | JSON | XML |
|---|---|---|
| **Verbosity** | Compact, minimal syntax | Verbose, tag-heavy |
| **Readability** | Very easy for developers | Readable but wordy |
| **Schema** | JSON Schema, optional | XSD / DTD, strict |
| **Data Types** | String, Number, Boolean, Null, Array, Object | Everything is text unless schema defines type |
| **Comments** | Not natively supported | Supported using `<!-- comment -->` |
| **Browser Support** | Native `JSON.parse()` | `DOMParser`, XSLT |
| **Best For** | REST APIs, web apps, configs | Enterprise systems, SOAP, B2B |

## When to Use JSON

Use JSON when:

- Building REST APIs
- Working with JavaScript or frontend apps
- You want compact and readable data
- You need easy parsing in web applications
- You do not need strict document-style markup

## When to Use XML

Use XML when:

- Working with legacy or enterprise systems
- Using SOAP or B2B integrations
- Strict schema validation is required
- You need namespaces
- You need comments or document-like structure

> [!summary]
> JSON is usually better for modern web APIs. XML is still useful in enterprise systems where strict schemas, namespaces, and legacy compatibility matter.

---

# 7. REST API Core Principles

## What is REST?

**REST** stands for **Representational State Transfer**. It is an architectural style for designing networked applications, especially web APIs.

In REST, clients interact with **resources** through standard HTTP methods and URIs.

Example resource:

```text
/books/101
```

This represents a specific book.

## REST Core Principles

| Principle | Meaning |
|---|---|
| **Stateless** | Each request contains all information needed. No server-side session is required. |
| **Client–Server** | UI and data are separated. The client calls resources through URIs. |
| **Uniform Interface** | Uses standard HTTP verbs and resource URIs. |
| **Cacheable** | Responses declare if they can be cached to improve scalability. |
| **Layered System** | Client may not know if it talks directly to the final server or through a proxy/gateway. |
| **HATEOAS** | Responses include links that guide the client to next actions. |

## Stateless Explained

A REST API should not depend on stored server-side session state. Each request must include the information needed to process it, such as:

- Authentication token
- Request body
- Query parameters
- Headers
- Target resource URI

Example:

```http
GET /api/books/101 HTTP/1.1
Host: api.library.com
Authorization: Bearer <token>
Accept: application/json
```

The server can process the request because everything it needs is included.

> [!important]
> Stateless does not mean the database has no state. It means the server does not rely on hidden client session data between requests.

## Uniform Interface Explained

A uniform interface means APIs should use standard HTTP conventions:

```text
GET /books        → retrieve books
POST /books       → create a book
GET /books/101    → retrieve one book
PUT /books/101    → replace one book
PATCH /books/101  → partially update one book
DELETE /books/101 → delete one book
```

---

# 8. HTTP Verbs and Resource Design

## Main HTTP Verbs

| Verb | Action | Purpose | Example |
|---|---|---|---|
| **GET** | Read | Retrieve a resource or collection | `GET /books` or `GET /books/101` |
| **POST** | Create | Submit a new resource | `POST /books` |
| **PUT** | Replace | Full update or replacement | `PUT /books/101` |
| **PATCH** | Update | Partial update | `PATCH /books/101` |
| **DELETE** | Remove | Delete a resource | `DELETE /books/101` |

## GET

Use `GET` to retrieve data.

```http
GET /books HTTP/1.1
```

```http
GET /books/101 HTTP/1.1
```

Characteristics:

- Safe
- Idempotent
- Can be cached
- Should not change server state

## POST

Use `POST` to create a new resource.

```http
POST /books HTTP/1.1
Content-Type: application/json

{
  "title": "Clean Code",
  "author": "Robert C. Martin"
}
```

Characteristics:

- Not safe
- Not idempotent
- Calling it twice may create two resources

## PUT

Use `PUT` to fully replace a resource.

```http
PUT /books/101 HTTP/1.1
Content-Type: application/json

{
  "title": "Clean Code",
  "author": "Robert C. Martin",
  "year": 2008,
  "available": true
}
```

Characteristics:

- Idempotent
- Usually requires sending the full representation
- Same request repeated should result in the same final state

## PATCH

Use `PATCH` for partial updates.

```http
PATCH /books/101 HTTP/1.1
Content-Type: application/json

{
  "available": false
}
```

Characteristics:

- Usually not considered idempotent by default
- Only sends fields that need to change

## DELETE

Use `DELETE` to remove a resource.

```http
DELETE /books/101 HTTP/1.1
```

Characteristics:

- Idempotent
- The resource is gone after the first successful delete
- Repeating it may return `404 Not Found`, but the final outcome is still that the resource does not exist

---

# 9. HTTP Request Anatomy

## What is an HTTP Request?

An HTTP request is the message sent by the client to the server.

It contains:

1. Request line
2. Headers
3. Blank line
4. Optional body

## Full HTTP Request Example

```http
POST /api/books HTTP/1.1
Host: api.library.com
Content-Type: application/json
Accept: application/json
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Accept-Language: en-US
Cache-Control: no-cache
X-Request-ID: abc-123-def

{ "title": "Clean Code", "author": "Robert Martin", "year": 2008 }
```

## Request Parts

| Part | Meaning |
|---|---|
| **Request Line** | Method + path + HTTP version. Defines what action to perform and where. |
| **Headers** | Key-value metadata such as content type, auth token, accepted formats, and caching rules. |
| **Blank Line** | Mandatory separator between headers and body. |
| **Body** | Payload such as JSON, XML, or form data. Usually used with POST, PUT, and PATCH. |

## Request Line Breakdown

```http
POST /api/books HTTP/1.1
```

| Segment | Meaning |
|---|---|
| `POST` | HTTP method/action |
| `/api/books` | Target resource path |
| `HTTP/1.1` | HTTP version |

---

# 10. HTTP Request Headers

## What are Request Headers?

HTTP request headers are metadata that tell the server how to handle the request.

## Important Request Headers

| Header | Example | Meaning |
|---|---|---|
| `Content-Type` | `application/json` | Format of the request body being sent |
| `Accept` | `application/json, application/xml` | Response formats the client can accept |
| `Authorization` | `Bearer <JWT>` or `Basic <base64>` | Authentication credentials |
| `Host` | `api.library.com` | Target domain; required in HTTP/1.1 for virtual hosting |
| `User-Agent` | `Mozilla/5.0`, `PostmanRuntime/7.x` | Identifies client application |
| `Cache-Control` | `no-cache`, `max-age=3600` | Caching directives |
| `Accept-Language` | `en-US`, `tl` | Preferred language for content negotiation |
| `Accept-Encoding` | `gzip, deflate, br` | Compression formats the client accepts |
| `If-None-Match` | `"abc123etag"` | ETag from previous response for conditional GETs |
| `X-Request-ID` | `uuid-abc-123` | Custom tracing ID across services |

## Content-Type vs Accept

| Header | Direction | Meaning |
|---|---|---|
| `Content-Type` | Client → Server | “This is the format of the data I am sending.” |
| `Accept` | Client → Server | “This is the format I want to receive.” |

Example:

```http
POST /api/books HTTP/1.1
Content-Type: application/json
Accept: application/xml
```

This means the client sends JSON but is willing to receive XML.

## Authorization Header

Example JWT auth:

```http
Authorization: Bearer <token>
```

Example Basic auth:

```http
Authorization: Basic <base64>
```

> [!warning]
> Never expose real tokens, API keys, passwords, or credentials in public code or screenshots.

---

# 11. HTTP Response Headers and Structure

## What is an HTTP Response?

An HTTP response is the message sent by the server after processing a client request.

It contains:

1. Status line
2. Response headers
3. Blank line
4. Optional response body

## Full HTTP Response Example

```http
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
Location: /api/books/42
ETag: "abc123def456"
Cache-Control: no-store
X-RateLimit-Remaining: 98
Date: Sat, 03 May 2026 08:00:00 GMT

{ "id": 42, "title": "Clean Code", "available": true }
```

## Important Response Headers

| Header | Example | Meaning |
|---|---|---|
| `Content-Type` | `application/json; charset=utf-8` | Format and encoding of response body |
| `Location` | `/api/books/42` | URL of newly created resource after `201 Created` |
| `ETag` | `"abc123def456"` | Entity tag/checksum for cache validation |
| `Cache-Control` | `no-store`, `max-age=3600` | Tells the client how long to cache the response |
| `X-RateLimit-Remaining` | `98` | Custom header showing remaining API calls |
| `WWW-Authenticate` | `Bearer realm="api"` | On `401`, tells client required auth scheme |
| `Access-Control-Allow-Origin` | `*` or `https://app.com` | CORS header defining allowed origins |

## Status Line Breakdown

```http
HTTP/1.1 201 Created
```

| Segment | Meaning |
|---|---|
| `HTTP/1.1` | Protocol version |
| `201` | Status code |
| `Created` | Reason phrase |

---

# 12. Richardson Maturity Model

## What is the Richardson Maturity Model?

The **Richardson Maturity Model** measures how RESTful an API is. It has four levels: **0, 1, 2, and 3**.

Each level adds better structure and better use of HTTP.

## Levels Overview

| Level       | Name                 | Main Idea                                    |
| ----------- | -------------------- | -------------------------------------------- |
| **Level 0** | The Swamp of POX     | One endpoint, action defined in body         |
| **Level 1** | Resources            | Separate URL per resource, but poor verb use |
| **Level 2** | HTTP Verbs           | Uses correct HTTP verbs and status codes     |
| **Level 3** | Hypermedia / HATEOAS | Responses include links to next actions      |

## Level 0 — The Swamp of POX

POX means **Plain Old XML**, but the concept also applies to RPC-style APIs using JSON.

Characteristics:

- Single URL for everything
- Action is defined in the body
- HTTP is used only as a tunnel
- No proper HTTP semantics

Example:

```http
POST /api
Content-Type: application/json

{
  "action": "getBook",
  "id": 1
}
```

## Level 1 — Resources

Characteristics:

- Individual resources get their own URIs
- Better structure than Level 0
- Still often uses only POST
- Does not fully use HTTP verbs

Example:

```http
POST /api/books
Content-Type: application/json

{
  "action": "get",
  "id": 1
}
```

## Level 2 — HTTP Verbs

Characteristics:

- Uses correct HTTP methods
- Uses correct status codes
- Most public APIs stop here

Example:

```http
GET /api/books/1
```

## Level 3 — Hypermedia / HATEOAS

Characteristics:

- Responses carry links to next actions
- API is self-describing
- Client does not need hardcoded URLs
- True RESTful architecture

Example:

```json
{
  "id": 1,
  "title": "Clean Code",
  "_links": {
    "self": { "href": "/books/1", "method": "GET" },
    "borrow": { "href": "/books/1/borrow", "method": "POST" }
  }
}
```

---

# 13. Level 0 and Level 1 REST Examples

## Level 0 — Single Endpoint RPC Style

```http
POST /api
Content-Type: application/json

{
  "action": "getBook",
  "id": 1
}
```

```http
POST /api
Content-Type: application/json

{
  "action": "createBook",
  "title": "Clean Code"
}
```

```http
POST /api
Content-Type: application/json

{
  "action": "deleteBook",
  "id": 1
}
```

### Problems with Level 0

- No HTTP semantics used
- Cannot cache GET-like responses properly
- Not self-describing
- Action is buried inside the request body
- SOAP and XML-RPC-style APIs live here

## Level 1 — Resource URLs but Poor Verbs

```http
POST /api/books
Content-Type: application/json

{
  "action": "get",
  "id": 1
}
```

```http
POST /api/books
Content-Type: application/json

{
  "action": "list"
}
```

```http
POST /api/books
Content-Type: application/json

{
  "action": "create",
  "title": "Clean Code"
}
```

### Progress in Level 1

- Separate URL per resource
- Better than one endpoint for everything

### Remaining Problems

- Still misuses HTTP verbs
- No standard status codes
- Caching is still broken

> [!quote]
> Key idea: Level 0 and Level 1 APIs can work, but they ignore the power that HTTP gives for free, such as caching, semantics, and proxies.

---

# 14. Level 2 — HTTP Verbs and Status Codes

Level 2 REST uses the correct HTTP verb for the correct action and returns meaningful HTTP status codes.

## Level 2 in Practice

| Request | Successful Response | Possible Error |
|---|---|---|
| `GET /api/books` | `200 OK` + array of books | — |
| `GET /api/books/1` | `200 OK` + book object | `404 Not Found` |
| `POST /api/books` | `201 Created` + new book | `400 Bad Request` |
| `PUT /api/books/1` | `200 OK` + updated book | `404 Not Found` |
| `PATCH /api/books/1` | `200 OK` + patched book | — |
| `DELETE /api/books/1` | `204 No Content` | `404 Not Found` |

## Safe and Idempotent

| Verb | Safe? | Idempotent? | Explanation |
|---|---:|---:|---|
| `GET` | Yes | Yes | Retrieve only. Should not change server state. |
| `POST` | No | No | Creates a new resource. Repeating may create duplicates. |
| `PUT` | No | Yes | Full replacement. Same request repeated gives same result. |
| `PATCH` | No | Usually no | Partial update. Behavior depends on implementation. |
| `DELETE` | No | Yes | Resource is removed. Repeating keeps final state the same. |

## Safe vs Idempotent

### Safe

A method is **safe** if it does not change server state.

Example:

```http
GET /books/1
```

### Idempotent

A method is **idempotent** if repeating the same request results in the same final state.

Example:

```http
DELETE /books/1
DELETE /books/1
DELETE /books/1
```

Even if later calls return `404`, the final state is still the same: the book is gone.

---

# 15. HTTP Status Codes Reference

## 2xx — Success

| Status Code | Meaning | Use Case |
|---|---|---|
| `200 OK` | Request succeeded | GET succeeded, or PUT/PATCH updated |
| `201 Created` | Resource created | POST succeeded |
| `204 No Content` | Success, no body returned | DELETE succeeded |

## 3xx — Redirect / Caching

| Status Code | Meaning | Use Case |
|---|---|---|
| `301 Moved Permanently` | Resource has permanent new URL | Client should use new URL |
| `304 Not Modified` | Cached copy is still valid | ETag matched; use cached copy |

## 4xx — Client Error

| Status Code | Meaning | Use Case |
|---|---|---|
| `400 Bad Request` | Bad syntax or malformed request | Malformed JSON, validation failed |
| `401 Unauthorized` | No or invalid authentication | Missing/invalid auth token |
| `403 Forbidden` | Authenticated but not allowed | User lacks permission |
| `404 Not Found` | Resource does not exist | Wrong URI or missing record |
| `405 Method Not Allowed` | HTTP verb not supported on this URL | `POST /books/1` when only GET/PUT/PATCH/DELETE allowed |
| `409 Conflict` | Resource or state conflict | Duplicate resource, conflicting update |
| `422 Unprocessable Entity` | Request body is syntactically valid but semantically invalid | Invalid business rule, e.g. rating above max |

## 5xx — Server Error

| Status Code | Meaning | Use Case |
|---|---|---|
| `500 Internal Server Error` | Unhandled exception on server | Unexpected server-side error |
| `503 Service Unavailable` | Server unavailable | Server down or overloaded |

## Status Code Tips

- Use `201 Created` when a new resource is created.
- Use `204 No Content` when deletion succeeds and no response body is needed.
- Use `400 Bad Request` for malformed input.
- Use `401 Unauthorized` when authentication is missing or invalid.
- Use `403 Forbidden` when the user is authenticated but not allowed.
- Use `404 Not Found` when the resource does not exist.
- Use `422 Unprocessable Entity` when the data is valid JSON but violates business rules.

---

# 16. Path Parameters vs Query Parameters

## Main Difference

| Parameter Type | Example | Purpose |
|---|---|---|
| **Path Parameter** | `/books/1` | Identifies a specific resource |
| **Query Parameter** | `/books?id=1` | Filters, searches, sorts, or paginates a collection |

## Path Parameter Example

```http
GET /api/books/1
GET /api/authors/42
GET /api/users/99/orders/7
```

The value is part of the path itself. It identifies the target resource.

## Query Parameter Example

```http
GET /api/books?id=1
GET /api/books?genre=fiction&available=true
GET /api/books?search=clean&sort=year&page=2
```

The value appears after `?`. Query parameters modify how a collection is retrieved.

## `/books/1` vs `/books?id=1`

| Aspect | `/books/1` Path | `/books?id=1` Query |
|---|---|---|
| **Purpose** | Identify a specific resource | Filter/search/sort/paginate a collection |
| **RESTful use** | Preferred for single resource identity | Fine for optional collection modifiers |
| **Required?** | Yes; missing it changes the route | No; optional, server may set defaults |
| **Cacheability** | Excellent, URL is unique per resource | Varies; each query combo is treated differently |
| **Example** | `/books/1`, `/users/42`, `/orders/7` | `/books?genre=fiction&sort=title&page=2` |
| **Looks RESTful?** | Clean and hierarchical | Less clean for single resource, but OK for filters |

## Rule of Thumb

> [!important]
> **Path parameters identify a resource. Query parameters modify how you retrieve a collection.**

---

# 17. Query Parameters in Depth

## Query Parameter Anatomy

```text
https://api.library.com/books?genre=fiction&available=true&sort=year&order=desc&page=2&size=10
```

Breakdown:

| Part | Meaning |
|---|---|
| `?` | Marks the start of the query string |
| `genre=fiction` | Key-value pair |
| `&` | Separates key-value pairs |
| `sort=year` | Sort by year |
| `order=desc` | Descending order |
| `page=2&size=10` | Pagination settings |

## Filtering

```http
GET /books?genre=fiction
GET /books?available=true
GET /books?year=2020
GET /books?author=Martin
```

Filtering narrows down the collection.

## Searching

```http
GET /books?search=clean+code
GET /books?q=robert+martin
GET /books?title=pragmatic
```

Searching looks for a keyword or text match.

## Sorting

```http
GET /books?sort=title&order=asc
GET /books?sort=year&order=desc
GET /books?sortBy=author
```

Sorting changes the order of returned results.

## Pagination

```http
GET /books?page=2&size=10
GET /books?offset=20&limit=10
GET /books?cursor=abc123
```

Pagination splits large results into smaller pages.

## Page-Based vs Offset-Based vs Cursor-Based Pagination

| Type | Example | Best For |
|---|---|---|
| Page-based | `?page=2&size=10` | Simple UI pages |
| Offset-based | `?offset=20&limit=10` | SQL-style result offsets |
| Cursor-based | `?cursor=abc123` | Large or constantly changing datasets |

---

# 18. Resource-Based Routing

## What is Resource-Based Routing?

Resource-based routing means designing URLs around **nouns/resources**, not verbs/actions.

Good REST URLs should read like objects or collections:

```text
/books
/books/1
/books/1/authors
/books/1/reviews
```

They should not read like commands:

```text
/getBooks
/createAuthor
/deleteBook
```

## Resource URL Patterns

| Endpoint | Meaning |
|---|---|
| `GET /books` | All books collection |
| `GET /books/1` | Book with id `1` |
| `GET /books/1/authors` | All authors of book `1` |
| `GET /books/1/authors/2` | Author `2` of book `1` |
| `GET /books/1/reviews` | All reviews for book `1` |
| `GET /books/1/reviews/5` | Review `5` on book `1` |
| `POST /books/1/reviews` | Add a review to book `1` |
| `GET /authors/2/books` | All books written by author `2` |
| `GET /libraries/3/books?available=true` | Available books in library `3` |

## Resource Routing Rules

| Rule | Good | Bad |
|---|---|---|
| Use nouns for resources | `/books`, `/authors`, `/loans` | `/getBooks`, `/createAuthor`, `/deleteBook` |
| Use plural for collections | `/books`, `/users`, `/orders` | `/book`, `/user`, `/order` |
| Nest to show relationships | `/books/1/authors` | `/getAuthorsOfBook?bookId=1` |
| Keep nesting shallow | `/books/1/reviews` | `/books/1/chapters/3/paragraphs/7/words` |

## Good Endpoint Design

```http
GET /books
GET /books/1
POST /books
PUT /books/1
PATCH /books/1
DELETE /books/1
GET /books/1/authors
GET /books/1/reviews
POST /books/1/reviews
```

## Bad Endpoint Design

```http
GET /getBooks
POST /createBook
POST /deleteBook
GET /getAuthorsOfBook?bookId=1
```

> [!tip]
> Let the HTTP verb describe the action. Let the URL describe the resource.

---

# 19. Deep Dive: `/books/1/authors/2`

## Reading the URL Step by Step

```text
/ books / 1 / authors / 2
```

| Segment | Meaning |
|---|---|
| `/books` | Collection of all books |
| `/1` | Specific book with id `1` |
| `/authors` | Sub-collection: authors of that book |
| `/2` | Specific author with id `2` |

## Valid Routes for This Structure

| Endpoint | Meaning |
|---|---|
| `GET /books` | All books |
| `GET /books/1` | Book 1 |
| `GET /books/1/authors` | All authors of book 1 |
| `GET /books/1/authors/2` | Author 2 of book 1 |
| `POST /books/1/authors` | Add an author to book 1 |
| `PUT /books/1/authors/2` | Update author 2 of book 1 |
| `DELETE /books/1/authors/2` | Remove author 2 from book 1 |

## Response Example

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 2,
  "fullName": "Robert C. Martin",
  "nationality": "American",
  "_links": {
    "self": { "href": "/books/1/authors/2" },
    "book": { "href": "/books/1" },
    "allBooks": { "href": "/authors/2/books" }
  }
}
```

## Why This Route is RESTful

It is RESTful because:

- It uses nouns, not verbs.
- It shows resource hierarchy.
- It identifies a specific nested resource.
- It can work with standard HTTP verbs.
- It is readable and predictable.

---

# 20. HATEOAS — Level 3 REST

## What is HATEOAS?

**HATEOAS** means **Hypermedia As The Engine Of Application State**.

In HATEOAS, API responses include links that tell the client what it can do next.

The client starts at a known entry point and discovers other actions by following links in responses.

## Main Idea

Without HATEOAS, a client may hardcode URLs:

```text
Client manually builds /books/1/borrow
```

With HATEOAS, the client follows a link given by the server:

```json
"borrow": {
  "href": "/books/1/borrow",
  "method": "POST"
}
```

## HATEOAS Response Example

```http
HTTP/1.1 200 OK
Content-Type: application/hal+json

{
  "id": 1,
  "title": "Clean Code",
  "available": true,
  "genre": "Programming",
  "_links": {
    "self": {
      "href": "/books/1",
      "method": "GET"
    },
    "update": {
      "href": "/books/1",
      "method": "PUT"
    },
    "delete": {
      "href": "/books/1",
      "method": "DELETE"
    },
    "borrow": {
      "href": "/books/1/borrow",
      "method": "POST"
    },
    "reviews": {
      "href": "/books/1/reviews",
      "method": "GET"
    },
    "authors": {
      "href": "/books/1/authors",
      "method": "GET"
    },
    "collection": {
      "href": "/books",
      "method": "GET"
    }
  }
}
```

## Why HATEOAS Matters

| Feature | Meaning |
|---|---|
| **Self link** | Always present; canonical URL of the resource itself |
| **Conditional links** | Show links only when valid, such as `borrow` only if `available === true` |
| **Method hints** | Tell the client which HTTP verb to use |
| **Standard formats** | HAL, Siren, and JSON:API can standardize link structure |
| **No hardcoding** | Client follows links instead of building URLs manually |
| **Self-documenting API** | API tells the client what it can do next |

## Conditional Link Example

If a book is available:

```json
{
  "available": true,
  "_links": {
    "borrow": {
      "href": "/books/1/borrow",
      "method": "POST"
    }
  }
}
```

If a book is not available:

```json
{
  "available": false,
  "_links": {
    "self": {
      "href": "/books/1",
      "method": "GET"
    }
  }
}
```

The `borrow` link disappears because the action is not currently allowed.

---

# 21. HATEOAS Client Navigation Flow

A HATEOAS client follows links like browsing a website.

## Step 1: Entry Point

```http
GET /api
```

Response:

```json
{
  "_links": {
    "books": "/books",
    "authors": "/authors"
  }
}
```

## Step 2: Browse Books

The client follows the `books` link.

```http
GET /books
```

Response:

```json
{
  "items": [
    {
      "id": 1,
      "title": "Clean Code",
      "_links": {
        "self": "/books/1"
      }
    }
  ],
  "_links": {
    "next": "/books?page=2"
  }
}
```

## Step 3: Select Book

The client follows the item `self` link.

```http
GET /books/1
```

Response:

```json
{
  "id": 1,
  "title": "Clean Code",
  "available": true,
  "_links": {
    "borrow": "/books/1/borrow"
  }
}
```

## Step 4: Take Action

The client follows the `borrow` link.

```http
POST /books/1/borrow
```

Response:

```json
{
  "loanId": 99,
  "dueDate": "2026-06-01"
}
```

> [!summary]
> HATEOAS reduces hardcoded URLs because the server guides the client through links.

---

# 22. Practice Activities

## Activity 1: JSON Modeling — Library Book

Create a JSON object for a library book with these fields:

- `id` integer
- `title` string
- `authors` array of strings
- `published_year` integer
- `available` boolean
- `genres` array of strings, at least 2
- `publisher` object with `name` and `city`

### Sample Answer

```json
{
  "id": 101,
  "title": "Clean Code",
  "authors": ["Robert C. Martin"],
  "published_year": 2008,
  "available": true,
  "genres": ["programming", "software engineering"],
  "publisher": {
    "name": "Prentice Hall",
    "city": "Upper Saddle River"
  }
}
```

## Activity 2: XML Structuring

Convert the JSON book into XML.

### Sample Answer

```xml
<?xml version="1.0" encoding="UTF-8"?>
<library xmlns="http://example.com/lib">
  <!-- Library book record -->
  <book id="101">
    <title>Clean Code</title>
    <author>Robert C. Martin</author>
    <published_year>2008</published_year>
    <available>true</available>
    <genres>
      <genre>programming</genre>
      <genre>software engineering</genre>
    </genres>
    <publisher>
      <name>Prentice Hall</name>
      <city>Upper Saddle River</city>
    </publisher>
  </book>
</library>
```

## Activity 3: Movie Watchlist REST API

Scenario: Build a REST API for a movie watchlist.

Fields:

- `title`
- `year`
- `genre`
- `watched`
- `rating`

### Level 2 Endpoints

| Endpoint | Purpose | Success Code |
|---|---|---|
| `GET /movies` | Get all movies | `200 OK` |
| `GET /movies/{id}` | Get one movie | `200 OK` or `404 Not Found` |
| `POST /movies` | Create movie | `201 Created` |
| `PUT /movies/{id}` | Replace movie | `200 OK` or `404 Not Found` |
| `PATCH /movies/{id}` | Partially update movie | `200 OK` or `404 Not Found` |
| `DELETE /movies/{id}` | Delete movie | `204 No Content` or `404 Not Found` |
| `GET /movies/{id}/reviews` | Get movie reviews | `200 OK` or `404 Not Found` |

### Query Parameters for `GET /movies`

```http
GET /movies?genre=action&watched=false&sort=rating&order=desc&page=1&size=5
```

| Query Param | Purpose |
|---|---|
| `genre=action` | Filter by genre |
| `watched=false` | Filter by watched status |
| `sort=rating` | Sort by rating |
| `order=desc` | Descending order |
| `page=1` | Page number |
| `size=5` | Results per page |

### `GET /movies/5` vs `GET /movies?id=5`

| Endpoint | Use When |
|---|---|
| `GET /movies/5` | You want the specific movie resource with id 5. Preferred RESTful style. |
| `GET /movies?id=5` | You are filtering the movies collection by id. Less ideal for single-resource identity. |

### HATEOAS Links for `GET /movies/{id}`

```json
{
  "id": 5,
  "title": "Inception",
  "year": 2010,
  "genre": "sci-fi",
  "watched": false,
  "rating": 4.8,
  "_links": {
    "self": {
      "href": "/movies/5",
      "method": "GET"
    },
    "collection": {
      "href": "/movies",
      "method": "GET"
    },
    "update": {
      "href": "/movies/5",
      "method": "PUT"
    },
    "partialUpdate": {
      "href": "/movies/5",
      "method": "PATCH"
    },
    "delete": {
      "href": "/movies/5",
      "method": "DELETE"
    },
    "reviews": {
      "href": "/movies/5/reviews",
      "method": "GET"
    }
  }
}
```

### Status Codes for Activity

| Situation | Status Code |
|---|---|
| Successful creation | `201 Created` |
| Resource not found | `404 Not Found` |
| Validation error | `400 Bad Request` or `422 Unprocessable Entity` |
| Successful delete | `204 No Content` |

---

# 23. Hands-On Lab Reviewer

## Lab Theme

**Library Management System — REST API Design to HATEOAS**

## Part 1 — JSON and XML

Tasks:

- Create `books.json` with at least 5 books.
- Write a JSON Schema.
- Convert to `books.xml`.
- Create an XSD.
- Parse and filter books by genre.

### Example `books.json`

```json
[
  {
    "id": 1,
    "title": "Clean Code",
    "authors": ["Robert C. Martin"],
    "genre": "programming",
    "published_year": 2008,
    "available": true
  },
  {
    "id": 2,
    "title": "The Pragmatic Programmer",
    "authors": ["Andrew Hunt", "David Thomas"],
    "genre": "programming",
    "published_year": 1999,
    "available": true
  },
  {
    "id": 3,
    "title": "1984",
    "authors": ["George Orwell"],
    "genre": "fiction",
    "published_year": 1949,
    "available": false
  },
  {
    "id": 4,
    "title": "Animal Farm",
    "authors": ["George Orwell"],
    "genre": "fiction",
    "published_year": 1945,
    "available": true
  },
  {
    "id": 5,
    "title": "Design Patterns",
    "authors": ["Erich Gamma", "Richard Helm", "Ralph Johnson", "John Vlissides"],
    "genre": "software engineering",
    "published_year": 1994,
    "available": true
  }
]
```

## Part 2 — REST API Design

Design `/api/books` with at least 8 endpoints.

| Endpoint | Purpose |
|---|---|
| `GET /api/books` | List books |
| `GET /api/books/{id}` | Get one book |
| `POST /api/books` | Create a book |
| `PUT /api/books/{id}` | Replace a book |
| `PATCH /api/books/{id}` | Partially update a book |
| `DELETE /api/books/{id}` | Delete a book |
| `GET /api/books/{id}/authors` | Get authors of a book |
| `GET /api/books/{id}/authors/{aid}` | Get one author of a book |
| `POST /api/books/{id}/authors` | Add author to a book |
| `DELETE /api/books/{id}/authors/{aid}` | Remove author from a book |
| `POST /api/books/{id}/borrow` | Borrow a book |
| `POST /api/books/{id}/return` | Return a book |

## Query Parameters for `GET /api/books`

```http
GET /api/books?genre=programming&available=true&author=Martin&sort=year&order=desc&page=1&size=10
```

| Query Param | Purpose |
|---|---|
| `genre` | Filter by genre |
| `available` | Filter by availability |
| `author` | Filter by author |
| `search` or `q` | Search by title/author |
| `sort` | Field to sort by |
| `order` | `asc` or `desc` |
| `page` | Page number |
| `size` | Results per page |
| `cursor` | Cursor-based pagination token |

## Part 3 — Headers and Status Codes

### Recommended Request Headers

| Header | Use |
|---|---|
| `Content-Type: application/json` | For requests with JSON body |
| `Accept: application/json` | Client expects JSON response |
| `Authorization: Bearer <token>` | Authenticated requests |
| `X-Request-ID: <uuid>` | Request tracing |

### Endpoint Status Code Guide

| Endpoint | Success | Possible Errors |
|---|---|---|
| `GET /api/books` | `200 OK` | — |
| `GET /api/books/{id}` | `200 OK` | `404 Not Found` |
| `POST /api/books` | `201 Created` | `400 Bad Request`, `422 Unprocessable Entity`, `409 Conflict` |
| `PUT /api/books/{id}` | `200 OK` | `400 Bad Request`, `404 Not Found`, `422 Unprocessable Entity` |
| `PATCH /api/books/{id}` | `200 OK` | `400 Bad Request`, `404 Not Found`, `422 Unprocessable Entity` |
| `DELETE /api/books/{id}` | `204 No Content` | `404 Not Found` |
| `GET /api/books/{id}/authors` | `200 OK` | `404 Not Found` |
| `POST /api/books/{id}/borrow` | `201 Created` or `200 OK` | `404 Not Found`, `409 Conflict`, `422 Unprocessable Entity` |

## Part 4 — HATEOAS

Add `_links` to all responses.

### Entry Point

```http
GET /api
```

```json
{
  "_links": {
    "books": {
      "href": "/api/books",
      "method": "GET"
    },
    "authors": {
      "href": "/api/authors",
      "method": "GET"
    }
  }
}
```

### Book Response with HATEOAS

```json
{
  "id": 1,
  "title": "Clean Code",
  "available": true,
  "_links": {
    "self": {
      "href": "/api/books/1",
      "method": "GET"
    },
    "collection": {
      "href": "/api/books",
      "method": "GET"
    },
    "authors": {
      "href": "/api/books/1/authors",
      "method": "GET"
    },
    "borrow": {
      "href": "/api/books/1/borrow",
      "method": "POST"
    },
    "update": {
      "href": "/api/books/1",
      "method": "PUT"
    },
    "delete": {
      "href": "/api/books/1",
      "method": "DELETE"
    }
  }
}
```

### Navigation Flow

```text
GET /api
  → follow books link
GET /api/books
  → follow item self link
GET /api/books/1
  → follow borrow link
POST /api/books/1/borrow
```

---

# 24. Common Mistakes to Avoid

## JSON Mistakes

- Using single quotes instead of double quotes
- Forgetting commas between fields
- Adding comments inside JSON
- Mixing up arrays and objects
- Forgetting that `null` is different from an empty string

## XML Mistakes

- Missing one root element
- Forgetting closing tags
- Incorrect nesting
- Misusing attributes for large content
- Not matching XSD element order

## REST Design Mistakes

- Using verbs in URLs, like `/getBooks`
- Using `POST` for every action
- Using query parameters for required resource identity
- Deeply nesting URLs too much
- Returning `200 OK` for every situation
- Not using `201 Created` after creation
- Not using `404 Not Found` when a resource does not exist
- Hardcoding URLs in clients when HATEOAS links are available

## HTTP Header Mistakes

- Confusing `Content-Type` and `Accept`
- Forgetting `Authorization` for protected endpoints
- Sending a body with `GET` requests
- Not setting `Content-Type` for JSON request bodies
- Exposing real tokens in screenshots or logs

---

# 25. Quick Quiz

## Multiple Choice

### 1. What does JSON stand for?

A. Java Source Object Notation  
B. JavaScript Object Notation  
C. JavaScript Online Network  
D. Java Standard Object Naming  

**Answer:** B

### 2. Which JSON value represents no value?

A. `undefined`  
B. `none`  
C. `null`  
D. `empty`  

**Answer:** C

### 3. Which HTTP method is used to retrieve data?

A. POST  
B. PUT  
C. GET  
D. DELETE  

**Answer:** C

### 4. Which HTTP method is usually used for partial updates?

A. PATCH  
B. GET  
C. POST  
D. OPTIONS  

**Answer:** A

### 5. What status code is commonly returned after successful creation?

A. 200 OK  
B. 201 Created  
C. 204 No Content  
D. 404 Not Found  

**Answer:** B

### 6. What status code means a resource does not exist?

A. 400 Bad Request  
B. 401 Unauthorized  
C. 403 Forbidden  
D. 404 Not Found  

**Answer:** D

### 7. Which is the most RESTful endpoint for getting book 5?

A. `/getBook?id=5`  
B. `/books?id=5`  
C. `/books/5`  
D. `/api?action=getBook&id=5`  

**Answer:** C

### 8. What does HATEOAS provide?

A. Database indexing  
B. Hypermedia links for next actions  
C. Password encryption  
D. XML-only validation  

**Answer:** B

### 9. Which Richardson level uses correct HTTP verbs and status codes?

A. Level 0  
B. Level 1  
C. Level 2  
D. Level 3 only  

**Answer:** C

### 10. Which Richardson level includes hypermedia links?

A. Level 0  
B. Level 1  
C. Level 2  
D. Level 3  

**Answer:** D

## Short Answer

### 1. Difference between `Content-Type` and `Accept`?

**Answer:** `Content-Type` describes the format of the request body being sent. `Accept` describes the response formats the client is willing to receive.

### 2. Difference between path and query parameters?

**Answer:** Path parameters identify a specific resource, while query parameters filter, search, sort, or paginate a collection.

### 3. Why is `GET` considered safe?

**Answer:** Because it should only retrieve data and should not change server state.

### 4. Why is `PUT` idempotent?

**Answer:** Because sending the same full replacement request multiple times should result in the same final resource state.

### 5. Why should REST URLs use nouns instead of verbs?

**Answer:** The URL should identify the resource, while the HTTP method should describe the action.

---

# 26. Day 1 Recap

> [!summary]
> Day 1 focused on how data is represented, validated, transmitted, and exposed through REST APIs.

## Big Picture

Today’s topics connect like this:

```text
Data Formats → Schemas → HTTP Messages → REST Design → HATEOAS
```

You first learned how data can be represented using **JSON** and **XML**. Then you learned how to validate those formats using **JSON Schema** and **XSD**. After that, you moved into how this data travels through **HTTP requests and responses**. Finally, you learned how to design RESTful APIs using proper resources, verbs, status codes, routing, query parameters, and HATEOAS links.

## Main Takeaways

### 1. Serialization converts data for storage or transmission

Objects must be converted into text or bytes before they can be sent over APIs, stored in files, or exchanged across systems.

```text
Serialize: object → text/bytes
Deserialize: text/bytes → object
```

### 2. JSON is the common format for REST APIs

JSON is compact, readable, and easy for web applications to parse.

Important JSON types:

- String
- Number
- Boolean
- Null
- Array
- Object

### 3. JSON Schema validates JSON structure

JSON Schema defines required fields, data types, length limits, numeric bounds, patterns, enums, and references.

Use JSON Schema when you want to enforce that incoming JSON follows a contract.

### 4. XML is structured and schema-driven

XML uses tags, attributes, namespaces, root elements, and declarations. It is more verbose than JSON but still important in enterprise, SOAP, and B2B systems.

### 5. XSD validates XML structure

XSD defines allowed XML elements, attributes, types, order, and cardinality.

Key XSD terms:

- `xs:element`
- `xs:complexType`
- `xs:sequence`
- `minOccurs`
- `maxOccurs`
- `xs:attribute`

### 6. HTTP requests have a clear structure

An HTTP request contains:

1. Request line
2. Headers
3. Blank line
4. Optional body

Example:

```http
POST /api/books HTTP/1.1
Content-Type: application/json
Accept: application/json

{ "title": "Clean Code" }
```

### 7. HTTP responses return status, headers, and body

A response contains a status line, headers, and sometimes a body.

Example:

```http
HTTP/1.1 201 Created
Location: /api/books/42
Content-Type: application/json

{ "id": 42, "title": "Clean Code" }
```

### 8. REST APIs are resource-based

RESTful URLs should use nouns:

```text
/books
/books/1
/books/1/authors
```

Avoid verb-based URLs:

```text
/getBooks
/createBook
/deleteBook
```

### 9. HTTP verbs define the action

| Verb | Purpose |
|---|---|
| `GET` | Retrieve |
| `POST` | Create |
| `PUT` | Replace |
| `PATCH` | Partially update |
| `DELETE` | Remove |

### 10. Status codes communicate results

| Code | Meaning |
|---|---|
| `200 OK` | Successful request |
| `201 Created` | Resource created |
| `204 No Content` | Success with no body |
| `400 Bad Request` | Invalid request |
| `401 Unauthorized` | Missing/invalid auth |
| `403 Forbidden` | No permission |
| `404 Not Found` | Resource missing |
| `409 Conflict` | State conflict |
| `422 Unprocessable Entity` | Semantic validation error |
| `500 Internal Server Error` | Server failure |

### 11. Path parameters identify resources

Use path parameters when the value identifies a specific resource.

```http
GET /books/1
```

### 12. Query parameters modify collections

Use query parameters for filtering, searching, sorting, and pagination.

```http
GET /books?genre=fiction&sort=year&page=2
```

### 13. Richardson Maturity Model shows RESTfulness

| Level | Description |
|---|---|
| Level 0 | One endpoint, action in body |
| Level 1 | Resource URLs, poor verb use |
| Level 2 | Correct HTTP verbs and status codes |
| Level 3 | HATEOAS links guide next actions |

### 14. HATEOAS makes APIs discoverable

HATEOAS responses include `_links` so clients can follow actions instead of hardcoding URLs.

```json
{
  "id": 1,
  "title": "Clean Code",
  "_links": {
    "self": { "href": "/books/1", "method": "GET" },
    "borrow": { "href": "/books/1/borrow", "method": "POST" }
  }
}
```

## Final Memory Aid

```text
JSON = lightweight API data
XML = structured enterprise data
Schema = validation contract
HTTP = message protocol
REST = resource-oriented API style
Verb = action
Status code = result
Path param = resource identity
Query param = collection modifier
HATEOAS = links to next actions
```

## One-Minute Review

- Use **JSON** for most REST API data.
- Use **XML** when strict enterprise-style structure is required.
- Use **schemas** to validate data.
- Use **GET** to retrieve, **POST** to create, **PUT** to replace, **PATCH** to update partially, and **DELETE** to remove.
- Use **path parameters** for specific resources.
- Use **query parameters** for filtering, searching, sorting, and pagination.
- Use correct **HTTP status codes** instead of always returning `200 OK`.
- Use **HATEOAS** links when you want a self-describing API.

## What to Practice Next

- Create sample JSON objects and validate them with JSON Schema.
- Convert JSON to XML and write an XSD.
- Design REST endpoints for a simple system such as books, movies, students, products, or tasks.
- For every endpoint, write the HTTP method, path, request headers, possible response codes, and HATEOAS links.

