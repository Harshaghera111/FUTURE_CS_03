# F-06 – Error Handling

| Field | Detail |
|---|---|
| **Finding ID** | F-06 |
| **Category** | Security Misconfiguration – OWASP API8:2023 |
| **Risk Level** | Informational |
| **Status** | Open |

---

## Observation

Two deliberate error scenarios were tested to evaluate the API's error handling behaviour.

### Test 1 – Invalid Endpoint

```
GET {{base_url}}/invalidendpoint
```

**Response:** `404 Not Found` · `465 ms` · `1.08 KB`

**Response Body:**
```json
{}
```

### Test 2 – Non-Existent Resource

```
GET {{base_url}}/users/999
```

**Response:** `404 Not Found` · `840 ms` · `1.07 KB`

**Response Body:**
```json
{}
```

**In both cases:**
- ✅ No stack traces
- ✅ No internal error codes or class names
- ✅ No file system paths
- ✅ No database query details
- ✅ No framework or library names
- ✅ Response is minimal, valid JSON
- ✅ Content-type consistent with API format

This represents a **positive security posture** for error handling and information disclosure prevention.

## Evidence

- `Invalid_Endpoint.png`
- `User_Not_Found.png`

## Risk Level

**Informational** (Positive finding – no information leakage observed)

## Business Impact

Proper minimal error handling prevents information leakage that could assist an attacker in mapping the internal architecture, framework, or data model of an application. The current error handling behaviour is appropriate and consistent with OWASP secure coding guidelines. No current risk is identified.

## Recommendation

- Maintain the current minimal error response approach in production implementations.
- Ensure all error responses return generic, non-verbose messages and **never expose**:
  - Stack traces
  - Internal class or method names
  - Database query fragments
  - File system paths
  - Server environment details
- Consider adopting **RFC 9457 (Problem Details for HTTP APIs)** for standardised, consumer-friendly error responses without disclosing internal implementation details.
