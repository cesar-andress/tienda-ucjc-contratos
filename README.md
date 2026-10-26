# tienda-ucjc-contratos

Event contracts between the four pieces of the **UCJC Store**. Negotiation happens here; each piece repository only implements what was signed.

## Negotiation rules

1. One file per event under `eventos/`, named after the event (`ucjc-compra-confirmar@1.md`). Start from [`PLANTILLA-EVENTO.md`](PLANTILLA-EVENTO.md).
2. **The emitting team chooses the event name; emitter and consumers jointly sign the fields.** An event with no signed consumer is a proposal, not a contract.
3. Changes are opened as issues labelled `mayor`, `menor`, or `parche`, depending on whether another team must redeploy. A **major** change publishes a new event version (`@2`); the previous version stays alive for at least two weeks.
4. Each team may only edit files for events it emits. Everything else goes through an issue or a PR comment.
5. The lecturer arbitrates only when asked; the arbitration is written into the event file.
6. If it is not written in this repository, it does not exist. No globals, no cross-team imports, no verbal agreements.

## Naming convention

`ucjc:<pieza>:<verbo>@<n>` — lowercase, Spanish, no spaces.

Examples: `ucjc:descubrimiento:añadir@1`, `ucjc:identidad:sesion@1`, `ucjc:compra:confirmar@1`, `ucjc:datos:pedido-guardado@1`.

The version sits in the **name**, not inside `detail`, so two versions can coexist and each consumer can listen to the one it understands.

## Contract v0 (Mon 26 Oct)

Classroom board photo of the signed agreements: `contrato-v0-aula.jpg` (uploaded after the session). Teams transcribe it into `eventos/` with one PR per team before Wed 28 Oct.

## Open conflicts

See issues labelled `conflicto`.
