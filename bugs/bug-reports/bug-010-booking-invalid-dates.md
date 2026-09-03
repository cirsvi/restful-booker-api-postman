# BUG-010: POST '/booking' accepts invalid 'checkin'/'checkout' dates and returns '200 OK' instead of '400 Bad Request'

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-010 |
| **Priority**       | High |
| **Severity**        | High |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | Create booking with invalid checkin/checkout dates |

## Preconditions:
- None

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/booking` with body (the `checkin` and `checkout` are **invalid**):
```json
{
    "firstname": "{{$randomFirstName}}",
    "lastname": "{{$randomLastName}}",
    "totalprice": {{$randomInt}},
    "depositpaid": {{$randomBoolean}},
    "bookingdates": {
        "checkin": "13-13-2026",
        "checkout": "13-13-2027"
    },
    "additionalneeds": "{{$randomProduct}}"
}
```
2. Observe the response status code and body.

## Expected Results:
- Status code: `400 Bad Request`.
- Response body has a structure with a reason field containing a message that clearly indicates the invalid values for `checkin` and `checkout` (e.g., "checkin and checkout dates have invalid values"). For example:
```json
{
    "reason": "checkin and checkout dates have invalid values"
}
```

## Actual Results:
- Status code: `200 OK`.
- New booking object is created with invalid `checkin` and `checkout` (the values will change for each request, below is just an example):
```json
{
    "bookingid": 5332,
    "booking": {
        "firstname": "Jonatan",
        "lastname": "MacGyver",
        "totalprice": 577,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "0NaN-aN-aN",
            "checkout": "0NaN-aN-aN"
        },
        "additionalneeds": "Bike"
    }
}
```
