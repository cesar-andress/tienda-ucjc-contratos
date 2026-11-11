# Carpeta `eventos/`

Aquí viven los contratos **firmados** (un fichero Markdown por evento).

- Repositorio **público**. Si el fichero no está en esta carpeta de `main`, **no cuenta** para la tienda.
- Hoy (**11/11/2026**, tag del repo **`v0.2.0`**): los tres del flujo mínimo están **`firmado`**. El [ejemplo de formato](EJEMPLO-como-rellenar.md) sigue siendo solo plantilla (**no implementar**).
- Mapa del camino punta a punta: [`FLUJO-MINIMO.md`](FLUJO-MINIMO.md).
- No dejéis borradores en la **raíz** del repositorio.

## Contratos activos (`firmado`)

| Evento | Fichero |
| --- | --- |
| `ucjc:identidad:sesion-cambiada@1` | [`ucjc-identidad-sesion-cambiada@1.md`](ucjc-identidad-sesion-cambiada@1.md) |
| `ucjc:descubrimiento:anadir-al-carrito@1` | [`ucjc-descubrimiento-anadir-al-carrito@1.md`](ucjc-descubrimiento-anadir-al-carrito@1.md) |
| `ucjc:compra:pedido-confirmado@1` | [`ucjc-compra-pedido-confirmado@1.md`](ucjc-compra-pedido-confirmado@1.md) |

## Cómo proponer un contrato nuevo

1. Copiad [`../PLANTILLA-EVENTO.md`](../PLANTILLA-EVENTO.md).
2. Mirad el ejemplo: [`EJEMPLO-como-rellenar.md`](EJEMPLO-como-rellenar.md) (**no implementar**).
3. Guardad el fichero aquí, p. ej. `ucjc-descubrimiento-anadir-al-carrito@2.md`.
4. Abrid un Pull Request. El profesor fusiona a `main` cuando el estado sea `firmado`.
