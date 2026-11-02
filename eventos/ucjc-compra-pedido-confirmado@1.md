# Contrato: `ucjc:compra:pedido-confirmado@1`

## Nombre del evento

```text
ucjc:compra:pedido-confirmado@1
```

Nombre de fichero: `ucjc-compra-pedido-confirmado@1.md`

## Versión

| Campo | Valor |
| --- | --- |
| Versión del contrato del evento | `1` |
| ¿Sustituye a una versión anterior? | no |

## Equipo emisor

**Compra**

## Equipos consumidores

- **Datos** (variante A — Hans Jefferson Arauco Sanchez / `tienda-ucjc-datos`)
- **Datos** (variante B — cuando publiquen repo; deben confirmar en el PR o en uno posterior)

Otros equipos no consumen este evento en `@1`.

## Descripción

Compra emite este evento **después** de que el usuario confirma el pedido (fin del checkout).  
Datos lo escucha para **persistir** el pedido (simulado) y mostrarlo en «Mis pedidos».

El identificador del pedido (`pedidoId`) lo genera y envía **Compra** en el mismo evento. Datos no inventa el id en el mismo ciclo asíncrono.

## Campos y tipos (`event.detail`)

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `pedidoId` | texto | obligatorio | Identificador único del pedido, generado por Compra. |
| `usuarioId` | texto | obligatorio | Identificador del usuario que confirma (el mismo que Identidad usa en sesión, cuando haya sesión). |
| `creadoEn` | texto (ISO 8601) | obligatorio | Instantánea de la confirmación. |
| `total` | número | obligatorio | Importe total del pedido en la misma moneda que usan las líneas (euros, sin símbolo). |
| `lineas` | lista de objetos | obligatorio | Líneas del pedido. Puede ser lista vacía solo en pruebas; en flujo real tendrá al menos un elemento. |

### Elementos de `lineas[]`

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `productoId` | texto | obligatorio | Id de producto (el que viajó desde Descubrimiento → Compra). |
| `nombre` | texto | obligatorio | Nombre para mostrar en «Mis pedidos». |
| `precio` | número | obligatorio | Precio unitario. |
| `cantidad` | número | obligatorio | Unidades (≥ 1 en flujo real). |

## Campos obligatorios y opcionales

- **Obligatorios:** `pedidoId`, `usuarioId`, `creadoEn`, `total`, `lineas` (y dentro de cada línea: `productoId`, `nombre`, `precio`, `cantidad`)
- **Opcionales:** ninguno en `@1`

## Ejemplo de payload

```json
{
  "pedidoId": "PED-2026-0042",
  "usuarioId": "u-123",
  "creadoEn": "2026-10-28T16:40:00+01:00",
  "total": 39.98,
  "lineas": [
    {
      "productoId": "prod-101",
      "nombre": "Camiseta UCJC",
      "precio": 19.99,
      "cantidad": 2
    }
  ]
}
```

## Correspondencia con borradores previos (no usar en código)

| Borrador antiguo | Canónico `@1` |
| --- | --- |
| `ucjc:compra:pedido-confirmado:v1` (README Compra) | `ucjc:compra:pedido-confirmado@1` |
| `ucjc:compra:añadir@1` (Hoja B Compra↔Datos, entrega Rodrigo; solo `pedidoID`) | `ucjc:compra:pedido-confirmado@1` — el verbo correcto es **pedido-confirmado** (checkout), no «añadir». El `detail` lleva el pedido completo, no solo el id. |
| `order:confirmed` / sin `@n` (README Datos A) | `ucjc:compra:pedido-confirmado@1` |
| `orderId` / `pedidoId` / `pedidoID` | `pedidoId` |
| `userId` / `usuarioId` | `usuarioId` |
| `createdAt` / `fecha` / `timestamp` | `creadoEn` |
| `items` / `lineas` | `lineas` |
| `productId`·`name`·`price`·`quantity` | `productoId`·`nombre`·`precio`·`cantidad` |

## Conflictos de aula y resolución adoptada en `@1`

| Tema | Posiciones | Resolución en este contrato |
| --- | --- | --- |
| Quién genera el id del pedido | En aula hubo duda; Datos no puede devolver id en el mismo ciclo de evento | **Compra genera `pedidoId` y lo envía** en el `detail` (coherente con el README de Compra, que ya lista `pedidoId`) |
| Nombre «añadir» vs «pedido-confirmado» | Hoja B Compra↔Datos: `ucjc:compra:añadir@1` solo con `pedidoID`. README Compra y Datos A: pedido confirmado con líneas y total | Se adopta **`pedido-confirmado@1`** con el payload completo. «añadir» se reserva para el carrito (evento Descubrimiento→Compra), no para el checkout hacia Datos. |

Si Compra no acepta esta resolución, abrir Issue `conflicto` y **no** marcar el contrato como `firmado`.

## Responsables que aprueban

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| Compra | Emisor | Adrián Pingarrón (u otro responsable vigente) | pendiente | confirmar en el PR |
| Datos A | Consumidor | Hans Jefferson Arauco Sanchez | pendiente | confirmar en el PR |
| Datos B | Consumidor | pendiente de equipo/repo | pendiente | confirmar cuando exista |

## Estado del contrato

- [x] `propuesto` — texto de referencia en negociación; los equipos alinean README/código hacia este texto.
- [ ] `firmado` — emisor y consumidores han confirmado en el PR (o Hoja B + comentario); el profesor puede fusionar.
- [ ] `deprecado`

## Criterio para pasar a `firmado`

1. Compra confirma el nombre del evento, los campos y que emitirá `pedidoId`.
2. Datos A (Hans) confirma que con este `detail` puede persistir y pintar «Mis pedidos».
3. (Opcional pero deseable) Datos B confirma o deja Issue de discrepancia.
4. El profesor marca `firmado` en este fichero y hace merge a `main`.

## Historial

- `2026-10-26` — Negociación en aula (Hoja B Datos↔Compra); firma en papel de Datos; falta firma de Compra.
- `2026-11-02` — Redacción canónica en este repositorio (campos en español, sufijo `@1`, resolución del conflicto de `pedidoId`) a partir de Hoja B + README de Datos A + borrador de Compra.
- `2026-11-02` — Entrega Compra (Rodrigo / ZIP hojas A–C): Hoja B↔Datos con `añadir@1` + solo `pedidoID` mapeada a este contrato; el README del equipo ya estaba más cerca del canónico.
