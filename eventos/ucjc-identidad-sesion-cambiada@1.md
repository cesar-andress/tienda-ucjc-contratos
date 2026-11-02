# Contrato: `ucjc:identidad:sesion-cambiada@1`

## Nombre del evento

```text
ucjc:identidad:sesion-cambiada@1
```

Nombre de fichero: `ucjc-identidad-sesion-cambiada@1.md`

## Versión

| Campo | Valor |
| --- | --- |
| Versión del contrato del evento | `1` |
| ¿Sustituye a una versión anterior? | no |

## Equipo emisor

**Identidad**

## Equipos consumidores

- **Datos** (variante A — Hans Jefferson Arauco Sanchez / `tienda-ucjc-datos`)
- **Datos** (variante B — cuando publiquen repo; deben confirmar)
- **Compra** (necesita saber si hay sesión para checkout; debe confirmar este contrato o uno posterior si sus campos difieren)

## Descripción

Identidad emite este evento:

1. al **iniciar** sesión,
2. al **cerrar** sesión,
3. al **cargar** la pieza, con el estado actual (para quien llegue tarde).

Datos lo usa para filtrar «Mis pedidos» por `usuario.id` y para **vaciar la vista** cuando `autenticado` es `false` (no dejar pedidos de otro usuario en pantalla).

## Campos y tipos (`event.detail`)

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `autenticado` | booleano | obligatorio | `true` si hay sesión activa; `false` al cerrar sesión o sin sesión. |
| `usuario` | objeto o `null` | obligatorio | Si `autenticado` es `true`, objeto de usuario. Si `autenticado` es `false`, debe ser `null`. |
| `momento` | texto (ISO 8601) | opcional | Instantánea del cambio de sesión (útil para depuración y logs). |

### Campos de `usuario` (cuando no es `null`)

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `id` | texto | obligatorio | Identificador estable del usuario (el que Compra pondrá en `usuarioId` del pedido). |
| `email` | texto | obligatorio | Correo legible para mostrar en la UI de pedidos / perfil. |
| `nombre` | texto | opcional | Nombre para mostrar; no sustituye a `id` ni a `email`. |

## Campos obligatorios y opcionales

- **Obligatorios:** `autenticado`, `usuario` (`null` o objeto completo según el caso); si hay objeto: `id`, `email`
- **Opcionales:** `momento`; `usuario.nombre`

## Ejemplos de payload

### Sesión iniciada (o estado actual autenticado)

```json
{
  "autenticado": true,
  "usuario": {
    "id": "u-123",
    "email": "ana@alumno.ucjc.edu",
    "nombre": "Ana Pérez"
  },
  "momento": "2026-10-26T10:00:00Z"
}
```

### Sesión cerrada (o sin sesión)

```json
{
  "autenticado": false,
  "usuario": null,
  "momento": "2026-10-26T10:05:00Z"
}
```

## Correspondencia con borradores previos (no usar en código)

| Borrador antiguo | Canónico `@1` |
| --- | --- |
| `Sesiones guardadas ()` (Hoja B Identidad↔Datos, entrega Sebastián) | `ucjc:identidad:sesion-cambiada@1` |
| `ucjc:sesion-cambiada:v1` (README Identidad) | `ucjc:identidad:sesion-cambiada@1` |
| `ucjc:identidad:sesion-cambiada:v1` (README Compra) | `ucjc:identidad:sesion-cambiada@1` |
| `auth:session-changed` / `ucjc:session:changed` | `ucjc:identidad:sesion-cambiada@1` |
| `ID` / `datos del usuario` (Hoja B Identidad) | `usuario.id` + `usuario.email` (+ `usuario.nombre` opcional) |
| `permisos` / `roles` (Hoja B Identidad) | **no** van en el `detail` de `@1` (se gestionan dentro de la pieza Identidad) |
| `isAuthenticated` / `autenticado` | `autenticado` |
| `user` / `usuario` | `usuario` |
| `usuarioId` + `nombre` planos (README Compra) | van **dentro** de `usuario` (`usuario.id`, `usuario.nombre`); el top-level es `autenticado` + `usuario` / `null` |
| `version` dentro del `detail` | **no** forma parte de `@1` (la versión va en el **nombre** del evento con `@1`) |
| `ucjc:sesion-solicitada:v1` / `ucjc:sesion-consultada:v1` (README Identidad) | **fuera de este contrato**; si hacen falta, otro PR con nombre `ucjc:identidad:…@1` |

## Conflictos de aula y resolución adoptada en `@1`

| Tema | Posiciones | Resolución en este contrato |
| --- | --- | --- |
| Privacidad vs historial | Identidad prefería id anónimo; Datos necesita identificar pedidos | Con sesión activa, **`usuario.id` y `usuario.email` son obligatorios** (email legible para la UI de Datos). No basta un id opaco sin email si Datos debe mostrar «User: …@…». |
| Logout | Plenario | Si `autenticado` es `false`, Datos **limpia** la lista visible de pedidos. |
| Roles / permisos en el bus | Hoja B Identidad lista `permisos` y `roles` como campos del evento | En `@1` **no** viajan por el bus. Login/registro/roles siguen siendo responsabilidad de Identidad; el evento solo avisa del cambio de sesión. Si Identidad necesita emitir roles a otras piezas, abrir Issue `conflicto` o un `@2` / evento aparte. |

Si Identidad no acepta email obligatorio, o exige `permisos`/`roles` en el `detail`, abrir Issue `conflicto` y no marcar `firmado`.

## Responsables que aprueban

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| Identidad | Emisor | Sebastián Blanco (u otro responsable vigente) | pendiente | confirmar en el PR |
| Datos A | Consumidor | Hans Jefferson Arauco Sanchez | pendiente | confirmar en el PR |
| Compra | Consumidor | Adrián Pingarrón (u otro responsable vigente) | pendiente | confirmar en el PR |
| Datos B | Consumidor | pendiente | pendiente | cuando exista equipo |

## Estado del contrato

- [x] `propuesto`
- [ ] `firmado`
- [ ] `deprecado`

## Criterio para pasar a `firmado`

1. Identidad confirma nombre del evento y forma del `detail` (incluida la obligación de `email` con sesión).
2. Datos A confirma que puede filtrar y limpiar «Mis pedidos».
3. Compra confirma que puede usar `usuario.id` como `usuarioId` al confirmar pedidos (o abre Issue si necesita más campos).
4. El profesor marca `firmado` y fusiona.

## Historial

- `2026-10-26` — Negociación en aula (Hoja B Datos↔Identidad); firma en papel de Datos; falta firma de Identidad.
- `2026-11-02` — Redacción canónica (nombre con pieza `identidad`, campos en español, `@1`, sin `version` en el payload) unificando borradores de Identidad, Compra y Datos A.
- `2026-11-02` — Entrega Hoja B del equipo Identidad (Sebastián): nombre informal «Sesiones guardadas ()» y campos `ID` / `datos del usuario` / `permisos` / `roles`; mapeados arriba; `permisos`/`roles` quedan fuera de `@1`.
