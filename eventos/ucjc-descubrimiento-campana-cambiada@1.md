# Contrato: `ucjc:descubrimiento:campana-cambiada@1`

## Nombre del evento

```text
ucjc:descubrimiento:campana-cambiada@1
```

Nombre de fichero: `ucjc-descubrimiento-campana-cambiada@1.md`

## Versión

| Campo | Valor |
| --- | --- |
| Versión del contrato del evento | `1` |
| ¿Sustituye a una versión anterior? | no |

## Equipo emisor

**Descubrimiento**

## Equipos consumidores

- **Compra**
- **Datos** (A y B)

Identidad no interviene.

## Descripción

Descubrimiento avisa cuando Black Friday (u otra campaña) se enciende o se apaga.
También avisa al cargar la pieza, con el estado actual.

Compra y Datos solo tienen que enterarse (por ejemplo, mostrar u ocultar un texto).
No cambia `anadir-al-carrito@1` ni `pedido-confirmado@1`.

## Campos y tipos (`event.detail`)

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `activa` | booleano | obligatorio | `true` si la campaña está encendida. |
| `codigo` | texto | obligatorio | p. ej. `black-friday-2026` |
| `etiqueta` | texto | obligatorio | Texto en pantalla, p. ej. `Black Friday UCJC` |
| `momento` | texto (ISO 8601) | obligatorio | Cuándo se anuncia. |

## Campos obligatorios y opcionales

- **Obligatorios:** `activa`, `codigo`, `etiqueta`, `momento`
- **Opcionales:** ninguno

## Ejemplo de payload

```json
{
  "activa": true,
  "codigo": "black-friday-2026",
  "etiqueta": "Black Friday UCJC",
  "momento": "2026-11-27T09:00:00+01:00"
}
```

```json
{
  "activa": false,
  "codigo": "black-friday-2026",
  "etiqueta": "Black Friday UCJC",
  "momento": "2026-11-28T00:00:00+01:00"
}
```

## Responsables que aprueban

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| Descubrimiento | Emisor | Daniel Molina Viton | 25/11/2026 | Firmado |
| Compra A | Consumidor | | | |
| Compra B | Consumidor | Daniel Molina Viton | 25/11/2026 | Firmado |
| Datos A | Consumidor | Hans Jefferson Arauco Sanchez| 23/11/2026 | Firmado |
| Datos B | Consumidor | | | |

## Estado del contrato

- [ ] `propuesto`
- [x] `firmado`
- [ ] `deprecado`

## Historial

- `2026-11-23` — Propuesta del profesor (Black Friday).
- `2026-11-23` — Campos reducidos a cuatro; Identidad fuera.
- `2026-11-23` — Estado → **`firmado`** (PR #1 · dani84mol / Descubrimiento).
