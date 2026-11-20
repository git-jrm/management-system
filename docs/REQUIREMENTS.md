# REQUIREMENTS

**Audience:** Client / Stakeholders (What & Why) y Tech Lead (Base para `SPEC.md`).  
**Objective:** Replace the current isolated system with a centralized web platform that allows multiple organizations to manage their Clients, Transactions, Guarantees, and Investments (future module).

## Business Goals
* **Centralization:** Replace isolated legacy software with a modern, unified web platform.
* **Multi-Organization:** Support multiple independent client companies operating securely.
* **Core Entities:** Manage **Clients**, **Movements (Payments)**, **Guarantees**, and **Investments** (future module).

## User Roles
* **Manager:** Full operational control over their organization (clients, movements, guarantees, and balance history).
* **Client:** Read-only access to view their own payment history and balances.

---

## 1. Functional Requirements (RF)

| ID | Rol | Requerimiento | Criterio de Aceptación |
| :--- | :--- | :--- | :--- |
| **REQ-01** | Manager | **Gestión de Clientes:** Enrolar, consultar, editar y eliminar clientes dentro de su organización. | El directorio permite buscar/paginar por nombre y valida datos obligatorios antes de guardar. |
| **REQ-02** | Manager | **Gestión de Movimientos:** Registrar y administrar cobros y pagos recurrentes (transferencia o efectivo). | El saldo `adeudado` del cliente se actualiza automáticamente al registrar o eliminar un movimiento. |
| **REQ-03** | Manager | **Gestión de Garantías:** Registrar y controlar garantías iniciales y abonos asociados a cada cliente. | El sistema calcula y mantiene al día los montos de `garantía`, `pagado` y `pendiente`. |
| **REQ-04** | Manager | **Historial de Balance:** Consultar el estado financiero e historial de movimientos y saldos de la organización. | El Manager puede revisar el detalle cronológico de movimientos y saldos acumulados. |
| **REQ-05** | Client | **Consulta de Pagos:** Visualizar el historial personal de pagos realizados y su estado actual. | El cliente accede a un portal de solo lectura donde ve únicamente sus propios registros. |

---

## 2. Non-Functional Requirements (NFR)

| ID | Category | Description | Metric / Target |
| :--- | :--- | :--- | :--- |
| **NFR-1** | **Security & Privacy** | Protect financial integrity, isolate data between client companies, and avoid storing sensitive bank details. | Strict organization isolation, encrypted traffic (HTTPS), and compliance with Chilean Laws N° 21.719 & N° 21.663. |
| **NFR-2** | **Reliability** | Ensure system availability and exact mathematical accuracy in balance and guarantee calculations. | Minimum 98% uptime (MVP), error rate < 0.1%, and full balance consistency upon edits or deletions. |
| **NFR-3** | **Scalability** | Handle growth in the number of clients and transactions smoothly without performance degradation. | Response time < 500ms supporting up to 500 clients and 50,000 movements per organization. |
| **NFR-4** | **Modularity** | Allow the platform to evolve and add new business features without disrupting existing core operations. | Independent module structure enabling future additions (e.g., Investments) with minimal changes to existing modules. |



