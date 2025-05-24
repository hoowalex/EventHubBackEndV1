# QA Strategy and Test Plan – EventHubBackEndV1

## 1. QA Strategy Overview

This document outlines the QA (Quality Assurance) approach for the EventHub backend system. The goal is to ensure that the core functionalities (event creation, listing, and categorization) work as expected, are well-tested, and meet the requirements specified in the Solution Design Document.

### Testing Levels:
- **Unit Testing** – For serializers, models, and utility functions.
- **Integration Testing** – For API endpoints and database interactions.
- **Manual Exploratory Testing** – UI/UX and API behavior testing using tools like Postman.

### Testing Types:
- **Functional Testing** – Verifying correct implementation of features.
- **Regression Testing** – Ensuring new changes do not break existing functionality.
- **Negative Testing** – Validating behavior under invalid inputs or missing data.

### Tools:
- **Pytest** or **Unittest** (Python standard testing frameworks)
- **DRF test client** for endpoint tests
- **Postman** for manual API testing

---

## 2. Test Plan

### Scope:
- Event creation, listing, and detail retrieval
- Category creation and listing
- Image upload functionality

### Out of Scope:
- Authentication
- Ticket booking and notifications (future features)

### Roles:
- QA Engineer – Responsible for writing and executing tests
- Developer – Supports QA by fixing bugs and adding test coverage

### Entry Criteria:
- APIs must be functional and documented (via drf-yasg)
- Database models and serializers implemented

### Exit Criteria:
- All critical and high priority test cases passed
- No open high-severity bugs

---

## 3. Sample Test Cases

### Test Case 1: Create Event (Valid Data)
- **Objective:** Ensure event can be created with valid input
- **Preconditions:** Valid category and author exist
- **Steps:**
  1. Send POST request to `/event/create/` with all valid fields
- **Expected Result:** 201 Created, event appears in `/eventlist/`

### Test Case 2: Create Event (Missing Name)
- **Objective:** Validate required fields enforcement
- **Steps:**
  1. Send POST request to `/event/create/` without `name`
- **Expected Result:** 400 Bad Request, error message for missing field

### Test Case 3: List Events
- **Objective:** Confirm events can be listed
- **Steps:**
  1. Send GET request to `/eventlist/`
- **Expected Result:** 200 OK with list of events (if any)

### Test Case 4: Get Event by ID
- **Objective:** Validate retrieval of specific event
- **Steps:**
  1. Send GET request to `/event/<valid_id>/`
- **Expected Result:** 200 OK with event data

### Test Case 5: Create Category
- **Objective:** Validate category creation
- **Steps:**
  1. Send POST request to `/category/create/` with `name` and `slug`
- **Expected Result:** 201 Created, category appears in `/categorylist/`

---

## 4. Risks and Mitigations

| Risk | Mitigation |
|------|------------|
| Uploading invalid images | Validate file type and size on both frontend and backend |
| Invalid foreign keys (author, category) | Proper error handling and validation in serializer |
| Database lock/failure | Use transactions, backups, and error logging |

---

## 5. Conclusion

This QA strategy ensures that the EventHub backend is robust, reliable, and ready for deployment. Regular updates to the test plan and regression testing will be required as the project evolves with new features like authentication and ticketing.

---

*Document Version: 1.0*

*Author: QA Team – EventHub*

*Date: 2025-05-24*
