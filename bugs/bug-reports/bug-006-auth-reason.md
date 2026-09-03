# BUG-006: POST '/auth' returns misleading reason "Bad credentials" when fields are missing

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-006 |
| **Priority**       | Low |
| **Severity**        | Low |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Cases** | Missing username; Missing password; Empty body |

## Preconditions:
- None

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/auth` with **one or more fields missing** (e.g., only `username` or only `password`, or an empty body).
2. Observe the response status code and body.

## Expected Results:
- Response body contains a reson message that clearly indicates **which field** is missing, such as `Missing username` or `Missing password`.

## Actual Results:
- Response body always returns:
```json
{
    "reason": "Bad credentials"
}
```