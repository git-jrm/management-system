## Entity–relationship model · Business

```mermaid
erDiagram
    ADMIN ||--o{ BUSINESS : mantains
    BUSINESS ||--o{ COLLABORATOR : collaborates
    BUSINESS ||--o{ CLIENT : pay
    MANAGER ||--o{ BUSINESS : manages
    CLIENT ||--o{ MOVEMENT : generate
    BUSINESS ||--o{ MOVEMENT : incur
    BUSINESS ||--o{ APPORTIONMENT : generate
    MOVEMENT ||--o{ APPORTIONMENT : grouped
    MANAGER ||--o{ APPORTIONMENT : sees
    ADMIN {
        UUID id_admin
    }
    MANAGER {
        UUID id_manager
    }
    BUSINESS {
        UUID id_business
        UUID id_admin(FK)
        UUID id_manager(FK)
    }
    COLLABORATOR {
        UUID id_collaborator
        UUID id_business(FK)
    }
    APPORTIONMENT{ 
        UUID id_apportionment
        UUID id_manager(FK)
        UUID id_business(FK)
        int period
    }
    CLIENT {
        UUID id_client
        UUID id_business(FK)
    }
    MOVEMENT {
        UUID id_movement
        UUID id_client(FK)
        UUID id_business(FK)
        date date
    }
```

## Entity–relationship model · Partner

```mermaid
   erDiagram
    PARTNER |o--o{ INVESTMENT : finances
    PARTNER |o--o{ SIMULATION : save
    PARTNER |o--o{ REFERRED : refer
    INVESTMENT |o--o{ PAYMENTS : mantains
    INVESTMENT |o--o| REFERRED : mantains
    PARTNER {
        UUID id_bp
        UUID id_bp_referrer(FK)
        bool master
    }
    SIMULATION {
        UUID id_simulation
        UUID id_bp(FK)
        int int_amount
        date date_created
    }
    INVESTMENT {
        UUID id_investment
        UUID id_bp(FK)
        UUID id_bp_referrer(FK)
        UUID id_mbp(FK)       
    }
    REFERRED {
        UUID id_referred
        UUID id_bp(FK)
        string email_referred
        date date_sent
        date date_accepted
        date date_canceled
    }
    PAYMENTS {
        UUID id_payments
        UUID id_investment(FK)
        int int_amount
    }
```
