# Functional Documentation — ExpenseEase

## Overview
ExpenseEase enables users to securely log in, record income and expenses, and monitor their financial status in real time.  
It also includes an admin role with access to basic user statistics, ensuring visibility without compromising individual data privacy.

---

## Core Functionalities

| Feature | Description |
|----------|-------------|
| **Signup** | New users register via JWT authentication. Their details are synced to PostgreSQL. |
| **Login** | Authenticated access for existing users. |
| **Dashboard Summary** | Shows total income, total expenses, and calculates balance dynamically. |
| **Create Transaction** | Add income or expense with title, amount. |
| **View Transactions** | Display all recent transactions made by the user. |
| **Update Transactions** | Modify an existing transaction’s details. |
| **Update Balance** | Balance recalculates automatically after each add/update/delete. |
| **Delete Transaction** | Remove old or incorrect entries. |
| **Pull to Refresh** | Refresh dashboard data from backend. |
| **Logout** | Securely clear session and redirect to login. |

---

## Module Division

### 1. Authentication Module
- Handled entirely through **JWT**.  
- Provides user registration, login, and token-based session management.  
- Syncs user data into the `users` table on first login.

### 2. Dashboard Module
- Fetches summarized financial data (income, expense, balance).  
- Displays recent transactions and allows pull-to-refresh.

### 3. Transaction Module
- Handles creation, update, deletion, and listing of transactions.  
- Updates balance dynamically after every change.

### 4. Admin Module
- Restricted to users with the **admin** role.  
- Allows viewing total registered users and their names for reporting purposes.

---

## Roles and Authorization

| Role | Access Level | Description |
|------|---------------|-------------|
| **User** | Standard | Can perform all personal expense operations (CRUD). |
| **Admin** | Elevated | Can view total number of users and their names and their email. |

Authorization is enforced using JWT session verification and role-based access checks on the backend.

---

## Tech Stack

| Layer | Technology |
|--------|-------------|
| **Frontend** | Flutter |
| **Mobile** | Flutter |
| **Backend** | Node.js with Express |
| **Database** | PostgreSQL |
| **Authentication** | JWT |
| **Documentation** | MkDocs |