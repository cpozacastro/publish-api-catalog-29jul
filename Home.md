# Documentación de la API de Gestión de Órdenes

## Tabla de Contenidos

- [Introducción](#introducción)
- [Endpoints de la API](#endpoints-de-la-api)
  - [Obtener Todas las Órdenes](#obtener-todas-las-órdenes)
  - [Crear una Nueva Orden](#crear-una-nueva-orden)
  - [Obtener Detalles de una Orden](#obtener-detalles-de-una-orden)
  - [Actualizar una Orden](#actualizar-una-orden)
  - [Eliminar una Orden](#eliminar-una-orden)
  - [Actualizar Estado de la Orden](#actualizar-estado-de-la-orden)
- [Modelos de Datos (Esquemas)](#modelos-de-datos-esquemas)
  - [Orden](#orden)
  - [NuevaOrden](#nuevaorden)
  - [ÍtemDeOrden](#ítemdeorden)
  - [NuevoÍtemDeOrden](#nuevoítemdeorden)
  - [Dinero](#dinero)
  - [Dirección](#dirección)
  - [RespuestaDeError](#respuestadeerror)
- [Respuestas de Error](#respuestas-de-error)
- [Información de Contacto](#información-de-contacto)
- [Términos de Servicio](#términos-de-servicio)
- [Licencia](#licencia)

---

## Introducción

Esta API permite la gestión completa de órdenes de compra, desde su creación hasta el seguimiento de su estado y su actualización. Es fundamental para sistemas de comercio electrónico y logística, facilitando la interacción con los pedidos de los clientes.

---

## Endpoints de la API

La API de Gestión de Órdenes soporta las siguientes operaciones CRUD sobre los pedidos:

| Recurso | Descripción | Métodos HTTP |
|---|---|---|
| `/orders` | Creación y listado de órdenes. | `GET`, `POST` |
| `/orders/{orderId}` | Consulta, actualización y eliminación de una orden específica. | `GET`, `PUT`, `DELETE` |
| `/orders/{orderId}/status` | Actualización del estado de una orden. | `PUT` |

### Obtener Todas las Órdenes

`GET /orders`

Recupera una lista paginada de todas las órdenes existentes en el sistema.

**Parámetros:**

| Nombre | Tipo | En | Descripción | Ejemplo |
|---|---|---|---|---|
| `status` | `string` | `query` | Filtra las órdenes por su estado (ej. "PENDING", "SHIPPED", "DELIVERED"). | `PENDING`, `SHIPPED` |
| `limit` | `integer` | `query` | Número máximo de órdenes a devolver (valor por defecto: 10). | `20` |
| `offset` | `integer` | `query` | Número de órdenes a saltar para la paginación. | `0` |

**Respuestas:**

- **`200 OK`**: Lista de órdenes recuperada exitosamente.
  ```json
  [
    {
      "orderId": "ORD-20240729-001",
      "customerId": "CUST-001",
      "orderDate": "2024-07-28T14:30:00Z",
      "status": "DELIVERED",
      "totalAmount": { "amount": 120.50, "currency": "EUR" },
      "items": [
        { "productId": "PROD-A", "quantity": 2, "unitPrice": 50.00 },
        { "productId": "PROD-B", "quantity": 1, "unitPrice": 20.50 }
      ]
    }
  ]