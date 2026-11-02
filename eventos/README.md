# Contratos de eventos

Cada fichero de esta carpeta es **un** contrato versionado.

## Nombre

```text
ucjc:<pieza>:<verbo>@<n>
```

El fichero se llama igual, con guiones en lugar de dos puntos, por ejemplo:

`ucjc:compra:pedido-confirmado@1` → `ucjc-compra-pedido-confirmado@1.md`

## Estados

| Estado | Significado |
| --- | --- |
| `propuesto` | Texto en negociación. Aún no es la referencia obligatoria de implementación. |
| `firmado` | Emisor y consumidores han confirmado; el profesor lo ha integrado en `main`. |
| `deprecado` | Sustituido por `@n+1`; se mantiene un tiempo por compatibilidad. |

## Cómo se da el OK

En el Pull Request correspondiente, el responsable de cada equipo afectado deja un comentario explícito (ver plantilla del PR). Las firmas de la Hoja B de aula siguen valiendo como evidencia académica, pero **también** hace falta la confirmación en el PR.

## Flujo mínimo

Con estos tres eventos basta un camino completo (login → añadir → confirmar → ver pedidos).  
Detalle y checklist por equipo para las PRs de código: [`FLUJO-MINIMO.md`](FLUJO-MINIMO.md).

## Contratos en este árbol

| Evento | Emisor | Consumidores | Estado |
| --- | --- | --- | --- |
| [`ucjc:identidad:sesion-cambiada@1`](ucjc-identidad-sesion-cambiada@1.md) | Identidad | Datos A/B, Compra | propuesto |
| [`ucjc:descubrimiento:anadir-al-carrito@1`](ucjc-descubrimiento-anadir-al-carrito@1.md) | Descubrimiento | Compra | propuesto |
| [`ucjc:compra:pedido-confirmado@1`](ucjc-compra-pedido-confirmado@1.md) | Compra | Datos A/B | propuesto |
