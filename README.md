# tienda-ucjc-contratos

Repositorio central de **contratos de eventos** de la práctica **Tienda UCJC** (Desarrollo de Front-End, UCJC, curso 2026/2027).

## Qué es Tienda UCJC

Tienda UCJC es una tienda web de campus construida por cuatro equipos independientes. Cada equipo desarrolla y publica su propio micro-frontend. El shell del profesor los carga en tiempo de ejecución y los une en una sola experiencia de usuario.

Nadie programa la tienda entera. Cada equipo posee una pieza y solo esa pieza.

## Los cuatro equipos

| Equipo | Responsabilidad |
| --- | --- |
| **Descubrimiento** | Catálogo de productos, búsqueda y ficha. |
| **Compra** | Carrito y proceso de compra. |
| **Identidad** | Usuario y sesión. |
| **Datos** | Pedidos y persistencia simulada. |

Los equipos **no** pueden abrir ni importar el código de otro micro-frontend. La única referencia compartida entre piezas son los contratos aprobados en este repositorio.

## Para qué sirve este repositorio

Aquí se documenta **qué eventos** puede emitir o escuchar cada pieza y **qué campos** viajan en cada evento.

- Si un acuerdo no está escrito aquí, **no existe** para la tienda.
- El código de cada equipo implementa lo firmado; no inventa campos ni nombres por su cuenta.
- El shell no conoce el interior de las piezas: solo carga releases y deja que los eventos circulen por `window`.

La carpeta [`eventos/`](eventos/) empieza vacía a propósito. Los contratos se escriben **después** de negociarlos en clase, no antes.

## Qué es un contrato entre micro-frontends

Un contrato es el acuerdo escrito entre el equipo que **emite** un evento y el equipo (o equipos) que lo **consumen**.

Incluye, como mínimo:

- el nombre del evento,
- su versión,
- quién emite y quién consume,
- la descripción de cuándo se dispara,
- los campos del `detail`, con tipo y carácter obligatorio u opcional,
- un ejemplo de payload,
- quién lo aprobó,
- el estado del contrato (`propuesto`, `firmado`, `deprecado`).

Sin contrato firmado no hay integración fiable: un cambio de nombre o de tipo en un campo rompe a quien escucha, aunque el código de cada lado “funcione” por separado.

## Convención de nombres

Formato obligatorio:

```text
ucjc:<pieza>:<verbo>@<version>
```

- Minúsculas, en español, sin espacios.
- La versión va en el **nombre** del evento (`@1`, `@2`, …), no solo dentro del `detail`.
- Así pueden convivir dos versiones mientras los consumidores migran.

Ejemplo **ilustrativo** (no es un contrato definitivo; no lo copies a `eventos/` como si ya estuviera aprobado):

```text
ucjc:descubrimiento:añadir@1
```

## Cómo se negocian los eventos

1. En aula se acuerdan en papel (emisor, consumidores y campos).
2. El equipo **emisor** abre un Pull Request que añade un fichero en `eventos/` partiendo de [`PLANTILLA-EVENTO.md`](PLANTILLA-EVENTO.md).
3. El nombre del fichero refleja el del evento, por ejemplo `ucjc-descubrimiento-añadir@1.md`.
4. Los equipos **consumidores** revisan el PR y lo aprueban (o piden cambios).
5. Solo cuando emisor y consumidores están de acuerdo, el contrato pasa a estado `firmado` y puede fusionarse.

Reglas:

- El **nombre** del evento lo propone quien emite; los **campos** se firman entre emisor y consumidores.
- Un evento sin al menos un consumidor firmado es una **propuesta**, no un contrato.
- Cada equipo solo edita los ficheros de los eventos que **emite**. El resto se discute en el PR o en una Issue.

## Cómo proponer cambios mediante Pull Requests

Cualquier alta o modificación de contrato va por Pull Request. Usa la plantilla del repositorio.

- **Cambio compatible** (campo opcional nuevo, corrección de documentación): puede mantener la misma versión `@n` si no obliga a redeploy a nadie. Documentadlo igual.
- **Cambio incompatible** (renombrar campo, cambiar tipo, hacer obligatorio lo opcional, eliminar campo usado): **nueva versión** del evento (`@n+1`). La versión anterior permanece al menos dos semanas etiquetada como `deprecado` si aún hay consumidores.

Nadie fusiona un PR de contrato sin el visto bueno de los equipos afectados.

## Cómo registrar desacuerdos mediante Issues

Si en la negociación no hay acuerdo (nombre, tipos, obligatoriedad, semántica), abrid una **Issue** con la plantilla de conflicto entre equipos.

La Issue debe dejar claro:

- qué equipos intervienen,
- qué evento o cambio se discute,
- la posición de cada parte,
- qué decidís que haga falta del profesor (si hace falta).

El arbitraje del profesor, cuando exista, se escribe también en el fichero del evento.

## Por qué nadie debe modificar un contrato unilateralmente

Un contrato firmado es una dependencia entre equipos. Cambiarlo en silencio equivale a romper el build de integración de otra persona sin aviso.

- No editéis `eventos/` directamente en `main`.
- No “arregléis” un campo en vuestro código sin actualizar el contrato.
- No asumáis que un acuerdo verbal vale: **solo cuenta lo escrito y aprobado aquí**.

La disciplina de releases de la tienda (tags + manifest del shell) solo funciona si los contratos son estables y versionados.

## Contenido del repositorio

| Ruta | Uso |
| --- | --- |
| [`PLANTILLA-EVENTO.md`](PLANTILLA-EVENTO.md) | Modelo para cada contrato. |
| [`CONTRIBUYENDO.md`](CONTRIBUYENDO.md) | Cómo trabajar día a día. |
| [`eventos/`](eventos/) | Contratos aprobados o en PR (vacía al inicio). |
| [`.github/`](.github/) | Plantillas de Issue y Pull Request. |

## Referencias del bloque

- Shell de integración: [tienda-ucjc-shell](https://github.com/cesar-andress/tienda-ucjc-shell)
- Tienda en vivo (Pages): https://cesar-andress.github.io/tienda-ucjc-shell/
