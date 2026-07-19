# Findings Summary

## Assessment Overview

| Property | Detail |
|---|---|
| **Target** | JSONPlaceholder REST API (https://jsonplaceholder.typicode.com) |
| **Assessment Date** | 17 July 2026 |
| **Tester** | Harsh Aghera |
| **Tool** | Postman – API Security Testing Collection |
| **Scope** | Read-only GET requests across 8 endpoints |
| **Methodology** | Manual black-box testing |

---

## Findings Distribution

| ID | Finding | Category | Likelihood | Impact | Risk Level |
|---|---|---|---|---|---|
| F-01 | Authentication Controls | API1:2023 | Low | High | **Informational** |
| F-02 | Authorization Controls | API1:2023 | Low | High | **Informational** |
| F-03 | Sensitive Data Exposure | API3:2023 | Low | Medium | **Low** |
| F-04 | Security Headers | API8:2023 | Medium | Low | **Low** |
| F-05 | Rate Limiting | API4:2023 | Low | Medium | **Informational** |
| F-06 | Error Handling | API8:2023 | Low | Low | **Informational** |
| F-07 | Input Validation | API3/8:2023 | Low | Low | **Informational** |

---

## Risk Summary

| Risk Level | Count | Findings |
|---|---|---|
| 🔴 Critical | 0 | — |
| 🟠 High | 0 | — |
| 🟡 Medium | 0 | — |
| 🔵 Low | 2 | F-03, F-04 |
| ⚪ Informational | 5 | F-01, F-02, F-05, F-06, F-07 |
| **Total** | **7** | |

---

## Key Findings Summary

### F-01 – Authentication Controls (Informational)
All endpoints return data without any authentication. By design for JSONPlaceholder. Would be Critical in production. Evidence: all 6 Postman request/response screenshots.

### F-02 – Authorization Controls (Informational)
No ownership or entitlement checks on any resource. By design for JSONPlaceholder. Would be High (BOLA) in production. Evidence: GET_Users_Request_Response.png, GET_Users_Response.png.

### F-03 – Sensitive Data Exposure (Low)
GET /users returns name, email, address, geo-coordinates, phone, company. GET /comments returns emails. Fictional data only. Response schema demonstrates excessive exposure pattern. Evidence: GET_Users_Response.png, GET_Comments_Request_Response.png, GET_Users_Headers.png.

### F-04 – Security Headers (Low)
Missing: CSP, X-Frame-Options, HSTS, Referrer-Policy, Permissions-Policy. Present: x-content-type-options: nosniff. x-powered-by: Express discloses framework. Evidence: GET_Users_Headers.png (26 headers inspected).

### F-05 – Rate Limiting (Informational)
x-ratelimit-limit: 1000 observed. Positive indicator. Time window, remaining count, and reset timestamp headers not visible. Cannot fully verify enforcement. Evidence: GET_Users_Headers.png.

### F-06 – Error Handling (Informational)
Both error tests returned {} (empty JSON) with 404. No information leakage. Positive security posture. Evidence: Invalid_Endpoint.png, User_Not_Found.png.

### F-07 – Input Validation (Informational)
Read-only scope only. /Comments (uppercase C) returned 200 OK – case-insensitive routing noted. No write-operation testing performed. Unable to verify. Evidence: GET_Comments_Request_Response.png.

---

## Overall Assessment

The security posture of JSONPlaceholder is **appropriate for a publicly accessible demonstration API** with entirely fictional data. The primary actionable observation is the absence of standard HTTP security response headers (F-04), which can be remediated at the infrastructure layer. Authentication (F-01) and authorization (F-02) findings are by design and would require full implementation in any production equivalent.
