# F-03 – Sensitive Data Exposure

| Field | Detail |
|---|---|
| **Finding ID** | F-03 |
| **Category** | Excessive Data Exposure – OWASP API3:2023 |
| **Risk Level** | Low |
| **Status** | Open |

---

## Observation

The `GET /users` endpoint returns a comprehensive fictional user profile for each record, including:

- Full name, username
- Email address
- Full postal address (street, suite, city, zip code)
- Geographical coordinates (latitude and longitude)
- Phone number, personal website URL
- Company details: name, catch phrase, business tagline

The `GET /comments` endpoint additionally returns **email addresses** associated with each comment entry.

All data returned by JSONPlaceholder is entirely synthetic. However, the response schema demonstrates a pattern of **excessive data exposure** with no field-level filtering or data minimisation applied.

The response header `x-powered-by: Express` also discloses the underlying application framework, which could assist targeted exploit selection in a production context.

## Evidence

- `GET_Users_Response.png`
- `GET_Users_Request_Response.png`
- `GET_Comments_Request_Response.png`
- `GET_Users_Headers.png`

## Risk Level

**Low**

*Rationale: All exposed data is entirely fictional (demonstration API). The risk rating reflects the pattern and potential impact in a production-equivalent system, not actual PII exposure.*

## Business Impact

For this demonstration API, actual business impact is nil as no real personal data is exposed.

In a production environment, unnecessary exposure of PII fields such as email addresses, full postal addresses, and geolocation coordinates could facilitate social engineering attacks, targeted phishing campaigns, physical location tracking, and violations of data protection regulations including **GDPR**.

## Recommendation

- Apply **response field filtering** to return only data fields required by the consuming application.
- Exclude geolocation coordinates, full postal addresses, and internal company metadata from general list endpoints unless explicitly required by a documented use case.
- Remove the `x-powered-by` header from all responses to prevent server technology fingerprinting.
- Implement a data classification policy to govern which fields are permissible in API responses.
