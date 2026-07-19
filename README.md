<div align="center">

# API Security Risk Analysis

### Future Interns – Cyber Security Internship · Task 3

![Internship](https://img.shields.io/badge/Future%20Interns-Cyber%20Security-0D1B3E?style=for-the-badge&logo=shield&logoColor=white)
![OWASP](https://img.shields.io/badge/OWASP-API%20Security%20Top%2010-1A5C96?style=for-the-badge&logo=owasp&logoColor=white)
![Postman](https://img.shields.io/badge/Postman-API%20Testing-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github&logoColor=white)

</div>

---

## 📌 Project Overview

This repository documents a manual **API Security Risk Analysis** conducted against the [JSONPlaceholder REST API](https://jsonplaceholder.typicode.com) — a publicly available demonstration API — as part of the **Future Interns Cyber Security Internship, Task 3**.

The assessment was performed for **educational purposes only**, using Postman to systematically test API endpoints across seven security categories aligned with the **OWASP API Security Top 10 (2023)**. A professional security report was produced documenting all findings, risk ratings, and remediation recommendations.

> **Target:** `https://jsonplaceholder.typicode.com`  
> **Assessment Date:** 17 July 2026  
> **Scope:** Read-only black-box testing · 8 endpoints  
> **Total Findings:** 7 (0 Critical · 0 High · 0 Medium · 2 Low · 5 Informational)

---

## 🎯 Objectives

- Evaluate the security posture of the JSONPlaceholder REST API across OWASP-defined categories
- Identify authentication and authorization control gaps
- Inspect HTTP response headers for missing security configurations
- Test error handling behaviour for information disclosure risk
- Observe rate limiting mechanisms
- Produce a professional, evidence-based security assessment report

---

## 🔍 Scope of Assessment

| Property | Detail |
|---|---|
| **Target API** | JSONPlaceholder REST API (https://jsonplaceholder.typicode.com) |
| **HTTP Methods** | GET only (read-only; write operations out of scope) |
| **Endpoints Tested** | `/users`, `/posts`, `/comments`, `/albums`, `/photos`, `/todos` |
| **Error Scenarios** | `/invalidendpoint`, `/users/999` |
| **In Scope** | Authentication, Authorization, Sensitive Data, Headers, Rate Limiting, Error Handling, Input Validation |
| **Out of Scope** | POST/PUT/PATCH/DELETE operations · Automated scanning · Load testing |
| **Context** | JSONPlaceholder is a public demonstration API containing entirely fictional data |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Postman** | API request execution, header inspection, response analysis |
| **OWASP API Security Top 10 (2023)** | Risk categorisation framework |
| **Microsoft Word** | Professional report authoring (`.docx`) |
| **Git / GitHub** | Version control and submission |

---

## 📁 Repository Structure

```
FUTURE_CS_03/
│
├── Assets/
│   ├── Cover.png                              # Project cover image
│   └── Internship_Task.png                    # Task description screenshot
│
├── Findings/
│   ├── Authentication.md                      # F-01 – Authentication Controls
│   ├── Authorization.md                       # F-02 – Authorization Controls
│   ├── Sensitive_Data_Exposure.md             # F-03 – Sensitive Data Exposure
│   ├── Security_Headers.md                    # F-04 – Security Headers
│   ├── Rate_Limiting.md                       # F-05 – Rate Limiting
│   ├── Error_Handling.md                      # F-06 – Error Handling
│   ├── Input_Validation.md                    # F-07 – Input Validation
│   └── Summary.md                             # Findings summary & risk matrix
│
├── Postman_Collection/
│   ├── API_Security_Testing.postman_collection.json
│   └── Environment.postman_environment.json
│
├── Report/
│   ├── API_Security_Risk_Analysis_Report.docx # Full security assessment report
│   └── API_Security_Risk_Analysis_Report.pdf  # PDF version
│
├── Resources/
│   ├── API_Documentation.pdf
│   ├── OWASP_API_Security_Top_10.md
│   └── References.md
│
├── Screenshots/
│   ├── API_Responses/                         # Raw API response body captures
│   ├── Evidence/                              # Error handling test evidence
│   ├── HTTP_Headers/                          # Response header inspection
│   └── Postman/                               # Endpoint request/response pairs
│
├── LICENSE
└── README.md
```

---

## 🧪 Testing Methodology

Testing followed a structured manual black-box approach across seven assessment categories:

1. **Information Gathering** – Identified endpoints, data schemas, and server metadata
2. **Authentication Review** – Verified whether credentials were required to access any endpoint
3. **Authorization Review** – Checked for object-level access controls and ownership validation
4. **Response Header Analysis** – Inspected all HTTP response headers against OWASP recommendations
5. **Sensitive Data Review** – Examined response payloads for excessive field exposure
6. **Error Handling Testing** – Sent requests to invalid endpoints and non-existent resources to assess error responses
7. **Rate Limiting Observation** – Inspected rate limiting response headers

All requests were executed manually via **Postman** using the provided collection and environment files.

---

## 📊 Key Findings

| ID | Finding | OWASP Category | Risk Level |
|---|---|---|---|
| F-01 | Authentication Controls | API1:2023 | ⚪ Informational |
| F-02 | Authorization Controls | API1:2023 | ⚪ Informational |
| F-03 | Sensitive Data Exposure | API3:2023 | 🔵 Low |
| F-04 | Security Headers | API8:2023 | 🔵 Low |
| F-05 | Rate Limiting | API4:2023 | ⚪ Informational |
| F-06 | Error Handling | API8:2023 | ⚪ Informational |
| F-07 | Input Validation | API3/8:2023 | ⚪ Informational |

**Summary:** 0 Critical · 0 High · 0 Medium · **2 Low** · **5 Informational**

> F-01 and F-02 are rated Informational because JSONPlaceholder is a public demonstration API that intentionally requires no authentication or authorization. These controls would be mandatory in any production equivalent.  
> F-04 (Security Headers) is the primary actionable finding — five standard headers are absent and can be configured at the infrastructure layer.

For detailed findings including observations, evidence, business impact, and recommendations, see the [`Findings/`](./Findings/) directory or the full [Report](./Report/).

---

## 📸 Evidence Collected

| Screenshot | Location | Content |
|---|---|---|
| `GET_Users_Request_Response.png` | `Screenshots/Postman/` | GET /users · 200 OK · No auth header |
| `GET_Posts_Request_Response.png` | `Screenshots/Postman/` | GET /posts · 200 OK · 7.98 KB response |
| `GET_Comments_Request_Response.png` | `Screenshots/Postman/` | GET /Comments · 200 OK · 40.77 KB; email fields visible |
| `GET_Albums_Request_Response.png` | `Screenshots/Postman/` | GET /albums · 200 OK · 3.13 KB |
| `GET_Photos_Request_Response.png` | `Screenshots/Postman/` | GET /photos · 200 OK · 129.91 KB |
| `GET_Todos_Request_Response.png` | `Screenshots/Postman/` | GET /todos · 200 OK · 5.05 KB |
| `GET_Users_Response.png` | `Screenshots/API_Responses/` | Full user object: name, email, address, geo, phone |
| `GET_Users_Headers.png` | `Screenshots/HTTP_Headers/` | 26 response headers · missing CSP, HSTS, X-Frame-Options |
| `Invalid_Endpoint.png` | `Screenshots/Evidence/` | GET /invalidendpoint · 404 · body: `{}` |
| `User_Not_Found.png` | `Screenshots/Evidence/` | GET /users/999 · 404 · body: `{}` |

---

## 📄 Report

The full security assessment report is available in two formats:

| Format | File |
|---|---|
| Microsoft Word | [`Report/API_Security_Risk_Analysis_Report.docx`](./Report/API_Security_Risk_Analysis_Report.docx) |
| PDF | [`Report/API_Security_Risk_Analysis_Report.pdf`](./Report/API_Security_Risk_Analysis_Report.pdf) |

The report covers: Executive Summary · Objectives · Scope · Target API Overview · Testing Environment · Methodology · Findings (7) · Risk Assessment Matrix · Recommendations · Conclusion · References.

---

## 🎓 Learning Outcomes

Through this project, the following skills were developed and demonstrated:

- **API Security Testing** – Structured manual assessment of REST API endpoints against OWASP API Security Top 10
- **HTTP Analysis** – Inspection and interpretation of request/response headers, status codes, and response bodies
- **Risk Classification** – Assigning evidence-based risk ratings (Informational / Low / Medium / High / Critical) with documented rationale
- **Technical Report Writing** – Producing a professional, client-ready security assessment document
- **Tool Proficiency** – Postman collection design, environment variables, and response analysis
- **Git & GitHub** – Structured repository organisation with clean commit history

---

## 📚 References

- [OWASP API Security Top 10 – 2023](https://owasp.org/API-Security/editions/2023/en/0x00-header/)
- [JSONPlaceholder – Free Fake REST API](https://jsonplaceholder.typicode.com)
- [RFC 9110 – HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110)
- [RFC 9457 – Problem Details for HTTP APIs](https://www.rfc-editor.org/rfc/rfc9457)
- [NIST SP 800-95 – Guide to Secure Web Services](https://csrc.nist.gov/publications/detail/sp/800-95/final)
- [MDN Web Docs – HTTP Headers Reference](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [Postman Documentation](https://learning.postman.com/docs/)

---

## ⚠️ Disclaimer

This assessment was conducted **strictly for educational purposes** as part of a structured cyber security internship programme. The target API — [JSONPlaceholder](https://jsonplaceholder.typicode.com) — is a publicly available, free, and openly accessible demonstration API containing **entirely fictional, non-personal data**.

No private systems, production environments, or real user data were accessed at any point. No attempt was made to modify, delete, or exploit any API resource. All testing was passive and read-only in nature.

This repository and its contents are intended solely for learning and academic documentation purposes.

---

## 👤 Author

**Harsh Aghera**  
Cyber Security Intern – Future Interns Programme  
GitHub: [@Harshaghera111](https://github.com/Harshaghera111)

---

<div align="center">

*Future Interns Cyber Security Internship · Task 3 · API Security Risk Analysis*

</div>
