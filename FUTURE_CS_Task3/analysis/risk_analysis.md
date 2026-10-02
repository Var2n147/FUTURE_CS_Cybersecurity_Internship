# API Security Risk Analysis

## Future Interns Cybersecurity Internship – Task 3

**Project:** API Security Risk Analysis  
**API Tested:** JSONPlaceholder  
**Base URL:** https://jsonplaceholder.typicode.com  
**Testing Date:** 2 October 2026  
**Tester:** Varun Pant  
**Assessment Type:** Safe, non-destructive API security review

---

## 1. Executive Summary

This assessment presents a controlled security-oriented review of the publicly available JSONPlaceholder demonstration API.

The objective was to examine common API security considerations involving authentication, authorization, object-level access control, response-data exposure, rate limiting, query parameters, HTTP security headers, technology disclosure, caching behavior, and input validation considerations.

Testing was restricted to safe HTTP GET requests against the public demonstration API. No authentication bypass, authorization bypass, brute-force activity, denial-of-service testing, flooding, destructive operations, malicious payload injection, or attacks against private or production systems were performed.

JSONPlaceholder behaved consistently with its purpose as a public testing and prototyping API.

Several security-relevant observations were documented. The `/users` endpoint returns multiple user-related properties, which provides a useful example of a data-minimization consideration for production APIs. Predictable numeric identifiers were also observed, but predictable identifiers alone are not a vulnerability. In a production environment, object-level authorization must be enforced independently of whether resource identifiers are predictable.

Positive security controls were also observed, including the `X-Content-Type-Options: nosniff` header and rate-limit-related response headers.

No high-severity vulnerability was established during this assessment.

---

## 2. Objective

The objective of this assessment was to analyze a public/test API and identify common API security risks while documenting:

- Authentication
- Authorization
- Object-level access control
- Data exposure
- Rate limiting
- Query parameters
- HTTP security headers
- Technology disclosure
- Caching behavior
- Input validation considerations
- Business impact
- Security remediation

The purpose of the assessment was educational and defensive.

---

## 3. API Selected

### JSONPlaceholder

JSONPlaceholder is a public fake REST API designed for testing, development, prototyping, and demonstration purposes.

The API provides resources including:

- Users
- Posts
- Comments
- Albums
- Photos
- Todos

The API does not require an API key for normal public test requests.

Because JSONPlaceholder is intentionally designed as a public demonstration service, unauthenticated access is expected behavior.

The returned records are synthetic demonstration data and were therefore not treated as real confidential personal information.

---

## 4. Scope

### In Scope

The assessment included:

- Public API endpoint review
- Safe HTTP GET requests
- Collection endpoint testing
- Individual object endpoint testing
- Query-parameter filtering
- Nested resource retrieval
- HTTP response-header inspection
- Authentication observation
- Authorization considerations
- Data exposure review
- Rate-limit header observation
- Basic input and parameter behavior

### Out of Scope

The following activities were intentionally excluded:

- Authentication bypass
- Authorization bypass
- BOLA/IDOR exploitation
- Credential attacks
- Brute-force attacks
- Denial-of-service testing
- Flooding
- High-volume automated requests
- Destructive API operations
- Malicious payload injection
- Attacks against private APIs
- Attacks against production systems
- Collection of real confidential information

---

## 5. Methodology

The following methodology was used:

1. Select a permitted public demonstration API.
2. Review the purpose and expected behavior of the API.
3. Test collection endpoints.
4. Test individual resource endpoints.
5. Test a query-parameter filter.
6. Test a nested resource endpoint.
7. Inspect HTTP response headers.
8. Review returned data fields.
9. Observe authentication requirements.
10. Consider authorization requirements.
11. Observe rate-limit indicators without attempting to exhaust the limit.
12. Identify security-relevant observations.
13. Assign contextual severity.
14. Document potential business impact.
15. Provide production-oriented remediation recommendations.

---

# 6. Endpoint Testing

## 6.1 GET /users

### Request

GET https://jsonplaceholder.typicode.com/users

### Observation

The endpoint returned a collection of ten test user objects.

The objects contained fields including:

- `id`
- `name`
- `username`
- `email`
- `address`
- `phone`
- `website`
- `company`

The endpoint did not require an API key.

### Security Interpretation

Because JSONPlaceholder is intentionally a public demonstration API, unauthenticated access is expected.

However, the response demonstrates a security consideration relevant to production APIs: collection endpoints should not return more properties than the client actually requires.

If a real production API returned unnecessary sensitive fields for every user, the design could contribute to excessive data exposure.

### Severity

**Low – contextual data-exposure consideration**

This is not classified as a confirmed vulnerability in JSONPlaceholder because the API is intentionally public and the returned records are synthetic.

### Evidence

`../evidence/users_response.txt`

---

## 6.2 GET /users/1

### Request

GET https://jsonplaceholder.typicode.com/users/1

### Observation

A single user object was successfully returned using the numeric identifier `1`.

The response contained properties including:

- `id`
- `name`
- `username`
- `email`
- `address`
- `phone`
- `website`
- `company`

### Security Interpretation

Predictable numeric identifiers are not automatically a vulnerability.

In a production system, however, every object request should be protected by appropriate server-side authorization.

For example, if an authenticated user requests another user's record, the server should determine whether that requester has permission to access the requested object.

No authorization bypass was attempted during this assessment.

### Severity

**Informational**

### Evidence

`../evidence/user_1_response.txt`

---

## 6.3 GET /posts

### Request

GET https://jsonplaceholder.typicode.com/posts

### Observation

The endpoint returned a collection of 100 synthetic posts.

Each post contained:

- `userId`
- `id`
- `title`
- `body`

### Security Interpretation

The endpoint is publicly accessible without authentication.

This is expected for JSONPlaceholder.

The response demonstrates why production collection endpoints should use data minimization and appropriate authorization when the underlying data is sensitive.

### Severity

**Informational / Low contextual consideration**

### Evidence

`../evidence/posts_response.txt`

---

## 6.4 GET /posts?userId=1

### Request

GET https://jsonplaceholder.typicode.com/posts?userId=1

### Observation

The API returned ten posts.

Every returned post contained:

`"userId": 1`

This demonstrates that the API processes the `userId` query parameter as a collection filter.

### Security Interpretation

The filter behaved as expected.

No attempt was made to bypass access controls or retrieve private information belonging to another user.

In a production API, query parameters used to select resources should still be subject to server-side authorization.

A query parameter such as `userId=1` must not itself be considered proof that the requester is authorized to access that user's information.

### Severity

**Informational**

### Evidence

`../evidence/posts_user1_response.txt`

---

## 6.5 GET /posts/1

### Request

GET https://jsonplaceholder.typicode.com/posts/1

### Observation

The API returned a single post containing:

- `userId`
- `id`
- `title`
- `body`

The post was accessed through the numeric identifier `1`.

### Security Interpretation

Predictable resource identifiers are common in REST APIs and are not inherently vulnerabilities.

The important security control in production environments is object-level authorization.

The server should verify that the authenticated requester has permission to access the requested object.

Because JSONPlaceholder does not provide a normal authenticated multi-user environment for this assessment, BOLA/IDOR could not be established.

### Severity

**Informational**

### Evidence

`../evidence/post_1_response.txt`

---

## 6.6 GET /posts/1/comments

### Request

GET https://jsonplaceholder.typicode.com/posts/1/comments

### Observation

The endpoint returned comments associated with post ID `1`.

The response objects included:

- `postId`
- `id`
- `name`
- `email`
- `body`

### Security Interpretation

The nested endpoint correctly returned resources associated with the requested post.

The email addresses in the JSONPlaceholder dataset are synthetic test data and were not treated as real personal information.

For production APIs, nested resources containing user-related properties should be reviewed carefully to ensure that clients receive only the fields they require.

### Severity

**Low – contextual data-exposure consideration**

### Evidence

`../evidence/post_1_comments_response.txt`

---

# 7. Authentication Analysis

The tested JSONPlaceholder endpoints did not require an API key or authentication token.

This is consistent with the purpose of JSONPlaceholder as a public test API.

Therefore, the absence of authentication was not classified as a confirmed vulnerability.

### Assessment

**Informational – expected behavior for a public demonstration API**

### Production Recommendation

Sensitive production APIs should require authentication for protected resources and operations.

Authentication mechanisms should be securely implemented and supported by appropriate session or token controls.

---

# 8. Authorization Analysis

The assessment observed predictable resource identifiers such as:

`/users/1`

and:

`/posts/1`

It also observed filtering through:

`/posts?userId=1`

However, no authenticated multi-user environment was available.

No authorization bypass was attempted.

Therefore, BOLA/IDOR was **not established**.

### Production Recommendation

Production APIs should enforce authorization on the server side for every protected object.

For example:

`GET /users/123`

should result in an authorization check determining whether the authenticated requester is allowed to access user `123`.

Authorization should never depend solely on the client supplying an identifier.

---

# 9. Data Exposure Analysis

The `/users` endpoint returned multiple user-related properties.

The `/posts/1/comments` endpoint also returned properties including `name` and `email`.

For JSONPlaceholder, these values are synthetic demonstration data.

However, excessive property exposure can become a security problem when a real API returns sensitive information that the requesting client does not require.

### Potential Production Impact

Excessive data exposure could contribute to:

- Privacy violations
- Unnecessary disclosure of personal information
- Increased attack impact if an endpoint is compromised
- Regulatory or contractual problems
- Greater reconnaissance value

### Recommendation

Production APIs should apply data minimization.

Only fields necessary for the requested operation should be returned.

Sensitive internal properties should not be exposed merely because they exist in an underlying database object.

### Severity

**Low – contextual design consideration**

---

# 10. Rate-Limiting Analysis

The tested responses included rate-limit-related headers:

- `x-ratelimit-limit`
- `x-ratelimit-remaining`
- `x-ratelimit-reset`

For example, the API returned:

`x-ratelimit-limit: 3600000`

### Security Interpretation

The presence of rate-limit information is a positive control indicator.

The assessment did not attempt to exhaust the rate limit because flooding and denial-of-service testing were outside the approved scope.

Therefore, this assessment does not determine whether the configured rate limit is appropriate for a real production workload.

### Assessment

**Positive control observed**

### Production Recommendation

Production APIs should implement appropriate rate limiting based on factors such as:

- User identity
- API key
- IP address
- Endpoint sensitivity
- Request cost
- Business requirements

Rate limiting should be supported by monitoring and alerting.

---

# 11. HTTP Security Headers

## 11.1 X-Content-Type-Options

The API returned:

`x-content-type-options: nosniff`

This is a positive security configuration because it helps prevent browsers from interpreting content as a different MIME type than the server declares.

### Assessment

**Positive control**

---

## 11.2 X-Powered-By

The API returned:

`x-powered-by: Express`

This reveals the use of the Express framework.

Technology disclosure does not automatically provide unauthorized access, but reducing unnecessary technology information can reduce passive reconnaissance value.

### Severity

**Informational**

### Recommendation

Production applications can remove unnecessary framework-identification headers where practical.

---

# 12. Caching Behavior

The responses included cache-related headers such as:

- `cache-control: max-age=43200`
- `etag`
- `expires: -1`
- `pragma: no-cache`

Cloudflare also indicated cached responses through:

`cf-cache-status: HIT`

Caching is not automatically a vulnerability.

However, production APIs containing sensitive or user-specific information must be carefully configured so that shared caches cannot accidentally serve one user's information to another user.

### Assessment

**Informational**

### Recommendation

Sensitive user-specific API responses should use appropriate cache-control policies and should be reviewed for shared-cache behavior.

---

# 13. Input Validation

The safe query parameter:

`/posts?userId=1`

was tested and returned the expected filtered result.

No malicious payloads were submitted.

No injection attempts were performed.

No malformed or intentionally hostile input was used because such testing was outside the safe scope of this educational assessment.

### Assessment

**Not fully assessed**

### Production Recommendation

Production APIs should validate:

- Query parameters
- Path parameters
- Request bodies
- Headers
- Data types
- Length limits
- Allowed values

Strict schema validation should be applied before processing user-controlled input.

---

# 14. Risk Summary

| ID | Observation | Severity | Assessment Status |
|---|---|---|---|
| API-01 | Public unauthenticated endpoints | Informational / Low | Expected behavior for demo API |
| API-02 | Broad user object response | Low | Contextual data-exposure consideration |
| API-03 | Predictable numeric resource IDs | Informational | Not a vulnerability by itself |
| API-04 | BOLA/IDOR | Not established | No authenticated bypass testing |
| API-05 | Rate-limit headers observed | Positive control | No stress testing performed |
| API-06 | X-Content-Type-Options: nosniff | Positive control | Security header observed |
| API-07 | X-Powered-By: Express | Informational | Technology disclosure |
| API-08 | Nested comments expose user-related fields | Low | Synthetic demo data; production consideration |
| API-09 | Input validation | Not fully assessed | No malicious input testing |
| API-10 | Cache behavior | Informational | Requires production-specific review |

---

# 15. Business Impact

If similar API design patterns existed in a real production application without appropriate security controls, possible consequences could include:

- Unauthorized access to customer records
- Exposure of unnecessary personal information
- Privacy violations
- Increased attack surface
- Resource enumeration
- Increased reconnaissance value
- API abuse
- Regulatory or contractual consequences where sensitive information is involved

These are potential production consequences and were not demonstrated against JSONPlaceholder.

---

# 16. Recommended Remediation

## 1. Implement Strong Authentication

Use a secure authentication mechanism appropriate for the application, such as secure sessions or properly designed token-based authentication.

## 2. Enforce Server-Side Authorization

Every protected object and sensitive operation should be checked against the authenticated user's permissions.

## 3. Apply Least Privilege

Users and API clients should receive only the permissions necessary for their role.

## 4. Minimize Response Data

Return only the properties required by the requesting client.

Avoid exposing sensitive or internal fields unnecessarily.

## 5. Implement Rate Limiting

Use appropriate limits based on users, API keys, IP addresses, endpoint sensitivity, and business requirements.

## 6. Validate Input

Validate query parameters, path parameters, request bodies, and headers against strict schemas.

## 7. Reduce Unnecessary Technology Disclosure

Remove unnecessary framework-identification headers where appropriate.

## 8. Configure Caching Carefully

Ensure that sensitive user-specific responses cannot be served from shared caches to unauthorized users.

## 9. Monitor API Activity

Monitor authentication failures, authorization failures, abnormal request rates, resource enumeration, and other suspicious patterns.

## 10. Perform Regular API Security Testing

Use threat modeling, code review, automated testing, security testing, and periodic assessments.

---

# 17. Ethical and Safety Considerations

All testing was restricted to the publicly available JSONPlaceholder demonstration API.

Only safe requests were performed.

No credentials were attacked.

No authentication bypass was attempted.

No authorization bypass was attempted.

No private system was accessed.

No production system was targeted.

No flooding or denial-of-service testing was performed.

No destructive operations were performed.

No malicious payloads were submitted.

The purpose of the assessment was security education and defensive risk identification.

---

# 18. Assessment Limitations

This assessment was a limited security review of a public demonstration API.

The following limitations apply:

- JSONPlaceholder is intentionally designed for testing and development.
- The returned records are synthetic.
- No authenticated multi-user environment was available.
- BOLA/IDOR could not be conclusively tested.
- No authorization bypass was attempted.
- No destructive operations were performed.
- No high-volume traffic was generated.
- No denial-of-service testing was performed.
- No malicious payloads were submitted.
- Rate limiting was observed through response headers but was not stress-tested.
- Input validation was only lightly assessed using safe query behavior.
- The assessment cannot establish the presence or absence of every possible API vulnerability.

---

# 19. Overall Assessment

JSONPlaceholder behaved as expected for a public demonstration API during the tests performed.

The assessment identified several observations that are useful from a production API security perspective, particularly:

- Authentication expectations
- Server-side authorization
- Object-level authorization
- Data minimization
- Predictable resource identifiers
- Rate limiting
- Security headers
- Technology disclosure
- Cache configuration
- Input validation

No high-severity vulnerability was established during the assessment.

The main security lesson is that API behavior must always be interpreted in context. A public endpoint in a deliberately public test API is not automatically a vulnerability. The same design pattern can become a serious security issue in a production application when sensitive data, weak authorization, or insufficient access controls are involved.

---

# 20. Evidence Collected

The following response evidence files were collected:

- `../evidence/users_response.txt`
- `../evidence/user_1_response.txt`
- `../evidence/posts_response.txt`
- `../evidence/posts_user1_response.txt`
- `../evidence/post_1_response.txt`
- `../evidence/post_1_comments_response.txt`

The request methodology is documented in:

`../tests/requests.md`

Visual evidence is stored under:

`../evidence/screenshots/`

---

# 21. References

The references used for this project are documented in:

`../references/sources.md`

Key security guidance includes OWASP API Security resources and API security best-practice references.

---

# 22. Disclaimer

This report documents a controlled educational security assessment of a public test API.

It is not a penetration test, security certification, or guarantee of the security of JSONPlaceholder.

Production systems require additional testing based on their architecture, threat model, authentication mechanisms, authorization model, business logic, data sensitivity, infrastructure, and organizational requirements.
