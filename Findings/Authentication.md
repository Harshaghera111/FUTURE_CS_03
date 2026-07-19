# F-01 – Authentication Controls

| Field | Detail |
|---|---|
| **Finding ID** | F-01 |
| **Category** | Authentication – OWASP API1:2023 |
| **Risk Level** | Informational |
| **Status** | Open |

---

## Observation

All eight tested endpoints responded with HTTP 200 OK without requiring any form of authentication credential. No API key, Bearer token, session cookie, or HTTP Basic Authentication header was present in any request. The Postman Authorization tab was configured to **No Auth** for all requests, confirming the API enforces no authentication mechanism.

This behaviour is intentional for JSONPlaceholder, a publicly available demonstration API containing entirely fictional data. In a production environment, unauthenticated access to equivalent endpoints would constitute a **Critical** vulnerability under OWASP API Security Top 10 – API1:2023 (Broken Authentication).

## Evidence

- `GET_Users_Request_Response.png`
- `GET_Posts_Request_Response.png`
- `GET_Comments_Request_Response.png`
- `GET_Albums_Request_Response.png`
- `GET_Photos_Request_Response.png`
- `GET_Todos_Request_Response.png`

## Risk Level

**Informational** (for demonstration API – would be **Critical** in production)

## Business Impact

For JSONPlaceholder as a demonstration API, the absence of authentication carries no real business impact as all data is entirely fictitious.

In a production-equivalent system, unrestricted unauthenticated access would expose all user records, enabling mass data enumeration, account discovery, and potential violations of applicable data protection legislation.

## Recommendation

For production API implementations, enforce **OAuth 2.0 with JWT Bearer token authentication** or API key authentication enforced at the gateway layer. All endpoints must validate a credential before returning data. Unauthenticated requests should receive **HTTP 401 Unauthorized** with an appropriate `WWW-Authenticate` response header.
