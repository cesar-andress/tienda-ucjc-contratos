# Cómo contribuir (alumnos)

Este documento resume el flujo de trabajo sobre **tienda-ucjc-contratos**. Leed también el [`README.md`](README.md).

## Antes de tocar nada

1. Clonad o actualizad este repositorio (`git pull` en `main`).
2. Confirmad con vuestro equipo qué eventos emitís y cuáles necesitáis consumir.
3. Comprobad que en `eventos/` no exista ya un fichero para el mismo nombre y versión.

No abráis el código de otro micro-frontend para “mirar cómo lo hacen”. Si falta un dato, se negocia aquí.

## Alta de un contrato nuevo

1. Copiad [`PLANTILLA-EVENTO.md`](PLANTILLA-EVENTO.md) a `eventos/<nombre-del-evento>.md`.
2. Rellenad todos los campos. Dejad el estado en `propuesto` hasta que firmen los consumidores.
3. Abrid una rama, por ejemplo `contrato/ucjc-compra-confirmar-1`.
4. Abrid un **Pull Request** con la plantilla del repositorio.
5. Pedid revisión explícita a los responsables de los equipos consumidores.
6. Cuando esté `firmado` y revisado, el PR puede fusionarse a `main`.

## Modificación de un contrato existente

1. Decidid si el cambio es compatible o incompatible (ver README).
2. Si es **incompatible**, cread un fichero nuevo con `@n+1` y marcad el anterior como `deprecado` (en el mismo PR o en uno enlazado).
3. Si es compatible y manteneis `@n`, documentad el cambio en el historial del fichero.
4. Nunca editéis `main` a mano: siempre PR.

## Desacuerdos

Si no hay consenso:

1. Abrid una **Issue** con la plantilla de conflicto entre equipos.
2. Enlazad el PR o el fichero de `eventos/` si existe.
3. No implementéis “vuestra versión” del evento en el micro-frontend mientras el conflicto esté abierto.

## Qué no hacer

- No inventar eventos solo en el código.
- No cambiar tipos o nombres de campos sin PR.
- No borrar un contrato que otro equipo aún consume.
- No fusionar un PR sin el visto bueno de los afectados.
- No usar este repositorio para entregar el código de vuestra pieza (eso va en el repo de vuestro equipo).

## Commits y mensajes

Mensajes claros y en español o inglés, pero concretos. Ejemplos:

- `Añade propuesta ucjc:identidad:sesion@1`
- `Depreca ucjc:compra:vaciar@1 y propone @2`

Firmad los contratos con el **nombre del responsable** del equipo, no con un nick anónimo sin identificar en el aula.
