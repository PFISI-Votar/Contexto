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

## 2026-06-24 — sprint-1 (US-355 — Boleta Única Digital / confirmación off-chain)

- **Tipo de cambio**: nueva entidad `VOTO_CONFIRMACION` en DER; extensión del modelo de análisis y C4 con módulo BUD de confirmación.
- **Motivo**: US-355 — Documentar recepción off-chain del voto desde la BUD con idempotencia, anti doble voto por `votante_hash` y persistencia exclusiva de hashes (sin selección en claro). Alineación con migración `VotoConfirmacion1782160000000` en `back`.
- **Archivos modificados**:
  - `sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`
  - `sprint-1/Diagrama de clases - Sprint 1 - PFISI.mmd`
  - `sprint-1/votar.c4`

---

## 2026-06-21 — sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd

- **Tipo de cambio**: extensión de `PADRON_ELECTORAL` con la persistencia del reporte de novedades de importación.
- **Motivo**: US-331 — Importador tolerante a errores. Para permitir la re-descarga del archivo de auditoría tras cerrar el modal, se persisten `total_procesados` (int), `total_omitidos` (int) y `novedades` (jsonb, array `[linea, tipo, motivo]`). El reporte no contiene datos identificatorios en texto plano (Ley 25.326). Migración `AddNovedadesPadron1782050000000`.
- **Archivo modificado**: `sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`

---

## 2026-06-20 — sprint-1 (US-319 — corrección modelo de análisis y DER)

- **Tipo de cambio**: alineación del diagrama de clases (modelo de análisis) y limpieza del DER con la implementación US-319.
- **Motivo**: US-319 — El mínimo de candidatos es por rol (`CATEGORIA.minimo_postulantes`), no por lista. El diagrama de clases no debe incluir servicios de implementación (`RulesEngineService`); la regla de negocio se modela en `Categoria`, `Lista` y value objects transitorios de validación.
- **Diagrama de clases**:
  - Eliminados `RulesEngineService`, `Eleccion.minimoCandidatosPorLista` y `Lista.minimoCandidatos`.
  - Agregados value objects `ViolacionMinimoCandidatos` y `ResultadoValidacionMinimos`.
  - Agregadas operaciones de dominio `Lista.contarCandidatosPorCategoria()` y `Lista.cumpleMinimosCandidatos()`.
  - Notas US-319 en `Eleccion.oficializarOferta()` y `Lista`.
- **DER**:
  - Eliminado `LISTA.minimo_candidatos` (no existe en esquema implementado).
  - Aclarado `ELECCION.minimo_candidatos_por_lista` como legacy/no usado por US-319.
  - Documentada regla de validación en `CATEGORIA.minimo_postulantes`.
- **Archivos modificados**:
  - `sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`
  - `sprint-1/Diagrama de clases - Sprint 1 - PFISI.mmd`

---

## 2026-06-20 — sprint-1 (US-319 — Validar mínimo de candidatos)

- **Tipo de cambio**: extensión de `CATEGORIA` con mínimo por rol; componente `RulesEngineService` en diagrama de clases.
- **Motivo**: US-319 — Bloquear oficialización si alguna lista no alcanza `minimo_postulantes` por categoría; motor de reglas devuelve desglose por lista/categoría antes de transicionar a CONFIGURADA.
- **Archivos modificados**:
  - `sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`
  - `sprint-1/Diagrama de clases - Sprint 1 - PFISI.mmd`
- **Nota**: superseded parcialmente por la entrada «corrección modelo de análisis y DER» del mismo día.

---

## 2026-06-20 — sprint-1/Diagrama de clases - Sprint 1 - PFISI.mmd (corrección)

- **Tipo de cambio**: refactor del diagrama de clases a modelo de análisis de dominio.
- **Motivo**: eliminar artefactos de implementación (DTOs, repositories, servicios NestJS) y conservar entidades de negocio, value objects, enumeraciones y operaciones del dominio electoral (US-316 + US-318).
- **Archivo modificado**: `sprint-1/Diagrama de clases - Sprint 1 - PFISI.mmd`

---

## 2026-06-20 — sprint-1 (US-316 — Crear comicio)

- **Tipo de cambio**: extensión de modelo relacional, diagrama de clases y C4 para alta de comicio en BORRADOR.
- **Motivo**: US-316 — Implementación de creación de comicio con `tipo_votacion`, roles/categorías dinámicas (`cantidad_cargos` = máximo postulantes), `configuracion_comicio.metodos_autenticacion[]` (Google, SSO Institucional), validación temporal HTTP 422, sanitización de entrada y aislamiento on-chain en estado BORRADOR.
- **Archivos modificados**:
  - `sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`
  - `sprint-1/Diagrama de clases - Sprint 1 - PFISI.mmd`
  - `sprint-1/votar.c4`

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
