# Registro de Cambios en Diagramas

Este archivo documenta todas las modificaciones realizadas a los diagramas de arquitectura del sistema VOTAR, siguiendo la norma establecida en `CLAUDE.md`.

---

## [2026-09-06] — Sprint 6 — VOTAR-464 feedback en dashboard de resultados (vía VOTAR-474)

- **Tipo de cambio**: `contexto-sistema.md` (sin diagramas nuevos)
- **Motivo**: Feedback QA en VOTAR-464 — voto por lista/mixto solo reflejaba un cargo en la UI; se pidió agregar por lista y ruedas/modal por cargo
- **Cambios específicos**:
  1. Dashboard Resultados: `POR_LISTA` agrega tallies por lista; `POR_CANDIDATO` muestra una dona por categoría + modal de ganadores
  2. On-chain sigue siendo `candidateIds[]` (VOTAR-474); la agregación por lista usa `max(votos)` dentro de la lista
- **User Stories relacionadas**: VOTAR-464 (feedback), VOTAR-474
- **Archivos**: `contexto-sistema.md`

---

## [2026-09-03] — Sprint 6 — VOTAR-474 feedback: multi-selección por categoría en BUD

- **Tipo de cambio**: `contexto-sistema.md` (sin diagramas nuevos)
- **Motivo**: Feedback de QA — el BUD no permitía elegir N candidatos dentro de una categoría multi-banca (`cantidadCargos > 1`) ni había copy claro de configuración
- **Cambios específicos**:
  1. `CATEGORIA.cantidadCargos` documentado como tope de postulantes **y** de selecciones del votante
  2. Alineado con boleta digital (`cantidadCargos` en API) + BUD multi-select + merge de diseño VOTAR-464
- **User Stories relacionadas**: VOTAR-474 (feedback), VOTAR-464
- **Archivos**: `contexto-sistema.md`

---

## [2026-08-31] — Sprint 6 — VOTAR-474 escrutinio multi-categoría on-chain

- **Tipo de cambio**: Diagrama de clases + C4 + secuencia de resultados + nota DER en `diagramas/sprint-6/` (norma: no editar in-place sprints anteriores)
- **Motivo**:
  - Bug: `VoteRegistry` solo almacenaba un `candidateId` por `voterHash`; el escrutinio público no incrementaba tallies de categorías no-primarias
  - Fix: `recordVote` / `castSignedVote` aceptan `candidateIds[]` (EIP-712 domain v2); un `VoteCast` por boleta + `VoteUpdated` por cada id
- **Cambios específicos**:
  1. Clases: `ContratoBoleta.castSignedVote(..., candidatoIds int[])`; `RegistroVoto.recordVote(..., candidatoIds int[])` + `MAX_CANDIDATES_PER_BALLOT`; notas VOTAR-474
  2. C4: descripciones de `BallotContract` / `VoteRegistry` y relación `recordVote(candidateIds[])`
  3. Secuencia VOTAR-364: `castSignedVote (candidateIds[])` → `VoteCast + VoteUpdated×N`
  4. DER: `TRANSACCION_BLOCKCHAIN.nombre_evento` incluye `VoteUpdated` (índice on-chain; sin entidades off-chain nuevas)
  5. `contexto-sistema.md`: flujo de sufragio y política LAST_WINS con `candidateIds[]`
- **User Stories relacionadas**: VOTAR-474
- **Archivos**: `diagramas/sprint-6/Diagrama de clases - Sprint 6 - PFISI.mmd`, `diagramas/sprint-6/votar.c4`, `diagramas/sprint-6/secuencia-visualizacion-resultados-votar-364.mmd`, `diagramas/sprint-6/Diagrama Entidad Relación - Sprint 6 - PFISI.mmd`, `contexto-sistema.md`

---

## [2026-08-27] — Sprint 6 — VOTAR-466 persistencia de imágenes en PostgreSQL

- **Tipo de cambio**: DER + Diagrama de clases + C4 de `diagramas/sprint-6/` (norma: no editar in-place Sprint 5; carpeta Sprint 6 tomada como base desde `feature/VOTAR-459-fix-visibilidad-de-dashboard-publico`, ver entrada anterior, para evitar divergencia al mergear ambas ramas)
- **Motivo**:
  - Las imágenes electorales (foto de candidato, logo de lista, logo institucional) se guardaban en el disco local del contenedor `back` y se servían por `/uploads/`. La fila de dominio (`candidato.foto_url`, etc.) persiste en el volumen de Postgres; el archivo referenciado no — al recrear el contenedor (`docker compose down/up`) el archivo se pierde y la referencia queda rota
  - Se verificó explícitamente que ninguna imagen viaja a la blockchain: los contratos en `blockchain/contracts/` solo manejan `bytes32`, pruebas Merkle y firmas EIP-712; el único dato de candidato on-chain es un `uint256` sellado en `VoteRegistry.registerCandidates`
  - Volumen bajo (decenas de imágenes, ≤100 KB cada una tras optimizar) → `bytea` en PostgreSQL es la opción adecuada frente a un servicio de almacenamiento externo
- **Cambios específicos**:
  1. DER: nueva entidad `IMAGEN_ELECTORAL` (`id_imagen` uuid PK, `tipo`, `mime_type`, `contenido` bytea, `tamano_bytes`, `checksum_sha256`, `ancho`, `alto`, `fecha_creacion`)
  2. DER: `CANDIDATO.foto_url` y `CONFIGURACION_SISTEMA.logo_url` documentan que ahora contienen `/imagenes/{id_imagen}` en lugar de una ruta a archivo en disco (`/uploads/...`)
  3. DER: se documenta `LISTA.logo_url`, atributo existente en la base desde Sprint 2 (migración `AddListaLogoUrl`) pero ausente del diagrama hasta ahora
  4. DER: nota explícita — `IMAGEN_ELECTORAL` no tiene FK desde `CANDIDATO`/`LISTA`/`CONFIGURACION_SISTEMA`; el vínculo es por URL en varchar, decisión consciente para acotar el blast radius del cambio
  5. Diagrama de clases: nuevas clases `ImagenElectoral` (entidad), `ElectoralImageService` (`saveImage`, `obtenerImagen`, `deleteIfManagedUrl`), `ElectoralImageController` (`obtener`); se agrega `Lista.logoUrl` (mismo gap que en el DER)
  6. C4: nuevo componente `electoralImageService` dentro del contenedor backend (`votar.api`), con su relación hacia `dataAccess`
- **User Stories relacionadas**: VOTAR-466
- **Archivos**: `Contexto/diagramas/sprint-6/Diagrama Entidad Relación - Sprint 6 - PFISI.mmd`, `Contexto/diagramas/sprint-6/Diagrama de clases - Sprint 6 - PFISI.mmd`, `Contexto/diagramas/sprint-6/votar.c4`

---

## [2026-08-26] — Sprint 6 — VOTAR-459 visibilidad configurable del Dashboard Público

- **Tipo de cambio**: Nueva carpeta `diagramas/sprint-6/` (norma: no editar in-place Sprint 5) + DER + Diagrama de clases (copiados de Sprint 5 y actualizados)
- **Motivo**:
  - US: Como Autoridad Electoral quiero configurar la visibilidad de las solapas Resultados, Participación, Re-voto y Transacciones del Dashboard Público mientras el comicio está ABIERTO, para no inducir comportamiento estratégico del electorado con datos parciales en vivo
  - La restricción rige solo mientras el comicio no cerró: en CERRADA/ESCRUTADA/ARCHIVADA todas las secciones vuelven a ser públicas
  - Editable solo en BORRADOR y CONFIGURADA (se congela al abrir el comicio)
- **Cambios específicos**:
  1. DER: `CONFIGURACION_COMICIO` agrega `mostrar_dashboard_resultados`, `mostrar_dashboard_participacion`, `mostrar_dashboard_revoto`, `mostrar_dashboard_transacciones` (boolean, default true)
  2. Diagrama de clases: nota de evolución Sprint 6 (sin nuevas clases de dominio; lógica en `ConfiguracionComicioService` y `SeccionDashboardVisibleGuard`)
  3. Resto de los archivos del sprint (secuencias, `votar.c4`) copiados sin cambios de contenido como base de Sprint 6
- **User Stories relacionadas**: VOTAR-459
- **Archivos**: `Contexto/diagramas/sprint-6/Diagrama Entidad Relación - Sprint 6 - PFISI.mmd`, `Contexto/diagramas/sprint-6/Diagrama de clases - Sprint 6 - PFISI.mmd`

---

## [2026-08-23] — Sprint 5 — Ciclo de vida, pausa, actas, cooldown y RPC failover

- **Tipo de cambio**: Carpeta `diagramas/sprint-5/` completa + C4 + secuencias + contexto-sistema
- **Motivo**:
  - Documentar Sprint 5 conforme norma (no editar in-place Sprint 4)
  - Reflejar entregas: archivado, pausa, actas PDF, export PNG, failover RPC, faucet, fixes re-voto
- **Cambios específicos**:
  1. DER: `ARCHIVADA`, `pausada`/`pausada_en`, `CONFIGURACION_SISTEMA`, `REGISTRO_INTENTO_SUFRAGIO`, audit events pausa/archivado
  2. Clases: `ArchivarComicioService`, `PausaComicioService`, `ActaApertura/Cierre`, `CooldownAnchor`, `RpcFailoverService`, `FaucetService`, `RevotePolicyService.registrarConsumo(votosObjetivo)`
  3. Secuencias nuevas: `secuencia-archivar-comicio-votar-322.mmd`, `secuencia-pausa-comicio-votar-347.mmd`, `secuencia-intervalo-sufragios-votar-452.mmd`, `secuencia-acta-apertura-votar-374.mmd`
  4. C4: cooldownClock, election seed, documentosComicio, pausaComicioPanel, rpcBackup, participacionExporter, dynamic views Sprint 5
  5. `contexto-sistema.md`: sección 18 actualizada (2026-08-23)
- **User Stories relacionadas**: VOTAR-322, VOTAR-347, VOTAR-348, VOTAR-374, VOTAR-375, VOTAR-376, VOTAR-386, VOTAR-387, VOTAR-451, VOTAR-452, VOTAR-453, VOTAR-456
- **Archivos**: `Contexto/diagramas/sprint-5/*`, `Contexto/contexto-sistema.md`

---

## [2026-08-11] — Sprint 5 — VOTAR-322 archivado lógico de comicios finalizados (borrador inicial)

- **Tipo de cambio**: Nueva carpeta `diagramas/sprint-5/` (norma: no editar in-place Sprint 4) + DER + Diagrama de clases
- **Motivo**:
  - US: Como Autoridad Electoral quiero archivar comicios en estado CERRADA para removerlos del panel de gestión activa, preservando el acceso público a la evidencia digital on-chain
  - Nuevo estado `ARCHIVADA` en `ELECCION.estado` (transición CERRADA → ARCHIVADA)
  - Operación estrictamente relacional: prohibido enviar transacciones a Sepolia; el Smart Contract permanece inmutable en `CLOSED`
  - Nuevo evento de auditoría `COMICIO_ARCHIVADO` en `AUDIT_LOG.tipo_evento`
- **Cambios específicos**:
  1. DER: `ELECCION.estado` → agrega `ARCHIVADA` a la lista de valores
  2. DER: `AUDIT_LOG.tipo_evento` → agrega `COMICIO_ARCHIVADO`
  3. Diagrama de clases: enum `EleccionEstado` → agrega valor `ARCHIVADA`
  4. Ampliado en entrada 2026-08-23 con el resto de tickets Sprint 5
- **User Stories relacionadas**: VOTAR-322 (archivado de comicios finalizados)
- **Archivos**: `diagramas/sprint-5/Diagrama Entidad Relación - Sprint 5 - PFISI.mmd`, `diagramas/sprint-5/Diagrama de clases - Sprint 5 - PFISI.mmd`

---

## [2026-08-11] — Sprint 4 — Secuencias dinámicas LikeC4 en votar.c4

- **Tipo de cambio**: C4 (`votar.c4`) + CambiosIA
- **Motivo**:
  - Publicar en LikeC4 (`c4.votar.net.ar`) las secuencias del Sprint 4 como `dynamic view` navegables con `?dynamic=sequence`
  - Alinear flujos `.mmd` con elementos C4 existentes (sin duplicar participantes Mermaid)
- **Cambios específicos**:
  1. `sufragio_flow`: pasos 16–17 indexación post-voto VOTAR-373
  2. Nuevas vistas: `auditoria_publica_flow` (350), `cierre_comicio_flow` (321), `estado_contrato_flow` (367), `revoto_stats_flow` (329), `transacciones_flow` (373), `escrutinio_tiempo_real_flow` (364)
  3. URLs interactivas: `https://c4.votar.net.ar/view/<view_id>/?dynamic=sequence`
- **User Stories relacionadas**: VOTAR-350, VOTAR-321, VOTAR-364, VOTAR-367, VOTAR-329, VOTAR-373
- **Archivos**: `diagramas/sprint-4/votar.c4`, `diagramas/CambiosIA.md`

---

## [2026-08-09] — Sprint 4 — VOTAR-373 trazabilidad on-chain (C4 + secuencia)

- **Tipo de cambio**: C4 + secuencia Mermaid
- **Motivo**:
  - Documentar índice append-only `transaccion_blockchain` (patrón VOTAR-433)
  - Corregir desalineación C4: blockScanner en front escaneaba RPC; la lectura pública usa PostgreSQL
  - Fix error Alchemy Free tier: `eth_getLogs` con rango `[0, latest]` inviable (~300 req/usuario)
- **Cambios específicos**:
  1. C4: `transaccionesViewer` (front) + `transaccionBlockchainIndexer` (back); eliminado scan RPC desde dashboard
  2. Nueva secuencia `secuencia-transacciones-votar-373.mmd` (POST transaccion-publica + GET transacciones-publica)
  3. Vista dinámica `transacciones_flow` en LikeC4 (ver entrada 2026-08-11)
- **User Stories relacionadas**: VOTAR-373 (Sprint 4)
- **PRs**: Contexto (esta PR), back #68, front #82
- **Archivos**: `diagramas/sprint-4/votar.c4`, `diagramas/sprint-4/secuencia-transacciones-votar-373.mmd`

---

## [2026-08-08] — Sprint 4 — VOTAR-367 visualización del estado del contrato

- **Tipo de cambio**: Secuencia + clases + contexto-sistema
- **Motivo**:
  - Documentar exposición pública de metadatos criptográficos (direcciones, estado on-chain, Merkle, re-voto)
  - Alinear diagramas con `GET /elecciones/:id/contrato-estado-publica` y `/dashboard/estado`
- **Cambios específicos**:
  1. Nueva secuencia `secuencia-estado-contrato-votar-367.mmd`
  2. Clases Sprint 4: `MetadatosContratoPublico` + relaciones con `VistaAuditoria` / `AlmacenRaizMerkle`
  3. `contexto-sistema.md`: ruta `/dashboard/estado`, endpoint público y ticket en PR
- **User Stories relacionadas**: VOTAR-367 (Sprint 4)
- **PRs**: Contexto (esta PR), back #67, front #81
- **Archivos**: `diagramas/sprint-4/secuencia-estado-contrato-votar-367.mmd`, `Diagrama de clases - Sprint 4 - PFISI.mmd`, `contexto-sistema.md`

---

## [2026-08-08] — Sprint 4 — VOTAR-329 estadísticas de re-voto en Dashboard

- **Tipo de cambio**: Nueva carpeta `diagramas/sprint-4/` + implementación on-chain / API / UI
- **Motivo**:
  - Documentar Sprint 4 en Contexto (norma: no editar in-place Sprint 3)
  - Cumplir criterio: `AuditViewContract.getRevoteStats(id)` → `(totalRevotes, uniqueVoters, overwriteRatio)`
  - Reflejar stack real (NestJS 11, React 19) y dashboard público ampliado

- **Cambios específicos**:
  1. Creada carpeta `diagramas/sprint-4/` (DER, clases, C4, secuencias heredadas + nueva VOTAR-329)
  2. `VoteRegistry`: contador `_totalRevotes` + `getRevoteStats`
  3. `AuditViewContract.getRevoteStats` delega a `VoteRegistry` (ratio WAD)
  4. Back: `GET /elecciones/:id/revoto-stats-publica` + curva temporal
  5. Front: `/dashboard/revoto` con polling 4s (UAT-02)
  6. Diagrama de clases Sprint 4: `StatsRevoto`, métodos en `RegistroVoto` y `VistaAuditoria`
  7. C4 Sprint 4: NestJS, Recharts, sección re-voto en dashboard
  8. `contexto-sistema.md`: sección 18 (repos, rutas, tickets)

- **User Stories relacionadas**: VOTAR-329 (Sprint 4)

- **PRs**: Contexto #30, blockchain #36, back #66, front #80

- **Archivos**: `Contexto/diagramas/sprint-4/*`, `Contexto/contexto-sistema.md`

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
