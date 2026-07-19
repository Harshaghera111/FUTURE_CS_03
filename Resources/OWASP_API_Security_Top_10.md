# OWASP API Security Top 10 – 2023

Reference document for the API Security Risk Analysis conducted as part of Future Interns Cyber Security Internship – Task 3.

Source: https://owasp.org/API-Security/editions/2023/en/0x00-header/

---

## API1:2023 – Broken Object Level Authorization (BOLA)

APIs tend to expose endpoints that handle object identifiers, creating a wide attack surface. Object level authorization checks should be considered in every function that accesses a data source using an input from the user.

**Assessed in this project:** F-01 (Authentication Controls), F-02 (Authorization Controls)

---

## API2:2023 – Broken Authentication

Authentication mechanisms are often implemented incorrectly, allowing attackers to compromise authentication tokens or exploit implementation flaws to assume other user identities temporarily or permanently.

**Assessed in this project:** F-01 (Authentication Controls)

---

## API3:2023 – Broken Object Property Level Authorization

This category combines API3:2019 Excessive Data Exposure and API6:2019 Mass Assignment, focusing on the root cause: the lack of or improper authorization validation at the object property level.

**Assessed in this project:** F-03 (Sensitive Data Exposure), F-07 (Input Validation)

---

## API4:2023 – Unrestricted Resource Consumption

Satisfying API requests requires resources such as network bandwidth, CPU, memory, and storage. Other resources such as emails/SMS/phone calls or biometrics validation are made available by service providers via API integrations, and paid for per request.

**Assessed in this project:** F-05 (Rate Limiting)

---

## API5:2023 – Broken Function Level Authorization

Complex access control policies with different hierarchies, groups, and roles, and an unclear separation between administrative and regular functions, tend to lead to authorization flaws.

**Assessed in this project:** F-02 (Authorization Controls)

---

## API6:2023 – Unrestricted Access to Sensitive Business Flows

APIs vulnerable to this risk expose a business flow — such as buying a ticket, or posting a comment — without compensating for how the functionality could harm the business if used excessively in an automated manner.

**Assessed in this project:** Not in scope for this assessment (demonstration API context).

---

## API7:2023 – Server Side Request Forgery (SSRF)

Server-Side Request Forgery (SSRF) flaws can occur when an API is fetching a remote resource without validating the user-supplied URL.

**Assessed in this project:** Not in scope for this assessment.

---

## API8:2023 – Security Misconfiguration

APIs and the systems supporting them typically contain complex configurations, intended to make the APIs more customizable. Software and DevOps engineers can miss these configurations, or don't follow security best practices when it comes to configuration, opening the door to different types of attacks.

**Assessed in this project:** F-04 (Security Headers), F-06 (Error Handling), F-07 (Input Validation)

---

## API9:2023 – Improper Inventory Management

APIs tend to expose more endpoints than traditional web applications, making proper and updated documentation highly important. A proper inventory of hosts and deployed API versions also is important to mitigate issues such as deprecated API versions and exposed debug endpoints.

**Assessed in this project:** Not in scope for this assessment.

---

## API10:2023 – Unsafe Consumption of APIs

Developers tend to trust data received from third-party APIs more than user input, and so tend to adopt weaker security standards. In order to compromise APIs, attackers go after integrated third-party services instead of trying to compromise the target API directly.

**Assessed in this project:** Not in scope for this assessment.

---

## Mapping to This Assessment

| Finding | OWASP Category | API Security Top 10 Reference |
|---|---|---|
| F-01 – Authentication Controls | API1:2023, API2:2023 | Broken Object Level Authorization / Broken Authentication |
| F-02 – Authorization Controls | API1:2023 | Broken Object Level Authorization |
| F-03 – Sensitive Data Exposure | API3:2023 | Broken Object Property Level Authorization |
| F-04 – Security Headers | API8:2023 | Security Misconfiguration |
| F-05 – Rate Limiting | API4:2023 | Unrestricted Resource Consumption |
| F-06 – Error Handling | API8:2023 | Security Misconfiguration |
| F-07 – Input Validation | API3:2023 / API8:2023 | Broken Object Property Level Authorization / Security Misconfiguration |
