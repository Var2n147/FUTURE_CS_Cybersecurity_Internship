# Task 3 – API Security Risk Analysis

## Future Interns Cybersecurity Internship

Task: API Security Risk Analysis (Modern SaaS Skill)
Task ID: FUTURE_CS_03
Prepared by: Varun Pant
Date: October 2026

---

## 1. Objective

The objective of this assessment is to perform a read-only security analysis
of a public or test API and identify common API security risks.

The assessment focuses on authentication, access control, response-data
exposure, rate limiting, input validation, and unauthenticated endpoints.

The findings are documented in simple technical and business language,
with recommended remediation steps.

---

## 2. Scope

The assessment is limited to a publicly available or intentionally
test-oriented API.

### Allowed Activities

- Documentation review
- Read-only GET requests
- Safe requests supported by the test API
- Request and response inspection
- HTTP header inspection
- Authentication behavior review
- Response-data analysis
- Documentation-based security analysis

### Prohibited Activities

- Exploitation
- Authentication bypass attempts
- Authorization bypass attempts
- Destructive requests
- Denial-of-service testing
- Flooding or excessive automated requests
- Testing private or production APIs without authorization

No attempt is made to compromise the selected API.

---

## 3. API Under Assessment

The API selected for this assessment will be documented here after
the API has been selected and tested.

Details to be recorded:

- API name
- Official/documentation URL
- Base URL
- Purpose of the API
- Available endpoints
- Authentication model
- Testing limitations

---

## 4. Security Areas Assessed

The following areas are reviewed according to the Future Interns Task 3
requirements.

### 4.1 Open or Unauthenticated Endpoints

Determine whether endpoints are accessible without authentication and
whether the exposed information is appropriate for public access.

### 4.2 Excessive Data Exposure

Review API responses to determine whether unnecessary or sensitive fields
are returned to clients.

### 4.3 Authentication

Review whether authentication is required where appropriate and examine
the documented authentication mechanism.

### 4.4 Authorization

Review the API's authorization model and determine whether the available
test functionality provides evidence of access-control risks.

Authorization bypass techniques are not attempted.

### 4.5 Rate Limiting

Review available documentation, response headers, and controlled requests
for evidence of rate-limiting controls.

No flooding or denial-of-service testing is performed.

### 4.6 Input Validation

Review documented parameters and safe requests to determine whether
inputs appear to be appropriately constrained and validated.

No malicious payloads or exploitation attempts are performed.

---

## 5. Methodology

The assessment follows this workflow:

API Selection
     ↓
Documentation Review
     ↓
Endpoint Identification
     ↓
Safe Request Testing
     ↓
Request / Header / Response Inspection
     ↓
Security Risk Identification
     ↓
Risk Severity Assessment
     ↓
Business Impact Analysis
     ↓
Remediation Recommendations
     ↓
Final Security Report

---

## 6. Tools

The assessment may use:

- Postman
- Insomnia
- Browser Developer Tools
- cURL
- Linux
- Git
- GitHub
- Markdown
- PDF documentation

---

## 7. Risk Severity

Findings are classified using three severity levels.

### High

A security issue that could result in significant unauthorized access,
sensitive-data exposure, account compromise, or substantial business
impact.

### Medium

A security weakness that could enable meaningful abuse or information
exposure but has more limited impact or requires additional conditions.

### Low

A security weakness with limited security impact, informational value,
or low exploitation potential within the assessed scope.

---

## 8. Evidence

Evidence will be stored in the evidence/ directory.

Where applicable, evidence includes:

- Postman request screenshots
- Response screenshots
- HTTP header observations
- API documentation references
- Safe request/response examples

Potentially sensitive information will not be intentionally collected
or published.

---

## 9. Testing Safety

Testing is performed against a public or intentionally test-oriented API.

Only safe and read-only operations are used unless a documented test API
explicitly permits a harmless request.

Potentially harmful payloads, authentication bypass attempts, destructive
operations, and excessive request generation are excluded.

---

## 10. Reporting

The final report will document:

- API tested
- Testing scope
- Methodology
- Endpoints reviewed
- Security observations
- Identified risks
- Severity
- Evidence
- Business impact
- Remediation recommendations
- Testing limitations

---

## 11. References

Security concepts are informed by established API security guidance,
including the OWASP API Security Top 10.

Reference details are maintained in:

references/sources.md

---

## 12. Disclaimer

This assessment is performed for educational and authorized internship
purposes.

No attempt is made to gain unauthorized access, bypass security controls,
disrupt services, or access private information.
