# VOTAR — Contexto del Sistema para Consulta IA

> Documento de referencia rápida para agentes IA. Sintetiza toda la documentación del proyecto.
> Última actualización: 2026-06-12 | Equipo: Five Stack | UTN FRVM

---

## 1. Identificación del Proyecto

| Campo | Valor |
|---|---|
| Nombre corto | **VOTAR** |
| Nombre completo | VOTAR – Plataforma de Votación Electrónica con Tecnología Blockchain |
| Institución | UTN FRVM – Ingeniería en Sistemas de Información, 5° año |
| Cátedra | Proyecto Final ISI |
| Docentes | Ing. Christian Villafañe, Ing. Matías Cassani |
| Equipo | Five Stack |
| Director del proyecto | Ignacio Mosconi |
| Inicio | 27/04/2026 |
| Fin estimado | Noviembre 2026 (~34 semanas) |

### Integrantes

| Nombre | Legajo | Email |
|---|---|---|
| Liendo, Alejo | 15074 | alejoliendo2004@gmail.com |
| Lucarelli, Bruno | 14988 | brunolucarelli5@gmail.com |
| Magni, Gastón | 14991 | gastonmagni@hotmail.com |
| Mosconi, Ignacio | 15288 | ignamosconi@gmail.com |
| Terreno, Valentino | 15079 | ninot2016@gmail.com |

---

## 2. Descripción y Propósito

VOTAR es una plataforma **open source** para digitalizar procesos electorales de **pequeña y mediana escala** (centros de estudiantes, consejos directivos, empresas, cooperativas, sindicatos, organismos públicos), garantizando:

- Seguridad criptográfica
- Transparencia e inmutabilidad (blockchain)
- Verificabilidad extremo a extremo (E2E)
- Anonimato del votante (desvinculación criptográfica identidad→voto)

**Caso piloto:** Centro de Estudiantes CEUTI – UTN FRVM.

**Problemas que resuelve:**
1. Falta de trazabilidad E2E en sistemas actuales ("caja negra")
2. Punto único de fallo por bases de datos centralizadas
3. Imposibilidad de verificación individual sin comprometer anonimato
4. Riesgo de coerción / compra de votos (mitigado con voto múltiple)
5. Centralización manipulable de resultados
6. Exclusión digital por interfaces complejas

---

## 3. Alcance

### Incluido
- Gestión de padrón electoral (carga CSV, hash Keccak-256, Árbol de Merkle)
- Autenticación institucional OAuth 2.0 / OIDC con desvinculación criptográfica
- Emisión de voto múltiple (solo el último cuenta — `LAST_VOTE_WINS`)
- Registro inmutable en blockchain (smart contracts Solidity / Ethereum Sepolia)
- Recibo criptográfico por sufragio (verificación E2E individual)
- Dashboard Público de resultados en tiempo real (sin autenticación)
- Panel de Administración (configuración de comicios, gestión de padrón, reportes)
- Voto en blanco y contabilización separada de votos nulos
- Despliegue en **Testnet Sepolia** (producción en Mainnet fuera del alcance académico)

### Excluido
- Migración a Mainnet
- Comicios gubernamentales con efectos jurídicos ante el Estado
- Certificación normativa adicional para uso estatal

---

## 4. Arquitectura del Sistema

### 4.1 Diagrama de contexto (nivel 1)

```
[Votante] ──────────────────────────────────────────────────►
[Autoridad Electoral] ──────────────────────────────────────►  [ PLATAFORMA VOTAR ]
[Auditor] ───────────────────────────────────────────────────►
                                                                      │
                                                          ┌───────────┼───────────┐
                                                          ▼           ▼           ▼
                                               [SSO Institucional] [RPC Nodo] [Ethereum]
                                               OAuth 2.0/OIDC     Infura/     Sepolia
                                                                   Alchemy     Testnet
```

### 4.2 Contenedores (nivel 2)

| Contenedor | Tecnología | Descripción |
|---|---|---|
| **BUD** (Boleta Única Digital) | React.js / Ethers.js | Frontend de votación y firma criptográfica |
| **Panel de Administración** | React.js | Gestión institucional del padrón y comicios |
| **Dashboard Público** | React.js / Ethers.js | Auditoría ciudadana, resultados en tiempo real |
| **API Backend** | Node.js (Express) / Python (FastAPI) | Motor off-chain: Merkle, reglas electorales, desvinculación de identidad |
| **Base de Datos** | PostgreSQL 16 | Persistencia off-chain (configuración, padrón hasheado, audit log). **NO almacena votos ni PII** |
| **Ecosistema On-Chain** | Solidity ^0.8.24 / OpenZeppelin v5 | Smart contracts de lógica electoral inmutable |

### 4.3 Componentes clave del API Backend

| Componente | Rol |
|---|---|
| `jwtValidator` | Valida tokens SSO (OAuth2/OIDC) contra JWKS |
| `identityDecoupler` | Separa criptográficamente identidad→voto (Ley 25.326) |
| `merkleBuilder` | Construye Merkle Tree (keccak256), genera proofs bajo demanda |
| `voterCsvProcessor` | Parsea CSV, deduplica, hashea votantes |
| `rulesEngine` | Valida reglas de negocio electorales |
| `revotePolicyService` | Gestiona política de voto múltiple |
| `lifecycleManager` | Ciclo de vida del comicio (apertura/cierre/archivado) |
| `auditLogger` | Registro append-only de acciones críticas |

### 4.4 Smart Contracts (On-Chain)

| Contrato | Rol |
|---|---|
| `ElectionFactory.sol` | Despliega conjunto de contratos por comicio. Patrón UUPS Proxy Factory |
| `BallotContract.sol` | Orquesta `castVote()`: valida Merkle Proof, firma ECDSA, política re-voto. Patrón CEI + ReentrancyGuard |
| `VoteRegistry.sol` | Estado canónico de sufragios por nullifier. Soporta sobrescritura (LAST_WINS) |
| `TallyContract.sol` | Contadores incrementales por candidato. Resultados en tiempo real |
| `AuditViewContract.sol` | Funciones `view/pure` para auditores externos (no muta estado) |
| `MerkleRootStore.sol` | Almacena y versiona Merkle Roots publicadas por la autoridad |
| OZ: `MerkleProof.sol` | Verifica pertenencia al árbol (OpenZeppelin v5) |
| OZ: `ECDSA.sol` | Recupera firmante del payload del voto (Ley 25.506) |
| OZ: `AccessControl.sol` | RBAC vía `VotarAccessControl`: `DEFAULT_ADMIN_ROLE`, `PAUSER_ROLE`, `MERKLE_UPDATER_ROLE`, `BALLOT_ROLE` (US-349) |
| OZ: `Pausable.sol` | Circuit breaker en `castVote()` |

---

## 5. Flujo de Emisión de Sufragio (E2E)

```
[Autoridad]
  0a. Solicita publicación de Merkle Root
  0b. Panel → RPC → MerkleRootStore.sol (almacena root on-chain)

[Votante]
  1. Inicia sesión → BUD.auth → SSO (OAuth2/OIDC)
  2. Backend valida JWT, ejecuta identityDecoupler
  3. merkleBuilder genera MerkleProof individual (off-chain)
  4. BUD recibe MerkleProof
  5. cryptoEngine genera billetera efímera ECC (Web Crypto API)
     → firma sufragio ECDSA
     → calcula nullifier = H(clavePublica, idEleccion)
  6. blockchainClient envía castVote(payload, sig, proof) → RPC → BallotContract
  7. BallotContract:
     a. Consulta MerkleRoot activa
     b. MerkleProof.verify(proof, root, leaf) ← verifica padrón
     c. ECDSA.recover(payload, sig) ← verifica Firma Digital (Ley 25.506)
     d. Valida política re-voto (RevoteConfig)
     e. VoteRegistry.sol: registra/sobrescribe por nullifier (LAST_WINS)
     f. TallyContract: actualiza contadores por delta
     g. Emite VoteCast(electionId, nullifier, candidateId, isOverwrite)
  8. Votante recibe recibo criptográfico (hash tx + código verificación)
```

**Invariante clave:** En ningún momento existe una FK persistente entre la identidad del votante y su voto. La clave privada de la billetera efímera **nunca se persiste** (se genera en el navegador y se destruye post-firma).

---

## 6. Modelo de Datos (off-chain — PostgreSQL)

### Entidades principales

| Entidad | Descripción |
|---|---|
| `ELECCION` | Comicio: nombre, descripción, fechas, estado (`BORRADOR→CONFIGURADA→ABIERTA→CERRADA→ESCRUTADA`) |
| `CONFIGURACION_COMICIO` | Parámetros: voto múltiple, max intentos, intervalo mínimo, política de cómputo |
| `BOLETA` | Boleta electoral vinculada a una elección |
| `CATEGORIA` | Cargo/categoría dentro de la boleta (ej. Presidente, Vocales) |
| `LISTA` | Agrupación/lista electoral |
| `CANDIDATO` | Candidato dentro de una lista y categoría |
| `PADRON_ELECTORAL` | Metadatos del padrón (hash SHA-256, total habilitados, estado) |
| `PADRON_VOTANTE` | Hoja del árbol de Merkle: almacena solo `hash_hoja` (keccak-256). **Sin PII** (Ley 25.326) |
| `MERKLE_TREE` | Árbol de Merkle: raíz, total hojas, versión, estado |
| `VOTANTE` | Email institucional + SSO identifier. Separado del voto |
| `AUTORIDAD_ELECTORAL` | Rol: `ELECTION_ADMIN`, `PAUSER`, `MERKLE_UPDATER` |
| `OBSERVADOR` | Tipo: `FISCAL`, `AUDITOR_PUBLICO`, `VEEDOR` |
| `SMART_CONTRACT_ELECCION` | Referencia off-chain al deployment: address, merkle_root, red, tx_hash |
| `VOTO` | Anónimo. Sin FK a VOTANTE. Hash voto, firma, nullifier, tipo, `computado`, `es_ultimo` |
| `VOTO_DETALLE` | Candidato seleccionado por categoría en cada voto |
| `BILLETERA_EFIMERA` | Solo clave pública ECC. Clave privada nunca persiste |
| `TRANSACCION_BLOCKCHAIN` | Hash tx, bloque, estado, gas usado |
| `RECIBO_VOTACION` | Código de verificación E2E para el votante |
| `REGISTRO_NULLIFIER` | Motor off-chain anti-doble voto. Rastreo por nullifier (no por identidad) |
| `AUDIT_LOG` | Bitácora append-only de eventos críticos |
| `RESULTADO_ELECCION` | Agregado del escrutinio (off-chain): votos por candidato/lista/categoría |

> **Nota Sprint 1:** `PADRON_VOTANTE` ya no referencia `VOTANTE`. Solo persiste `hash_hoja` (keccak-256). Cambio aplicado en US-330.

---

## 7. Reglas de Negocio

| Regla | Descripción |
|---|---|
| Padrón previo | Solo votantes del padrón pueden sufragar |
| Unicidad del voto | Múltiples emisiones permitidas; solo el **último** cuenta |
| Voto en blanco | Opción válida y contabilizable |
| Voto nulo | Registrado y contabilizado por separado |
| Roles | `ELECTION_ADMIN` / `VOTANTE` / `OBSERVADOR` — sin cruce de permisos |
| Bajas de listas | Prohibidas una vez oficializadas |
| Mínimo de candidatos | Configurado por comicio; lista sin mínimo no participa |
| Inmutabilidad | Voto en blockchain: ni autoridades pueden modificarlo |
| Recibo criptográfico | Cada sufragio emite recibo para verificación E2E |
| Desvinculación | Identidad separada del voto post-autenticación |
| Escrutinio público | Disponible en tiempo real sin autenticación |
| Auditabilidad | Todo on-chain es auditable por observadores externos |
| Publicidad del padrón | Total de habilitados público antes del inicio |

---

## 8. Marco Legal

| Ley | Impacto |
|---|---|
| **Ley 25.326** – Protección de Datos Personales | Prohíbe almacenar PII en blockchain. Arquitectura resuelve con hashes y billeteras efímeras (disociación de datos nativa) |
| **Ley 25.506** – Firma Digital | Voto instrumentado como Firma Digital (ECDSA). Equivale a firma manuscrita. Presunción de autoría e integridad |
| **Ley 24.521** – Educación Superior | Cumplimiento para uso en centros de estudiantes universitarios |
| **Ley 23.551** – Asociaciones Sindicales | Dashboard de escrutinio satisface requisitos del Ministerio de Trabajo |
| ISO/IEC 27000 | Referencia para seguridad de infraestructura crítica |

---

## 9. Stack Tecnológico

| Capa | Tecnología |
|---|---|
| Frontend | React.js, Ethers.js, Web Crypto API, Chart.js, PapaParse |
| Backend | Node.js / Express **o** Python / FastAPI, Prisma / SQLAlchemy, merkletreejs / py-merkle, Winston / structlog |
| Base de datos | PostgreSQL 16 |
| Smart contracts | Solidity ^0.8.24, OpenZeppelin v5, Hardhat / Ganache (dev local) |
| Blockchain | Ethereum Sepolia Testnet (dev/academia), Mainnet (fuera de alcance) |
| Nodo RPC | Infura / Alchemy (free tier) |
| Autenticación | OAuth 2.0 / OpenID Connect |
| Criptografía | ECC (billetera efímera), keccak-256 (hashes), ECDSA (firma voto), Merkle Tree |

---

## 10. Actores del Sistema

| Actor | Rol |
|---|---|
| **Votante** | Ciudadano empadronado. Se autentica vía SSO, emite voto(s), recibe recibo criptográfico |
| **Autoridad Electoral** | Configura comicio, gestiona padrón, publica Merkle Root on-chain, genera reportes |
| **Auditor / Observador** | Acceso de solo lectura al Dashboard Público. Verifica transacciones y escrutinio |
| **SSO Institucional** | Proveedor de identidad externo (ej. CEUTI/UTN FRVM via OAuth2/OIDC) |

---

## 11. Criterios de Éxito

1. Proceso electoral completo en entorno simulado CEUTI sin incidentes de integridad
2. Cada votante verifica su voto vía recibo criptográfico
3. Dashboard Público con resultados auditables en tiempo real
4. Plataforma operativa sobre Sepolia Testnet
5. Código publicado open source con documentación técnica suficiente para adopción por terceros
6. Entrega dentro del plazo académico con todos los entregables requeridos

---

## 12. Riesgos Principales

| ID | Riesgo | Mitigación |
|---|---|---|
| R1 | Subestimación de complejidad del stack → demora en entregas | Revisiones quincenales, ajuste temprano de alcance |
| R2 | Capacitación insuficiente en Solidity/ECC/OAuth2 | Plan individual de capacitación por área desde inicio |
| R3 | Inestabilidad de Sepolia / restricciones de faucet | Entornos locales Hardhat/Ganache como respaldo |
| R4 | CEUTI no valida formalmente el uso | Demo en entorno simulado como alternativa |
| R5 | Vulneración del SSO → Merkle proofs ilegítimas | Validación de estado de certificado en tiempo real + monitoreo |

---

## 13. Hitos del Proyecto

| Hito | Descripción | Semana |
|---|---|---|
| H1 | Kick-off, Project Charter, repo Git | Sem. 1-3 |
| H2 | Gestión de interesados | Sem. 4-6 |
| H3 | Alcance completo (EDT, scope statement) | Sem. 7-8 |
| H4 | Cronograma y sprints Scrum | Sem. 9 |
| H5 | Registro de riesgos, plan de comunicaciones | Sem. 10 |
| H6 | Smart contracts en Testnet + backend + Merkle Tree | Sem. 11-17 |
| H7 | **MVP funcional**: flujo E2E completo | Sem. 18-23 |
| H8 | **Demo piloto** en entorno CEUTI o simulado | Sem. 24-28 |
| H9 | Producto final, open source, documentación técnica | Sem. 29-32 |
| H10 | Cierre, tomos, presentación ante cátedra | Sem. 33-34 |

---

## 14. Metodología de Desarrollo

- **Ciclo de vida**: híbrido — gestión predictiva + desarrollo iterativo incremental (Scrum)
- **Sprints**: duración a definir en H4
- **Repositorio**: Git (ya inicializado)
- **Licencia**: Open Source

---

## 15. Restricciones del Proyecto

- Presupuesto: mínimo (solo infraestructura básica, todo open source / free tier)
- Hardware: equipos personales del equipo
- Despliegue de producción: limitado a Testnet durante el ciclo académico
- No aplica a procesos electorales gubernamentales con efectos jurídicos plenos

---

## 16. Antecedentes Relevantes

| Sistema | Similitud con VOTAR |
|---|---|
| **Voatz** | Blockchain + móvil + biometría. Compartimos premisa anti-centralización |
| **Agora** | Blockchain permisionada + anclaje a Bitcoin. Usaba mixnets para anonimato |
| **Follow My Vote** | Recibo criptográfico + re-voto + auditoría pública on-chain. Muy similar en diseño |

---

## 17. Notas de Arquitectura Críticas

- **La clave privada de la billetera efímera NUNCA se persiste** en ningún storage (ni BD ni blockchain). Se genera en Web Crypto API del navegador, firma el voto y se destruye.
- **Merkle Proofs NO se almacenan en BD**. Son calculados en tiempo de ejecución por el backend bajo demanda autenticada.
- **VOTO no tiene FK a VOTANTE**. El voto "nace huérfano de identidad" (diseño intencional Ley 25.326).
- **Política LAST_VOTE_WINS**: el VoteRegistry sobrescribe el candidateId del nullifier en cada re-voto mientras el comicio esté abierto. Post-cierre, inmutable.
- **Nullifier** = derivado de `H(clavePublica, idEleccion)`. Permite unicidad por comicio sin revelar identidad.
- **Sprint 1 (US-330)**: `PADRON_VOTANTE` eliminó FK a `VOTANTE`. Solo persiste `hash_hoja` (keccak-256). Cambio documentado en `diagramas/CambiosIA.md`.
