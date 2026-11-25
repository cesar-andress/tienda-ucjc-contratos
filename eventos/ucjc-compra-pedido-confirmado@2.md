# Contrato: `ucjc:compra:pedido-confirmado@2`

## Nombre del evento

```text
ucjc:compra:pedido-confirmado@2
```

Nombre de fichero: `ucjc-compra-pedido-confirmado@2.md`

## Versión

| Campo | Valor |
| --- | --- |
| Versión del contrato del evento | `2` |
| ¿Sustituye a una versión anterior? | sí: `ucjc:compra:pedido-confirmado@1` |

## Equipo emisor

**Compra**

## Equipos consumidores

- **Datos** (A y B)

Descubrimiento e Identidad no intervienen.

## Descripción

Como el `@1`, pero el pedido lleva `moneda` y puede llevar `campaña`.

Ojo: firmar el `@2` obliga a Compra y a las dos Datos a cambiar a la vez.
Si preferís algo más suave, en clase podéis elegir el **cambio menor** del `@1`
(ver `PROPUESTA-BLACK-FRIDAY.md`) en lugar de este fichero.

Mientras esté `propuesto`, Compra sigue emitiendo el `@1`.

## Campos y tipos (`event.detail`)

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `pedidoId` | texto | obligatorio | Lo genera Compra. |
| `usuarioId` | texto | obligatorio | Usuario de la sesión. |
| `creadoEn` | texto (ISO 8601) | obligatorio | Momento de la confirmación. |
| `total` | número | obligatorio | Total en la moneda del pedido. |
| `lineas` | lista | obligatorio | Igual que en el `@1`. |
| `moneda` | texto | obligatorio | `EUR`, `USD` o `GBP`. |
| `campaña` | texto | opcional | p. ej. `black-friday-2026` |

### Elementos de `lineas[]`

Igual que en `@1`: `productoId`, `nombre`, `precio`, `cantidad` (todos obligatorios).

## Campos obligatorios y opcionales

- **Obligatorios:** `pedidoId`, `usuarioId`, `creadoEn`, `total`, `lineas`, `moneda`
- **Opcionales:** `campaña`

## Ejemplo de payload

```json
{
  "pedidoId": "PED-2026-1101",
  "usuarioId": "u-123",
  "creadoEn": "2026-11-27T11:05:00+01:00",
  "moneda": "EUR",
  "campaña": "black-friday-2026",
  "total": 31.98,
  "lineas": [
    {
      "productoId": "prod-101",
      "nombre": "Camiseta UCJC",
      "precio": 15.99,
      "cantidad": 2
    }
  ]
}
```

## Responsables que aprueban

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| Compra | Emisor | Daniel Molina Viton | 25/11/2026 | Firmado |
| Datos A | Consumidor | Hans Jefferson Arauco Sanchez| 23/11/2026 | Firmado |
| Datos B | Consumidor | | | |

## Estado del contrato

- [x] `propuesto`
- [ ] `firmado`
- [ ] `deprecado`

## Historial

- `2026-11-23` — Propuesta del profesor (Black Friday).
