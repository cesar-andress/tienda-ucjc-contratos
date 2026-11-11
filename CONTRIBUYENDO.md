# Cómo contribuir (alumnos)

Este documento resume el flujo sobre **tienda-ucjc-contratos**. Leed también el [`README.md`](README.md).

## Importante: no tenéis escritura en el original

El repositorio https://github.com/cesar-andress/tienda-ucjc-contratos es de **solo lectura** para los equipos.

- **No** hagáis `git clone` del original pensando que luego podréis hacer `git push`.
- Trabajad siempre sobre un **fork** (copia bajo vuestra cuenta) y abrid un **Pull Request** hacia el original.

## Conceptos en una frase

- **Original:** repo del profesor.
- **Fork:** vuestra copia.
- **Rama:** línea de trabajo en el fork (`contrato/...`).
- **Pull Request:** petición de integrar esa rama en `main` del original.
- **Revisión / confirmación:** los consumidores validan el texto.
- **Merge:** lo hace solo el profesor.

## Antes de tocar nada

1. Confirmad en el equipo qué eventos **emitís** y cuáles necesitáis consumir (lo negociado en papel).
2. Mirad en el original (pestaña *Code* → `eventos/`) si ya existe un fichero para el mismo nombre y versión.
3. Tened a mano la Hoja B firmada: las firmas de clase siguen valiendo.

No abráis el código de otro micro-frontend para “mirar cómo lo hacen”. Si falta un dato, se negocia aquí.

## Alta de un contrato nuevo (fork + PR)

1. En el original, pulsad **Fork**.
2. Clonad **vuestro fork**:
   ```bash
   git clone https://github.com/<vuestra-cuenta>/tienda-ucjc-contratos.git
   cd tienda-ucjc-contratos
   ```
3. Cread la rama:
   ```bash
   git checkout -b contrato/ucjc-<pieza>-<verbo>-<n>
   ```
4. Copiad `PLANTILLA-EVENTO.md` a `eventos/<nombre-del-evento>.md` (el nombre del fichero debe coincidir con el evento).
5. Rellenad **solo** lo que emite vuestro equipo. Estado inicial: `propuesto`.
6. Commit en español:
   ```bash
   git add eventos/
   git commit -m "Añade propuesta ucjc:<pieza>:<verbo>@<n>"
   git push -u origin contrato/ucjc-<pieza>-<verbo>-<n>
   ```
7. En GitHub: **Contribute → Open pull request** hacia `cesar-andress/tienda-ucjc-contratos` (`main`).
8. Completad la plantilla del PR (emisor, consumidores, checklist).
9. Pedid a cada responsable consumidor una confirmación en el PR, por ejemplo:  
   `Confirmo que el equipo Identidad acepta este contrato según lo acordado en clase.`
10. Cuando el texto esté alineado, el profesor podrá marcar el contrato como `firmado` e integrar.

## Modificación de un contrato existente

1. Decidid si el cambio es compatible o incompatible (README: contrato `@n` ≠ release `vX.Y.Z`).
2. Si es **incompatible**, proponed un fichero nuevo con `@n+1` y deprecad el anterior en el mismo PR (o en uno enlazado).
3. Si es compatible y mantenéis `@n`, documentad el cambio en el historial del fichero.
4. Siempre vía fork + PR; nunca edición directa del original.

## Desacuerdos

1. Abrid una **Issue** con la plantilla de conflicto (etiqueta `conflicto`).
2. Enlazad el PR o el fichero propuesto.
3. No implementéis “vuestra versión” del evento en el micro-frontend mientras el conflicto esté abierto.

## Qué no hacer

- No pedir ser colaborador con escritura en el repo del profesor para “ir más rápido”.
- No inventar eventos solo en el código.
- No cambiar tipos o nombres de campos sin PR.
- No borrar un contrato que otro equipo aún consume.
- No asumir que podéis fusionar el PR vosotros.
- No usar este repositorio para entregar el código de vuestra pieza.

## Commits y mensajes

Los mensajes de commit deben estar **en español**, ser claros y concretos. Ejemplos:

- `Añade propuesta ucjc:identidad:sesion@1`
- `Depreca ucjc:compra:vaciar@1 y propone @2`

En las firmas del fichero y en los comentarios del PR usad el **nombre del responsable** del equipo, reconocible en el aula.
