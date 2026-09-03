# BUG-007: POST '/booking' returns '500 Internal Server Error' for invalid 'firstname' datatype instead of '400 Bad Request'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-007 |
| **Priority**       | Medium |
| **Severity**        | Medium |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | Create booking fails with invalid datatype for firstname |

## Preconditions:
- `checkIn` and `checkOut` environment variables are set (by the pre-request script).

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/booking` with body (the `firstname` is **integer**):
```json
{
    "firstname": {{$randomInt}},
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
- Response body has a structure with a reason field containing a message that clearly indicates the incorrect type of `firstname` (e.g., "firstname must be a string"). For example:
```json
{
    "reason": "firstname must be a string"
}
```


## Actual Results:
- Status code: `500 Internal Server Error`.
- Response body: `Internal Server Error`.
