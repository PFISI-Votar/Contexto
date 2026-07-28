# Lineamientos de desarrollo para agentes de IA — Proyecto VOTAR

> **Propósito:** Este documento define el estándar de trabajo que todo agente de IA (Cursor, Claude Code, Copilot, etc.) debe seguir al implementar tareas en el ecosistema VOTAR. Está alineado con la documentación académica del Equipo 09 (*Five stack*), el Definition of Done del equipo y las convenciones ya establecidas en `Contexto/claude/CLAUDE.md`.

---

## 1. Contexto del proyecto

**VOTAR** es una plataforma de votación electrónica descentralizada (Proyecto Final ISI — UTN FRVM) orientada a elecciones de pequeña y mediana escala. Resuelve opacidad, doble voto y falta de verificabilidad E2E mediante arquitectura híbrida **blockchain + backend off-chain**.

| Capa | Tecnología |
|---|---|
| Backend | NestJS 11 + TypeScript + TypeORM |
| Frontend | React 19 + Vite + TypeScript + Tailwind CSS 4 + shadcn/ui |
| Base de datos | PostgreSQL 16 (off-chain) |
| Blockchain | Solidity + Ethereum Sepolia testnet |
| Autenticación | SSO/OIDC (OAuth 2.0 institucional) |
| Criptografía cliente | Web Crypto API (billetera efímera) |

### Repositorios

| Repo | Ruta local | GitHub |
|---|---|---|
| Frontend | `votar.front/` | [PFISI-Votar/front](https://github.com/PFISI-Votar/front) |
| Backend | `votar.back/` | [PFISI-Votar/back](https://github.com/PFISI-Votar/back) |
| Blockchain | *(repo separado)* | [PFISI-Votar/blockchain](https://github.com/PFISI-Votar/blockchain) |

### Documentación de referencia

- Alcance y reglas de negocio: `Contexto/md/01 UTN FRVM - PF 2026 - Propuesta y Alcance - Equipo 09 v2.1.0.md`
- Ciclo de vida y DoD: `Contexto/md/03 UTN FRVM - PF 2026 - Ciclo de Vida y Enfoque de Desarrollo - Equipo 09 v2.0.2.md`
- Sprint 0 (diagramas, stack): `Contexto/md/01 UTN FRVM - PF 2026 – Sprint 0 - Equipo 09 v1.8.3.md`
- Diagramas: `Contexto/diagramas/`
- Contexto técnico para agentes: `Contexto/claude/CLAUDE.md`

---

## 2. Checklist obligatorio por tarea

**Antes de considerar una tarea terminada**, el agente debe completar **todos** los ítems aplicables. Si un ítem no aplica, documentar brevemente por qué en el resumen de la tarea.

### 2.1. Pre-desarrollo

- [ ] **Identificar la User Story (US)** en Jira: ID, épica, criterios de aceptación y pruebas de usuario.
- [ ] **Leer el contexto de dominio** relevante (estados de `ELECCION`, invariantes de privacidad, reglas de negocio).
- [ ] **Diseñar antes de codificar** si la tarea lo amerita: diagrama de secuencia, ajuste al DER o diagrama de clases (ver §6).
- [ ] **Crear rama** según convención Git (ver §8): `feature/modulo-descripcion-breve` o `fix/...`.

### 2.2. Desarrollo

- [ ] **Implementar la funcionalidad** siguiendo las convenciones de código (§4 y §5).
- [ ] **Respetar invariantes de seguridad y privacidad** (§7): anonimato del sufragio, Ley 25.326, separación identidad/contenido del voto.
- [ ] **No introducir deuda técnica crítica** ni cambios fuera del alcance de la US.
- [ ] **Minimizar el diff**: solo archivos estrictamente necesarios para la tarea.

### 2.3. Pruebas

- [ ] **Escribir o actualizar pruebas unitarias** que cubran los casos principales de la US (§9).
- [ ] **Ejecutar la suite de tests** del repo afectado y confirmar que pasan.
- [ ] **Ejecutar linter** (`npm run lint`) y corregir errores introducidos.
- [ ] Si aplica **smart contract**: pruebas locales (Hardhat/Ganache) y despliegue en Sepolia testnet sin errores.

### 2.4. Documentación de API (backend)

- [ ] **Documentar endpoints nuevos o modificados con Swagger** (`@nestjs/swagger`) antes de dar por cerrada la implementación (§10).
- [ ] Verificar que DTOs de request/response tengan decoradores `@ApiProperty` cuando corresponda.

### 2.5. Diagramas y artefactos de diseño

- [ ] **Actualizar diagramas si la tarea modifica** entidades, relaciones, cardinalidades, flujos o componentes (§6).

### 2.6. Control de versiones

- [ ] **Nombrar commits** según la convención del equipo (§8).
- [ ] **Commits atómicos**: un commit = un cambio lógico coherente.
- [ ] **No commitear** a menos que el usuario lo solicite explícitamente.
- [ ] **No incluir secretos** (`.env`, claves, tokens) en commits.

### 2.7. Cierre

- [ ] **Verificar Definition of Done** del equipo (§3).
- [ ] **Resumir al usuario**: qué se hizo, qué tests corrieron, qué diagramas se actualizaron, endpoints documentados y pasos manuales pendientes (PR, deploy, Jira).

---

## 3. Definition of Done (DoD)

Una historia de usuario se considera **terminada** solo cuando se cumplen **todos** estos criterios (fuente: documento de Ciclo de Vida v2.0.2):

1. Código revisado y aprobado por al menos un compañero (PR revisado y aprobado).
2. Existen **pruebas unitarias o de integración** que cubren los casos de uso principales.
3. El **smart contract**, si aplica, fue auditado localmente y desplegado en Testnet sin errores.
4. La **documentación técnica** asociada (comentarios de código, README, Swagger) fue actualizada.
5. La **documentación funcional** asociada (workflows PUD, backlogs) fue actualizada cuando corresponda.
6. **No hay deuda técnica crítica** pendiente relacionada con el ítem.

### Flujo de una historia hasta Testnet

```
Definición (US en Jira)
  → Diseño (diagramas técnicos)
  → Desarrollo (rama feature/*)
  → Validación (PR + revisión por pares + tests automatizados)
  → Integración (merge a dev)
  → Cierre y Deploy (Sprint Review + Sepolia testnet)
```

---

## 4. Convenciones — Backend (NestJS)

### 4.1. Estructura modular

Seguir arquitectura NestJS por dominio:

```
src/
├── [dominio]/
│   ├── [dominio].module.ts
│   ├── [dominio].controller.ts
│   ├── [dominio].service.ts
│   ├── dto/
│   ├── entities/
│   └── [dominio].service.spec.ts
├── config/
├── database/
│   ├── data-source.ts
│   └── migrations/
└── main.ts
```

- Un **módulo por dominio** principal (ej. `eleccion`, `padron`, `auth`).
- Dominios grandes pueden subdividirse en submódulos NestJS (ej. `eleccion/lista/`, `eleccion/candidato/` importados desde `eleccion.module.ts`).
- Lógica de negocio en **services**; controllers delgados.
- DTOs validados con `class-validator` / `class-transformer`.
- Entidades con TypeORM en `entities/`.

### 4.2. Base de datos y migraciones

- **Nunca** modificar el esquema manualmente en producción; usar migraciones TypeORM.
- Generar migración: `npm run makemigrations` (desde `votar.back/`).
- Ejecutar migración: `npm run migrate`.
- Si la tarea agrega/modifica tablas o columnas → **actualizar DER** (§6).

### 4.3. Comandos útiles

```bash
npm run dev          # desarrollo con watch
npm run build        # compilar
npm run lint         # ESLint
npm run test         # Jest unitarios (*.spec.ts en src/)
npm run test:watch   # Jest en modo watch
npm run test:e2e     # tests end-to-end
npm run test:cov     # cobertura
```

### 4.4. Estilo TypeScript

- Tipado explícito; evitar `any`.
- `PascalCase` para clases; `camelCase` para variables/funciones/métodos.
- `kebab-case` para archivos y directorios.
- Funciones cortas, early returns, una responsabilidad por función.
- Nombres descriptivos: `isLoading`, `hasError`, `canDelete`.
- Event handlers con prefijo `handle`: `handleClick`, `handleSubmit`.
- JSDoc en clases y métodos públicos cuando el comportamiento no sea obvio.

---

## 5. Convenciones — Frontend (React + Vite)

### 5.1. Estructura

```
src/
├── components/
│   └── ui/          # shadcn/ui
├── lib/
│   └── utils.ts
├── features/        # agrupar por dominio (ej. eleccion/lista/, eleccion/candidato/)
├── hooks/
├── services/        # llamadas API
└── App.tsx
```

### 5.2. UI y estilos

- **Tailwind CSS** para todo el styling; evitar CSS suelto salvo `index.css` global.
- Componentes reutilizables con **shadcn/ui** y Radix.
- Accesibilidad: `aria-label`, roles, navegación por teclado en elementos interactivos.
- Usar `const` para componentes y handlers: `const handleClick = () => { ... }`.

### 5.3. Comandos útiles

```bash
npm run dev      # servidor Vite
npm run build    # tsc + vite build
npm run lint     # ESLint
npm run preview  # preview del build
```

### 5.4. Criptografía cliente (billetera efímera)

- Clave privada generada con **Web Crypto API**; **nunca** persistir en BD ni enviar al backend.
- Solo la clave pública puede almacenarse off-chain.
- Destruir referencias a la clave privada del RAM tras emitir el voto.

---

## 6. Gestión de diagramas

Los diagramas en `Contexto/diagramas/` son artefactos oficiales del proyecto. **Cualquier cambio estructural obliga a versionarlos.**

### 6.0. Estructura de carpetas

```
diagramas/
├── sprint-0/             # diagramas del Sprint 0
│   ├── Diagrama Entidad Relación - Sprint 0 - PFISI.mmd
│   ├── Diagrama de clases - Sprint 0 - PFISI(1).mmd
│   └── votar.c4
├── sprint-1/             # diagramas del Sprint 1
│   ├── Diagrama Entidad Relación - Sprint 1 - PFISI.mmd
│   ├── Diagrama de clases - Sprint 1 - PFISI.mmd
│   └── votar.c4
├── sprint-2/             # diagramas del Sprint 2
│   ├── Diagrama Entidad Relación - Sprint 2 - PFISI.mmd
│   ├── Diagrama de clases - Sprint 2 - PFISI.mmd
│   ├── secuencia-cierre-comicio-votar-321.mmd
│   └── votar.c4
└── sprint-3/             # diagramas del Sprint 3
    ├── Diagrama Entidad Relación - Sprint 3 - PFISI.mmd
    ├── Diagrama de clases - Sprint 3 - PFISI.mmd
    ├── secuencia-cierre-comicio-votar-321.mmd
    ├── secuencia-consulta-auditoria-votar-350.mmd
    └── votar.c4
```

Cada sprint tiene su carpeta (`sprint-N/`). DER, diagrama de clases y C4 (`votar.c4`) viven dentro de la carpeta del sprint al que corresponden.

### 6.1. Cuándo actualizar

| Diagrama | Actualizar si... |
|---|---|
| **DER** (`.mmd`) | Nueva entidad, atributo, relación, FK, índice o constraint |
| **Diagrama de clases** (`.mmd`) | Nueva clase de dominio, método público relevante o relación |
| **C4** (`votar.c4`) | Nuevo contenedor, componente o integración externa |
| **Secuencia** (si existe) | Cambio en flujo crítico: auth SSO, emisión de voto, recibo, escrutinio |

### 6.2. Procedimiento obligatorio

1. **No editar in-place** la versión anterior del sprint.
2. **Crear nueva versión** en la carpeta del sprint correspondiente:
   - Ejemplo DER: `diagramas/sprint-0/Diagrama Entidad Relación - Sprint 0 - PFISI.mmd` → `diagramas/sprint-1/Diagrama Entidad Relación - Sprint 1 - PFISI.mmd`
   - Ejemplo C4: `diagramas/sprint-0/votar.c4` → `diagramas/sprint-1/votar.c4`
3. Si el cambio proviene de una US, referenciar el **ID de Jira** en el commit o en la descripción del cambio.

---

## 7. Invariantes de dominio y seguridad (no negociables)

Estas reglas son **estructurales**. Un agente **no debe violarlas** aunque simplifiquen la implementación.

### 7.1. Privacidad del sufragio (Ley 25.326)

- `VOTO` **no tiene FK a `VOTANTE`**. El voto nace huérfano de identidad.
- El padrón almacena **hashes** (Keccak-256), no datos identificatorios en texto plano.
- `MerkleProof` se calcula **on-demand**; no se persiste en BD.
- Clave privada de billetera efímera **jamás** se persiste (ni encriptada).

### 7.2. Ciclo de vida de `ELECCION`

Estados: `BORRADOR → CONFIGURADA → ABIERTA → CERRADA → ESCRUTADA`.

- En estado `BORRADOR`: **prohibido** desplegar o escribir en blockchain (Sepolia).
- Transiciones de estado deben validarse en backend y reflejarse en documentación si cambian reglas.

### 7.3. Anti-doble-voto y re-voto

- `NULLIFIER = hash(clavePublica + idEleccion)`.
- Política `LAST_VOTE_WINS` cuando `permitirVotoMultiple = true`.
- Registrar `REGISTRO_NULLIFIER` off-chain y en smart contract.

### 7.4. Sanitización y validación

- Sanitizar inputs de texto (prevención SQL injection / XSS).
- Validar rangos de fechas: apertura en futuro, cierre > apertura → HTTP 422 en inconsistencias.
- Endpoints protegidos con guards de autenticación/autorización según rol (`ELECTION_ADMIN`, `PAUSER`, etc.).

### 7.5. Actores

| Rol | Capacidades |
|---|---|
| **Autoridad Electoral** | Gestión completa del comicio |
| **Votante** | Autenticado vía SSO; nunca vinculado estructuralmente a su voto |
| **Observador / Auditor** | Solo lectura y auditoría |

---

## 8. Git: ramas y commits

### 8.1. Estrategia de branching (GitHub Flow simplificado)

| Rama | Propósito |
|---|---|
| `master` | Producción. Solo merges vía PR desde `dev`. |
| `dev` | Integración continua. Destino de features. |
| `feature/[nombre]` | Nueva funcionalidad por US. Ej: `feature/votar-313-login-autoridad` |
| `fix/[nombre]` | Corrección de bugs. |
| `docs/[nombre]` | Solo documentación. |

**Reglas:**

- Ningún merge directo a `master` sin PR.
- Todo PR requiere aprobación de **al menos un integrante** distinto al autor.
- PR debe pasar **tests automatizados** antes del merge.
- **No hacer push** salvo solicitud explícita del usuario.

### 8.2. Convención de commits

**Formato:**

```
<tipo>[scope]: <descripción en imperativo>
```

| Tipo | Uso |
|---|---|
| `feat` | Nueva funcionalidad para el usuario |
| `fix` | Corrección de error |
| `perf` | Mejora de rendimiento |
| `build` | Build, dependencias, despliegue |
| `ci` | Integración continua |
| `docs` | Documentación |
| `refactor` | Refactor sin cambio funcional |
| `test` | Pruebas nuevas o refactor de tests |

**Scope** (opcional): módulo o capa. Ejemplos: `backend`, `frontend`, `padron`, `eleccion`, `blockchain`, `diagramas`.

**Verbos imperativos sugeridos:** Add, Change, Update, Upgrade, Fix, Remove.

**Ejemplos válidos:**

```
feat(padron): add CSV import endpoint with Keccak-256 anonymization
fix(auth): change token expiry comparison to inclusive bound
refactor(eleccion): rename estado field for consistency
docs(diagramas): update Sprint 1 ER diagram with MerkleTree entity
build(backend): upgrade typeorm to 0.3.20
test(padron): add assertion for plaintext absence in padron rows
feat(api): document eleccion endpoints with Swagger decorators
```

**Atomicidad:** un commit = un cambio lógico. Separar `feat`, `test` y `docs` cuando sea razonable.

---

## 9. Pruebas

### 9.1. Backend — Jest

- Archivos: `*.spec.ts` colocados junto al código bajo prueba (`src/`).
- Patrón **Arrange – Act – Assert**.
- Nombrar variables: `inputX`, `mockX`, `expectedX`, `actualX`.
- Cubrir como mínimo:
  - **Flujo feliz** de la US.
  - **Casos de error** explícitos en criterios de aceptación (HTTP 422, 401, 403, etc.).
  - **Reglas de negocio** críticas (estados de elección, validaciones temporales, anonimización).
- Ejecutar test específico: `npx jest --testPathPattern=nombre.spec.ts`
- Objetivo: los casos principales de la US deben tener cobertura; no escribir tests triviales que no aporten valor.

### 9.2. Backend — E2E

- Ubicación: `test/*.e2e-spec.ts`
- Usar para flujos HTTP completos cuando la US lo requiera.
- Ejecutar: `npm run test:e2e`

### 9.3. Frontend

- Al incorporar framework de testing (Vitest/Jest), seguir el mismo criterio: flujo feliz + errores de la US.
- Mientras no exista suite configurada, documentar **casos de prueba manual** derivados de los criterios de aceptación.

### 9.4. Smart contracts

- Pruebas locales con Hardhat/Ganache antes de Testnet.
- Verificar despliegue en Sepolia sin errores.
- Documentar dirección del contrato desplegado cuando aplique.

### 9.5. Trazabilidad con Jira

- Los tests deben mapear a **criterios de aceptación** y **pruebas de usuario** de la US.
- En el resumen de la tarea, indicar qué criterio cubre cada test relevante.

---

## 10. Documentación Swagger (obligatoria en backend)

Todo endpoint **nuevo o modificado** en un `*.controller.ts` debe documentarse con `@nestjs/swagger` **antes de dar por cerrada la tarea**.

### 10.1. Decoradores requeridos

**En el controlador:**

```typescript
@ApiTags('nombre-recurso')
@Controller('recurso')
export class RecursoController {}
```

**En cada método HTTP:**

```typescript
@ApiOperation({ summary: 'Descripción breve del endpoint' })
@ApiResponse({ status: 200, description: 'OK', type: ResponseDto })
@ApiResponse({ status: 400, description: 'Bad Request' })
@ApiResponse({ status: 401, description: 'Unauthorized' })
@ApiResponse({ status: 422, description: 'Unprocessable Entity' })
```

**Según corresponda:**

| Decorador | Cuándo |
|---|---|
| `@ApiBody({ type: CreateDto })` | POST, PUT, PATCH con body |
| `@ApiParam({ name, type })` | Parámetros de ruta |
| `@ApiQuery({ name, type, required })` | Query params |
| `@ApiBearerAuth()` | Endpoints protegidos con JWT |

### 10.2. DTOs

- Propiedades expuestas en Swagger deben tener `@ApiProperty()` (o `@ApiPropertyOptional()`).
- Usar `type`, `example` y `description` cuando ayuden al consumidor de la API.

### 10.3. Verificación

- Confirmar que el endpoint aparece en la UI de Swagger (`/api` o ruta configurada en `main.ts`).
- Responses documentados deben coincidir con los códigos HTTP reales del servicio.

---

## 11. Qué evitar

- **Alcance no solicitado:** no refactorizar, renombrar o “mejorar” código ajeno a la US.
- **Commits/push no pedidos:** solo cuando el usuario lo solicite.
- **Secretos en repo:** usar `.env` (referenciar `.env.example`).
- **Violaciones de privacidad:** FK votante↔voto, persistir MerkleProof, guardar claves privadas.
- **Escritura en blockchain en BORRADOR.**
- **Editar diagramas sin versionar** en la carpeta del sprint correspondiente.
- **Endpoints sin Swagger.**
- **Merge sin tests pasando.**
- **Archivos markdown no solicitados** (README, docs extra) salvo que la tarea lo requiera.

---

## 12. Plantilla de entrega del agente

Al finalizar una tarea, el agente debe reportar:

```markdown
## Tarea: [ID Jira — título]

### Implementado
- [bullets concretos]

### Tests
- [ ] `npm run test` — OK / FAIL
- [ ] `npm run lint` — OK / FAIL
- Casos cubiertos: [listar]

### Swagger
- [ ] Endpoints documentados: [listar rutas o N/A]

### Diagramas
- [ ] Actualizados: [archivo nuevo o N/A]

### Commits sugeridos
- `feat(modulo): add ...`
- `test(modulo): add ...`

### Pendiente manual
- [ ] Abrir PR hacia `dev`
- [ ] Actualizar estado en Jira
- [ ] Deploy Sepolia (si aplica)
```

---

## 13. Referencias cruzadas

| Tema | Documento |
|---|---|
| Arquitectura y flujo de voto | `Contexto/claude/CLAUDE.md` |
| DoD y Scrum | `Contexto/md/03 ... Ciclo de Vida ... v2.0.2.md` §1 |
| Commits y branching | `Contexto/md/03 ... Ciclo de Vida ... v2.0.2.md` §Plan de Gestión de la Configuración |
| Reglas de negocio | `Contexto/md/01 ... Propuesta y Alcance ... v2.1.0.md` |
| Historias de usuario | Jira + `Contexto/md/01 ... Sprint 0 ... v1.8.3.md` |
| Diagramas por sprint | `Contexto/diagramas/sprint-N/` |
| Hook Swagger (Claude Code) | `Contexto/claude/.claude/hookify.require-swagger-docs.local.md` |

---

*Versión: 1.0.0 — Equipo Five stack (PFISI 2026)*
