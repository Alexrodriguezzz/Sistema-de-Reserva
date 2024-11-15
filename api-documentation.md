# API REST - Sistema de Gestión de Reservas en Parcelas

## Introducción
Esta API proporciona los endpoints necesarios para gestionar un sistema de reservas de parcelas y salones de eventos. Permite la gestión de usuarios, parcelas, reservas y reseñas.

## Base URL
`http://localhost:5000/api`

## Autenticación
La API utiliza JWT (JSON Web Tokens) para la autenticación. Los tokens deben ser incluidos en el header de las peticiones:
```
Authorization: Bearer <token>
```

## Endpoints

### Parcelas

#### GET /parcelas
Obtiene todas las parcelas disponibles.

**Parámetros de consulta opcionales:**
- `tipo`: Filtrar por tipo (parcela/salon)
- `capacidadMin`: Capacidad mínima
- `precioMax`: Precio máximo
- `disponible`: true/false

**Respuesta exitosa (200):**
```json
[
  {
    "_id": "string",
    "nombre": "string",
    "descripcion": "string",
    "capacidad": "number",
    "precio": "number",
    "tipo": "string",
    "imagenes": ["string"],
    "disponible": "boolean"
  }
]
```

#### POST /parcelas
Crea una nueva parcela.

**Body:**
```json
{
  "nombre": "string",
  "descripcion": "string",
  "capacidad": "number",
  "precio": "number",
  "tipo": "string",
  "imagenes": ["string"],
  "disponible": "boolean"
}
```

### Reservas

#### POST /reservas
Crea una nueva reserva.

**Body:**
```json
{
  "clienteId": "string",
  "parcelaId": "string",
  "fechaInicio": "date",
  "fechaFin": "date",
  "metodoPago": "string"
}
```

**Respuesta exitosa (201):**
```json
{
  "_id": "string",
  "estado": "pendiente",
  "montoPagado": "number",
  "fechaCreacion": "date"
}
```

## Códigos de Estado

- 200: Operación exitosa
- 201: Recurso creado exitosamente
- 400: Error en la solicitud
- 401: No autorizado
- 403: Prohibido
- 404: Recurso no encontrado
- 500: Error interno del servidor

## Límites y Cuotas
- Máximo 100 peticiones por minuto por IP
- Tamaño máximo de payload: 10MB
- Tiempo máximo de respuesta: 30 segundos

## Consideraciones de Seguridad
- Todas las comunicaciones son a través de HTTPS
- Los tokens JWT expiran después de 24 horas
- Implementación de rate limiting para prevenir ataques DDoS
- Validación de datos de entrada para prevenir inyecciones
- Sanitización de datos de salida para prevenir XSS
