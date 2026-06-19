# Registro de cambios asistidos por IA — Diagramas

Bitácora de modificaciones a los diagramas de `diagramas/`. Cada entrada documenta tipo, motivo y archivo nuevo versionado, según la norma definida en `CLAUDE.md`.

Estructura actual:

```
diagramas/
├── CambiosIA.md
├── sprint-0/
│   ├── Diagrama Entidad Relación - Sprint 0 - PFISI.mmd
│   ├── Diagrama de clases - Sprint 0 - PFISI(1).mmd
│   └── votar.c4
└── sprint-1/
    ├── Diagrama Entidad Relación - Sprint 1 - PFISI.mmd
    ├── Diagrama de clases - Sprint 1 - PFISI.mmd
    └── votar.c4
```

---

## 2026-06-19 — Reorganización por carpetas de sprint (incl. votar.c4)

- **Tipo de cambio**: reestructuración de directorios; `votar.c4` versionado por sprint.
- **Motivo**: agrupar todos los artefactos por sprint (`sprint-0/`, `sprint-1/`). Solo `CambiosIA.md` permanece en la raíz de `diagramas/`.
- **Archivos**:
  - `sprint-0/votar.c4` — versión base (Sprint 0)
  - `sprint-1/votar.c4` — extensión US-318 (Sprint 1)
  - `.mmd` movidos a `sprint-0/` y `sprint-1/` (ver entrada anterior)

---

## 2026-06-19 — sprint-1/votar.c4

- **Tipo de cambio**: extensión de componentes C4 (Panel y API) para US-318.
- **Motivo**: US-318 — Gestionar listas y candidatos. Se agregan `ofertaElectoralPanel`, `configDatosCandidatoPanel`, `eleccionModule` (subdominios `lista/` y `candidato/`), relaciones con `rulesEngine` y `dataAccess`, y ampliación de `candidateSchema` con tablas normalizadas de configuración de campos.
- **Archivo nuevo**: `sprint-1/votar.c4` (evolución de `sprint-0/votar.c4`)

---

## 2026-06-19 — sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd

- **Tipo de cambio**: extensión de oferta electoral y normalización relacional de campos dinámicos de candidato (Sprint 1).
- **Motivo**: US-318 — Migración `NormalizeCampoDatosCandidato`: `LISTA.list_id` post-oficialización; `CANDIDATO.datos_adicionales` (JSONB validado); definición de campos en `CONFIGURACION_DATOS_CANDIDATO` (1:1 con elección) y `CAMPO_DATOS_CANDIDATO` (clave, tipo, obligatoriedad, validaciones, orden).
- **Archivo modificado**: `sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`

---

## 2026-06-19 — sprint-0/Diagrama de clases - Sprint 0 - PFISI(1).mmd

- **Tipo de cambio**: nuevo diagrama de clases de dominio electoral y servicios NestJS (Sprint 1).
- **Motivo**: US-318 — Documentar Boleta como contenedor de listas/categorías, entidades `ConfiguracionDatosCandidato` / `CampoDatosCandidato`, `Lista.listId`, `Candidato.datosAdicionales` y servicios `ListaService`, `CandidatoService`, `OficializacionService`, `ConfiguracionDatosCandidatoService`.
- **Archivo nuevo**: `sprint-1/Diagrama de clases - Sprint 1 - PFISI.mmd`

---

## 2026-06-11 — sprint-0/Diagrama Entidad Relación - Sprint 0 - PFISI.mmd

- **Tipo de cambio**: refinamiento semántico y estructural de `PADRON_VOTANTE`.
- **Motivo**: implementación de la User Story 330 ("Importar padrón por CSV"). La entidad pasa a almacenar exclusivamente el hash Keccak-256 del votante (`hash_hoja` = `votanteHash`) en cumplimiento de la Ley 25.326 (anonimización estructural). Se elimina la FK a `VOTANTE` para evitar cualquier vínculo persistente con identidad civil. Se agrega `generado_en` (auditoría), `UNIQUE(id_padron, hash_hoja)` (anti-duplicados) e índice sobre `hash_hoja` (lookup eficiente durante validación de sufragio).
- **Archivo nuevo**: `sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`
