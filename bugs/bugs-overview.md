# Bug Report Overview - RestfulBooker

All bug reports below are grouped by feature/endpoint. Click any ID to open the detailed bug report file for more details.

## Ping

| ID | HTTP Method | Description | Severity | Priority | Test(s) |
|----|-------------|-------------|----------|----------|------|
|[BUG-001](bug-reports/bug-001-ping-get.md) | `GET` | `/ping` returns `201 Created` instead of `200 OK` | Low | Low | API health check |


## Authorization

| ID | HTTP Method | Description | Severity | Priority | Test(s) |
|----|-------------|-------------|----------|----------|------|
|[BUG-002](bug-reports/bug-002-auth-invalid-credential.md) | `POST` | `/auth` returns `200 OK` for invalid credentials instead of `401 Unauthorized` | Medium | Medium | Invalid credentials |
|[BUG-003](bug-reports/bug-003-auth-missing-username.md) | `POST` |  `/auth` returns `200 OK` for missing `username` instead of `400 Bad Request` | Medium | Medium | Missing username |
|[BUG-004](bug-reports/bug-004-auth-missing-password.md) | `POST` | `/auth` returns `200 OK` for missing `password` instead of `400 Bad Request` | Medium | Medium | Missing password |
|[BUG-005](bug-reports/bug-005-auth-missing-credentials.md) | `POST` | `/auth` returns `200 OK` for missing credentials instead of `400 Bad Request` | Medium | Medium | Empty body |
|[BUG-006](bug-reports/bug-006-auth-reason.md) | `POST` | `/auth` returns misleading reason "Bad credentials" when fields are missing | Low | Low | Missing username; Missing password; Empty body |

## Booking

| ID | HTTP Method | Description | Severity | Priority | Test(s) |
|----|-------------|-------------|----------|----------|------|
|[BUG-007](bug-reports/bug-007-booking-invalid-datatype.md) | `POST` | `/booking` returns `500 Internal Server Error` for invalid `firstname` datatype instead of `400 Bad Request` | Medium | Medium | Create booking fails with invalid datatype for firstname |
|[BUG-008](bug-reports/bug-008-booking-negative-totalprice.md) | `POST` | `/booking` accepts negative `totalprice` and returns `200 OK` instead of `400 Bad Request` | High | High | Create booking fails with negative totalprice |
|[BUG-009](bug-reports/bug-009-booking-missing-firstname.md) | `POST` | `/booking` returns `500 Internal Server Error` for missing `firstname` instead of `400 Bad Request` | Medium | Medium | Create booking with missing required field |
|[BUG-010](bug-reports/bug-010-booking-invalid-dates.md) | `POST` | `/booking` accepts invalid `checkin`/`checkout` dates and returns `200 OK` instead of `400 Bad Request` | High | High | Create booking with invalid checkin/checkout dates |
|[BUG-011](bug-reports/bug-011-booking-checkin-bigger-than-checkout.md) | `POST` | `/booking` accepts `checkin` date that is after `checkout` date and returns `200 OK` instead of `400 Bad Request` | High | High | Create booking fails when checkin > checkout |
|[BUG-012](bug-reports/bug-012-booking-really-long-firstname.md) | `POST` | `/booking` returns `200 OK` for really long `firstname` input (1000 characters) instead of `400 Bad Request` | Low | Low | Create booking with really long firstname |
|[BUG-013](bug-reports/bug-013-booking-delete-non-existing.md) | `DELETE` | `/booking/:id` returns `405 Method Not Allowed` for non-existing ID instead of `404 Not Found` | Medium | Medium | Delete booking that doesn't exist |
|[BUG-014](bug-reports/bug-014-booking-update-non-existing.md) | `PUT` | `/booking/:id` returns `405 Method Not Allowed` for non-existing ID instead of `404 Not Found`| Medium | Medium | Update booking that doesn't exist |
|[BUG-015](bug-reports/bug-015-booking-delete-status-code.md) | `DELETE` | `/booking/:id` returns `201 Created` instead of `204 No Content` | Low | Low | Delete booking |
|[BUG-016](bug-reports/bug-016-booking-dates-query.md) | `GET` | GET `/booking` with `checkin` and `checkout` query parameters returns unrelated bookings | High | High | Filter booking ids by check in and check out |