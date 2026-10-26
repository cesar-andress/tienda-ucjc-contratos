# Plantilla de contrato de evento

Copiad este fichero a `eventos/` y renombradlo según el evento, por ejemplo `ucjc-pieza-verbo@1.md`.  
Sustituid todos los marcadores `<…>`. No dejéis ejemplos inventados como si ya estuvieran firmados.

## Nombre del evento

```text
ucjc:<pieza>:<verbo>@<version>
```

## Versión

| Campo | Valor |
| --- | --- |
| Versión del evento | `<n>` (la misma que aparece tras `@` en el nombre) |
| ¿Sustituye a una versión anterior? | `no` / `sí: ucjc:<pieza>:<verbo>@<n-1>` |

## Equipo emisor

`<Descubrimiento | Compra | Identidad | Datos>`

## Equipos consumidores

- `<equipo>`
- `<equipo>`

## Descripción

Una o dos frases: cuándo se emite el evento y qué significa para quien lo escucha.

## Campos y tipos

| Campo | Tipo | Obligatorio / opcional | Descripción |
| --- | --- | --- | --- |
| `<nombre>` | `<texto \| número \| booleano \| objeto \| lista>` | obligatorio | |
| `<nombre>` | `<…>` | opcional | |

## Campos obligatorios y opcionales

- **Obligatorios:** `<lista>`
- **Opcionales:** `<lista>`

Si un consumidor necesita un dato que hoy es opcional, negociad si pasa a obligatorio en una **nueva versión** del evento.

## Ejemplo de payload

```json
{
  "campo": "valor"
}
```

El ejemplo debe coincidir con la tabla de campos. No añadáis claves que no estén documentadas.

## Responsables que aprobaron el contrato

| Equipo | Rol | Nombre del responsable | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- |
| `<emisor>` | Emisor | | | |
| `<consumidor>` | Consumidor | | | |

## Estado del contrato

Marcad **uno**:

- [ ] `propuesto` — borrador en negociación; aún no se implementa como referencia.
- [ ] `firmado` — aprobado por emisor y consumidores; es la referencia compartida.
- [ ] `deprecado` — sustituido por una versión nueva; se mantiene temporalmente por compatibilidad.

## Historial

- `<AAAA-MM-DD>` — creación / cambio / deprecación (una línea).
