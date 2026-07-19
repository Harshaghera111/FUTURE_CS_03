# F-02 – Authorization Controls

| Field | Detail |
|---|---|
| **Finding ID** | F-02 |
| **Category** | Authorization – OWASP API1:2023 (BOLA) |
| **Risk Level** | Informational |
| **Status** | Open |

---

## Observation

No authorization controls were observed across any tested endpoint. All resources were accessible to any client without identity verification or ownership checks. Individual user resources could be retrieved by numeric ID (e.g., `GET /users/1`) without any mechanism to confirm the requesting client's entitlement to that specific record.

This behaviour is consistent with the public nature of JSONPlaceholder and is not a defect in this context. In a production API, this pattern would constitute a **Broken Object Level Authorization (BOLA)** vulnerability – OWASP API Security Top 10 – API1:2023, consistently ranked as the most prevalent and impactful API security weakness.

## Evidence

- `GET_Users_Request_Response.png`
- `GET_Users_Response.png`

## Risk Level

**Informational** (for demonstration API – would be **High** in production)

## Business Impact

For this demonstration API, no business impact exists as all data is fictional.

In a production API, the absence of object-level authorization would permit any client to access records belonging to other users by simply enumerating sequential resource IDs, representing a severe and easily exploitable data breach risk.

## Recommendation

Production APIs must implement **per-object authorization checks** that verify the requesting user's entitlement to each specific resource before returning data. Authorization logic must not rely on the obscurity of resource IDs. Return **HTTP 403 Forbidden** for unauthorized access attempts and log all such events for audit review.
