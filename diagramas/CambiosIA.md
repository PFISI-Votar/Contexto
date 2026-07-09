# Bitácora de cambios en diagramas (IA)

Registro de modificaciones a diagramas del proyecto VOTAR, según `lineamientos-desarrollo.md` §6.

---

## [2026-07-07] — Diagrama de clases / C4 Sprint 2 (VOTAR-339)

- **Tipo de cambio**: Agregado `ContratoBoleta` (BallotContract) con validación Merkle on-chain; actualizada descripción de `BallotContract.sol` en C4 y flujo `sufragio_flow` con error `InvalidMerkleProof`.
- **Motivo**: VOTAR-339 — Validación criptográfica de electores en la Blockchain.
- **Archivos modificados**:
  - `diagramas/sprint-2/Diagrama de clases - Sprint 2 - PFISI.mmd`
  - `diagramas/sprint-2/votar.c4`
  - `contexto-sistema.md`
