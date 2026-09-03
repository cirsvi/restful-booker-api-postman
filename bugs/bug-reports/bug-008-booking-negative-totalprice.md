# BUG-008: POST '/booking' accepts negative 'totalprice' and returns '200 OK' instead of '400 Bad Request'
| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-008 |
| **Priority**       | High |
| **Severity**        | High |
| **Reproducibility** | 5/5 |
| **Build Version**        | V1.0 |
| **Environment**        | PROD |
| **Test Case** | Create booking fails with negative totalprice |

## Preconditions:
- `checkIn` and `checkOut` environment variables are set (by the pre-request script).

## Steps to Reproduce:
1. Send `POST` request to `{{baseUrl}}/booking` with body (the `totalprice` is **negative**):
```json
{
    "firstname": "{{$randomFirstName}}",
    "lastname": "{{$randomLastName}}",
    "totalprice": -{{$randomInt}},
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
- Response body has a structure with a reason field containing a message that clearly indicates the incorrect value for `totalprice` (e.g., "totalprice must be greater than 0"). For example:
```json
{
    "reason": "totalprice must be greater than 0"
}
```

## Actual Results:
- Status code: `200 OK`.
- New booking object is created with invalid `totalprice` (the values will change for each request, below is just an example):
```json
{
    "bookingid": 2840,
    "booking": {
        "firstname": "Katlynn",
        "lastname": "Orn",
        "totalprice": -163,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2026-09-03",
            "checkout": "2027-08-19"
        },
        "additionalneeds": "Tuna"
    }
}
```