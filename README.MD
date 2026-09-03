# :orange_circle: RestfulBooker API Postman Testing

<div align="center">

[![Postman](https://img.shields.io/badge/Postman-FF6C37?logo=postman&logoColor=white)](#) [![Newman](https://img.shields.io/badge/Newman-00B265?logo=postman&logoColor=white)](#) [![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=000)](#) ![Markdown](https://img.shields.io/badge/Markdown-000000?logo=markdown&logoColor=white) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

</div>

## Overview

This repository contains a **Postman** collection for automated API testing of **[RestfulBooker](https://restful-booker.herokuapp.com) demo hotel booking API**. 

The collection includes positive and negative test scenarios, validation of response schemas, and checks for expected status codes. All discovered defects are documented in the **[Bug Report Overview](/bugs/bugs-overview.md)** section with full reproduction steps.

Link to **RestfulBooker Documentation**: https://restful-booker.herokuapp.com/apidoc/index.html

## Test Coverage

The collection covers total of **25 test cases**.

| Feature / Area | Test Scenarios | Test Count |
|----------------|----------------|------------|
| Health Check   | Ping endpoint status code and body | 1 |
| Authentication | Valid login, invalid credentials, missing fields | 5 |
| Booking CRUD   | Create, read, update, delete (valid, invalid, and access restriction) | 17 |
| Filtering      | By name, dates | 2 |
