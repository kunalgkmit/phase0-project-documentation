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
K --> L[User can perform CRUD transactions]


```

---

## Data Flow Diagram

```mermaid
graph TD
    %% === AUTHENTICATION FLOW ===
    U[User] -->|Login / Signup Email, Password| B[Express Backend]
    B -->|Validate credentials| DB[PostgreSQL]
    DB -->|Return user record + role| B
    B -->|Generate JWT Token| U

    %% === USER DASHBOARD FLOW ===
    U -->|Authenticated request JWT| B
    B -->|Verify token| Auth[JWT Verification]
    Auth --> B
    B -->|Fetch user transactions| DB
    B -->|Return dashboard data Balance, Income, Expense| U

    %% === USER CRUD OPERATIONS ===
    U -->|Create / Read / Update / Delete Transactions| B
    B -->|Perform CRUD on transactions table| DB
    DB -->|Return updated data| B
    B -->|Update dashboard summary| U

    %% === ADMIN DASHBOARD FLOW ===
    A[Admin] -->|Login / Verify JWT| B
    B -->|Check role = 'admin'| DB
    DB -->|Confirm admin role| B
    A -->|View Registered Users & Count| B
    B -->|Fetch user list + total count| DB
    DB -->|Return users data| B
    B -->|Display admin dashboard| A



```



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

## Authentication and Authorization flow
```mermaid
sequenceDiagram
    participant U as User
    participant B as Backend (Express)
    participant DB as PostgreSQL
    participant SM as Secrets Manager

    U->>B: POST /login (email, password)
    B->>DB: Validate user credentials
    DB-->>B: Return user + role
    B->>SM: Fetch JWT secret
    B-->>U: Return JWT (includes user_id, role)
    U->>B: Access API with JWT
    B->>SM: Verify token using secret
    SM-->>B: Token valid
    B-->>U: Authorized response

```