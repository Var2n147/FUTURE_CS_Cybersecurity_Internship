# API Security Risk Analysis — Evidence

## Future Interns Cybersecurity Internship – Task 3

---

## 1. Evidence Overview

This document contains the evidence collected during the API Security Risk Analysis assessment performed for Future Interns Cybersecurity Internship Task 3.

The assessment was conducted against the public demonstration API:

**JSONPlaceholder**

Base URL:

`https://jsonplaceholder.typicode.com`

The testing was performed using safe, read-only HTTP GET requests. The purpose was to understand API exposure, authentication requirements, response data, HTTP security headers, rate-limiting indicators, and other API security considerations.

No destructive, intrusive, or unauthorized exploitation activities were performed.

---

# 2. Assessment Scope

The following security areas were examined:

- Public API endpoint exposure
- Authentication requirements
- Authorization considerations
- Response data exposure
- HTTP security headers
- Rate-limiting indicators
- Cache-related behavior
- Technology disclosure
- Query-parameter behavior
- API response structure
- Secure testing methodology

The assessment was limited to publicly accessible demonstration endpoints.

---

# 3. Ethical Testing Boundaries

The assessment followed a safe and ethical testing approach.

The following activities were NOT performed:

- Authentication bypass
- Authorization bypass
- IDOR exploitation
- Credential attacks
- Brute-force attacks
- Password attacks
- Denial-of-service testing
- API flooding
- Malicious payload injection
- SQL injection
- Cross-site scripting payload testing
- Path traversal
- Destructive API requests
- Data deletion
- Unauthorized modification of data
- Testing private production APIs

Only safe, read-only requests were used.

---

# 4. Evidence 01 — GET /users

## Endpoint

`GET https://jsonplaceholder.typicode.com/users`

## Purpose

The `/users` endpoint was tested to observe a public collection endpoint, inspect the returned JSON structure, and examine HTTP response headers.

## Observed Result

The endpoint returned:

`HTTP/2 200`

The response contained multiple demonstration user objects.

The returned objects contained fields including:

- `id`
- `name`
- `username`
- `email`
- `address`
- `phone`
- `website`
- `company`

The endpoint did not require an API key or authentication token.

## Security Observation

The endpoint is publicly accessible without authentication.

For JSONPlaceholder this is expected because it is a public fake API designed for testing and development.

However, if a production API exposed equivalent user information without authentication or authorization, it could create information-exposure risks.

## Classification

**Low — Contextual Security Observation**

## Evidence File

`FUTURE_CS_Task3/evidence/users_response.txt`

---

# 5. Evidence 02 — GET /users/1

## Endpoint

`GET https://jsonplaceholder.typicode.com/users/1`

## Purpose

This request was used to inspect an individual resource and determine how the API responds when a specific numeric resource identifier is supplied.

## Observed Result

The endpoint returned:

`HTTP/2 200`

The response contained one demonstration user object.

The object contained fields such as:

- `id`
- `name`
- `username`
- `email`
- `address`
- `phone`
- `website`
- `company`

No API key or authentication token was required.

## Security Observation

The endpoint uses a predictable numeric identifier.

Predictable IDs by themselves are not a security vulnerability.

No attempt was made to bypass authorization or access private user records.

In a real production API, every request for a protected resource should be checked against the authenticated user's permissions.

## Classification

**Informational / Contextual Observation**

## Evidence File

`FUTURE_CS_Task3/evidence/user_1_response.txt`

---

# 6. Evidence 03 — GET /posts

## Endpoint

`GET https://jsonplaceholder.typicode.com/posts`

## Purpose

The `/posts` endpoint was tested to examine a public collection endpoint and inspect the structure of returned objects and security-related HTTP headers.

## Observed Result

The endpoint returned:

`HTTP/2 200`

The response contained multiple demonstration post objects.

Each post contained fields including:

- `userId`
- `id`
- `title`
- `body`

No authentication token was required.

## Security Observation

The endpoint is publicly accessible because JSONPlaceholder is intentionally designed as a public demonstration API.

For a production SaaS application, an equivalent endpoint containing private or business-sensitive information would require appropriate authentication and authorization controls.

## Classification

**Low — Contextual Security Observation**

## Evidence File

`FUTURE_CS_Task3/evidence/posts_response.txt`

---

# 7. Evidence 04 — GET /posts/1

## Endpoint

`GET https://jsonplaceholder.typicode.com/posts/1`

## Purpose

This request was used to inspect an individual post resource and observe the API's handling of a specific resource identifier.

## Observed Result

The endpoint returned:

`HTTP/2 200`

The response contained one demonstration post.

The response included:

- `userId`
- `id`
- `title`
- `body`

No authentication token was required.

## Security Observation

The resource is accessible using a predictable numeric identifier.

This does not establish an IDOR or authorization vulnerability.

No attempt was made to access private resources or bypass authorization.

In a production environment, protected resources should always be checked using server-side authorization.

## Classification

**Informational / Contextual Observation**

## Evidence File

`FUTURE_CS_Task3/evidence/post_1_response.txt`

---

# 8. Evidence 05 — GET /posts?userId=1

## Endpoint

`GET https://jsonplaceholder.typicode.com/posts?userId=1`

## Purpose

This request was used to safely examine query-parameter behavior.

The `userId` parameter was supplied as part of a normal documented API request.

## Observed Result

The endpoint returned:

`HTTP/2 200`

The response contained posts associated with:

`userId: 1`

The API accepted the query parameter and returned matching demonstration records.

## Security Observation

This test demonstrates normal query-parameter filtering.

No malicious input was used.

No attempt was made to manipulate the parameter to bypass authorization or access another user's private information.

In a production API, user-specific query parameters must always be combined with server-side authorization checks.

## Classification

**Informational — Limited Input Validation Assessment**

## Evidence File

`FUTURE_CS_Task3/evidence/posts_user1_response.txt`

---

# 9. Evidence 06 — GET /posts/1/comments

## Endpoint

`GET https://jsonplaceholder.typicode.com/posts/1/comments`

## Purpose

This request was used to inspect a related-resource endpoint and observe how comments associated with a specific post are exposed.

## Observed Result

The endpoint returned:

`HTTP/2 200`

The response contained multiple demonstration comment records.

The endpoint was accessible without an API key or authentication token.

## Security Observation

The endpoint is publicly accessible because JSONPlaceholder is a demonstration API.

For production systems, related resources should be protected by authorization controls when they contain private or user-specific information.

## Classification

**Low — Contextual Security Observation**

## Evidence File

`FUTURE_CS_Task3/evidence/post_1_comments_response.txt`

---

# 10. HTTP Security Header Evidence

The API responses were inspected for security-relevant HTTP headers.

Several useful headers were observed.

---

## 10.1 X-Content-Type-Options

Observed:

`X-Content-Type-Options: nosniff`

### Security Meaning

This header instructs browsers not to MIME-sniff the response away from its declared content type.

This is considered a positive security configuration.

### Assessment

**Positive Security Control**

---

## 10.2 X-Powered-By

Observed:

`X-Powered-By: Express`

### Security Meaning

This header reveals the server-side framework or technology being used.

It is not automatically a vulnerability, but unnecessary technology disclosure can provide useful information during reconnaissance.

### Assessment

**Informational Observation**

### Recommendation

Production applications can remove unnecessary technology-identification headers where practical.

---

## 10.3 Rate-Limit Headers

Observed headers included:

`X-RateLimit-Limit`

`X-RateLimit-Remaining`

`X-RateLimit-Reset`

### Security Meaning

These headers indicate that rate-limit information is available at the API layer.

Rate limiting can help protect APIs against:

- Excessive automated requests
- Resource exhaustion
- Abuse
- Brute-force activity
- Excessive scraping

### Assessment

**Positive Control Observed**

No high-volume stress test was performed because such testing was outside the safe scope of this internship assessment.

---

## 10.4 Content-Type

Observed:

`Content-Type: application/json; charset=utf-8`

### Security Meaning

The response correctly identifies itself as JSON.

This provides predictable content handling and works together with the `nosniff` security header.

### Assessment

**Positive Configuration Observation**

---

## 10.5 Cache-Control

Observed cache-related behavior included:

`Cache-Control: max-age=43200`

### Security Meaning

Caching can improve performance.

However, production APIs containing private or user-specific data must ensure that caching does not expose sensitive information to unauthorized users.

### Assessment

**Informational Observation**

The JSONPlaceholder data is demonstration data and does not represent private production information.

---

# 11. Authentication Evidence

The tested JSONPlaceholder endpoints did not require an API key or authentication token.

For example:

`GET /users`

returned a successful response without an Authorization header.

## Security Interpretation

For JSONPlaceholder, this is expected behavior because the service is specifically designed as a public demonstration API.

Therefore, the absence of authentication is NOT classified as a confirmed vulnerability in JSONPlaceholder.

However, an equivalent production API containing private user or business information should require appropriate authentication.

## Recommended Production Controls

- Strong authentication
- Secure token validation
- Short-lived access tokens where appropriate
- Secure credential management
- Server-side authentication checks
- Authorization after authentication

## Classification

**Low — Contextual Observation**

---

# 12. Authorization Evidence

A complete authorization assessment requires multiple authenticated users or roles.

JSONPlaceholder does not provide the type of private multi-user environment required for such testing.

Therefore, comprehensive authorization testing was not possible within the safe scope.

The following were NOT attempted:

- Accessing another user's private information
- Manipulating authorization controls
- IDOR exploitation
- Session manipulation
- Privilege escalation
- Authorization bypass

## Security Requirement for Production APIs

Every request to a protected resource should perform server-side authorization checks.

The API should verify that the authenticated user has permission to access the requested object.

## Classification

**Not Fully Testable Within Demo Scope**

---

# 13. Excessive Data Exposure Observation

The `/users` endpoint returned multiple fields for each demonstration user.

Examples include:

- Name
- Username
- Email
- Address
- Phone
- Website
- Company

## Security Significance

Returning unnecessary fields can create excessive data exposure in production applications.

Sensitive APIs should follow data-minimization principles.

Applications should return only the information required by the client.

## Recommended Controls

- Return only required fields
- Apply field-level authorization
- Use strict response schemas
- Avoid exposing internal database fields
- Review API responses for unnecessary personal information
- Apply data minimization

## Classification

**Low — Contextual Observation**

The information returned by JSONPlaceholder is fake demonstration data.

---

# 14. Input Validation Evidence

A safe query parameter was tested:

`GET /posts?userId=1`

The API accepted the parameter and returned matching demonstration records.

No malicious payloads were used.

The following were intentionally excluded:

- SQL injection
- XSS
- Command injection
- Path traversal
- Server-side template injection
- Fuzzing
- Malformed payload flooding

## Assessment

Basic query-parameter behavior was successfully observed.

A complete input-validation security assessment was outside the scope of this safe internship exercise.

## Classification

**Informational — Limited Assessment**

---

# 15. API Endpoint Test Summary

| Test | HTTP Method | Endpoint | Result | Security Area |
|---|---|---|---|---|
| Test 01 | GET | `/users` | 200 OK | Public endpoint / data exposure |
| Test 02 | GET | `/users/1` | 200 OK | Resource access / IDs |
| Test 03 | GET | `/posts` | 200 OK | Public endpoint |
| Test 04 | GET | `/posts/1` | 200 OK | Resource access |
| Test 05 | GET | `/posts?userId=1` | 200 OK | Query parameters |
| Test 06 | GET | `/posts/1/comments` | 200 OK | Related resources |

All tests were read-only.

---

# 16. Positive Security Controls Observed

The assessment also identified positive security controls.

### HTTPS

The API was accessed over HTTPS.

### Content-Type

The API returned an appropriate JSON content type.

### X-Content-Type-Options

The API returned:

`X-Content-Type-Options: nosniff`

### Rate-Limit Headers

Rate-limit information was present in the responses.

These observations indicate that the API has several basic security-related controls or infrastructure protections.

---

# 17. Risk Summary

| Finding | Severity | Business/Security Impact | Recommended Action |
|---|---|---|---|
| Public unauthenticated demo endpoints | Low / Contextual | Could expose information if replicated in production without controls | Require authentication for protected resources |
| Broad user-object response | Low | Unnecessary information could be exposed in production | Apply data minimization and field filtering |
| X-Powered-By disclosure | Informational | Provides technology information for reconnaissance | Remove unnecessary technology disclosure |
| Predictable numeric IDs | Informational | IDs may be enumerable if authorization is missing | Enforce server-side object authorization |
| Rate-limit headers | Positive Control | Helps indicate API rate-limiting capability | Maintain and monitor rate limits |
| X-Content-Type-Options | Positive Control | Reduces MIME-sniffing risk | Maintain security header |
| HTTPS | Positive Control | Protects data in transit | Continue enforcing HTTPS |

---

# 18. No Confirmed High-Severity Vulnerability

The assessment did not establish a High-severity vulnerability.

No confirmed:

- Authentication bypass
- Authorization bypass
- IDOR
- SQL injection
- XSS
- Command injection
- Data destruction
- Denial-of-service vulnerability

was identified.

This conclusion is limited to the tested public demonstration API and the safe testing methodology used.

---

# 19. Evidence Files

The following raw evidence files contain captured API responses:

`users_response.txt`

`user_1_response.txt`

`posts_response.txt`

`posts_user1_response.txt`

`post_1_response.txt`

`post_1_comments_response.txt`

These files are stored under:

`FUTURE_CS_Task3/evidence/`

---

# 20. Evidence-to-Analysis Mapping

The evidence supports the following analysis documents:

### Endpoint Analysis

`FUTURE_CS_Task3/analysis/endpoint_analysis.md`

Contains endpoint-level observations and HTTP header analysis.

### Risk Analysis

`FUTURE_CS_Task3/analysis/risk_analysis.md`

Contains the detailed security-risk assessment, severity classification, business impact, limitations, and recommendations.

### Test Requests

`FUTURE_CS_Task3/tests/requests.md`

Documents the API requests used during the assessment.

### References

`FUTURE_CS_Task3/references/sources.md`

Contains the security references and external sources used for the assessment methodology.

---

# 21. Evidence Limitations

This evidence has several limitations.

## Demonstration API

JSONPlaceholder is a fake API intended for development and testing.

It does not represent a production SaaS application.

## No Real User Accounts

No real authenticated users were available.

Therefore, complete authorization testing was not possible.

## No Exploitation

No exploitation was performed.

Therefore, the assessment documents observable behavior and security considerations rather than confirmed exploitable vulnerabilities.

## No Stress Testing

Rate limiting was observed through HTTP response headers.

No high-volume requests were sent.

## No Real Sensitive Data

The returned records are demonstration data.

They should not be interpreted as real customer information.

## Limited Input Testing

Only safe documented query parameters were tested.

---

# 22. Recommended Production Security Controls

For a real SaaS API, the following controls are recommended:

1. Implement strong authentication.
2. Apply server-side authorization to every protected object.
3. Prevent unauthorized object access.
4. Apply object-level access controls.
5. Minimize returned data.
6. Apply field-level authorization where required.
7. Implement rate limiting.
8. Monitor API traffic.
9. Validate all input server-side.
10. Use strict request and response schemas.
11. Remove unnecessary technology-disclosure headers.
12. Review caching behavior for sensitive data.
13. Enforce HTTPS.
14. Maintain security logging.
15. Monitor suspicious API activity.
16. Regularly review exposed endpoints.
17. Follow OWASP API Security guidance.

---

# 23. Final Evidence Conclusion

The evidence demonstrates a controlled API security assessment of JSONPlaceholder.

Six safe read-only endpoints were tested:

- `/users`
- `/users/1`
- `/posts`
- `/posts/1`
- `/posts?userId=1`
- `/posts/1/comments`

The assessment identified several contextual security observations, including public endpoint exposure, broad demonstration-data responses, predictable resource identifiers, and technology disclosure.

The assessment also identified positive controls including HTTPS, JSON content types, `X-Content-Type-Options: nosniff`, and rate-limit headers.

No High-severity or Medium-severity vulnerability was established.

No authentication bypass, authorization bypass, IDOR exploitation, injection attack, denial-of-service activity, or destructive action was performed.

The results should therefore be interpreted as a controlled educational API security assessment and as production-security considerations rather than as a complete penetration test.

---

**End of Evidence**
