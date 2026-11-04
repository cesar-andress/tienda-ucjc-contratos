
# Contrato de evento: pedido confirmado

## Nombre del evento

`ucjc:compra:pedido-confirmado@1`

## Versión

| **Campo** | **Valor** |
|---|---|
| Versión del evento | 1 |
| ¿Sustituye a una versión anterior? | no |

## Equipo emisor

Compra

## Equipos consumidores

- Datos

## Descripción

Compra emite este evento cuando el usuario confirma un pedido. El equipo Datos recibe la información del pedido para registrarlo.

## Campos y tipos

| **Campo** | **Tipo** | **Obligatorio / opcional** | **Descripción** |
|---|---|---|---|
| `pedidoId` | texto | obligatorio | Identificador del pedido generado por Compra. |
| `usuarioId` | texto | obligatorio | Identificador del usuario autenticado. |
| `creadoEn` | texto | obligatorio | Fecha y hora de creación en formato ISO 8601. |
| `total` | número | obligatorio | Importe total del pedido. |
| `lineas` | lista | obligatorio | Productos del pedido, cada uno con `productoId`, `nombre`, `precio` y `cantidad`. |

## Campos obligatorios y opcionales

- **Obligatorios:** `pedidoId`, `usuarioId`, `creadoEn`, `total`, `lineas`.
- **Opcionales:** ninguno.

## Ejemplo de payload

```json
{
  "pedidoId": "PED-001",
  "usuarioId": "USR-001",
  "creadoEn": "2026-11-04T10:00:00Z",
  "total": 19.98,
  "lineas": [
    {
      "productoId": "PROD-001",
      "nombre": "Cuaderno",
      "precio": 9.99,
      "cantidad": 2
    }
  ]
}
```

## Responsables que aprobaron el contrato

| **Equipo** | **Rol** | **Nombre del responsable** | **Fecha** | **Firma / visto bueno** |
|---|---|---|---|---|
| Compra | Emisor | Adrián Pingarrón | — | Pendiente |
| Datos | Consumidor | Pendiente de identificar | — | Pendiente |

## Estado del contrato

**propuesto**

## Historial

- 2026-11-04 — Creación de la propuesta del contrato `ucjc:compra:pedido-confirmado@1`.
