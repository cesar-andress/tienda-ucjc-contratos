# Flujo mínimo (v0.2) — tres eventos

Con **solo** estos tres contratos `firmado` la tienda ya tiene un camino de punta a punta:

```text
1. Identidad  →  emite  ucjc:identidad:sesion-cambiada@1
                 (login demo / estado al cargar)

2. Descubrimiento  →  emite  ucjc:descubrimiento:anadir-al-carrito@1
                      (botón «añadir» en catálogo / ficha)

3. Compra  →  escucha (2) y (1); guarda carrito + usuarioId
           →  emite  ucjc:compra:pedido-confirmado@1
              (botón «confirmar pedido»; exige sesión)

4. Datos (A o B)  →  escucha (1) y (3)
                  →  filtra «Mis pedidos» por usuario.id
                  →  vacía la vista si autenticado === false
```

Nada más entra en el paquete `@1`. Listados de usuarios, stock inverso Compra→Descubrimiento, `pedido-guardado`, etc. quedan **fuera**.

## Quién hace qué

| Equipo | Emite | Escucha | Checklist mínima |
| --- | --- | --- | --- |
| **Identidad** | `sesion-cambiada@1` al login, logout y al `connectedCallback` | — | `detail` con `autenticado` + `usuario`/`null` (`id`, `email`) |
| **Descubrimiento** | `anadir-al-carrito@1` al añadir | — | `productoId`, `nombre`, `precio`, `cantidad` |
| **Compra** | `pedido-confirmado@1` al checkout | `anadir-al-carrito@1`, `sesion-cambiada@1` | Generar `pedidoId` + `creadoEn` + `lineas` + `total`; sin sesión → no confirmar |
| **Datos A / B** | — (en `@1`) | `pedido-confirmado@1`, `sesion-cambiada@1` | CE **`ucjc-pedidos`**; persistir y pintar por `usuarioId` / `usuario.id` |

Además, para entrar en el shell: `remote.js` + `export default` + Pages HTTPS (ver contrato de carga del shell). Eso es **release**, no contrato.

## Estado (11/11/2026) · tag `v0.2.0`

1. Los tres ficheros están en `eventos/` de `main` con estado **`firmado`** (tag del repo de contratos: **`v0.2.0`**).
2. Varios equipos ya publicaron `remote.js` HTTPS alineados a estos nombres.
3. El shell (`v0.2.0`) enchufa las URLs activas en su `manifest.json` (ver README del shell).
