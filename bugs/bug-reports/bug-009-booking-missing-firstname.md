# BUG-009: POST '/booking' returns '500 Internal Server Error' for missing 'firstname' instead of '400 Bad Request'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-009 |
| **Priority**       | Medium |
| **Severity**        | Medium |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | Create booking with missing required field |

## Preconditions:
- `checkIn` and `checkOut` environment variables are set (by the pre-request script).

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/booking` with body (the `firstname` is **missing**):
```json
{
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
- Status code: `400 Bad Request`.
- Response body has a structure with a reason field containing a message that clearly indicates the missing value for `firstname` (e.g., "firstname is a required field"). For example:
```json
{
    "reason": "firstname is a required field"
}
```

## Actual Results:
- Status code: `500 Internal Server Error`.
- Response body: `Internal Server Error`.
