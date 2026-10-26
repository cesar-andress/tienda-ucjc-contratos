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
- su versión de contrato (`@n`),
- quién emite y quién consume,
- la descripción de cuándo se dispara,
- los campos del `detail`, con tipo y carácter obligatorio u opcional,
- un ejemplo de payload,
- quién lo aprobó,
- el estado del contrato (`propuesto`, `firmado`, `deprecado`).

Sin contrato firmado no hay integración fiable: un cambio de nombre o de tipo en un campo rompe a quien escucha, aunque el código de cada lado “funcione” por separado.

## Convención de nombres de eventos

Formato obligatorio:

```text
ucjc:<pieza>:<verbo>@<n>
```

- Minúsculas, en español, sin espacios.
- El sufijo `@n` es la **versión del contrato del evento**, no la versión `vX.Y.Z` del micro-frontend.
- Así pueden convivir dos versiones de contrato mientras los consumidores migran.

Ejemplo **ilustrativo** (no es un contrato definitivo; no lo copies a `eventos/` como si ya estuviera aprobado):

```text
ucjc:descubrimiento:añadir@1
```

### Versión del contrato (`@n`) frente a versión de la release (`vX.Y.Z`)

Son dos números distintos:

| Concepto | Ejemplo | Qué identifica |
| --- | --- | --- |
| **Contrato de evento** | `ucjc:identidad:sesion@1` → `@2` | Forma del mensaje entre piezas |
| **Release del micro-frontend** | `v0.1.0` → `v0.2.0` → `v1.0.0` | Artefacto publicado (`remote.js`) |

- Un cambio interno de UI puede ser un **parche** de release (`v0.1.0` → `v0.1.1`) **sin** tocar `@n`.
- Añadir un campo opcional que nadie obliga a usar puede ser **menor** en la release y, si los consumidores existentes siguen válidos, **mantener** `@n`.
- Renombrar un campo, cambiar su tipo o hacerlo obligatorio cuando ya hay consumidores suele exigir **`@n+1`** (nuevo contrato) y a menudo una release **mayor** o, como mínimo, una release nueva que emita o entienda esa versión.
- La compatibilidad la marcan los **consumidores existentes**, no el hecho aislado de “añadir” o “quitar” un campo.

No hay equivalencia automática entre `v1.0.0` y `@1`.

## Cómo se negocian los eventos

1. En aula se acuerdan en papel (emisor, consumidores y campos). Las firmas de las hojas siguen siendo válidas.
2. El equipo **emisor** transcribe lo acordado mediante un **fork + Pull Request** (véase abajo). No tenéis escritura directa en este repositorio.
3. El nombre del fichero refleja el del evento, por ejemplo `ucjc-descubrimiento-añadir@1.md`.
4. Los equipos **consumidores** confirman en el PR (revisión de GitHub si pueden, o comentario identificable).
5. El **profesor** comprueba el acuerdo e integra el PR cuando procede. Solo el profesor hace el *merge*.

Reglas:

- El **nombre** del evento lo propone quien emite; los **campos** se firman entre emisor y consumidores.
- Un evento sin al menos un consumidor confirmado es una **propuesta**, no un contrato.
- Cada equipo solo propone ficheros de los eventos que **emite**.

## Modelo de contribución: fork + Pull Request

**No podéis hacer `git push` al repositorio del profesor.** Trabajáis así:

| Concepto | Significado |
| --- | --- |
| **Repositorio original** | `cesar-andress/tienda-ucjc-contratos` (solo lectura para alumnos) |
| **Fork** | Copia del repo bajo **vuestra** cuenta de GitHub |
| **Rama de trabajo** | Rama en vuestro fork, p. ej. `contrato/ucjc-identidad-sesion-1` |
| **Pull Request (PR)** | Petición para integrar vuestra rama en `main` del original |
| **Revisión** | Comentarios y confirmaciones de los equipos afectados |
| **Merge** | Integración en `main`; la hace solo el profesor |

### Procedimiento paso a paso

1. Entrad en https://github.com/cesar-andress/tienda-ucjc-contratos
2. Pulsad **Fork** y cread la copia en vuestra cuenta (o en la organización del equipo).
3. Clonad **vuestro fork** (o editad en la web de GitHub).
4. Cread la rama `contrato/<nombre-del-evento>` (sin espacios).
5. Copiad [`PLANTILLA-EVENTO.md`](PLANTILLA-EVENTO.md) a `eventos/<nombre-del-evento>.md`.
6. Rellenad **solo** los contratos que emite vuestro equipo.
7. Haced un commit con mensaje **en español**.
8. Subid la rama a **vuestro fork** (`git push -u origin contrato/...`).
9. Abrid un Pull Request: base = `cesar-andress/tienda-ucjc-contratos` → `main`; compare = vuestra rama del fork.
10. En el PR indicad equipos consumidores y usad la plantilla.
11. Pedid a los responsables consumidores que confirmen (véase firmas).
12. Resolved comentarios y desacuerdos (o abrid una Issue `conflicto`).
13. Esperad a que el profesor apruebe e integre.

Guía operativa ampliada: [`CONTRIBUYENDO.md`](CONTRIBUYENDO.md).

### Ejemplo ilustrativo (no es un contrato aprobado)

Supongamos que Identidad acordó en papel un evento de sesión:

1. Fork de `tienda-ucjc-contratos` a la cuenta del responsable.
2. Rama `contrato/ucjc-identidad-sesion-1`.
3. Fichero propuesto: `eventos/ucjc-identidad-sesion@1.md` (rellenado desde la plantilla).
4. Commit: `Añade propuesta ucjc:identidad:sesion@1`.
5. PR hacia `cesar-andress/tienda-ucjc-contratos` (`main`).
6. Compra y Datos dejan en el PR: *«Confirmo que el equipo Compra acepta este contrato según lo acordado en clase»* (o el equivalente para Datos).
7. El profesor revisa e integra si el acuerdo es coherente.

Ese ejemplo **no** autoriza a copiar el evento a `eventos/` como si ya estuviera firmado en `main`.

## Firmas y confirmaciones

- Las **firmas en papel** de la negociación en aula siguen siendo válidas.
- Además, el responsable de cada equipo **consumidor** debe dejar confirmación **explícita** en el Pull Request:
  - una revisión de GitHub, si sus permisos lo permiten, **o**
  - un comentario identificable, por ejemplo:  
    `Confirmo que el equipo Compra acepta este contrato según lo acordado en clase.`
- La confirmación académica (papel + comentario/revisión) y el botón “Approve” de GitHub **no son lo mismo**. El profesor comprueba el acuerdo real antes de fusionar.
- **Solo el profesor** decide cuándo se hace el *merge*.

## Cambios compatibles e incompatibles

Cualquier alta o modificación de contrato va por fork + PR.

- **Cambio compatible** (p. ej. campo opcional nuevo que no rompe a quien ya consume): puede mantener `@n` si los consumidores existentes siguen siendo válidos. Documentadlo.
- **Cambio incompatible** (renombrar campo, cambiar tipo, hacer obligatorio lo opcional, eliminar campo usado): **nueva versión** `@n+1`. La anterior queda `deprecado` al menos dos semanas si aún hay consumidores.

Etiquetas útiles en Issues: `mayor`, `menor`, `parche`, `conflicto` (véase plantillas).

## Cómo registrar desacuerdos mediante Issues

Si no hay acuerdo, abrid una **Issue** con la plantilla de conflicto entre equipos (etiqueta `conflicto`).

Dejad claro: equipos, evento, posiciones y si pedís arbitraje del profesor.

## Por qué nadie debe modificar un contrato unilateralmente

Un contrato firmado es una dependencia entre equipos.

- No editéis `eventos/` en el original (no tenéis push).
- No “arregléis” un campo en vuestro código sin actualizar el contrato vía PR.
- No asumáis que un acuerdo verbal vale: **solo cuenta lo escrito y aprobado aquí**.

## Contenido del repositorio

| Ruta | Uso |
| --- | --- |
| [`PLANTILLA-EVENTO.md`](PLANTILLA-EVENTO.md) | Modelo para cada contrato. |
| [`CONTRIBUYENDO.md`](CONTRIBUYENDO.md) | Flujo día a día (fork + PR). |
| [`eventos/`](eventos/) | Contratos aprobados (vacía al inicio). |
| [`.github/`](.github/) | Plantillas de Issue y Pull Request. |

## Referencias del bloque

- Shell de integración: [tienda-ucjc-shell](https://github.com/cesar-andress/tienda-ucjc-shell)
- Tienda en vivo (Pages): https://cesar-andress.github.io/tienda-ucjc-shell/
