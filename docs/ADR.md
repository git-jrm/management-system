# Architecture Decision Records (ADRs)

Log of key technical and product decisions made during the SaaS prototype development.

## Decision Index

| ID | Title | Status | Date |
| :--- | :--- | :--- | :--- |
| [ADR-001](#adr-001-log-recurring-payments--status-accepted--date-2026-11-20) | Log recurring payments via bank transfer and cash | Accepted | 2026-11-20 |
| [ADR-002](#adr-002-platform-is-multitenant--status-accepted--date-2026-11-20) | Platform is multitenant | Accepted | 2026-11-20 |
| [ADR-003](#adr-003-core-tech-stack-selection-for-the-mvp--status-proposed--date-2026-11-20) | Core tech stack selection for the MVP | Proposed | 2026-11-20 |

---

## Template (Copy for new ADRs)

    ### **ADR-XXXX**: [Short Title] | **Status**: Proposed / Accepted / Deprecated | **Date**: YYYY-MM-DD

    * **Context:** What problem are we solving and what are the constraints?
    * **Decision:** What did we choose to do?
    * **Trade-offs:** What do we gain and what do we sacrifice?

---

## Decisions

### **ADR-001**: Log recurring payments | **Status**: Accepted | **Date**: 2026-11-20

* **Context:** We need to track recurring payments for the MVP without delaying launch due to payment gateway integrations, transaction fees, or strict PCI-DSS compliance.
* **Decision:** Build an internal logging system only for payments made externally via bank transfer or cash, excluding credit/debit card processing.
* **Trade-offs:** Faster time-to-market and minimal compliance overhead, at the cost of requiring manual payment verification.

---

### **ADR-002**: Platform is multitenant | **Status**: Accepted | **Date**: 2026-11-20

* **Context:** Multiple organizations/clients will use the SaaS prototype simultaneously, and we need to keep infrastructure costs and maintenance low.
* **Decision:** Implement a shared-database, shared-schema multitenant architecture isolating data logically via a `tenant_id` column on core tables.
* **Trade-offs:** Low hosting costs and simplified deployments, at the cost of requiring strict query filtering and Row-Level Security (RLS) to prevent data leaks between tenants.

---

### **ADR-003**: Core tech stack selection for the MVP | **Status**: Proposed | **Date**: 2026-11-20

* **Context:** We need a reliable, fast-to-develop, and cost-effective stack to validate the prototype quickly with a small team.
* **Decision:** Use a modern monolithic full-stack framework (e.g., Next.js / TypeScript) backed by a managed PostgreSQL database (e.g., Supabase) and cloud hosting with built-in TLS/encryption.
* **Trade-offs:** High development velocity and low initial ops overhead, at the cost of potential refactoring if specific microservices are needed at massive scale.
