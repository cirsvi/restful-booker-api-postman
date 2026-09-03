# BUG-012: POST '/booking' returns '200 OK' for really long 'firstname' input (1000 characters) instead of '400 Bad Request'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-012 |
| **Priority**       | Low |
| **Severity**        | Low |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | Create booking with really long firstname |

## Preconditions:
- `checkIn` and `checkOut` environment variables are set (by the pre-request script).
- `firstName` environment variable (containing the letter 'a' repeated 1000 times) is set by the pre-request script.

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/booking` with body (the `firstname` value is letter `a` repeated 1000 times):
```json
{
    "firstname": "{{firstName}}",
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
- Response body has a structure with a reason field containing a message that clearly indicates the invalid value for `firstname` (e.g., "firstname cannot be longer than 100 characters"). For example:
```json
{
    "reason": "firstname cannot be longer than 100 characters"
}
```
> Note: The exact length limit is not documented; this example assumes a reasonable maximum of 100 characters.

## Actual Results:
- Status code: `200 OK`.
- New booking object is created with invalid `firstname` (the values will change for each request, below is just an example):
```json
{
    "bookingid": 2414,
    "booking": {
        "firstname": "<1000 a's>",
        "lastname": "Kerluke",
        "totalprice": 789,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2026-09-03",
            "checkout": "2027-07-21"
        },
        "additionalneeds": "Salad"
    }
}
```
