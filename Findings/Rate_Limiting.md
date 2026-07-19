# F-05 – Rate Limiting

| Field | Detail |
|---|---|
| **Finding ID** | F-05 |
| **Category** | Unrestricted Resource Consumption – OWASP API4:2023 |
| **Risk Level** | Informational |
| **Status** | Open |

---

## Observation

The response header `x-ratelimit-limit: 1000` was observed in the HTTP response headers for `GET /users`, indicating a rate limiting mechanism is implemented with a threshold of **1,000 requests**.

However:

- The **rate limiting time window** (per second, per minute, or per hour) was **not disclosed** in the captured response headers.
- Supplementary headers indicating remaining allowance (`x-ratelimit-remaining`) and reset timestamp (`x-ratelimit-reset`) were **not visible** in the response.
- **No rate limit enforcement was triggered** during testing, as only a small number of manual requests were submitted.
- Formal load or stress testing was outside the scope of this assessment.

> The effectiveness of the rate limiting mechanism cannot be fully verified within the scope of this assessment.

## Evidence

- `GET_Users_Headers.png`

## Risk Level

**Informational** (Positive indicator – rate limiting header observed)

## Business Impact

The presence of an `x-ratelimit-limit` header is a positive indicator that denial-of-service and enumeration risks have been considered. Without confirmation of the enforcement window and mechanism, residual risk cannot be precisely quantified.

In production, inadequate rate limiting could enable:
- Denial-of-service attacks
- Credential stuffing
- Mass data enumeration at scale

## Recommendation

- Verify and expose the full rate limiting configuration in response headers:
  - `x-ratelimit-window` (time window)
  - `x-ratelimit-remaining` (remaining request count)
  - `x-ratelimit-reset` (UTC reset timestamp)
- Ensure limits are enforced per authenticated identity or source IP for unauthenticated endpoints.
- Return **HTTP 429 Too Many Requests** with a `Retry-After` header when limits are exceeded.
- Consider implementing exponential backoff throttling before hard limits are reached.
