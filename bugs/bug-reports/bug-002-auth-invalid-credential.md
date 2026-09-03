# BUG-002: POST '/auth' returns '200 OK' for invalid credentials instead of '401 Unauthorized'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-002 |
| **Priority**       | Medium |
| **Severity**        | Medium |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | Invalid credentials |

## Preconditions:
- None

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/auth` with body containing JSON:
```json
{
    "username": "admin",
    "password": "wrongpassword"
}
```
2. Observe the response status code and body.

## Expected Results:
- Status code: `401 Unauthorized`.
- Response body contains reason message indicating wrong credentials.
- Token is **NOT** returned in response.

## Actual Results:
- Status code: `200 OK`.
- Response body JSON (see [BUG-006](bug-006-auth-reason.md) for more details):
```json
{
    "reason": "Bad credentials"
}
```
- Token is **NOT** returned in response.
