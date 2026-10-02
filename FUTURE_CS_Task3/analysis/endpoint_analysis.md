# Task 3 – API Endpoint Analysis

## API Tested

**API:** JSONPlaceholder

**Base URL:** https://jsonplaceholder.typicode.com

**Purpose:** Public fake REST API intended for testing, prototyping, and educational use.

**Authentication:** No API key or account is required for the public API.

---

# Test 01 – GET /users

## Request

GET /users

## URL

https://jsonplaceholder.typicode.com/users

## Testing Method

A standard read-only HTTP GET request was sent using cURL.

Command used:

    curl -i https://jsonplaceholder.typicode.com/users

No authentication bypass, destructive operation, automated flooding, or malicious payload was used.

---

## HTTP Response

The endpoint returned a successful HTTP response.

Observed response characteristics included:

- Content-Type: application/json; charset=utf-8
- Cache-Control: max-age=43200
- X-Content-Type-Options: nosniff
- X-RateLimit-Limit: 3600000
- X-RateLimit-Remaining: 3599991
- X-RateLimit-Reset: 1790812826
- Server: cloudflare
- X-Powered-By: Express

The exact infrastructure telemetry values are not reproduced in the public evidence where unnecessary.

---

# Observation 1 – Public / Unauthenticated Endpoint

## Finding

The /users endpoint can be accessed without an API key or user authentication.

## Evidence

A successful response was obtained using a normal GET request without providing an authentication token.

## Security Interpretation

This is an unauthenticated endpoint.

However, JSONPlaceholder is intentionally designed as a public fake API for testing and prototyping. Therefore, public accessibility of /users is an expected design characteristic and is not by itself evidence of a security vulnerability.

## Severity

Informational / Low

## Business Impact

For a production SaaS application, an unintentionally public endpoint could expose information that should only be available to authenticated users.

For this demonstration API, the returned information is part of the test dataset and is not treated as a confirmed production data exposure.

## Recommendation

For production APIs:

- Require authentication for non-public resources.
- Clearly classify endpoints as public or protected.
- Enforce authorization before returning user-specific information.
- Document which resources are intentionally public.

---

# Observation 2 – Broad User Object Response

## Finding

The /users endpoint returns multiple fields within each user object, including contact and location-related fields.

Observed fields include:

- id
- name
- username
- email
- address
- geo
- phone
- website
- company

## Security Interpretation

The endpoint demonstrates a broad object response containing several categories of information.

In a production application, returning fields that the requesting client does not need could create an excessive-data-exposure risk.

OWASP describes this class of issue as exposing object properties that a user should not be able to access. In the OWASP API Security Top 10 2023, this is covered by API3:2023 – Broken Object Property Level Authorization.

## Severity

Low – Demonstration Context

## Reason for Severity

The API is intentionally a fake test API and the returned records are not treated as real customer information.

The observation therefore demonstrates a security-design consideration rather than a confirmed sensitive-data breach.

## Potential Production Impact

If a real SaaS API returned unnecessary user information, unauthorized users could potentially obtain:

- personal contact information
- location-related information
- internal account attributes
- other unnecessary user properties

The actual impact would depend on the sensitivity of the data and the authorization model.

## Recommendation

Production APIs should:

1. Return only fields required by the client.
2. Apply object-property authorization.
3. Classify sensitive and personal information.
4. Use explicit response schemas.
5. Avoid serializing complete backend objects by default.
6. Review API responses independently of the user interface.

---

# Header Security Observations

The response included several security-relevant headers.

## Positive Control – MIME Sniffing Protection

Observed header:

    X-Content-Type-Options: nosniff

This indicates that the response includes a header intended to prevent MIME-type sniffing by browsers.

## Rate-Limit Information

The response included:

    X-RateLimit-Limit
    X-RateLimit-Remaining
    X-RateLimit-Reset

This provides evidence that the service exposes rate-limit information.

The observed values should not be interpreted as proof of complete resource-consumption protection. No flooding or high-volume testing was performed.

## Technology Disclosure

The response included:

    X-Powered-By: Express

This identifies Express as the application framework.

### Security Consideration

Technology disclosure can provide useful information to an attacker performing reconnaissance.

### Severity

Low / Informational

### Recommendation

Production systems can consider removing unnecessary technology-identifying headers where they provide no functional benefit.

---

# Response Data Observed

The /users endpoint returned ten user records in the tested response.

Each record contained several categories of fields, including identity, contact, location, website, and company information.

Because JSONPlaceholder is specifically a fake testing API, these values are treated as demonstration data rather than real personal information.

The observation is therefore documented as a potential API design risk rather than a confirmed privacy breach.

---

# Rate-Limiting Observation

The response exposed the following rate-limit indicators:

    X-RateLimit-Limit
    X-RateLimit-Remaining
    X-RateLimit-Reset

The observed limit was:

    3600000

The observed remaining quota was:

    3599991

This indicates that the service provides rate-limit information in the response.

No repeated high-volume requests were performed because the Future Interns task explicitly prohibits flooding and denial-of-service testing.

Therefore, the effectiveness of the rate limit was not independently stress-tested.

### Assessment

No missing-rate-limit finding is claimed from this test.

---

# Authentication Observation

The /users endpoint returned data without an API key or authentication token.

This confirms that the endpoint is publicly accessible.

However, the API is intentionally designed as a public test API and does not represent a normal authenticated SaaS application.

### Assessment

Public access is documented as an observation rather than a confirmed authentication vulnerability.

---

# Authorization Observation

Authorization could not be fully assessed because JSONPlaceholder does not provide a normal authenticated multi-user environment for this test.

No attempt was made to bypass authorization controls or access another user's private resource.

### Assessment

No authorization bypass vulnerability is claimed.

For a production SaaS API, authorization should be enforced at the object and property level.

---

# Input Validation Observation

The /users endpoint does not require user-controlled input for the basic GET request.

Therefore, meaningful input-validation testing cannot be established from this endpoint alone.

No malicious payloads were submitted.

Further safe testing of documented query parameters will be used to observe normal parameter handling.

### Assessment

No input-validation vulnerability is claimed from the /users endpoint.

---

# Limitations

This test has important limitations:

1. JSONPlaceholder is a fake API designed for testing and prototyping.
2. The returned user information is test data.
3. No authenticated user accounts were available for authorization testing.
4. No authorization bypass was attempted.
5. No high-volume requests were generated.
6. No malicious input was submitted.
7. The observations should not be interpreted as confirmed vulnerabilities in a production SaaS application.
8. The rate-limiting mechanism was observed but not stress-tested.
9. Authentication and authorization controls could not be fully evaluated because of the intentionally simple design of the test API.

---

# Evidence File

Raw response evidence is stored at:

    ../evidence/users_response.txt

The raw evidence may contain unnecessary infrastructure telemetry.

Before publication to the public GitHub repository, unnecessary tracking or infrastructure values should be sanitized where appropriate.

---

# Initial Risk Summary

| Finding | Severity | Status |
|---|---|---|
| Public / unauthenticated /users endpoint | Informational / Low | Observed |
| Broad user-object response | Low | Security-design consideration |
| X-Powered-By technology disclosure | Low / Informational | Observed |
| Rate-limit headers exposed | Positive control | Observed |
| X-Content-Type-Options header | Positive control | Observed |
| Authentication bypass | Not tested | No finding claimed |
| Authorization bypass | Not tested | No finding claimed |
| Missing rate limiting | Not observed | No finding claimed |
| Input validation vulnerability | Not established | No finding claimed |

---

# Conclusion

The initial JSONPlaceholder assessment demonstrates several useful API security observations without performing intrusive testing.

The /users endpoint is publicly accessible and returns a broad user object. These characteristics are expected to some extent because JSONPlaceholder is specifically designed as a public fake API.

The assessment also identified positive controls, including rate-limit headers and the X-Content-Type-Options response header.

Further read-only endpoint testing is required before the final API security risk assessment and severity conclusions are completed.
