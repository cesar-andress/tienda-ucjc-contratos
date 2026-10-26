# `ucjc:<pieza>:<verbo>@1`

| | |
| --- | --- |
| **Emits** | &lt;piece&gt; |
| **Consumes** | &lt;piece&gt;, &lt;piece&gt; |
| **Status** | proposed · signed · deprecated |
| **Since** | v0.x.0 of the emitting piece |

## When it is emitted

One sentence: which user action or internal fact triggers it.

## `detail`

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | text | yes | |
| `precio` | number (EUR, 2 decimals) | yes | |
| `rol` | `"alumno"` \| `"personal"` | no | |

## Example

```json
{ "id": "sud-01", "precio": 24.9 }
```

## What the consumer does if it never arrives

One sentence per consumer: degraded mode.

## Signatures

| Team | Responsible | Date |
| --- | --- | --- |
| &lt;emitter&gt; | | |
| &lt;consumer&gt; | | |

## History

- 26/10 — classroom contract v0.
