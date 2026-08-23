# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Proyecto: VOTAR

Plataforma de **votación electrónica descentralizada** desarrollada como Proyecto Final de ISI — UTN FRVM, Equipo 09 ("Five stack": Liendo, Lucarelli, Magni, Mosconi, Terreno).

Objetivo: resolver los problemas de los sistemas electorales centralizados (opacidad, doble voto, falta de verificabilidad E2E) mediante una arquitectura híbrida **blockchain + backend off-chain**, garantizando anonimato del sufragio (cumplimiento Ley 25.326) y verificabilidad matemática extremo a extremo.

---

## Stack técnico

| Capa | Tecnología |
|---|---|
| Backend | NestJS 11 + TypeScript |
| Frontend | React 19 + Vite + TypeScript + Tailwind CSS 4 + shadcn/ui |
| Base de datos | PostgreSQL 16 (off-chain) |
| Blockchain | Ethereum Sepolia testnet (Smart Contracts) |
| Autenticación | SSO/OIDC (OAuth 2.0 institucional) |
| Criptografía cliente | Web Crypto API (billetera efímera) |

---

## Comandos

### Backend (`back/`)
```bash
npm run dev          # watch mode (desarrollo)
npm run start:prod   # producción
npm run build        # compilar
npm run lint         # ESLint con autofix
npm run test         # Jest (unit)
npm run test:watch   # Jest watch
npm run test:e2e     # tests e2e
npm run test:cov     # coverage
```
Tests: archivos `*.spec.ts` en `src/`. Run unitario: `jest --testPathPattern=nombre.spec.ts`.

### Frontend (`front/`)
```bash
npm run dev      # Vite dev server
npm run build    # tsc + vite build
npm run lint     # ESLint
npm run preview  # preview del build
```

---

## Arquitectura del dominio

### Entidad central: `ELECCION`
Ciclo de vida con 5 estados: `BORRADOR → CONFIGURADA → ABIERTA → CERRADA → ESCRUTADA`.

Cada elección tiene composición 1:1 con:
- `CONFIGURACION_COMICIO` — parámetros (revoto, tiempo real, tipo auth, política de re-voto)
- `BOLETA` — estructura electoral (CATEGORIA → CANDIDATO, LISTA → CANDIDATO)
- `PADRON_ELECTORAL` — padrón habilitado; genera `MERKLE_TREE`
- `SMART_CONTRACT_ELECCION` — referencia al contrato desplegado en Sepolia

### Flujo de voto (crítico para entender la arquitectura completa)

```
1. Votante se autentica via SSO/OIDC
2. Backend valida en PADRON y provee MerkleProof (calculada on-demand, NO persistida)
3. Cliente genera BILLETERA_EFIMERA con Web Crypto API (clave privada NUNCA sale del RAM del navegador)
4. Cliente deriva NULLIFIER = hash(clavePublica + idEleccion)
5. Cliente firma payload del voto con clave privada
6. Cliente envía (votoFirmado + MerkleProof + nullifier) al Smart Contract en Sepolia
7. Backend registra REGISTRO_NULLIFIER off-chain y TRANSACCION_BLOCKCHAIN
8. Smart Contract emite evento → Backend persiste RECIBO_VOTACION
9. Clave privada efímera se destruye del RAM
```

**Invariante de privacidad**: `VOTO` no tiene FK a `VOTANTE`. El voto "nace huérfano de identidad" (Ley 25.326). La desvinculación es estructural, no solo de acceso.

### MerkleProofs
Los `MerkleProof` **no se persisten** en la BD. Se calculan en tiempo de ejecución desde `MERKLE_TREE` + `PADRON_VOTANTE` bajo demanda. El `MERKLE_TREE` puede tener múltiples versiones (una activa/publicada on-chain).

### Billetera efímera
Generada 100% client-side. La clave privada **jamás se persiste en BD** (ni encriptada). Solo se almacena la `clave_publica` en `BILLETERA_EFIMERA`. Estados: `ACTIVA → USADA → DESTRUIDA`.

### Nullifier (anti-doble-voto sin vincular identidad)
Derivado de `clavePublica + idEleccion`. Permite detectar revoto sin saber quién votó. `REGISTRO_NULLIFIER` es el motor off-chain; el Smart Contract también lleva su propio registro on-chain.

### Re-voto (política anti-coerción)
Si `CONFIGURACION_COMICIO.permitirVotoMultiple = true`, política `LAST_VOTE_WINS`: el votante puede sufragar múltiples veces; solo el último voto (`es_ultimo = true`) se computa en el escrutinio. El nullifier anterior se invalida.

### Actores del sistema
- **AUTORIDAD_ELECTORAL** — roles: `ELECTION_ADMIN | PAUSER | MERKLE_UPDATER`. Gestiona el comicio completo.
- **VOTANTE** — autenticado via SSO; jamás vinculado estructuralmente a su voto.
- **OBSERVADOR** — tipos: `FISCAL | AUDITOR_PUBLICO | VEEDOR`. Solo lectura/auditoría.

---

## Estructura del proyecto

```
codigo/
├── back/          # NestJS API
│   └── src/       # app.module.ts, main.ts — bootstrap NestJS estándar
├── front/         # React SPA
│   └── src/       # App.tsx, components/ui/ (shadcn), lib/utils.ts
└── diagramas/     # Diagramas de referencia por sprint
    ├── sprint-0/  # DER, clases y votar.c4 del Sprint 0
    ├── sprint-1/  # DER, clases y votar.c4 del Sprint 1
    ├── sprint-2/  # DER, clases y votar.c4 del Sprint 2 (VOTAR-334 Merkle)
    └── sprint-3/  # DER, clases, C4 y secuencias del Sprint 3 (VOTAR-346/350 auditoría on-chain)
    └── sprint-5/  # DER, clases, C4 y secuencias del Sprint 5 (VOTAR-322 archivado, VOTAR-347 pausa, VOTAR-374/375 actas, VOTAR-386 RPC failover, VOTAR-451/452 cooldown)
```

---

## Norma: Gestión de diagramas en `diagramas/`

Los archivos en `diagramas/sprint-N/` (`.mmd` y `votar.c4`) son documentos de referencia por sprint. Cualquier modificación que afecte el contenido de un diagrama **requiere obligatoriamente** crear una nueva versión del archivo en la carpeta del sprint correspondiente. Naming convention:

- Sprint 0: `diagramas/sprint-0/Diagrama Entidad Relación - Sprint 0 - PFISI.mmd`, `diagramas/sprint-0/votar.c4`
- Sprint 1: `diagramas/sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`, `diagramas/sprint-1/votar.c4` (o el sprint/versión correspondiente)

Esta norma aplica a cualquier modificación, incluyendo correcciones de atributos, relaciones nuevas, eliminación de entidades o cambios de cardinalidad.

---

## Convención para Commits

Los cambios se documentan vía commits para mantener un historial de desarrollo legible, escaneable y entendible por cualquier miembro del equipo. El equipo se compromete a cumplir las siguientes pautas:

**Atomicidad**: cada commit debe agrupar cambios lo más atómicos e independientes posibles.

**Formato**:

```
<tipo-de-commit>[scope]: <descripción>
```

### Prefijos (`tipo-de-commit`)

| Prefijo | Uso |
|---|---|
| `feat` | Nueva característica para el usuario. |
| `fix` | Arregla un error que afecta al usuario. |
| `perf` | Cambios que mejoran el rendimiento del sitio. |
| `build` | Cambios en el sistema, tareas de despliegue o instalación. |
| `ci` | Cambios en la integración continua. |
| `docs` | Cambios en la documentación. |
| `refactor` | Refactorización del código (renombres de variables/funciones, reorganización sin cambio funcional). |
| `test` | Añade pruebas o refactoriza pruebas existentes. |

### Scope (opcional)

Cuando se especifique, refiere a la funcionalidad principal del commit. Ejemplo:

```
feat(backend): add filter for customer
```

### Descripción

Usar **verbo imperativo**: cada commit se debe poder leer como una instrucción para cambiar el estado del proyecto. Verbos sugeridos:

- **Add**: agrega un nuevo archivo o funcionalidad.
- **Change**: modifica un archivo.
- **Update**: actualiza un archivo (cambios poco significativos).
- **Upgrade**: mejora el archivo sin cambiar su funcionalidad.
- **Fix**: arregla un problema de un archivo.
- **Remove**: elimina un archivo.

### Ejemplos válidos

```
feat(padron): add CSV import endpoint with Keccak-256 anonymization
fix(auth): change token expiry comparison to inclusive bound
refactor(eleccion): rename estado field for consistency
docs(diagramas): update Sprint 1 ER diagram with MerkleTree entity
build(backend): upgrade typeorm to 0.3.20
test(padron): add UAT-02 assertion for plaintext absence
```
