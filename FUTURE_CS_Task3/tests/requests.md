# Task 3 – API Testing Record

## API Under Test

**API Name:** JSONPlaceholder

**Base URL:** https://jsonplaceholder.typicode.com

**API Type:** Public fake REST API for testing and prototyping

**Authentication Required:** No API key or account required

**Official Documentation:** https://jsonplaceholder.typicode.com

---

## Testing Scope

Testing is limited to safe, read-only HTTP GET requests and inspection
of request/response behavior.

No authentication bypass, authorization bypass, destructive operation,
flooding, denial-of-service testing, or malicious payload testing is
performed.

---

## Test Environment

**Operating System:** Linux Mint

**Testing Tools:**
- cURL
- Browser
- Postman (where available)

---

## Test 01 – Users Endpoint

### Request

GET /users

### Full URL

https://jsonplaceholder.typicode.com/users

### Purpose

Determine whether the public users endpoint is accessible without
authentication and examine the type of information returned.

### Expected Observation

The endpoint is publicly accessible and returns JSON user records.

### Security Area

Open / unauthenticated endpoint

---

## Test 02 – Individual User Endpoint

### Request

GET /users/1

### Full URL

https://jsonplaceholder.typicode.com/users/1

### Purpose

Inspect whether an individual user record can be retrieved without
authentication.

### Security Area

Authentication and access-control observation

---

## Test 03 – Posts Endpoint

### Request

GET /posts

### Full URL

https://jsonplaceholder.typicode.com/posts

### Purpose

Review the amount and type of information returned by a collection
endpoint.

### Security Area

Response-data exposure

---

## Test 04 – Individual Post Endpoint

### Request

GET /posts/1

### Full URL

https://jsonplaceholder.typicode.com/posts/1

### Purpose

Inspect the response structure of an individual resource.

### Security Area

Response-data exposure and object-level access-control observation

---

## Test 05 – Filtered Posts

### Request

GET /posts?userId=1

### Full URL

https://jsonplaceholder.typicode.com/posts?userId=1

### Purpose

Review how query parameters affect returned data.

### Security Area

Input handling and response filtering

---

## Test 06 – Nested Comments

### Request

GET /posts/1/comments

### Full URL

https://jsonplaceholder.typicode.com/posts/1/comments

### Purpose

Inspect nested resource behavior and returned fields.

### Security Area

Response-data exposure

---

## Test 07 – HTTP Response Headers

### Request

GET /users

### Purpose

Inspect HTTP response headers for security-related controls and
rate-limiting indicators.

### Headers to Review

- Content-Type
- Cache-Control
- Content-Length
- Server
- Access-Control-Allow-Origin
- RateLimit-related headers, if present
- Other security-relevant headers, if present

---

## Safety Notes

Only safe GET requests are included in this testing record.

The API is intentionally designed for testing and returns fake data.
The presence or absence of a security control on this demonstration API
must not automatically be interpreted as proof of the same condition
in a production application.

---

## Evidence

Screenshots of selected requests and responses will be stored in:

evidence/screenshots/

The final report will reference the relevant evidence files.
