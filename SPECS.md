# SPECIFICATIONS (SPECS)

**Audience:** Developers, Tech Lead, AI Coding Agents  
**Purpose:** Technical blueprint for planning (`plan.md`) and task breakdown (`tasks.md`).

## 1. System Topology
The system consists of **4 components (3 interconnected applications + 1 public website)**:
1. **Public Website:** Landing page and product information.
2. **Manager Web App:** Backoffice for organization administrators (`REQ-01` to `REQ-04`).
3. **Client Portal App:** Read-only dashboard for end-customers (`REQ-05`).
4. **Core API Service:** Shared modular backend handling authentication, multitenancy (`tenant_id`), and ledger logic (`NFR-1`, `NFR-4`).

---

## 2. Functional Modules & UI Behavior

### FR-1: Client Module (`REQ-01`)
* **`FR-1.1` Client List:** Paginated table with name filter (`name`, `base_value`, `description`). Includes "Enroll" button + row actions (`details`, `delete`).
* **`FR-1.2` Enroll Client:** Creation form validating mandatory fields. Actions: "Cancel" | "Enroll".
* **`FR-1.3` Client Details:** Edit form for existing client data. Actions: "Cancel" | "Save Changes".

### FR-2: Movement Module (`REQ-02`, `REQ-04`, `REQ-05`)
* **`FR-2.1` Movement List:** Client summary table showing `name`, `base_value`, `description`, `owed_balance` (current balance). Actions: (`view`, `register`).
* **`FR-2.2` View Movements:** Client header, "Register" button, and ledger table (`date`, `type`, `amount`, `description`, `balance_after`, `delete`). *Rule:* Deleting a record recalculates subsequent `balance_after` and `owed_balance` in cascade.
* **`FR-2.3` Register Movement:** Form supporting `transfer` or `cash`. Actions: "Cancel" | "Register Movement".

### FR-3: Guarantee Module (`REQ-03`)
* **`FR-3.1` Guarantee List:** Client summary table showing `name`, `total_guarantee`, `paid_amount`, `pending_amount` (`total_guarantee - paid_amount`). Actions: (`view`, `register`).
* **`FR-3.2` View Guarantees:** Client header, "Register" button, and table (`date`, `type`, `amount`, `balance_after`, `delete`). *Rule:* Deleting recalculates `paid_amount` and `pending_amount`.
* **`FR-3.3` Register Guarantee:** Creation form. Actions: "Cancel" | "Register Guarantee".

---

## 3. Data Models (Core Entities)
*All tables enforce strict `tenant_id` isolation via Row-Level Security (RLS) (`NFR-1`).*

* **`clients`:** `id`, `tenant_id`, `user_id` (nullable, links to portal login), `name`, `base_value`, `description`, `status`, `created_at`
* **`movements`:** `id`, `tenant_id`, `client_id`, `type` (`charge` | `payment`), `method` (`transfer` | `cash`), `amount`, `description`, `balance_after`, `created_at`
* **`guarantees`:** `id`, `tenant_id`, `client_id`, `type` (`initial` | `payment`), `amount`, `balance_after`, `created_at`

---

## 4. API Contracts & Edge Cases
* **Manager Endpoints:**
  * `GET/POST /api/v1/clients` & `PATCH/DELETE /api/v1/clients/:id`
  * `GET/POST /api/v1/clients/:id/movements` & `DELETE /api/v1/movements/:id`
  * `GET/POST /api/v1/clients/:id/guarantees` & `DELETE /api/v1/guarantees/:id`
* **Client Portal Endpoints (`REQ-05`):**
  * `GET /api/v1/me/movements` (Resolves `client_id` and `tenant_id` strictly from auth token).
* **Edge Cases:**
  * **Mid-Ledger Deletion:** Deleting an older movement must trigger a chronological recalculation of all subsequent `balance_after` rows for that client inside a single SQL transaction.
  * **Concurrency:** Use row-level locking (`SELECT ... FOR UPDATE`) or `SERIALIZABLE` transactions when updating `owed_balance` or `pending_amount` to prevent race conditions.

---

## 5. Non-Functional Implementation (`NFR-1` to `NFR-4`)
* **Security & Compliance (`NFR-1`):** Enforce HTTPS (TLS 1.2+), encryption at rest (AES-256), OWASP Top 10 protections, and zero PII/bank account numbers in application logs (Chilean Laws N° 21.719 & N° 21.663).
* **Reliability (`NFR-2`):** Atomic ACID database transactions for all balance updates; automated daily database backups.
* **Scalability (`NFR-3`):** Composite database indexes on `(tenant_id, client_id, created_at)` to ensure `< 500ms` query latency up to 50,000 movements per tenant.
* **Modularity (`NFR-4`):** Domain-driven folder structure in the Core API (`/modules/clients`, `/modules/movements`, `/modules/guarantees`) so future modules (e.g., `/modules/investments`) plug in independently.
