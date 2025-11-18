# Testing Plan

---

## 1. Registration Tests

| TC-ID | Scenario            | Test Steps                                                                 | Expected                               |
|------|---------------------|----------------------------------------------------------------------------|-----------------------------------------|
| REG-01 | Valid Registration | 1. Enter valid name, email, password<br>2. Submit                         | User registered successfully            |
| REG-02 | Duplicate Email    | 1. Enter an already registered email<br>2. Submit                         | Error: "User already exists"            |
| REG-03 | Invalid Email      | 1. Enter invalid email format<br>2. Submit                                | Validation error                        |
| REG-04 | Weak Password      | 1. Enter short/weak password<br>2. Submit                                 | Validation error                        |
| REG-05 | Empty Fields       | 1. Leave name/email/password empty<br>2. Submit                           | Field validation errors                 |

---

## 2. Login Tests

| TC-ID | Scenario            | Test Steps                                                                 | Expected                               |
|------|---------------------|----------------------------------------------------------------------------|-----------------------------------------|
| LOG-01 | Valid Login       | 1. Enter valid email & password<br>2. Submit                              | Login successful, tokens returned       |
| LOG-02 | Invalid Password  | 1. Enter valid email but wrong password<br>2. Submit                      | Error: "Invalid credentials"            |
| LOG-03 | User Not Found    | 1. Enter unregistered email<br>2. Submit                                  | Error: "User does not exist"            |
| LOG-04 | Empty Fields      | 1. Leave required fields empty<br>2. Submit                               | Validation error                        |
| LOG-05 | Missing Password  | 1. Enter email only<br>2. Submit                                          | Error: "Invalid credentials"            |

---

## 3. Transaction Tests

| TC-ID | Scenario                       | Test Steps                                                                 | Expected                                   |
|------|--------------------------------|----------------------------------------------------------------------------|---------------------------------------------|
| TR-01 | Create Transaction (Valid)    | 1. Enter valid user_id, title, amount<br>2. Submit                        | Transaction created successfully            |
| TR-02 | Create Transaction (Missing Fields) | 1. Leave user_id or title or amount empty<br>2. Submit               | Error: "Invalid user_id, title, or amount"  |
| TR-03 | Get Summary (Valid user_id)   | 1. Call `/summary/:user_id` with valid ID                                 | Returns totalBalance, totalIncome, totalExpense |
| TR-04 | Get Summary (Missing user_id) | 1. Call `/summary/` without user_id                                       | Error: "user_id is required"                |
| TR-05 | Delete Transaction (Invalid)  | 1. Call delete API with missing/invalid user_id                           | Error: "user_id is required"                |

