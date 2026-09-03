# BUG-001: GET '/ping' returns '201 Created' instead of '200 OK'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-001 |
| **Priority**       | Low |
| **Severity**        | Low |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | API health check |

## Preconditions:
- None

## Steps to Reproduce:
1. Send `GET` request to `{{baseUrl}}/ping`.
2. Observe the response status code and body.

## Expected Results:
- Status code: `200 OK`.
- Response body contains `OK` or other reasonable messsage.

## Actual Results:
- Status code: `201 Created`.
- Response body: `Created`.
