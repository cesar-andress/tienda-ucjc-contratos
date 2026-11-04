# Plantilla de contrato de evento

Copiad este fichero a `eventos/` y renombradlo según el evento, por ejemplo `ucjc-pieza-verbo@1.md`.  
Sustituid todos los marcadores `<…>`. No dejéis ejemplos inventados como si ya estuvieran firmados.

## Nombre del evento
```text
ucjc:descubrimiento:anadir-al-carrito@1
```

## Versión
| Campo | Valor |
| --- | --- |
| Versión del evento | `1` |
| ¿Sustituye a una versión anterior? | `no` |

## Equipo emisor
`Descubrimiento`

## Equipos consumidores
- `Compra`

## Descripción
Se emite cuando el usuario hace clic en el botón de añadir un producto al carrito desde el catálogo o la ficha de detalle, enviando los datos necesarios para que el micro-frontend de Compra gestione el carrito.

## Campos y tipos
| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `version` | `número` | obligatorio | Versión del esquema del evento |
| `productId` | `texto` | obligatorio | Identificador único del producto |
| `sku` | `texto` | obligatorio | SKU del producto |
| `name` | `texto` | obligatorio | Nombre del producto |
| `price` | `número` | obligatorio | Precio unitario del producto |
| `currency` | `texto` | obligatorio | Moneda (ej. EUR) |
| `quantity` | `número` | obligatorio | Cantidad de unidades a añadir |
| `imageUrl` | `texto` | opcional | URL de la imagen del producto |

## Campos obligatorios y opcionales
- **Obligatorios:** `version`, `productId`, `sku`, `name`, `price`, `currency`, `quantity`
- **Opcionales:** `imageUrl`

## Ejemplo de payload
```json
{
  "detail": {
    "version": 1,
    "productId": "prod-101",
    "sku": "prod-101",
    "name": "Camiseta Técnica UCJC",
    "price": 19.99,
    "currency": "EUR",
    "quantity": 1,
    "imageUrl": ""
  }
}
```

## Responsables que aprobaron el contrato
| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| `Descubrimiento` | Emisor | Daniel Molina Vitón | 2026-11-03 | OK |
| `Compra` | Consumidor | | | |

## Estado del contrato
- [x] `propuesto`
- [ ] `firmado`
- [ ] `deprecado`

## Historial
- `2026-11-03` – Creación de la propuesta inicial del contrato de añadir al carrito por el equipo Descubrimiento.
