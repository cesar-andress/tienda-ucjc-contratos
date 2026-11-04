## Nombre del evento

```text
ucjc:compra:pedido-confirmado@1
```

## Versión

| Campo | Valor |
| --- | --- |
| Versión del evento | `1`|
| ¿Sustituye a una versión anterior? | `no` |

## Equipo emisor

**`Compra`**

## Equipos consumidores

**`Datos`**

## Descripción

Notifica que un pedido ha sido finalizado y pagado con éxito para que la pieza Datos lo registre en la persistencia y actualice el historial en «Mis pedidos».

## Campos y tipos

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `<pedidoId>` | `<texto>` | obligatorio | Identificador único del pedido |
| `<usuarioId>` | `<texto>` | obligatorio | Identificador del usuario que realizó la compra |
| `<creadoEn>` | `<texto>` | obligatorio | Fecha y hora en formato ISO |
| `<total>` | `<número>` | obligatorio | Importe total del pedido |
| `<lineas>` | `<lista>` | obligatorio | Artículos contenidos en el pedido |
| `<lineas[].productoId>` | `<texto>` | obligatorio | Identificador del producto |
| `<lineas[].nombre>` | `<texto>` | obligatorio | Nombre del producto |
| `<lineas[].precio>` | `<número>` | obligatorio | Precio unitario |
| `<lineas[].cantidad>` | `<número>` | obligatorio | Cantidad de unidades |

## Campos obligatorios y opcionales

- **Obligatorios:** `<pedidoId>`, `<usuarioId>`, `<creadoEn>`, `<total>`, `<lineas>` con (`<productoId>`, `<nombre>`, `<precio>`, `<cantidad>`)
- **Opcionales:** Ninguno.

## Ejemplo de payload

```json
{
  "pedidoId": "P-1001",
  "usuarioId": "User-8492",
  "creadoEn": "2026-11-04T10:00:00.000Z",
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

## Responsables que aprobaron el contrato

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| `<Compra>` | Emisor | Alessa Comparini | 2026-11-04 | Firmado / Aprobado |
| `<Datos>` | Consumidor | Hans Jefferson Arauco Sanchez | 2026-11-04 | Firmado Aprobado |

## Estado del contrato

Marcad **uno**:

- [ ] `propuesto` — borrador en negociación; aún no se implementa como referencia.
- [x] `firmado` — aprobado por emisor y consumidores; es la referencia compartida.
- [ ] `deprecado` — sustituido por una versión nueva; se mantiene temporalmente por compatibilidad.

## Historial

- `2026-11-04` — Aprobación y firma del contrato ucjc:compra:pedido-confirmado@1 entre Compra y Datos.