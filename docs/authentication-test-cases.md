# Authentication Module

| **Test Case No.** | **Module Name** | **Test Case Description** | **Acceptance Criteria** |
|--------------------|------------------|-----------------------------|--------------------------|
| TC01 | Authentication | Register a new user with valid name, email, and password | User record created successfully in DB and returns `201 Created` |
| TC02 | Authentication | Attempt to register using an existing email ID | API returns `409 Conflict` with message "User already exists" |
| TC03 | Authentication | Register a user without providing a required field (email/password) | API returns `400 Bad Request` with validation error |
| TC04 | Authentication | Register with invalid email format | API returns `400 Bad Request` with message "Invalid email format" |
| TC05 | Authentication | Login with valid credentials (existing user) | Returns `200 OK` and "Login successful" message |
| TC06 | Authentication | Login with invalid password | Returns `401 Unauthorized` with message "Invalid credentials" |
| TC07 | Authentication | Login with non-existing email | Returns `404 Not Found` with message "User not found" |
| TC08 | Authentication | Attempt login with empty email/password fields | Returns `400 Bad Request` with validation message |
| TC09 | Authentication | Check case sensitivity of email during login | Login should work regardless of email case (if case-insensitive) |
| TC10 | Authentication | Logout request from an active user session | Returns `200 OK` and session is cleared or token invalidated |
