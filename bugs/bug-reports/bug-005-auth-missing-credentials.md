# BUG-005: POST '/auth' returns '200 OK' for missing credentials instead of '400 Bad Request'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-005 |
| **Priority**       | Medium |
| **Severity**        | Medium |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | Empty body |

## Preconditions:
- None

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/auth` with **empty** body.
2. Observe the response status code and body.

## Expected Results:
- Status code: `400 Bad Request`.
- Response body contains reason message indicating missing credentials.
- Token is **NOT** returned in response.

## Actual Results:
- Status code: `200 OK`.
- Response body JSON:
```json
{
    "reason": "Bad credentials"
}
```
- Token is **NOT** returned in response.
