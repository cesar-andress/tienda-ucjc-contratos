# Contrato: ucjc:compra:pedido-confirmado@1

## Para verificar y dar el OK (Datos A — Hans)

Compara con tu Hoja B Datos↔Compra y tu README. Marca en el **comentario del Pull Request** (no edites este fichero salvo que el profesor te lo pida).

- [ ] Nombre del evento correcto: `ucjc:compra:pedido-confirmado@1`
- [ ] Emisor = Compra; consumidor = Datos
- [ ] Campos: `orderId`, `userId`, `createdAt`, `total`, `items[]` (`productId`, `name`, `price`, `quantity`) — todos obligatorios
- [ ] El ejemplo JSON coincide con la tabla
- [ ] Mantengo que `orderId` lo envía Compra (conflicto de aula)
- [ ] Estado `propuesto` OK hasta firma de Compra

Si todo encaja, comenta en el PR: `Confirmo que el equipo Datos acepta ucjc:compra:pedido-confirmado@1 según lo acordado en clase.`

Si algo falla, indica **campo concreto** y el valor que quieres.

---

## Nombre del evento

```text
ucjc:compra:pedido-confirmado@1
```

## Versión

| Campo | Valor |
| --- | --- |
| Versión del evento | `1` |
| ¿Sustituye a una versión anterior? | `no` |

## Equipo emisor

Compra

## Equipos consumidores

- Datos (variante A — Hans Jefferson Arauco Sanchez)
- Datos (variante B — cuando exista equipo/repo; pendiente de confirmar)

## Descripción

Compra emite este evento cuando el usuario confirma un pedido. Datos lo escucha para persistirlo (simulado) y mostrarlo en «Mis pedidos».

## Campos y tipos

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `orderId` | texto | obligatorio | Identificador único del pedido (lo aporta Compra al emitir). |
| `userId` | texto | obligatorio | Identificador del usuario que confirma el pedido. |
| `createdAt` | texto (ISO 8601) | obligatorio | Momento de confirmación del pedido. |
| `total` | número | obligatorio | Importe total del pedido. |
| `items` | lista de objetos | obligatorio | Líneas del pedido. Cada elemento: `productId` (texto), `name` (texto), `price` (número), `quantity` (número), todos obligatorios. |

## Campos obligatorios y opcionales

- **Obligatorios:** `orderId`, `userId`, `createdAt`, `total`, `items`
- **Opcionales:** ninguno en `@1`

## Ejemplo de payload

```json
{
  "orderId": "PED-2026-0042",
  "userId": "u-123",
  "createdAt": "2026-10-28T16:40:00+01:00",
  "total": 39.98,
  "items": [
    {
      "productId": "prod-101",
      "name": "Camiseta UCJC",
      "price": 19.99,
      "quantity": 2
    }
  ]
}
```

## Responsables que aprobaron el contrato

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| Compra | Emisor | *(pendiente — falta firma en Hoja B)* | | propuesto; confirmar en este PR |
| Datos A | Consumidor | Hans Jefferson Arauco Sanchez | 2026-10-26 | Hoja B en papel (firma Datos); revisión GitHub pendiente |

## Estado del contrato

Marcad **uno**:

- [x] `propuesto` — borrador en negociación; aún no se implementa como referencia.
- [ ] `firmado` — aprobado por emisor y consumidores; es la referencia compartida.
- [ ] `deprecado` — sustituido por una versión nueva; se mantiene temporalmente por compatibilidad.

## Historial

- `2026-11-02` — Transcripción docente a partir de la Hoja B Datos↔Compra y del README de `tienda-ucjc-datos` (Datos A), para que Hans revise el flujo de PR. Estado `propuesto`.
- Conflicto abierto en aula (Hoja B): Compra pretendía emitir sin `orderId` y que Datos lo generara; Datos exige `orderId` en el evento (asíncrono). Esta propuesta sigue la posición de Datos (`orderId` obligatorio). Debe confirmarse con Compra.
