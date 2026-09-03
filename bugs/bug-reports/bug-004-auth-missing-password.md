# BUG-004: POST '/auth' returns '200 OK' for missing 'password' instead of '400 Bad Request'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-004 |
| **Priority**       | Medium |
| **Severity**        | Medium |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | Missing password |

## Preconditions:
- None

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/auth` with body containing JSON:
```json
{
    "username": "{{username}}"
}
```
2. Observe the response status code and body.

## Expected Results:
- Status code: `400 Bad Request`.
- Response body contains reason message indicating missing credential/password.
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
