# BUG-011: POST '/booking' accepts 'checkin' date that is after 'checkout' date and returns '200 OK' instead of '400 Bad Request'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-011 |
| **Priority**       | High |
| **Severity**        | High |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | Create booking fails when checkin > checkout |

## Preconditions:
- `checkIn` and `checkOut` environment variables are set (by the pre-request script).

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/booking` with body (the `checkin` value is set to a date later than `checkout`):
```json
{
    "firstname": "{{$randomFirstName}}",
    "lastname": "{{$randomLastName}}",
    "totalprice": {{$randomInt}},
    "depositpaid": {{$randomBoolean}},
    "bookingdates": {
        "checkin": "{{checkOut}}",
        "checkout": "{{checkIn}}"
    },
    "additionalneeds": "{{$randomProduct}}"
}
```
2. Observe the response status code and body.

## Expected Results:
- Status code: `400 Bad Request`.
- Response body has a structure with a reason field containing a message that clearly indicates the invalid values for `checkin` and `checkout` (e.g., "checkin cannot be greater than checkout"). For example:
```json
{
    "reason": "checkin cannot be greater than checkout"
}
```

## Actual Results:
- Status code: `200 OK`.
- New booking object is created with invalid `checkin` and `checkout` (the values will change for each request, below is just an example):
```json
{
    "bookingid": 2518,
    "booking": {
        "firstname": "Lacy",
        "lastname": "Bashirian",
        "totalprice": 45,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2027-04-26",
            "checkout": "2026-09-03"
        },
        "additionalneeds": "Car"
    }
}
```
