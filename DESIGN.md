# Diseño de Alto Nivel (HLD): Módulo de Gestión de Notas

## 1. Diseño de la Base de Datos (MongoDB - Colección 'notes')

Una nota tendrá el siguiente esquema:

```json
{
  "_id": "<ObjectId>",
  "userId": "<ObjectId>",       // Referencia al usuario propietario (índice)
  "title": "Mi Primera Nota",   // String
  "content": "Este es el cuerpo de la nota...", // String
  "tags": ["personal", "importante"],          // Array de Strings (índice)
  "createdAt": "<ISODate>",
  "updatedAt": "<ISODate>"
}
