# Arquitectura del Sistema: [Nombre del Proyecto]

## 0. Lambdas Módulo Clientes:
* CustomerCreate
* CustomerRead
* CustomerUpdate
* CustomerDelete
* CustomersList

## 0. Lambdas Módulo Movimientos Cliente:
* MovementCreate
* MovementRead
* MovementUpdate
* MovementDelete
* MovementsList

## 0. Lambdas Módulo Garantías:
* GuaranteeCreate
* GuaranteeRead
* GuaranteeUpdate
* GuaranteeDelete
* GuaranteeList


## 1. Patrón Arquitectónico Principal

Se utilizará una arquitectura de **Microservicios** 

[Image of Microservices Architecture Diagram]
 para desacoplar las funcionalidades principales (Autenticación, Gestión de Notas, Búsqueda) y permitir el escalado independiente.

## 2. Componentes Principales

| Componente | Responsabilidad | Tecnología/Framework |
| :--- | :--- | :--- |
| **Servicio de Autenticación** | Gestión de usuarios, Login/Logout, Emisión de Tokens JWT. | Python (Flask) + PostgreSQL |
| **Servicio de Notas** | CRUD de las notas, almacenamiento del contenido. | Node.js (Express) + MongoDB |
| **API Gateway** | Punto de entrada único, enrutamiento y validación de JWT. | NGINX/Kong |
| **Base de Datos** | Persistencia de datos de usuario (PostgreSQL) y contenido de notas (MongoDB). | AWS RDS/MongoDB Atlas |

## 3. Flujo de Datos (Ejemplo: Creación de Nota)

1. El Cliente envía una solicitud **POST /api/v1/notes** al **API Gateway**.
2. **API Gateway** valida el token JWT.
3. El Gateway enruta la solicitud al **Servicio de Notas**.
4. El **Servicio de Notas** almacena el dato en MongoDB y responde al Gateway.
5. **API Gateway** devuelve la respuesta al Cliente.

## 4. Decisiones Clave (ADR)

* **ADR-001: Multitenancy:** Amazon Aurora con capacidad Multitenancy.

* **ADR-001: Autenticación:** Se considera uso de Amazon Cognito para autenticación.
