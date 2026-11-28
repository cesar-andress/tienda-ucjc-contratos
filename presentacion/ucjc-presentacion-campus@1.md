# Contrato: `ucjc-presentacion-campus@1`

## Nombre

```text
ucjc-presentacion-campus@1
```

No es un evento del bus. Es el contrato de estilo y script comunes que impone el shell. Desde que se firma, la tienda tiene un solo criterio de CSS y de JS.

## Versión

| Campo | Valor |
| --- | --- |
| Versión del contrato | `1` |
| ¿Sustituye a una versión anterior? | no |
| Shell mínimo | tag `v0.3.10` (sirve `comun/campus.css` y `comun/campus.js` con `adoptar`) |

## Quién lo impone

El profesor, desde el shell. Ficheros:

- `comun/campus.css`: variables `--ucjc-*` en `:root` y clases `.ucjc-btn`, `.ucjc-btn-primary`, `.ucjc-label`, `.ucjc-title`.
- `comun/campus.js`: `window.ucjcCampus` con la API de abajo.

En la tienda en vivo:

- https://cesar-andress.github.io/tienda-ucjc-shell/comun/campus.css
- https://cesar-andress.github.io/tienda-ucjc-shell/comun/campus.js

El shell carga los dos ficheros **antes** que cualquier `remote.js`.

## API de `window.ucjcCampus`

| Método / campo | Qué hace |
| --- | --- |
| `version` | Cadena `'1'`. Comprobad `=== '1'` al arrancar. |
| `emitir(nombre, detail)` | Emite `CustomEvent` en `window`. El nombre debe empezar por `ucjc:`. |
| `escuchar(nombre, manejador)` | Escucha en `window`. Devuelve una función que deja de escuchar; llamadla en `disconnectedCallback`. |
| `leerTokens()` | Lee las variables `--ucjc-*` ya calculadas (útil si pintáis desde JS). |
| `adoptar(shadowRoot)` | Entrega `campus.css` a la sombra (`adoptedStyleSheets`) para que las clases `.ucjc-*` funcionen dentro, también después de repintar con `innerHTML`. |

## Quién firma

Cada variante enchufada en la tienda, por medio del responsable del repo que la publica. La firma obliga al hueco: cualquier variante que quiera ocupar `identidad`, `descubrimiento`, `compra` o `datos` tiene que cumplir este contrato, la haya hecho el equipo de esa pieza o otro.

## Entrada en vigor

| Fecha | Qué ocurre |
| --- | --- |
| Miércoles 25/11/2026 | Propuesta del profesor. Se discute en aula. |
| Viernes 27/11/2026 | Demo de Black Friday con lo firmado; se mira también el aspecto. |
| Lunes 30/11/2026 | Firma en aula. Cada variante trae una release con color y tipografía en variables. Defensa oral de cada grupo (8 minutos). |
| Miércoles 2/12/2026 | Toda release nueva cumple el contrato completo. |
| Miércoles 9/12/2026 | El shell solo enchufa variantes conformes. Las demás pasan al relleno. |

## Variables disponibles

| Variable | Uso | Reserva típica |
| --- | --- | --- |
| `--ucjc-ink` | texto principal | `#1a242c` |
| `--ucjc-muted` | texto secundario | `#5a6a76` |
| `--ucjc-fog` | fondo de página | `#f3f6f4` |
| `--ucjc-mist` | fondo suave, separadores | `#e6ece8` |
| `--ucjc-panel` | superficie y texto sobre la marca | `#fbfcfb` |
| `--ucjc-edge` | bordes | (derivado de la marca) |
| `--ucjc-brand` | color de marca | `#0b3d4a` |
| `--ucjc-brand-bright` | marca en acciones y estados activos | `#146b7a` |
| `--ucjc-leaf` | éxito | `#2f6f4e` |
| `--ucjc-warn` | aviso y error | `#8a3a3a` |
| `--ucjc-font-sans` | texto (Figtree) | `"Segoe UI", sans-serif` |
| `--ucjc-font-display` | títulos (Fraunces) | `Georgia, serif` |
| `--ucjc-radius` | radio de esquinas | `6px` |
| `--ucjc-space` | espaciado corto | `0.75rem` |
| `--ucjc-space-lg` | espaciado largo | `1.25rem` |
| `--ucjc-max` | ancho máximo de layout | `72rem` |
| `--ucjc-ease` | curva de animación | — |
| `--ucjc-presentacion` | versión del contrato de presentación | `"1"` |

Si falta una variable que necesitáis, se pide por PR a este contrato. No se inventa en la pieza.

## Qué obliga

### CSS

1. Solo se pinta vuestro custom element. Nada en `html`, `body` ni en los huecos de otras piezas.
2. Color, tipografía, radios y espaciados salen de las variables `--ucjc-*`, siempre con valor de reserva: `var(--ucjc-brand, #0b3d4a)`. Un color escrito a mano solo puede aparecer como valor de reserva.
3. Tipografía: `--ucjc-font-sans` y `--ucjc-font-display`. Ni `@font-face`, ni `<link>` de fuentes, ni `font-family` propia.
4. Ningún `!important`.

### JS

5. Solo se emiten eventos firmados en `eventos/`, con `window.dispatchEvent` o con `ucjcCampus.emitir` (mismo efecto).
6. Lo que se escucha se deja de escuchar: el listener que se pone en `window` al montar la pieza se quita en `disconnectedCallback`. `ucjcCampus.escuchar` devuelve la función que lo quita.
7. Al arrancar se comprueba `window.ucjcCampus?.version === '1'`. Si no está (por ejemplo, en la página de demo del repo, fuera de la tienda), la pieza sigue funcionando con los valores de reserva y `window.dispatchEvent`.
8. Hay al menos un test que comprueba el `detail` de cada evento que la pieza emite.

### Nota técnica sobre las clases

Las variables `--ucjc-*` se heredan y atraviesan el Shadow DOM: con ellas basta para unificar color, tipografía, radios y espacios.

Las clases `.ucjc-*` no atraviesan el Shadow DOM. Si queréis usar `.ucjc-btn`, `.ucjc-label` o `.ucjc-title` dentro de la pieza, llamad una vez a `ucjcCampus.adoptar(this.shadowRoot)` al montar (por ejemplo en `connectedCallback`). La hoja de campus se entrega con `adoptedStyleSheets`: no es un nodo de vuestro árbol, así que sigue ahí aunque repintéis con `this.shadowRoot.innerHTML = ...`. Es asíncrono: las clases se aplican en cuanto la hoja termina de cargar. Sin `adoptar()`, las clases no pintan nada dentro del Shadow DOM.

## Qué no obliga

- El diseño interno de la pieza (rejillas, modales, animaciones).
- Usar las clases `.ucjc-*` (opcionales; si las usáis, con `adoptar()`).
- Usar Shadow DOM (recomendado; hoy lo usan las diez variantes).
- Campos nuevos en eventos: eso va en los contratos de `eventos/`.

## Cómo se comprueba

- Se mira la release del tag que enchufa el shell, no la rama `main`.
- DevTools sobre la pieza dentro de la tienda: se elige un color al azar y se mira si sale de una variable `--ucjc-*` o está escrito a mano.
- Consola filtrada por `[evento ucjc]`: cada evento emitido tiene nombre firmado.
- Si una regla no se cumple, la variante no es conforme.

## Ejemplo mínimo

```css
:host {
  display: block;
  color: var(--ucjc-ink, #1a242c);
  font-family: var(--ucjc-font-sans, "Segoe UI", sans-serif);
}
button.comprar {
  background: var(--ucjc-brand, #0b3d4a);
  color: var(--ucjc-panel, #fbfcfb);
  border-radius: var(--ucjc-radius, 6px);
  padding: var(--ucjc-space, 0.75rem);
}
```

```js
const EV_CAMPANA = 'ucjc:descubrimiento:campana-cambiada@1';

class UcjcCompra extends HTMLElement {
  #quitar = null;

  connectedCallback() {
    if (!this.shadowRoot) this.attachShadow({ mode: 'open' });
    if (window.ucjcCampus?.version !== '1') console.warn('[compra] sin campus');
    // Solo si usáis .ucjc-btn / .ucjc-label / .ucjc-title:
    window.ucjcCampus?.adoptar?.(this.shadowRoot);

    const alCambiar = (e) => this.#pintarCampana(e.detail);
    this.#quitar = window.ucjcCampus
      ? window.ucjcCampus.escuchar(EV_CAMPANA, alCambiar)
      : (window.addEventListener(EV_CAMPANA, alCambiar),
         () => window.removeEventListener(EV_CAMPANA, alCambiar));
  }

  disconnectedCallback() {
    this.#quitar?.();
  }

  #pintarCampana(detail) { /* ... */ }
}
```

## Responsables que aprueban

Una fila por variante. La release es el tag que demuestra la conformidad.

| Variante | Repo | Responsable | Release conforme | Fecha | Firma / visto bueno |
| --- | --- | --- | --- | --- | --- |
| Identidad A | `ucjc-ecommerce-identidad/tienda-ucjc-identidad` | | | | |
| Identidad B | `Juampee/ucjc-identidad-plus` | | | | |
| Descubrimiento A | `dani84mol/tienda-ucjc-descubrimiento` | | | | |
| Descubrimiento B | `tienda-ucjc-compra/tienda-ucjc-descubrimiento-B` | `Adrián Pingarrón`| `v0.2.1`| `2026-11-25`| Ok + nuevo release|
| Descubrimiento C | `Juampee/descubrimiento-muy-mejorado` | | | | |
| Compra A | `tienda-ucjc-compra/tienda-ucjc-compra` | `Adrián Pingarrón`| `v.0.3.1`| `2026-11-25`| Ok + Nuevo release|
| Compra B | `ucjc-ecommerce-identidad/tienda-ucjc-compra-b` | | | | |
| Compra C | `dani84mol/tienda-ucjc-compra` | | | | |
| Datos A | `hansjeffas/tienda-ucjc-datos` | | | | |
| Datos B | `Juampee/ucjc-datos-alt2` | | | | |

## Estado del contrato

- [ ] `propuesto`
- [x] `firmado`
- [ ] `deprecado`

## Historial

- `2026-11-25` — Propuesta del profesor: estilo y script comunes desde el shell; firma por variante.
- `2026-11-25` — API en español (`emitir` / `escuchar` / `leerTokens` / `adoptar`).
- `2026-11-25` — Fechas de entrada en vigor, valores de reserva, sin `!important`, listeners que se quitan, un test por evento emitido.
- `2026-11-25` — Tabla de variables con reserva típica; API documentada; shell mínimo `v0.3.10`.
- `2026-11-25` — `adoptar()` con `adoptedStyleSheets`: la hoja sobrevive a los repintados con `innerHTML`; `leerTokens().presentacion` devuelve `1` sin comillas.
- 2026-11-25` — Firma Compra A y Descubrimiento B