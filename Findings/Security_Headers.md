# F-04 – Security Headers

| Field | Detail |
|---|---|
| **Finding ID** | F-04 |
| **Category** | Security Misconfiguration – OWASP API8:2023 |
| **Risk Level** | Low |
| **Status** | Open |

---

## Observation

Inspection of the HTTP response headers returned by `GET /users` (26 headers total) identified that several security-relevant headers recommended by OWASP and industry best practice were absent.

### Headers Observed (Present)

| Header | Value |
|---|---|
| `x-content-type-options` | `nosniff` ✓ |
| `cache-control` | `max-age=43200` (12-hour client caching) |
| `pragma` | `no-cache` |
| `content-type` | `application/json; charset=utf-8` ✓ |
| `etag` | `W/"160d-1eMSsxeJRfnVLRBmYJSbCiJZ1qQ"` |
| `x-ratelimit-limit` | `1000` ✓ |
| `server` | `cloudflare` |

### Security Headers Absent

| Header | Status |
|---|---|
| `Content-Security-Policy` | ❌ Not present |
| `X-Frame-Options` | ❌ Not present |
| `Strict-Transport-Security` | ❌ Not present |
| `Referrer-Policy` | ❌ Not present |
| `Permissions-Policy` | ❌ Not present |

Additionally, `x-powered-by: Express` discloses the backend application framework.

## Evidence

- `GET_Users_Headers.png`

## Risk Level

**Low**

*Rationale: Missing security headers are a directly observable gap confirmed by screenshot evidence. Risk is rated Low (not Medium) because JSONPlaceholder is a demonstration API and the missing headers primarily affect browser-facing applications. In a production deployment, this would be rated Medium.*

## Business Impact

- **Absent HSTS**: Could permit SSL stripping on unprotected connections
- **Missing CSP**: Increases XSS exploitation risk in browser-facing frontend applications
- **Absent X-Frame-Options**: Could enable clickjacking attacks
- **`x-powered-by` disclosure**: Assists targeted exploit selection against known Express.js vulnerabilities
- **12-hour cache-control**: Could cause stale data to persist in client caches

## Recommendation

Configure the API server or reverse proxy to include the following headers on all responses:

```
Strict-Transport-Security: max-age=31536000; includeSubDomains
Content-Security-Policy: default-src 'none'
X-Frame-Options: DENY
Referrer-Policy: no-referrer
Permissions-Policy: geolocation=(), microphone=(), camera=()
```

Remove the `x-powered-by` header entirely. These settings are typically applied at the infrastructure layer (Nginx, Cloudflare, AWS CloudFront, API Gateway) and **require no application code changes**.
