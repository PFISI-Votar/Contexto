# Versionado y ramas

La documentación usa las mismas etiquetas semánticas que el código:
`vMAJOR.MINOR.PATCH`.

| Etiqueta | Fecha      | Hito                                                                 |
| -------- | ---------- | -------------------------------------------------------------------- |
| `v1.0.0` | 2026-07-28 | MVP: elección funcional extremo a extremo (Sprint 0 — Versión 1)     |
| `v2.0.0` | 2026-08-11 | Documentación y diagramas del Sprint 4 alineados al producto         |

## Ramas

| Rama   | Rol                                                                 |
| ------ | ------------------------------------------------------------------- |
| `main` | Producción / estable. Contiene `v2.0.0` y es la rama por defecto.   |
| `dev`  | Integración. Recibe los pull requests. Aún no es un release.        |

En los repositorios de código la rama estable se llama `master`. Acá se llama
`main`. En ambos casos es la rama por defecto de GitHub y la que ya contiene
`v2.0.0`.

No se vuelca todo `dev` sobre la rama estable: eso marcaría documentación sin
etiquetar como si fuera el release. El próximo corte es un merge a `main` y un
tag `v2.1.0` (o el número que corresponda), coordinado con front, back y
blockchain.

## Contratos

Las direcciones de Sepolia ligadas a `v2.0.0` están en
[blockchain/docs/VERSIONADO.md](https://github.com/PFISI-Votar/blockchain/blob/dev/docs/VERSIONADO.md).
Este repositorio no despliega contratos.
