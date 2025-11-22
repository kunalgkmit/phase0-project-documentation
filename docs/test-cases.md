# Testing Plan

---

## 1. Registration Tests

| Scenario            | Test Steps                                                                 | Expected                               |
|---------------------|----------------------------------------------------------------------------|-----------------------------------------|
| Valid Registration | 1. Enter valid name, email, password<br>2. Submit                         | User registered successfully            |
| Duplicate Email    | 1. Enter an already registered email<br>2. Submit                         | Error: "User already exists"            |
| Invalid Email      | 1. Enter invalid email format<br>2. Submit                                | Validation error                        |
| Weak Password      | 1. Enter short password<br>2. Submit                                 | Validation error                        |
| Empty Fields       | 1. Leave name/email/password empty<br>2. Submit                           | Field validation errors                 |

---

## 2. Login Tests

| Scenario            | Test Steps                                                                 | Expected                               |
|---------------------|----------------------------------------------------------------------------|-----------------------------------------|
| Valid Login       | 1. Enter valid email & password<br>2. Submit                              | Login successful, tokens returned       |
| Invalid Password  | 1. Enter valid email but wrong password<br>2. Submit                      | Error: "Invalid credentials"            |
| User Not Found    | 1. Enter unregistered email<br>2. Submit                                  | Error: "User does not exist"            |
| Empty Fields      | 1. Leave required fields empty<br>2. Submit                               | Validation error                        |
| Missing Password  | 1. Enter email only<br>2. Submit                                          | Error: "Invalid credentials"            |

---

## 3. Transaction Tests

| Scenario                       | Test Steps                                                                 | Expected                                   |
|--------------------------------|----------------------------------------------------------------------------|---------------------------------------------|
| Create Transaction (Valid)    | 1. Enter valid user_id, title, amount<br>2. Submit                        | Transaction created successfully            |
| Create Transaction (Missing Fields) | 1. Leave user_id or title or amount empty<br>2. Submit               | Error: "Invalid user_id, title, or amount"  |
| Get Summary (Valid user_id)   | 1. Call `/summary/:user_id` with valid ID                                 | Returns totalBalance, totalIncome, totalExpense |
| Get Summary (Missing user_id) | 1. Call `/summary/` without user_id                                       | Error: "user_id is required"                |
| Delete Transaction (Invalid)  | 1. Call delete API with missing/invalid user_id                           | Error: "user_id is required"                |

