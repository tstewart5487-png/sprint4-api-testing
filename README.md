# Sprint 4 – API Testing Project

**Course:** TripleTen QA Engineering Bootcamp  
**Sprint:** 4 of 9  
**Focus:** API Testing with Postman & Jira

---

## Overview

This project covers API test design, execution, and bug reporting for two backend features of a grocery delivery application. Tests were designed using boundary value analysis and equivalence partitioning, then executed in Postman.

---

## Features Tested

### 1. Working with Kits (`POST /api/v1/kits/:id/products`)
Tests cover adding products to kits via the REST API, including:
- Valid product and kit IDs
- Boundary values for product list size (up to 30 items)
- Invalid inputs: negative, decimal, string, empty, missing, and non-Latin values for both kit ID (path param) and product ID/quantity (request body)

### 2. Working with Deliveries (`POST /fast-delivery/v3.1.1/calculate-delivery.xml`)
Tests cover the Fast Delivery service calculation endpoint (XML-based), including:
- Operating hours boundary testing (`deliveryTime` 7–21)
- Delivery cost tiers by `productsCount` and `productsWeight`
- Client vs. host delivery cost logic
- Invalid inputs: non-Latin characters, special characters, empty and missing parameters, malformed XML

---

## Test Results Summary

| Feature | Total Tests | Passed | Failed |
|---|---|---|---|
| Working with Kits | 34 | 20 | 14 |
| Working with Deliveries | 48 | 22 | 26 |
| **Total** | **82** | **42** | **40** |

---

## Bugs Found

Bug reports were filed in Jira (project: **S4AT**). Key issues include:
- **500 Internal Server Error** returned instead of `400 Bad Request` for invalid input types (decimal, string, special characters, non-Latin) across both endpoints
- **Kit API accepts invalid data** — negative product IDs, missing product IDs, negative quantities, empty quantities, and extreme quantities all returned `200 OK` instead of `400 Bad Request`
- **Delivery time boundary failure** — `isItPossibleToDeliver="false"` not returned for times outside 7–21; endpoint returns a successful response instead
- **Delivery cost tier miscalculation** — incorrect `hostDeliveryCost` and `clientDeliveryCost` values returned for higher `productsCount` (≥15) and `productsWeight` (≥6.1 kg) values
- **405 Method Not Allowed** returned instead of `404 Not Found` for missing kit ID path param and special character kit IDs

---

## Files

| File | Description |
|---|---|
| `test-cases project 4.html` | [Interactive test case viewer](https://tstewart5487-png.github.io/sprint4-api-testing/test-cases%20project%204.html) — filterable by section, status, and keyword |
| `Project 4_ Task - Test Cases.csv` | Raw test cases with steps, test data, expected vs. actual results, and status |
| `README.md` | This file |

---

## Tools Used

- **Postman** – API request execution
- **Jira** – Bug tracking and reporting
- **Google Sheets** – Test case documentation
- **apiDoc** – API documentation reference

---

## Skills Demonstrated

- API test case design (boundary value analysis, equivalence partitioning)
- REST and XML API testing
- Bug report writing with reproduction steps
- Test result documentation and reporting
