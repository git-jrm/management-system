# Accounts Receivable & Client Ledger System

> **Status:** `[ ANALYSIS ]` — Prototype / MVP  
> Accounts receivable system that automates monthly client billing, logs and tracks payments, and reconciles the client ledger. Designed in AWS serverless architecture.

## Core Capabilities (MVP)
* **Automated Monthly Billing:** Scheduled generation of monthly recurring charges per client (`prorrateo` / base fee).
* **Payment Logging & Tracking:** Internal logging of external payments received via bank transfer or cash (zero card processing).
* **Client Ledger Reconciliation:** Real-time balance calculation (`owed`, `paid`, `pending`) and guarantee tracking per client.
* **Multi-Tenant Isolation:** Logical data separation per organization (`tenant_id`) with role-based access (`Manager` and `Client`).

## Architecture & Stack
* **Cloud Ecosystem:** AWS Serverless (API Gateway, AWS Lambda, Amazon Cognito, DynamoDB / Aurora Serverless, EventBridge for monthly billing schedules).
* **Design Principles:** Cloud-Native, Multi-Tenant, AWS Well-Architected Framework.

## Documentation
All product, architecture, and compliance blueprints live in `/docs`:
* [Documentation Hub](./docs/README.md) — Traceability index and contributor rules.
* [Requirements](./docs/REQUIREMENTS.md) — Business goals, roles, and functional/non-functional requirements.
* [Specifications](./docs/SPECS.md) — System topology, UI behavior, data models, and API contracts.
* [Architecture Decisions (ADRs)](./docs/ADR.md) — Key technical decisions and trade-offs.
* [Compliance & Security](./docs/COMPLIANCE.md) — Data minimization and Chilean regulatory baseline (Laws N° 21.719 & N° 21.663).

## Architectural References
* [Serverless Multi-Tier Architectures with API Gateway & Lambda (AWS Whitepaper)](https://amazon.com)
* [Serverless Applications Lens — AWS Well-Architected Framework](https://amazon.com)
* [Serverless Land Patterns](https://serverlessland.com)


---


# Integrated Platform

* vertical software
* critical mission software 

Platform for managing cashflow, guarantees, activities and investment.

* Stack: AWS ecosystem.
* Cloud Native.
* Well-Architected Framework.

The integrated systems consist in three platforms:
* Activities Platform: Mobile Webapp gamified for activities

* Management Platform:
- to manage clients payments, balances, prorrateo, guarantees and key activities.

* Investments Platform: to view the status of investment payments.
* click

## REFERENCES

* https://docs.aws.amazon.com/es_es/prescriptive-guidance/latest/micro-frontends-aws/introduction.html
* https://aws.amazon.com/blogs/mobile/backends-for-frontends-pattern/
* https://netflixtechblog.com/seamlessly-swapping-the-api-backend-of-the-netflix-android-app-3d4317155187

* Arquitecturas de varios niveles sin servidor de AWS con Amazon API Gateway y AWS Lambda (https://docs.aws.amazon.com/es_es/whitepapers/latest/serverless-multi-tier-architectures-api-gateway-lambda/welcome.html).

* https://aws.amazon.com/es/blogs/compute/server-side-rendering-micro-frontends-the-architecture/

* https://samnewman.io/patterns/architectural/bff/
* https://serverlessland.com/patterns
* https://teamtopologies.com/key-concepts

