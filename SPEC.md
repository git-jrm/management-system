# SPEC

Audience: Developers, Tech Lead, AI coding agents, inter alia.

-How the system will function (behavior-oriented description of functionality).

The System 

The system to achive the **requeriments** is compose and formed by three interconnected applications plus a public website. Each one will be explained below.

## Detailed functional requirements

### API contracts
### data models
### integration points
### edge cases


...
...
...


-A detailed blueprint used to generate technical plans (plan.md) and task lists (tasks.md).


I.1 Requerimiento inicial: Se requiere administrar las siguientes entidades: ** Clientes, Movimientos, Garantías e Inversiones.

I.2 Requerimiento desarrollado y validado:

## 1. Requisitos Funcionales (RF)

### RF-1: Módulo de Clientes

| ID | Descripción | Prioridad | Criterio de Aceptación |
| :--- | :--- | :--- | :--- |
| **RF-1.1** | **Página Clientes:** Visualizar la lista de clientes con `nombre`, `valor`, `descripción`. Incluye botón "Enrolar" y acciones (`datos`, `eliminar`). | Alta | La tabla debe ser paginada y permitir filtros por nombre. |
| **RF-1.2** | **Página Cliente Enrola:** Formulario para la creación de un nuevo Cliente. Acciones: "volver sin enrolar" y "enrolar". | Alta | La inserción debe validar campos obligatorios antes de guardar. |
| **RF-1.3** | **Página Cliente Datos:** Formulario para ver/editar los datos existentes del Cliente. Acciones: "Volver sin modificar Cliente" y "Modificar Cliente". | Alta | La edición solo es exitosa si los datos cumplen con las reglas de negocio. |

### RF-2: Módulo de Movimientos

| ID | Descripción | Prioridad | Criterio de Aceptación |
| :--- | :--- | :--- | :--- |
| **RF-2.1** | **Página Movimientos:** Visualizar lista de Clientes con `nombre`, `valor`, `descripción`, `adeudado`. Acciones: (`consultar`, `registrar`). | Alta | El campo `adeudado` debe ser el saldo actual de movimientos. |
| **RF-2.2** | **Página Movimientos Consultar:** Mostrar datos principales del Cliente, botón "Registrar" y tabla de Movimientos (`fecha`, `tipo`, `valor`, `descripción`, `saldo`, `acción: eliminar`). | Alta | El `saldo` se debe recalcular inmediatamente tras una eliminación. |
| **RF-2.3** | **Página Movimientos Registrar:** Formulario para la inserción de un nuevo Movimiento. Acciones: "volver sin registrar Movimiento" y "Registrar Movimiento". | Media | El registro debe actualizar el saldo adeudado del Cliente. |

### RF-3: Módulo de Garantías

| ID | Descripción | Prioridad | Criterio de Aceptación |
| :--- | :--- | :--- | :--- |
| **RF-3.1** | **Página Garantías:** Visualizar lista de Clientes con `nombre`, `garantía`, `pagado`, `pendiente`. Acciones: (`consultar`, `registrar`). | Alta | El campo `pendiente` es la diferencia entre `garantía` y `pagado`. |
| **RF-3.2** | **Página Garantías Consultar:** Mostrar datos principales del Cliente, botón "Registrar" y tabla de Garantías (`fecha`, `tipo`, `valor`, `saldo`, `acción: eliminar`). | Media | La eliminación debe actualizar el estado `pagado` y `pendiente`. |
| **RF-3.3** | **Página Garantías Registrar:** Formulario para la inserción de una nueva Garantía. Acciones: "volver sin registrar Garantía" y "Registrar Garantía". | Media | El registro debe actualizar el monto total `garantía` del Cliente. |

## 2. Requisitos No Funcionales (RNF)

| Categoría | Descripción | Métrica Específica |
| :--- | :--- | :--- |
| **RNF-1: Seguridad** | La aplicación debe proteger los datos sensibles del Cliente y asegurar la integridad de las transacciones financieras. | Cumplir con OWASP Top 10. Uso de HTTPS forzado y hashing robusto para credenciales. |
| **RNF-2: Confiabilidad** | El sistema debe estar disponible para su uso durante las horas pico y garantizar la consistencia de los datos. | Disponibilidad del 99.9%. Tasa de error de transacción (por API) inferior al 0.1%. |
| **RNF-3: Escalabilidad** | La arquitectura debe ser capaz de manejar un crecimiento en el número de Clientes y Movimientos sin degradación crítica. | Soportar 500 Clientes y 50.000 Movimientos totales manteniendo un tiempo de respuesta menor a 500ms. |
