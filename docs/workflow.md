## Workflow

1. **User Authentication**

   - User signs up or logs in via Clerk.
   - Backend verifies Clerk session and syncs the user.

2. **Dashboard Initialization**

   - App fetches total income, expense, and recent transactions.

3. **Transaction Operations**

   - User can add, edit, or delete transactions.
   - Each change updates totals in real time.

4. **Chart Visualization**

   - User selects a custom date range to analyze income vs. expense.

5. **Admin Operations**

   - Admin views registered users through a secure endpoint.

6. **Logout**
   - Session token is cleared; user redirected to login screen.

---

## Flow Chart

```mermaid
flowchart TD
A[Start] --> B[User opens app]
B --> C[Sign In via Clerk]
C --> D{Authentication Successful?}
D -- No --> E[Show Error Message]
D -- Yes --> F[Fetch User Role from DB]

F --> G{Role}
G -- Admin --> H[Redirect to Admin Dashboard]
G -- User --> I[Redirect to User Dashboard]

H --> J[Admin views number of users]
I --> K[User views personal dashboard]
J --> L[End]
K --> L[End]


```

---

## Data Flow Diagram

```mermaid
graph TD
  User[User] -->|Sign in| Clerk[Clerk Auth Service]
  Clerk -->|Auth token| Backend[Express Backend]
  Backend -->|Query role| DB[Postgres Users Table]
  DB -->|Return role| Backend
  Backend -->|role=user → dashboard data| User
  Backend -->|role=admin → admin data| Admin[Admin Panel]


```

---

## Schema Design

```mermaid
erDiagram
    users ||--o{ transactions : "has"
    roles ||--o{ users : "assigned to"

    users {
        uuid id PK
        uuid role_id FK "→ roles.id"
        varchar(100) first_name
        varchar(100) last_name
        varchar(255) email
        timestamp created_at
        timestamp updated_at
        timestamp deleted_at
    }

    roles {
        uuid id PK
        varchar(20) name "e.g., 'user', 'admin'"
        timestamp created_at
        timestamp updated_at
        timestamp deleted_at
    }

    transactions {
        uuid id PK
        uuid user_id FK "→ users.id"
        varchar(20) entry_type "income / expense"
        varchar(255) title
        decimal amount
        date occurred_at
        timestamp created_at
        timestamp updated_at
        timestamp deleted_at 
    }

```
