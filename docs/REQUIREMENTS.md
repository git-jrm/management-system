# Functional Requirements (MVP)

**Audience:** Client & Stakeholders (What & Why)  
**Scope:** Centralized management system replacing legacy siloed software.

## 1. Business Goals
* **Centralization:** Replace isolated legacy software with a modern web platform.
* **Multi-Organization:** Support multiple independent client companies securely.
* **Core Entities:** Manage **Clients**, **Movements (Payments)**, **Guarantees**, and **Investments** (future module).

## 2. User Roles
* **Manager:** Full operational control (clients, movements, guarantees, balance history).
* **Client:** Read-only access to their own payment history.

## 3. Core Requirements & Acceptance Criteria

| ID | Role | Requirement | Acceptance Criteria |
| :--- | :--- | :--- | :--- |
| **REQ-01** | Manager | **Client Management:** Enroll, view, edit, and remove clients. | Client directory supports search/pagination and validates mandatory fields. |
| **REQ-02** | Manager | **Movements & Payments:** Register and manage payments (transfer/cash) and charges. | Client balance (`adeudado`) updates automatically upon adding or voiding movements. |
| **REQ-03** | Manager | **Guarantees:** Track client collateral/guarantees and payments against them. | System accurately calculates `garantía`, `pagado`, and `pendiente` balances. |
| **REQ-04** | Manager | **Balance History:** View historical balance sheet and financial summaries. | Manager can inspect historical movements and balances filtered by date. |
| **REQ-05** | Client | **Payment History:** View personal payment and balance history. | Authenticated client sees a read-only list of their own confirmed movements. |
