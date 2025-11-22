# Technical Documentation — Architecture, DFD, Auth & Authentication and Authorization flow

## 1. Architecture (AWS-specific)

![AWS Architecture](assets/ExpenseEase (1).png)

---

## Data Flow Diagram

![AWS Architecture](assets/dfd.png)



## Schema Design

```mermaid
erDiagram
    users ||--o{ transactions : "has"
    roles ||--o{ users : "assigned to"

    users {
        uuid id PK
        uuid role_id FK "→ roles.id"
        string name
        string email
        string password "Hashed password"
        timestamp created_at
        timestamp updated_at
        timestamp deleted_at
    }

    roles {
        uuid id PK
        string name "e.g., 'user', 'admin'"
        timestamp created_at
        timestamp updated_at
        timestamp deleted_at
    }

    transactions {
        uuid id PK
        uuid user_id FK "→ users.id"
        string title
        decimal amount
        timestamp occurred_at
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
    B-->>U: Return JWT
    U->>B: Access API
    B->>SM: Verify token using secret
    SM-->>B: Token valid
    B-->>U: Authorized response

```