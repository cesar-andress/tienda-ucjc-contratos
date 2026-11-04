# EJEMPLO (no implementar)

> **Esto no es un contrato de la Tienda UCJC.**  
> Sirve solo para ver cómo se rellena la plantilla.  
> Los contratos reales se llaman `ucjc-<pieza>-<verbo>@<n>.md` y llevan estado `firmado` tras el OK en clase.

---

## Nombre del evento

```text
ucjc:ejemplo:producto-visto@1
```

Nombre de fichero (si fuera real): `ucjc-ejemplo-producto-visto@1.md`

## Versión

| Campo | Valor |
| --- | --- |
| Versión del evento | `1` |
| ¿Sustituye a una versión anterior? | no |

## Equipo emisor

**Descubrimiento** *(en el ejemplo inventado)*

## Equipos consumidores

- **Datos** *(en el ejemplo inventado)*

## Descripción

Se emitiría cuando el usuario abre la ficha de un producto. Quien escucha podría anotar interés; **en el flujo mínimo de la tienda este evento no existe**.

## Campos y tipos

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `productoId` | texto | obligatorio | Identificador del producto. |
| `nombre` | texto | obligatorio | Nombre para mostrar. |
| `vistoEn` | texto | opcional | Origen de la vista (`catalogo` / `busqueda`). |

## Campos obligatorios y opcionales

- **Obligatorios:** `productoId`, `nombre`
- **Opcionales:** `vistoEn`

## Ejemplo de payload

```json
{
  "productoId": "prod-42",
  "nombre": "Sudadera campus",
  "vistoEn": "catalogo"
}
```

## Responsables que aprobaron el contrato

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| Descubrimiento | Emisor | *(ejemplo)* | — | — |
| Datos | Consumidor | *(ejemplo)* | — | — |

## Estado del contrato

- [x] `propuesto` — **ejemplo**; no usar en código.
- [ ] `firmado`
- [ ] `deprecado`

## Historial

- `2026-11-04` — creación del ejemplo para la carpeta `eventos/`.
