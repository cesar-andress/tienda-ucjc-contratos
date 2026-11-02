# Contrato: `ucjc:descubrimiento:anadir-al-carrito@1`

## Nombre del evento

```text
ucjc:descubrimiento:anadir-al-carrito@1
```

Nombre de fichero: `ucjc-descubrimiento-anadir-al-carrito@1.md`

## Versión

| Campo | Valor |
| --- | --- |
| Versión del contrato del evento | `1` |
| ¿Sustituye a una versión anterior? | no |

## Equipo emisor

**Descubrimiento**

## Equipos consumidores

- **Compra** (añade la línea al carrito)

## Descripción

Descubrimiento emite este evento cuando el usuario elige un producto del catálogo / ficha para meterlo en el carrito.  
Compra lo escucha, actualiza el carrito local y (si quiere) puede emitir después un contador propio; eso no forma parte de este contrato.

## Campos y tipos (`event.detail`)

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `productoId` | texto | obligatorio | Identificador del producto en el catálogo. |
| `nombre` | texto | obligatorio | Nombre para mostrar en el carrito. |
| `precio` | número | obligatorio | Precio unitario (euros, sin símbolo). |
| `cantidad` | número | obligatorio | Unidades que se añaden (≥ 1). |

## Campos obligatorios y opcionales

- **Obligatorios:** `productoId`, `nombre`, `precio`, `cantidad`
- **Opcionales:** ninguno en `@1`

## Ejemplo de payload

```json
{
  "productoId": "prod-101",
  "nombre": "Camiseta UCJC",
  "precio": 19.99,
  "cantidad": 1
}
```

## Correspondencia con borradores previos (no usar en código)

| Borrador antiguo | Canónico `@1` |
| --- | --- |
| `ucjc:descubrir:añadir@1` (Hoja B Compra↔Descubrimiento) | `ucjc:descubrimiento:anadir-al-carrito@1` (pieza completa `descubrimiento`, verbo claro) |
| `ucjc:descubrimiento:anadir-al-carrito:v1` (README Compra) | `ucjc:descubrimiento:anadir-al-carrito@1` |
| `productoID` / `productoId` | `productoId` |
| `cantidadDisp` (Hoja B) | **no** va en `@1`; Compra no necesita stock para pintar el carrito. Si Descubrimiento quiere avisar stock, otro campo/opcional en `@2` o evento aparte |
| `cantidad` (README Compra) | `cantidad` |

## Conflictos de aula y resolución adoptada en `@1`

| Tema | Posiciones | Resolución en este contrato |
| --- | --- | --- |
| Nombre de pieza | Hoja B: `descubrir`; README Compra: `descubrimiento` | Pieza **`descubrimiento`** (nombre oficial del equipo) |
| Evento inverso Compra→Descubrimiento | Hoja B: `ucjc:comprar:añadir@1` con `cantidadPed`, `cantidadProd` | **No entra en este PR.** Para v0.2 el stock puede quedarse dentro de Descubrimiento. Si hace falta avisar cantidades pedidas, otro contrato cuando Descubrimiento confirme (con `productoId` obligatorio). |
| Solo `pedidoID` hacia Datos | Hoja B Compra↔Datos mezclaba «añadir» con Datos | Ese flujo es **`ucjc:compra:pedido-confirmado@1`**, no este evento |

Si Descubrimiento o Compra no aceptan el nombre o los campos, abrir Issue `conflicto` y no marcar `firmado`.

## Responsables que aprueban

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| Descubrimiento | Emisor | Daniel Molina Vitón (u otro responsable vigente) | pendiente | confirmar en el PR |
| Compra | Consumidor | Adrián Pingarrón (u otro responsable vigente) | pendiente | confirmar en el PR |

## Estado del contrato

- [x] `propuesto`
- [ ] `firmado`
- [ ] `deprecado`

## Criterio para pasar a `firmado`

1. Descubrimiento confirma que emitirá este nombre y estos campos.
2. Compra confirma que con este `detail` puede añadir al carrito.
3. El profesor marca `firmado` y fusiona.

## Historial

- `2026-10-26` — Negociación en aula (Hoja B Compra↔Descubrimiento); entrega PDF del equipo Compra (31/10).
- `2026-11-02` — Redacción canónica a partir de Hoja B + README de Compra; se deja fuera el evento inverso hacia Descubrimiento.
