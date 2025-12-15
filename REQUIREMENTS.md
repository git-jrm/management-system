# Sistema de Gestión para Casamanquehue

## I. Contexto
En este documento se presentan las especificaciones para

requerimientos del Sistema de gestión de clientes y movimientos (cobros, ingresos, egresos y garantías), considerando Mobile-first y Multitenency. Posteriormente el diseño del software.

## II. Requerimientos

### 1. Requerimientos Funcionales (RF):

RF-1: Módulo Clientes:
RF-1.1: Página Clientes: arriba botón "Enrolar"; Tabla Clientes (nombre, valor, descripción y acciones: datos|eliminar).
RF-1.2: Página Cliente Enrola: Formulario vacío para insertar Cliente; abajo "volver sin enrolar" y "enrolar".
RF-1.3: Página Cliente Datos: Formulario para ver/editar datos del Cliente; abajo "Volver sin modificar Cliente" y "Modificar Cliente".

RF-2: Módulo Movimientos:
RF-2.1: Página Movimientos: Tabla Clientes (nombre, valor, descripción, adeudado y acciones: consultar|registrar).
RF-2.2: Página Movimientos Consultar: arriba nombre y rut Cliente, botón "Registrar"; Tabla Movimientos (fecha, tipo, valor, descripción, saldo y acción: eliminar).
RF-2.3: Página Movimientos Registrar: Formulario vacío para insertar Movimiento; abajo "volver sin registrar Movimiento" y "Registrar Movimiento".

RF-3: Módulo Garantías
RF-3.1: Página Garantías: Tabla Clientes (nombre, garantía, pagado, pendiente y acciones: consultar|registrar).
RF-3.2: Página Garantías Consultar: arriba nombre y rut Cliente, botón "Registrar"; Tabla Garantías (fecha, tipo, valor, saldo y acción: eliminar).
RF-3.3: Página Garantías Registrar: Formulario vacío para insertar Garantía; abajo "volver sin registrar Garantía" y "Registrar Garantía".

### 2. Requerimientos No Funcionales (RNF)

RNF-1: Seguridad
RNF-2: Confiabilidad
RNF-3: Escalabilidad
