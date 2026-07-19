# F-07 – Input Validation

| Field | Detail |
|---|---|
| **Finding ID** | F-07 |
| **Category** | OWASP API3:2023 / API8:2023 |
| **Risk Level** | Informational |
| **Status** | Open |

---

## Observation

Input validation testing was limited to read-only GET requests within the agreed scope of this assessment. No POST, PUT, PATCH, or DELETE requests with crafted payloads were submitted, as write operations were outside the defined assessment scope.

All well-formed GET requests returned expected JSON responses with HTTP 200 OK.

### Notable Observation – Case-Insensitive Routing

The endpoint URL `/Comments` (with an uppercase **'C'**) returned:

```
HTTP 200 OK · 1.15 s · 40.77 KB
```

This suggests the server applies **case-insensitive URL routing**. This is not a vulnerability in isolation but is documented for completeness.

### Tests Not Performed (Out of Scope)

- SQL/NoSQL injection payloads
- Path traversal strings (`../`, `..%2F`)
- Parameter pollution
- Oversized input / fuzzing
- Mass assignment payloads

> **Unable to verify input validation robustness within the scope of this assessment.**

## Evidence

- `GET_Comments_Request_Response.png`

## Risk Level

**Informational** (Scope-limited – unable to assess write operations)

## Business Impact

Unable to fully assess within the current read-only scope.

In production APIs, insufficient input validation could enable:
- Injection attacks (SQL, NoSQL, command)
- Path traversal
- Mass assignment vulnerabilities
- Parameter pollution

Relevant OWASP references: API3:2023 (Broken Object Property Level Authorization), API8:2023 (Security Misconfiguration).

## Recommendation

- Production APIs must implement **server-side input validation** for all user-supplied inputs including path parameters, query strings, and request bodies.
- Prefer **allowlisting** over denylisting.
- Validate data types, lengths, formats, and value ranges.
- Return **HTTP 400 Bad Request** for invalid input without disclosing internal schema details or validation logic.
- Conduct a **dedicated input validation assessment** as a follow-up engagement covering POST/PUT/PATCH/DELETE operations and injection payloads.
