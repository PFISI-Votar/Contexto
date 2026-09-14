# VOTAR — Contexto y documentación

Documentación del proyecto **VOTAR** (_Plataforma de Votación Electrónica con
Tecnología Blockchain_), Proyecto Final de Ingeniería en Sistemas de
Información, UTN FRVM. Equipo Five Stack.

Este repositorio no es una aplicación. No tiene dependencias de runtime ni
comando de compilación. El código está en los repositorios hermanos.

| Repositorio | Rol                                      | Estable |
| ----------- | ---------------------------------------- | ------- |
| [front](https://github.com/PFISI-Votar/front) | Panel, BUD y dashboard            | `master` |
| [back](https://github.com/PFISI-Votar/back)   | API NestJS                        | `master` |
| [blockchain](https://github.com/PFISI-Votar/blockchain) | Contratos Solidity / Sepolia | `master` |
| Contexto (este repo) | Alcance, charter, diagramas, lineamientos | `main` |

## Equipo

| Integrante                  | Legajo |
| --------------------------- | ------ |
| Liendo, Alejo               | 15074  |
| Lucarelli, Bruno            | 14988  |
| Magni, Gastón               | 14991  |
| Mosconi, Ignacio (director) | 15288  |
| Terreno, Valentino          | 15079  |

**Cátedra:** Proyecto Final ISI — Ing. Christian Villafañe, Ing. Matías Cassani

## Qué hay en este repositorio

| Ruta | Contenido |
| ---- | --------- |
| `md/` | Charter, alcance, ciclo de vida, interesados |
| `diagramas/` | Diagramas C4 y de secuencia |
| `contexto-sistema.md` | Síntesis técnica para consulta |
| `lineamientos-desarrollo.md` | Convenciones de implementación |
| `docs/VERSIONADO.md` | Tags `vMAJOR.MINOR.PATCH` y rama estable |

## Rama estable y versionado

La rama por defecto es `main` (estable, incluye el tag `v2.0.0`). La integración
es `dev`. Detalle en [docs/VERSIONADO.md](./docs/VERSIONADO.md).

Los tags publicados son `v1.0.0` (2026-07-28) y `v2.0.0` (2026-08-11).

## Cómo verificar este repositorio

No hay `npm install` ni build. Un auditor externo confirma que puede leer el
árbol:

```bash
git clone https://github.com/PFISI-Votar/Contexto.git
cd Contexto
git checkout main
```

Archivos regulatorios en la raíz: `LICENSE` (MIT), `README.md`,
`CONTRIBUTING.md`, `SECURITY.md`.

No hay dependencias de terceros que escanear. La verificación de licencias del
stack está en cada repositorio de código (`npm run licenses:check`).

## Licencia y colaboración

MIT. Ver [LICENSE](./LICENSE), [CONTRIBUTING.md](./CONTRIBUTING.md) y
[SECURITY.md](./SECURITY.md). No incluyas padrones reales ni credenciales en la
documentación.
