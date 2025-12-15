# Arquitectura del Sistema: [Nombre del Proyecto]

## 1. Patrón Arquitectónico Principal

Se utilizará una arquitectura multitenancy de **Microservicios** 

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

* **ADR-001: Token JWT vs. Sesiones:** Se eligió JWT para permitir un *stateless* (sin estado) entre servicios y simplificar la escalabilidad horizontal.
* **ADR-002: Base de Datos Políglota:** PostgreSQL se usa para datos relacionales (usuarios), y MongoDB para datos menos estructurados/escalables (notas).
