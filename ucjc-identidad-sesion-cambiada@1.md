## Nombre del evento

```text
ucjc:identidad:sesion-cambiada@1
```

## Versión

| Campo | Valor |
| --- | --- |
| Versión del evento | `1`|
| ¿Sustituye a una versión anterior? | `no` |

## Equipo emisor

**`Identidad`**

## Equipos consumidores

**`Datos`**

## Descripción

Informa del estado de la sesión (login o logout) del usuario en la tienda para que la pieza Datos filtre los pedidos del usuario autenticado o limpie la vista al cerrar sesión.

## Campos y tipos

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `<autenticado>` | `<booleano>` | obligatorio | Identificador único del pedido |
| `<usuario>` | `<objeto>` | obligatorio | Identificador del usuario que realizó la compra |
| `<usuario.Id>` | `<texto>` | obligatorio | Identificador del usuario que realizó la compra |
| `<usuario.email>` | `<texto>` | obligatorio | Fecha y hora en formato ISO |

## Campos obligatorios y opcionales

- **Obligatorios:** `<autenticado>`
- **Opcionales:** `<usuario>` (presente si `<autenticado>` es true, null en caso contrario), `<usuario.id>`, `<usuario.email>`.

## Ejemplo de payload

```json
{
  "autenticado": true,
  "usuario": {
    "id": "usr-8492",
    "email": "demo@alumno.ucjc.edu"
  }
}
```

## Responsables que aprobaron el contrato

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| `<Identidad>` | Emisor | Sebastián Blanco | 2026-11-04 | Firmado |
| `<Datos>` | Consumidor | Hans Jefferson Arauco Sanchez | 2026-11-04 | Firmado |

## Estado del contrato

Marcad **uno**:

- [ ] `propuesto` — borrador en negociación; aún no se implementa como referencia.
- [x] `firmado` — aprobado por emisor y consumidores; es la referencia compartida.
- [ ] `deprecado` — sustituido por una versión nueva; se mantiene temporalmente por compatibilidad.

## Historial

- `2026-11-04` — Aprobación y firma del contrato ucjc:identidad:sesion-cambiada@1 entre Identidad y Datos.