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
| `ucjc:descubrimiento:envían` (Hoja B Descubrimiento↔«Carrito», entrega Daniel) | `ucjc:descubrimiento:anadir-al-carrito@1` — el verbo no es «envían»; hay que nombrar la acción |
| `ucjc:descubrimiento:anadir-al-carrito:v1` (README Compra) | `ucjc:descubrimiento:anadir-al-carrito@1` |
| `ProductoID` / `productoID` / `productoId` | `productoId` |
| `cantidadDisp` (Hoja B Compra) | **no** va en `@1` |
| `Cantidad` / `cantidad` | `cantidad` |
| `ucjc:carrito:envían` / `ucjc:comprar:añadir@1` (inverso hacia Descubrimiento) | **fuera de este PR** (ver conflictos) |

## Conflictos de aula y resolución adoptada en `@1`

| Tema | Posiciones | Resolución en este contrato |
| --- | --- | --- |
| Nombre de pieza | Hoja B Compra: `descubrir`; Descubrimiento dice «Carrito» | Pieza emisora **`descubrimiento`**; consumidor **`compra`** (no «carrito») |
| Verbo «envían» | Hoja B Descubrimiento | Se adopta **`anadir-al-carrito`** (acción concreta, español sin tilde en el token del nombre de fichero) |
| Evento inverso Compra→Descubrimiento | Hojas Compra y Descubrimiento (`comprar:añadir` / `carrito:envían` con añadir/quitar/cantidad) | **No entra en este PR.** Stock y catálogo se quedan en Descubrimiento para v0.2 |
| Solo `pedidoID` hacia Datos | Hoja B Compra↔Datos | Ese flujo es **`ucjc:compra:pedido-confirmado@1`**, no este evento |

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
- `2026-11-02` — Entrega Descubrimiento (Daniel): Hoja B↔Carrito con `…:envían`; mapeada a este contrato.
