# Registro de Cambios en Diagramas

Este archivo documenta todas las modificaciones realizadas a los diagramas de arquitectura del sistema VOTAR, siguiendo la norma establecida en `CLAUDE.md`.

---

## [2026-07-13] — Diagrama Entidad Relación - Sprint 2 - PFISI.mmd

- **Tipo de cambio**: Corrección de modelo de recibo (alineado a VOTAR-379 + VOTAR-360)
- **Motivo**:
  - No reintroducir `VOTO_CONFIRMACION` (eliminada en VOTAR-379: desvinculación identidad↔voto)
  - Documentar verificación pública por `TransactionHash` on-chain (`SignedVoteCast`)
  - Documentar recibo PDF como artefacto **client-side** con `FirmaDigital` del sistema, sin persistencia en BD

- **Cambios específicos**:
  1. Eliminada entidad `VOTO_CONFIRMACION` del DER Sprint 2
  2. Modeladas entidades aspiracionales `TRANSACCION_BLOCKCHAIN` y `RECIBO_VOTACION` (no TypeORM): clave = `hash_transaccion`
  3. Relación `TRANSACCION_BLOCKCHAIN ||--|| RECIBO_VOTACION` (PDF local materializa la evidencia on-chain)
  4. Anotado: portal `GET /recibos/verificar/:txHash` + `POST /recibos/firmar` sin almacenar PDF

- **User Stories relacionadas**: VOTAR-360 (recibo criptográfico), VOTAR-379 (voto anónimo)

- **Archivo modificado**: `Contexto/diagramas/sprint-2/Diagrama Entidad Relación - Sprint 2 - PFISI.mmd`

---
