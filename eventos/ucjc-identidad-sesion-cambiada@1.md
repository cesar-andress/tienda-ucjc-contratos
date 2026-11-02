# Contrato: ucjc:identidad:sesion-cambiada@1

## Nombre del evento

```text
ucjc:identidad:sesion-cambiada@1
```

## Versión

| Campo | Valor |
| --- | --- |
| Versión del evento | `1` |
| ¿Sustituye a una versión anterior? | `no` |

## Equipo emisor

Identidad

## Equipos consumidores

- Datos (variante A — Hans Jefferson Arauco Sanchez)
- Datos (variante B — cuando exista equipo/repo; pendiente de confirmar)
- Compra *(si también lo consume; confirmar)*

## Descripción

Identidad emite este evento al iniciar sesión, al cerrarla y, si procede, al cargar la pieza con el estado actual. Datos lo usa para filtrar «Mis pedidos» por usuario y para limpiar la vista al cerrar sesión (`isAuthenticated: false`).

## Campos y tipos

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `isAuthenticated` | booleano | obligatorio | `true` si hay sesión activa; `false` al cerrar sesión. |
| `user` | objeto | opcional; **obligatorio si** `isAuthenticated` es `true` | Datos del usuario. Si `isAuthenticated` es `false`, usar `null` o omitir. |
| `user.id` | texto | obligatorio (si hay `user`) | Identificador del usuario. |
| `user.email` | texto | obligatorio (si hay `user`) | Correo del usuario (legible para mostrar en historial, según acuerdo en plenario Datos). |

## Campos obligatorios y opcionales

- **Obligatorios:** `isAuthenticated`; `user` (con `id` y `email`) cuando `isAuthenticated` es `true`
- **Opcionales:** `user` cuando `isAuthenticated` es `false` (recomendado: `null`)

## Ejemplo de payload

Sesión iniciada:

```json
{
  "isAuthenticated": true,
  "user": {
    "id": "u-123",
    "email": "ana@alumno.ucjc.edu"
  }
}
```

Sesión cerrada:

```json
{
  "isAuthenticated": false,
  "user": null
}
```

## Responsables que aprobaron el contrato

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| Identidad | Emisor | *(pendiente — falta firma en Hoja B)* | | propuesto; confirmar en este PR |
| Datos A | Consumidor | Hans Jefferson Arauco Sanchez | 2026-10-26 | Hoja B en papel (firma Datos); revisión GitHub pendiente |

## Estado del contrato

Marcad **uno**:

- [x] `propuesto` — borrador en negociación; aún no se implementa como referencia.
- [ ] `firmado` — aprobado por emisor y consumidores; es la referencia compartida.
- [ ] `deprecado` — sustituido por una versión nueva; se mantiene temporalmente por compatibilidad.

## Historial

- `2026-11-02` — Transcripción docente a partir de la Hoja B Datos↔Identidad y del README de `tienda-ucjc-datos` (Datos A). Estado `propuesto`.
- Conflicto abierto en aula (Hoja B): Identidad prefería un id anónimo; Datos necesita al menos `id` o `email` legible para el historial. Esta propuesta incluye `user.id` y `user.email` obligatorios si hay sesión. Debe confirmarse con Identidad.
- Plenario: al cerrar sesión, Datos limpia la vista de pedidos.
