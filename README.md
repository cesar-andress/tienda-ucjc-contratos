# tienda-ucjc-contratos

Repositorio central de **contratos** de la práctica **Tienda UCJC** (Desarrollo de Front-End, UCJC, curso 2026/2027): eventos del bus y presentación (CSS/JS) del shell.

**Repositorio (público):** https://github.com/cesar-andress/tienda-ucjc-contratos  
**Shell en vivo:** https://cesar-andress.github.io/tienda-ucjc-shell/

## Situación actual (25/11/2026) · tag `v0.2.7`

| Hecho | Estado |
| --- | --- |
| Tag / release | **`v0.2.7`** — `presentacion-campus@1` completo + flujo mínimo + `campana-cambiada@1` |
| Este repositorio | **Público** (escritura solo el profesor) |
| Firmados | Flujo mínimo `@1` + [`campana-cambiada@1`](eventos/ucjc-descubrimiento-campana-cambiada@1.md) |
| Propuestos (eventos) | [`pedido-confirmado@2`](eventos/ucjc-compra-pedido-confirmado@2.md) · [`moneda-cambiada@1`](eventos/ucjc-descubrimiento-moneda-cambiada@1.md) |
| Propuesto (presentación) | [`presentacion-campus@1`](presentacion/ucjc-presentacion-campus@1.md) — CSS/JS del shell; firma cada variante el 30/11 |
| Mesa BF | [`PROPUESTA-BLACK-FRIDAY.md`](eventos/PROPUESTA-BLACK-FRIDAY.md) |
| Shell | Tag **`v0.3.10`** · https://cesar-andress.github.io/tienda-ucjc-shell/ |
| PR abierto | **#3** Compra — **no mergear tal cual** (depreca mal `sesion-cambiada@1`) |

### Los tres mensajes del flujo mínimo (nombres canónicos)

```text
ucjc:identidad:sesion-cambiada@1
ucjc:descubrimiento:anadir-al-carrito@1
ucjc:compra:pedido-confirmado@1
```

| Evento | Fichero | Estado |
| --- | --- | --- |
| `sesion-cambiada@1` | [`eventos/ucjc-identidad-sesion-cambiada@1.md`](eventos/ucjc-identidad-sesion-cambiada@1.md) | `deprecado` |
| `anadir-al-carrito@1` | [`eventos/ucjc-descubrimiento-anadir-al-carrito@1.md`](eventos/ucjc-descubrimiento-anadir-al-carrito@1.md) | `firmado` |
| `pedido-confirmado@1` | [`eventos/ucjc-compra-pedido-confirmado@1.md`](eventos/ucjc-compra-pedido-confirmado@1.md) | `firmado` |
| `campana-cambiada@1` | [`eventos/ucjc-descubrimiento-campana-cambiada@1.md`](eventos/ucjc-descubrimiento-campana-cambiada@1.md) | `firmado` |
| `pedido-confirmado@2` | [`eventos/ucjc-compra-pedido-confirmado@2.md`](eventos/ucjc-compra-pedido-confirmado@2.md) | `firmado` |
| `moneda-cambiada@1` | [`eventos/ucjc-descubrimiento-moneda-cambiada@1.md`](eventos/ucjc-descubrimiento-moneda-cambiada@1.md) | `propuesto` |
| `presentacion-campus@1` | [`presentacion/ucjc-presentacion-campus@1.md`](presentacion/ucjc-presentacion-campus@1.md) | `propuesto` |

El `@1` / `@2` es la versión del **contrato del evento**. No es lo mismo que el tag de la pieza (`v0.2.0`, `v1.0.0`, …). La presentación campus no es un evento: es el estilo y el script que impone el shell.

**Black Friday:** mesa 25/11 → demo 27/11. Ver [`PROPUESTA-BLACK-FRIDAY.md`](eventos/PROPUESTA-BLACK-FRIDAY.md).
## Qué es Tienda UCJC

Tienda UCJC es una tienda web de campus construida por cuatro equipos independientes. Cada equipo desarrolla y publica su propio micro-frontend. El shell del profesor los carga en tiempo de ejecución.

Nadie programa la tienda entera. Cada equipo posee una pieza y solo esa pieza.

## Los cuatro equipos

| Equipo | Responsabilidad |
| --- | --- |
| **Descubrimiento** | Catálogo de productos, búsqueda y ficha. |
| **Compra** | Carrito y proceso de compra. |
| **Identidad** | Usuario y sesión. |
| **Datos** | Pedidos y persistencia simulada (variantes A/B en el shell; query `?datos=a|b`). |

Los equipos **no** pueden abrir ni importar el código de otro micro-frontend. La única referencia compartida entre piezas son los contratos aprobados en este repositorio.

## Para qué sirve este repositorio

Aquí se documenta:

1. **Eventos** — qué puede emitir o escuchar cada pieza y qué campos viajan en `detail` ([`eventos/`](eventos/)).
2. **Presentación** — estilo y script comunes que impone el shell ([`presentacion/`](presentacion/)).

- Si el Markdown de un evento no está en [`eventos/`](eventos/) de `main`, **no existe** para la tienda.
- El código de cada equipo implementa lo firmado; no inventa campos, nombres ni paletas por su cuenta.
- El shell no conoce el interior de las piezas: carga releases, deja circular los eventos por `window` y entrega `comun/campus.*`.

Plantilla de evento: [`PLANTILLA-EVENTO.md`](PLANTILLA-EVENTO.md).  
Ejemplo de formato: [`eventos/EJEMPLO-como-rellenar.md`](eventos/EJEMPLO-como-rellenar.md).

## Qué es un contrato entre micro-frontends

Acuerdo escrito entre quien **emite** un evento y quien lo **consume**. Incluye, como mínimo:

- nombre del evento y versión `@n`,
- emisor y consumidores,
- cuándo se dispara,
- campos de `detail` (tipo, obligatorio/opcional),
- ejemplo de payload,
- quién lo aprobó,
- estado: `propuesto` · `firmado` · `deprecado`.

## Convención de nombres

```text
ucjc:<pieza>:<verbo>@<n>
```

Minúsculas, en español, sin espacios. El `@n` **no** es la release `vX.Y.Z` del micro-frontend.

| Concepto | Ejemplo | Qué identifica |
| --- | --- | --- |
| Contrato de evento | `…@1` | Forma del mensaje entre piezas |
| Release del micro-frontend | `v0.2.0` | Artefacto publicado (`remote.js`) |
| Versión en el manifest del shell | `0.2.2`, etc. | Release **activa** en la tienda en vivo |

No hay equivalencia automática entre `v1.0.0` y `@1`.

## Cómo se negocian los eventos

1. En aula se acuerda (emisor, consumidores, campos).
2. El equipo emisor puede proponer por **fork + Pull Request** (sin push al original).
3. El fichero va en `eventos/` con el nombre del evento.
4. Los consumidores confirman en el PR (comentario identificable).
5. **Solo el profesor** fusiona a `main` cuando el estado es `firmado`.

Reglas:

- El **nombre** lo propone quien emite; los **campos** se firman con quien consume.
- Cada equipo solo propone eventos que **emite**.
- No dejéis Markdown de contratos en la **raíz** del repo: eventos en `eventos/`, presentación en `presentacion/`.

## Modelo de contribución: fork + Pull Request

**No podéis hacer `git push` a este repositorio.** Flujo: fork → rama → PR hacia `main` → el profesor fusiona.

Detalle operativo: [`CONTRIBUYENDO.md`](CONTRIBUYENDO.md).

## Firmas y confirmaciones

- El OK oral (o la firma en papel) de clase sigue siendo válido.
- En un PR, el consumidor deja un comentario explícito de aceptación.
- El botón «Approve» de GitHub no sustituye el acuerdo académico.
- **Solo el profesor** decide el *merge*.

## Cambios compatibles e incompatibles

- Campo opcional nuevo que no rompe a nadie: puede mantener `@n` si se documenta.
- Renombrar campo, cambiar tipo o hacerlo obligatorio: nueva versión `@n+1`; la anterior pasa a `deprecado`.

Desacuerdos: Issue con etiqueta `conflicto`.

## Contenido del repositorio

| Ruta | Uso |
| --- | --- |
| [`PLANTILLA-EVENTO.md`](PLANTILLA-EVENTO.md) | Modelo para cada contrato de evento |
| [`CONTRIBUYENDO.md`](CONTRIBUYENDO.md) | Fork + PR día a día |
| [`eventos/`](eventos/) | Contratos de eventos (+ ejemplo + flujo mínimo + mesa BF) |
| [`presentacion/`](presentacion/) | Contrato de CSS/JS del shell (`presentacion-campus@1`) |
| [`.github/`](.github/) | Plantillas de Issue y Pull Request |

## Referencias

- Shell: https://github.com/cesar-andress/tienda-ucjc-shell  
- Tienda en vivo: https://cesar-andress.github.io/tienda-ucjc-shell/
