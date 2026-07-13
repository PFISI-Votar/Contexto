# Registro de Cambios en Diagramas

Este archivo documenta todas las modificaciones realizadas a los diagramas de arquitectura del sistema VOTAR, siguiendo la norma establecida en `CLAUDE.md`.

---

## [2026-07-12] — Diagrama Entidad Relación - Sprint 2 - PFISI.mmd

- **Tipo de cambio**: Actualización de entidad existente + eliminación de constraint
- **Motivo**:
  - Reintroducir entidad `VOTO_CONFIRMACION` que fue marcada como eliminada (VOTAR-379) pero existe en el código actual
  - Eliminar constraint `@Unique(['idEleccion', 'votanteHash'])` para permitir re-voto (política `LAST_VOTE_WINS`)
  - Unificar `TRANSACCION_BLOCKCHAIN` y `RECIBO_VOTACION` en una sola entidad `VOTO_CONFIRMACION` (VOTAR-360)
  - Soportar verificación E2E con UUID auto-generado por TypeORM

- **Cambios específicos**:
  1. Agregada entidad `VOTO_CONFIRMACION` con todos los campos de la migración `1782160000000-VotoConfirmacion.ts` + campos blockchain de `1782600000000-AddReciboBlockchainFields.ts`
  2. Eliminado constraint único `(id_eleccion, votante_hash)` - ahora permite múltiples votos del mismo votante por elección
  3. Mantenido constraint único `(id_eleccion, idempotency_key)` para anti-replay via nullifier
  4. Agregado campo `codigo_verificacion_e2e` (UUID) auto-generado para verificación pública
  5. Documentado que `TRANSACCION_BLOCKCHAIN` y `RECIBO_VOTACION` fueron unificadas en `VOTO_CONFIRMACION`
  6. Agregada relación `ELECCION ||--o{ VOTO_CONFIRMACION` (1:N - permite múltiples confirmaciones)

- **Migración asociada**: `1783903956193-migration.ts`
  - Elimina `UQ_voto_confirmacion_eleccion_votante`
  - Mantiene `UQ_voto_confirmacion_eleccion_idempotency`

- **User Stories relacionadas**: VOTAR-360 (Generación y verificación de recibo criptográfico)

- **Archivo modificado**: `Contexto/diagramas/sprint-2/Diagrama Entidad Relación - Sprint 2 - PFISI.mmd`

---
