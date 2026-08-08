# Registro de Cambios en Diagramas

Este archivo documenta todas las modificaciones realizadas a los diagramas de arquitectura del sistema VOTAR, siguiendo la norma establecida en `CLAUDE.md`.

---

## [2026-08-08] — Sprint 3 — VOTAR-329 estadísticas de re-voto en Dashboard

- **Tipo de cambio**: Implementación on-chain + API + UI de métricas de re-voto
- **Motivo**:
  - Cumplir criterio de aceptación: `AuditViewContract.getRevoteStats(id)` → `(totalRevotes, uniqueVoters, overwriteRatio)`
  - Exponer analíticas agregadas de sobreescritura en dashboard público sin autenticación
  - Actualizar documentación de contexto con stack real (NestJS, React 19) y estado de repos

- **Cambios específicos**:
  1. `VoteRegistry`: contador `_totalRevotes` incrementado en cada `isOverwrite=true`
  2. `AuditViewContract.getRevoteStats` delega a `VoteRegistry` (ratio WAD on-chain)
  3. Back: `GET /elecciones/:id/revoto-stats-publica` + curva temporal de sobreescritura
  4. Front: sección `/dashboard/revoto` con polling 4s (UAT-02)
  5. C4 Sprint 3: descripción actualizada de `AuditViewContract` y `VoteRegistry`
  6. Diagrama de clases: `StatsRevoto`, `getRevoteStats` en `RegistroVoto` y `VistaAuditoria`
  7. `contexto-sistema.md`: sección 18 con repos, rutas del dashboard y tickets recientes

- **User Stories relacionadas**: VOTAR-329

- **PRs**: blockchain #36, back #66, front #80

- **Archivos**: `Contexto/contexto-sistema.md`, `Contexto/diagramas/sprint-3/votar.c4`, `Contexto/diagramas/sprint-3/Diagrama de clases - Sprint 3 - PFISI.mmd`, `Contexto/diagramas/sprint-3/secuencia-revoto-stats-votar-329.mmd`

---

## [2026-07-17] — Sprint 3 — VOTAR-341 unicidad sin re-voto

- **Tipo de cambio**: Alineación on-chain de política de revoto (`RevoteDisabled`)
- **Motivo**:
  - Documentar `revoteEnabled` en `RegistroVoto` / `VoteRegistry`
  - Reflejar `enforceRevotePolicy` → `RevoteDisabled` en `ContratoBoleta` / `BallotContract`
  - Asentar deuda conocida: bandera inmutable por deploy (1 registry/comicio)

- **Cambios específicos**:
  1. Diagrama de clases: `RegistroVoto.revoteEnabled`, `ContratoBoleta.enforceRevotePolicy`
  2. Relación `ContratoBoleta ..> RegistroVoto` anotada con consulta `revoteEnabled`
  3. C4: `BallotContract` y `VoteRegistry` describen `RevoteDisabled` / política VOTAR-341
  4. Notas de clase actualizadas (VOTAR-341)

- **User Stories relacionadas**: VOTAR-341 (unicidad sin re-voto)

- **Archivos**: `Contexto/diagramas/sprint-3/Diagrama de clases - Sprint 3 - PFISI.mmd`, `Contexto/diagramas/sprint-3/votar.c4`

---

## [2026-07-13] — Sprint 3 (nueva carpeta) + VOTAR-350 / VOTAR-346

- **Tipo de cambio**: Versionado de sprint + alineación on-chain de auditoría pública
- **Motivo**:
  - Abrir `diagramas/sprint-3/` conforme a la norma (no editar in-place Sprint 2)
  - Documentar `AuditViewContract` y views de `VoteRegistry` implementadas en VOTAR-350
  - Alinear C4/`VoteRegistry` con el evento `VoteCast` de VOTAR-346

- **Cambios específicos**:
  1. Creada carpeta `diagramas/sprint-3/` (DER, clases, C4, secuencia de cierre heredada)
  2. C4: `AuditViewContract` con `getElectionState`, `getParticipationStats`, `getVotesByCandidate`, `verifyReceipt`
  3. C4: `VoteRegistry` con tallies + views; `BallotContract` delega `recordVote`
  4. Diagrama de clases: `RegistroVoto`, `VistaAuditoria`, `StatsParticipacion`
  5. Nueva secuencia `secuencia-consulta-auditoria-votar-350.mmd` (UAT-01..04)
  6. DER Sprint 3: sin cambio de esquema relacional (auditoría es on-chain)

- **User Stories relacionadas**: VOTAR-350 (views de auditoría), VOTAR-346 (VoteCast)

- **Archivos**: `Contexto/diagramas/sprint-3/*`

---

## [2026-07-13] — votar.c4 (Sprint 2) — VOTAR-314 Protección de identidad

- **Tipo de cambio**: Actualización de componente `jwtValidator` (HS256 → RS256/JWKS)
- **Motivo**:
  - Cerrar el “objetivo futuro JWKS” documentado en US-313
  - Reflejar validación de firma vía JWKS, claims `iss`/`aud`/`exp`, rechazo 401 + `auditLogger`
  - Documentar modos mutuamente excluyentes BFF interino vs SSO (`JWT_JWKS_URI`)

- **Cambios específicos**:
  1. Tecnología del componente: NestJS Passport JWT + JWKS (RS256)
  2. Descripción: Modo A (BFF firma + `/auth/.well-known/jwks.json`) vs Modo B (JWKS IdP)
  3. Relación `apiRouter → jwtValidator` y `jwtValidator → sso` actualizadas

- **User Stories relacionadas**: VOTAR-314 (protección de identidad), VOTAR-313 (login interino Autogestión)

- **Archivo modificado**: `Contexto/diagramas/sprint-2/votar.c4`

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
