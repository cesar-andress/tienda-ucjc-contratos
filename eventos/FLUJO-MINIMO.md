# Flujo mínimo (v0.2) — tres eventos

Con **solo** los tres contratos de este PR la tienda ya tiene un camino de punta a punta:

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

## Quién hace qué en el código (base de las PRs a cada repo)

| Equipo | Emite | Escucha | Checklist mínima de implementación |
| --- | --- | --- | --- |
| **Identidad** | `sesion-cambiada@1` al login, logout y al `connectedCallback` | — | `detail` con `autenticado` + `usuario`/`null` (`id`, `email`); nombre exacto del evento |
| **Descubrimiento** | `anadir-al-carrito@1` al añadir | — | Sustituir `ucjc:cart:add-item` (u otros) por el canónico; `productoId`, `nombre`, `precio`, `cantidad` |
| **Compra** | `pedido-confirmado@1` al checkout | `anadir-al-carrito@1`, `sesion-cambiada@1` | Carrito local; `usuarioId` = `usuario.id`; generar `pedidoId` + `creadoEn` + `lineas` + `total`; sin sesión → no confirmar |
| **Datos A / B** | — (en `@1`) | `pedido-confirmado@1`, `sesion-cambiada@1` | CE **`ucjc-pedidos`**; dejar de escuchar nombres viejos (`pedido-creado`, `usuarios-listados`, …); persistir y pintar por `usuarioId` / `usuario.id` |

Además, para entrar en el shell: `remote.js` + `export default` + Pages HTTPS (ver contrato de carga del shell). Eso es **release**, no contrato.

## Cómo se usa este documento

1. Los equipos dan **OK** en el [PR #2](https://github.com/cesar-andress/tienda-ucjc-contratos/pull/2).
2. El profesor marca `firmado` y fusiona.
3. Cada equipo recibe (o abre) una PR de código alineada con la fila de la tabla.
4. Cuando haya `remote.js` HTTPS, el profesor mueve **una** entrada del `manifest.json` del shell.

## Demo en el shell (rellenos del profesor)

Mientras no haya releases de alumno, los rellenos del shell pueden simular este mismo flujo con botones de prueba. Sirve para ver en clase que el bus **ya** funciona con estos tres nombres. No sustituye el trabajo de los equipos.
