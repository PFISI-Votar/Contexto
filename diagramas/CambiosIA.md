# Registro de cambios asistidos por IA — Diagramas

Bitácora de modificaciones a los diagramas de `diagramas/`. Cada entrada documenta tipo, motivo y archivo nuevo versionado, según la norma definida en `CLAUDE.md`.

---

## 2026-06-16 — Diagrama Entidad Relación - Sprint 1 - PFISI.mmd

- **Tipo de cambio**: extensión de `LISTA` y `CANDIDATO` para US-318 (CRUD pre-oficialización y mapeo Web3).
- **Motivo**: US-318 — Gestionar listas y candidatos. Se agrega `list_id` en `LISTA` (identificador congelado al oficializar) y `ficha_institucional` JSONB en `CANDIDATO` (legajo UTN, DNI, avales).
- **Archivo nuevo**: `Diagrama Entidad Relación - Sprint 2 - PFISI.mmd`

---

## 2026-06-11 — Diagrama Entidad Relación - Sprint 0 - PFISI.mmd

- **Tipo de cambio**: refinamiento semántico y estructural de `PADRON_VOTANTE`.
- **Motivo**: implementación de la User Story 330 ("Importar padrón por CSV"). La entidad pasa a almacenar exclusivamente el hash Keccak-256 del votante (`hash_hoja` = `votanteHash`) en cumplimiento de la Ley 25.326 (anonimización estructural). Se elimina la FK a `VOTANTE` para evitar cualquier vínculo persistente con identidad civil. Se agrega `generado_en` (auditoría), `UNIQUE(id_padron, hash_hoja)` (anti-duplicados) e índice sobre `hash_hoja` (lookup eficiente durante validación de sufragio).
- **Archivo nuevo**: `Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`
