# BUG-016: GET '/booking' with 'checkin' and 'checkout' query parameters returns unrelated bookings

| Attribute          | Value |
|--------------------|-------|
| **Bug ID**         | BUG-016 |
| **Priority**       | High |
| **Severity**        | High |
| **Reproducibility** | 5/5 |
| **Build Version**   | V1.0 |
| **Environment**     | PROD |
| **Test Case** | Filter booking ids by check in and check out |

## Preconditions:
- Booking exists and its `bookingId` is stored in the environment variable `{{bookingId}}`.
- `checkIn` and `checkOut` environment variables are set.

## Steps to Reproduce:
1. Send `GET` request to `{{baseUrl}}/booking?checkin={{checkIn}}&checkout={{checkOut}}` with `checkin` and `checkout` query parameters set to environment variables.
2. Observe the response status code and body.

## Expected Results:
- Status code: `200 OK`.
- Response body returns a list of bookingids and ID of previously created booking (e.g., {{bookingId}}=4488) is in the list:
```json
[
    {
        "bookingid": 4
    },
    {
        "bookingid": 520
    },
    {
        "bookingid": 4488
    }
]
```

## Actual Results:
- Status code: `200 OK`.
- Response body returns a list of bookingids and ID of previously created booking (e.g., {{bookingId}}=4488) is **NOT** in the list:
```json
[
    {
        "bookingid": 4
    },
    {
        "bookingid": 520
    },
    {
        "bookingid": 3810
    }
]
```
> Note: Sometimes, the same request submitted multiple times in a row results in completely different IDs listed.