# BUG-015: GET '/booking/:id' returns '201 Created' instead of '204 No Content'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-015 |
| **Priority**       | Low |
| **Severity**        | Low |
| **Reproducibility** | 5/5 |
| **Build Version**   | V1.0 |
| **Environment**     | PROD |
| **Test Case** | Delete booking |

## Preconditions:
- Valid authentication token is available (e.g., obtained via `POST /auth`) and included in the request as `Cookie: token={{token}}`.
- Booking exists and its `bookingId` is stored in the environment variable `{{bookingId}}`.

## Steps to Reproduce:
1. Send `DELETE` request to `{{baseUrl}}/booking/:id` with `id` set `{{bookingId}}`.
2. Observe the response status code and body.

## Expected Results:
- Status code: `204 No Content`.
- Response body is empty.

## Actual Results:
- Status code: `201 Created`.
- Response body: `Created`.
