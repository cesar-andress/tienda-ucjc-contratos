## Tipo de cambio

- [ ] Alta de contrato nuevo
- [ ] Modificación compatible (misma versión de contrato `@n`)
- [ ] Cambio incompatible (nueva versión `@n+1` + deprecación de la anterior)
- [ ] Corrección editorial / tipografía / aclaración sin cambiar semántica

## Origen del PR

- [ ] Este PR parte de un **fork** (flujo obligatorio; no tenemos push al original)
- Cuenta / organización del fork:
- Rama de trabajo:

## Evento

- Nombre: `ucjc:<pieza>:<verbo>@<n>`
- Equipo **emisor**:
- Equipos **consumidores** (lista completa):

## Confirmaciones de consumidores

Cada responsable consumidor debe dejar en este PR una revisión o un comentario del tipo:

`Confirmo que el equipo <nombre> acepta este contrato según lo acordado en clase.`

- [ ] Consumidor 1 ha confirmado
- [ ] Consumidor 2 ha confirmado (si aplica)
- [ ] Hay firma en papel de la negociación de aula (Hoja B)

## Resumen

Qué se propone y por qué hace falta para la Tienda UCJC.

## Ficheros

- Ruta en `eventos/`:
- ¿Se depreca algún contrato anterior? (ruta):

## Compatibilidad (contrato `@n` ≠ release `vX.Y.Z`)

- [ ] No obliga a adaptar a consumidores existentes
- [ ] Obliga a adaptar consumidores / redeploy (explicar abajo)

## Checklist

- [ ] Partimos de `PLANTILLA-EVENTO.md` y están todos los campos
- [ ] El ejemplo de payload coincide con la tabla de campos
- [ ] El estado del contrato es coherente (`propuesto` / `firmado` / `deprecado`)
- [ ] Solo se proponen eventos que **emite** nuestro equipo
- [ ] No se ha tocado código de ningún micro-frontend en este PR

## Issues relacionadas

Closes #
