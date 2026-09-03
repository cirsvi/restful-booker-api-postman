# BUG-014: PUT '/booking/:id' returns '405 Method Not Allowed' for non-existing ID instead of '404 Not Found'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-014 |
| **Priority**       | Medium |
| **Severity**        | Medium |
| **Reproducibility** | 5/5 |
| **Build Version**   | V1.0 |
| **Environment**     | PROD |
| **Test Case** | Update booking that doesn't exist |

## Preconditions:
- Valid authentication token is available (e.g., obtained via `POST /auth`) and included in the request as `Cookie: token={{token}}`.

## Steps to Reproduce:
1. Send `PUT` request to `{{baseUrl}}/booking/:id` with `id` set 99999 and body:
```json
{
    "firstname": "{{$randomFirstName}}",
    "lastname": "{{$randomLastName}}",
    "totalprice": {{$randomInt}},
    "depositpaid": {{$randomBoolean}},
    "bookingdates": {
        "checkin": "{{checkIn}}",
        "checkout": "{{checkOut}}"
    },
    "additionalneeds": "{{$randomProduct}}"
}
```
2. Observe the response status code and body.

## Expected Results:
- Status code: `404 Not Found`.
- Response body has a structure with a reason field containing a message that clearly indicates the non-existing ID (e.g., "booking with this ID does not exist"). For example:
```json
{
    "reason": "booking with this ID does not exist"
}
```

## Actual Results:
- Status code: `405 Method Not Allowed`.
- Response body: `Method Not Allowed`.
