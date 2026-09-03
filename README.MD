# :orange_circle: RestfulBooker API Postman Testing

<div align="center">

[![CI](https://github.com/cirsvi/restful-booker-api-postman/actions/workflows/newman.yml/badge.svg)](https://github.com/cirsvi/restful-booker-api-postman/actions/workflows/newman.yml) [![Postman](https://img.shields.io/badge/Postman-FF6C37?logo=postman&logoColor=white)](#) [![Newman](https://img.shields.io/badge/Newman-00B265?logo=postman&logoColor=white)](#) [![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=000)](#) ![Markdown](https://img.shields.io/badge/Markdown-000000?logo=markdown&logoColor=white) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

</div>

## Overview

This repository contains a **Postman** collection for automated API testing of **[RestfulBooker](https://restful-booker.herokuapp.com) demo hotel booking API**. 

The collection includes positive and negative test scenarios, validation of response schemas, and checks for expected status codes. All discovered defects are documented in the **[Bug Report Overview](/bugs/bugs-overview.md)** section with full reproduction steps.

- Link to **RestfulBooker Documentation**: https://restful-booker.herokuapp.com/apidoc/index.html

## Test Coverage

The collection covers a total of **26 test cases/requests**.

| Feature / Area | Test Scenarios | Test Count |
|----------------|----------------|------------|
| Health Check   | Ping endpoint status code and body | 1 |
| Authentication | Valid login, invalid credentials, missing fields | 5 |
| Booking CRUD   | Create, read, update, delete (valid, invalid, and access restriction) | 18 |
| Filtering      | By name, dates | 2 |

In total, there were **67 assertions** and **28 (42%) of them failed**:
<img src="/attachments/newman-summary.png" width="700" alt="Newman summary screenshot">

> [!NOTE]  
> The 28 failed assertions are mostly due to the documented bugs and are intentionally left failing to demonstrate the defects.

## Known Defects

During testing, 16 defects were identified and documented. Each bug report includes preconditions, steps to reproduce, and expected vs actual results.

See the **[Bug Report Overview](/bugs/bugs-overview.md)** for the full list.

**Example defects:**
- **[BUG-008](/bugs/bug-reports/bug-008-booking-negative-totalprice.md):** `POST` `/booking` accepts negative `totalprice` and returns `200 OK` instead of `400 Bad Request`
- **[BUG-010](/bugs/bug-reports/bug-010-booking-invalid-dates.md):** `POST` `/booking` accepts invalid `checkin`/`checkout` dates and returns `200 OK` instead of `400 Bad Request`
- **[BUG-015](/bugs/bug-reports/bug-015-booking-delete-status-code.md):** `DELETE` `/booking/:id` returns `201 Created` instead of `204 No Content`

Majority of the defects are due to misleading status codes returned with the response that do not follow good practices of REST APIs.

## Getting Started

### Prerequisites
- **Postman** (either desktop application or web-browser)
- Optionally: **Git**

### 1. Download the files
- Download individual .json files with collection and environment from `/postman` folder OR clone repository using Git:

```
git clone https://github.com/cirsvi/restful-booker-api-postman.git
```

### 2. Import into Postman
1. Open Postman.
2. Click **Import** in top-left corner and import the files/drag and drop them (from `/postman` folder).
<img src="/attachments/postman-import.png" width="500" alt="Postman import button">
3. In the top-right dropdown select the imported environment.
<img src="/attachments/postman-environment.png" width="700" alt="Postman environment dropdown">

### 3. Run the Collection:
1. Click the collection name and choose **Run** option:
<img src="/attachments/postman-collection-options.png" width="400" alt="Postman collection options">
2. Run the collection:
<img src="/attachments/postman-start-run.png" width="500" alt="Postman run window overview">


**Expected results:** 26 requests will run, with 67 assertions.

## Continuous Integration (CI)

This project uses **GitHub Actions** for CI. The workflow (`.github/workflows/newman.yml`, named "RestfulBooker API Tests") triggers on every `push` and `pull` request to the `main` branch.

The pipeline installs **Newman** and the **htmlextra** reporter, runs the full Postman collection against the demo API, and uploads the generated HTML report as an artifact.

> [!NOTE]  
> Because the API contains known defects, the workflow uses `continue-on-error: true` to ensure the CI run remains green while still reporting the failed assertions in the test report.

## Repository Structure
- **`.github/workflows/`**: GitHub Actions CI pipeline definitions.
- **`bugs/`**: Detailed bug reports with evidence and an overview.
    - **[`bugs-overview.md`](/bugs/bugs-overview.md)** - Full list of bugs by feature.
    - **`bug-reports/`** – Detailed bug report files (one per bug).
- **`attachments/`**: Screenshots used in the `README.md`.
- **`postman/`**: Contains Postman test collection and environment.
