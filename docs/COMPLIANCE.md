# Compliance & Seguridad Básica

**Estado:** Prototipo / MVP  
**Alcance:** Registro interno (logging) de cobros y pagos recurrentes realizados por transferencia bancaria o efectivo.  
**Marco de Referencia:** Ley de Protección de Datos Personales en Chile (Ley N° 21.719, diciembre 2024) y Ley Marco de Ciberseguridad (Ley N° 21.663, 2024).

---

## 1. Alcance y Exclusión de Tarjetas
* Este sistema **no procesa pagos electrónicos ni captura datos de tarjetas**.
* Opera exclusivamente como bitácora operativa para registrar cobros y pagos externos realizados por transferencia bancaria o efectivo.

---

## 2. Minimización de Datos (Ley N° 21.719)
En cumplimiento del principio de minimización y privacidad desde el diseño, los logs excluyen datos personales directos (nombres, RUT, correos) y se limitan a:
* `payment_id`: Identificador único del registro.
* `user_id`: ID interno seudonimizado del cliente.
* `method`: Método de pago (`transfer` o `cash`).
* `amount` & `currency`: Monto y moneda (ej. `15000 CLP`).
* `reference_code`: Folio o comprobante interno (sin números de cuenta bancaria).
* `status` & `timestamp`: Estado (`confirmed` / `pending`) y marca de tiempo.

---

## 3. Seguridad Técnica (Ley N° 21.663)
Como buena práctica de gestión de riesgos y protección de la información:
* **Cifrado en Tránsito:** Todas las comunicaciones operan bajo **HTTPS (TLS 1.2+)**.
* **Cifrado en Reposo:** La base de datos y los archivos de logs utilizan cifrado en disco (**AES-256** o cifrado nativo del proveedor).
* **Control de Acceso:** Acceso restringido exclusivamente a personal técnico autorizado mediante credenciales protegidas y secretos fuera del código fuente.

---

## 4. Ciclo de Vida y Derechos de los Titulares (Ley N° 21.719)
* **Retención limitada:** Los logs técnicos se purgan periódicamente (ej. cada 30-60 días). Los registros de pago se mantienen solo durante la fase de prueba o por exigencia tributaria básica.
* **Derechos ARSOP (Acceso, Rectificación, Supresión, Oposición y Portabilidad):** Si un usuario solicita eliminar sus datos del piloto, su `user_id` se anonimiza desvinculándolo de cualquier identidad real.

---

## 5. Gestión de Incidentes (Ley N° 21.663)
Ante cualquier acceso no autorizado o brecha de seguridad:
1. **Contención:** Revocar accesos y rotar llaves/contraseñas de inmediato.
2. **Evaluación:** Determinar el alcance de los registros afectados.
3. **Escalamiento:** Notificar internamente al responsable del proyecto para evaluar si corresponde reportar al **CSIRT Nacional** y/o a la **Agencia de Protección de Datos Personales** según la gravedad del incidente.
