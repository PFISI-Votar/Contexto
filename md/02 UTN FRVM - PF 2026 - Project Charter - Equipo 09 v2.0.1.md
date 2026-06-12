

*INGENIERÍA EN SISTEMAS DE INFORMACIÓN*  
*Quinto año*

CÁTEDRA:  
Proyecto Final \- Ingeniería en Sistemas de Información

**Project Charter**

DOCENTES:  
Ing. Christian Villafañe  
Ing. Matías Cassani

EQUIPO: Five stack

ALUMNOS:

Liendo, Alejo.			Legajo N° 15074		[alejoliendo2004@gmail.com](mailto:alejoliendo2004@gmail.com)  
Lucarelli, Bruno.		Legajo N° 14988		[brunolucarelli5@gmail.com](mailto:brunolucarelli5@gmail.com)	  
Magni, Gastón.		Legajo N° 14991		[gastonmagni@hotmail.com](mailto:gastonmagni@hotmail.com)  
Mosconi, Ignacio.		Legajo N° 15288		[ignamosconi@gmail.com](mailto:ignamosconi@gmail.com)   
Terreno, Valentino.		Legajo N° 15079		[ninot2016@gmail.com](mailto:ninot2016@gmail.com)

Universidad Tecnológica Nacional \- Facultad Regional Villa María  
*4 de Mayo de 2026*

# **ÍNDICE** {#índice}

**[ÍNDICE	2](#índice)**

[**CONSIGNA	3**](#consigna)

[**HISTORIAL DE REVISIONES	4**](#historial-de-revisiones)

[**DESARROLLO	5**](#desarrollo)

[Nombre y descripción del proyecto	5](#nombre-y-descripción-del-proyecto)

[Justificación / Propósito del proyecto	5](#nombre-y-descripción-del-proyecto)

[Objetivo del proyecto	5](#nombre-y-descripción-del-proyecto)

[Fechas y plazos del proyecto	5](#nombre-y-descripción-del-proyecto)

[Director del proyecto	6](#nombre-y-descripción-del-proyecto)

[Sponsors y principales Stakeholders	6](#nombre-y-descripción-del-proyecto)

[Criterios de éxito generales	6](#nombre-y-descripción-del-proyecto)

[Requerimientos de alto nivel	7](#requerimientos-de-alto-nivel)

[Funcionales	7](#funcionales)

[No funcionales	7](#nombre-y-descripción-del-proyecto)

[Presupuesto general	7](#nombre-y-descripción-del-proyecto)

[Riesgos generales	8](#nombre-y-descripción-del-proyecto)

[Hitos principales	8](#nombre-y-descripción-del-proyecto)

[Supuestos y restricciones	9](#nombre-y-descripción-del-proyecto)

[Supuestos	9](#nombre-y-descripción-del-proyecto)

[Restricciones	9](#restricciones)

# 

# **CONSIGNA** {#consigna}

En este documento se presenta una guía que ilustra los ítems que deberían ser considerados por los equipos de Proyecto Final para definir el Acta de Constitución del proyecto. Cada equipo deberá elaborar un documento que incluirá, entre otros temas, los siguientes

ítems:

* Carátula: con identificación de UTN FRVM – Carrera – Cátedra – Curso – Equipo – Año – Integrantes – Docentes.  
* Índice.  
* Historial de revisiones.  
* Nombre del proyecto con una breve descripción.  
* Breve descripción del proyecto  
* Justificación o propósito del proyecto.  
* Objetivo del proyecto.  
* Fecha de inicio y plazos (estimados).  
* Director del proyecto.  
* Sponsor y principales stakeholders del proyecto.  
* Criterios de éxito generales.  
* Requerimientos de alto nivel.  
* Presupuesto general.  
* Riesgos generales.  
* Hitos principales.  
* Supuestos y restricciones.

# **HISTORIAL DE REVISIONES** {#historial-de-revisiones}

A través de la siguiente tabla puede consultarse la evolución del documento presentado. El versionado sigue el código **\[a\].\[b\].\[c\]**, donde:

* \[**a**\] representa el número de versión del documento, y será incrementado con cada devolución de los profesores. De esta forma, la primera vez que enviamos el documento, a \= 1\. Si un profesor realiza correcciones, las aplicaremos y enviaremos la versión a \= 2, y así sucesivamente.  
* \[**b**\] representa un incremento realizado al documento dentro de una determinada versión \[**a**\]; es decir tras desarrollar títulos o secciones nuevas del informe.  
* \[**c**\]  representa una revisión por parte del equipo de trabajo a un incremento \[**b**\] realizado previamente. Es decir, correcciones propias del equipo, donde la cátedra no intervino. 

| Versión | Fecha | Autor/es | Descripción |
| :---: | :---: | :---: | ----- |
| *1.0.0* | *20/04/26* | *Gastón Magni* | Creación inicial del documento. Planteo de títulos a completar. Formato general del documento. |
| *1.1.0* | *20/04/26* | *Gastón Magni* | Secciones de Justificación, Objetivo y Fechas de Entrega del proyecto. |
| *1.2.0* | *20/04/26* | *Valentino Terreno* | Secciones de Director del proyecto, Principales Stakeholders y Criterios de éxito generales. |
| *1.3.0* | *20/04/26* | *Bruno Lucarelli* | Secciones de Requerimientos de alto nivel, Presupuesto general y riesgos generales. |
| *1.4.0* | *20/04/26* | *Alejo Liendo* | Secciones de Nombre y descripción del proyecto, Hitos principales, Supuestos y restricciones. |
| *1.4.1* | *20/04/26* | *Ignacio Mosconi* | Revisión del documento. |
| *1.4.2* | *21/04/26* | *Valentino Terreno* | Revisión completa del documento.  |
| *2.0.0* | *04/05/26* | *Bruno Lucarelli* | Correcciones en Presupuesto general e Hitos principales según feedback del docente. |
| *2.0.1* | *04/05/26* | *Ignacio Mosconi* | Verificación de correcciones realizadas en v2.0.0 |

# **DESARROLLO** {#desarrollo}

## **Nombre y descripción del proyecto** {#nombre-y-descripción-del-proyecto}

| Nombre | VOTAR |
| :---- | :---- |
| **Nombre completo** | **VOTAR \- Plataforma de Votación Electrónica con Tecnología Blockchain** |

VOTAR es una plataforma de software de código abierto orientada a digitalizar procesos electorales de pequeña y mediana escala (centros de estudiantes, consejos directivos, empresas, cooperativas, sindicatos y organismos públicos), garantizando seguridad criptográfica, transparencia e inmutabilidad de los resultados mediante tecnología blockchain.

La plataforma resuelve las principales falencias de los sistemas de votación actuales: falta de trazabilidad extremo a extremo (E2E), riesgo de manipulación centralizada, ausencia de verificación individual del votante y exclusión digital. Lo hace mediante una arquitectura híbrida compuesta por contratos inteligentes (smart contracts), autenticación con desvinculación criptográfica de identidad (Árboles de Merkle \+ billetera efímera ECC), y una Boleta Única Digital (BUD) de interfaz intuitiva. 

## **Justificación / Propósito del proyecto**

Los sistemas de votación actuales (papel y electrónicos centralizados) presentan vulnerabilidades estructurales que comprometen la integridad y la confianza pública en los procesos democráticos: servidores centralizados como punto único de fallo, imposibilidad de auditoría ciudadana independiente, riesgo de coerción en votación remota y tensión irresuelta entre anonimato y auditabilidad.

VOTAR responde a esta necesidad mediante un sistema que garantiza matemáticamente la integridad del sufragio, permitiendo a cualquier ciudadano auditar el proceso en tiempo real sin necesidad de confiar en intermediarios, y al votante verificar individualmente que su voto fue registrado y contabilizado. 

## **Objetivo del proyecto**

Desarrollar e implementar una plataforma de votación electrónica de código abierto basada en blockchain que permita a organizaciones de pequeña y mediana escala llevar adelante procesos electorales seguros, transparentes, auditables y con verificabilidad extremo a extremo (E2E), cumpliendo con los marcos legales argentinos vigentes (Ley N° 25506 de Firma Digital y Ley N° 25326 de Protección de Datos Personales).

## **Fechas y plazos del proyecto**

| Fecha de inicio | 27 de Abril de 2026 |
| :---- | :---- |
| **Fecha de finalización** | Noviembre de 2026 |
| **Duración estimada** | 34 semanas (≈ 8 meses) |

## **Director del proyecto**

| Director del proyecto | Ignacio Mosconi |
| :---- | :---- |
| **Sponsor del proyecto** | Ing. Christian Villafañe e Ing. Matías Cassani |

## **Sponsors y principales Stakeholders**

| Interesado | Rol / Relación | Interés principal |
| :---- | :---- | :---- |
| Equipo Five Stack | Equipo de desarrollo | Entregar el producto con calidad |
| Cátedra (Villafañe/Cassani) | Sponsor / Evaluadores | Cumplimiento académico y técnico |
| CEUTI \- UTN FRVM | Usuario piloto / cliente | Digitalizar sus elecciones estudiantiles |
| Votantes | Usuarios finales | Garantía de secreto e integridad del voto |
| Autoridad electoral | Operador del sistema | Gestión segura del comicio |
| Observadores externos | Auditores públicos | Transparencia y acceso a resultados |

## **Criterios de éxito generales**

* El sistema permite realizar un proceso electoral completo en un entorno simulado de la organización piloto (CEUTI) sin incidentes de integridad.  
* Cada votante puede verificar individualmente, mediante su recibo criptográfico, que su voto fue contabilizado.  
* El Dashboard Público muestra resultados en tiempo real auditables por cualquier observador externo.  
* La plataforma es operativa sobre red Testnet (Sepolia) y el equipo documenta el path de migración a Mainnet.  
* El código fuente se publica bajo licencia open source con documentación técnica suficiente para que otra institución pueda adoptarlo.  
* El proyecto se entrega dentro del plazo académico establecido con todos los entregables requeridos por la cátedra.

## **Requerimientos de alto nivel** {#requerimientos-de-alto-nivel}

#### **Funcionales** {#funcionales}

* Gestión de padrón electoral: carga, validación y publicación (*de libre acceso*) de votantes habilitados.  
* Autenticación institucional mediante OAuth 2.0 / OpenID Connect con desvinculación criptográfica de identidad (billetera efímera ECC \+ Árbol de Merkle).  
* Emisión de voto múltiple: el votante puede votar más de una vez; solo se computará el último sufragio registrado.  
* Registro inmutable de votos en blockchain mediante smart contracts (Solidity / Ethereum).  
* Emisión de recibo criptográfico por cada sufragio para verificación E2E individual.  
* Dashboard Público con resultados en tiempo real, sin autenticación requerida.  
* Panel de Administración para configuración del comicio, gestión del padrón y generación de reportes.  
* Soporte para voto en blanco y contabilización diferenciada de votos nulos.

#### **No funcionales**

* Seguridad: ningún actor (incluyendo administradores) puede vincular un voto a la identidad de su emisor.  
* Unicidad del voto: todos los votantes podrán emitir múltiples votos, pero únicamente el último emitido dentro del lapso del comicio contará para el conteo.  
* Inmutabilidad: una vez registrado en la blockchain, ningún voto puede ser modificado ni eliminado.  
* Transparencia: el código fuente es open source e inspeccionable por cualquier interesado.  
* Usabilidad: la interfaz abstrae toda la complejidad criptográfica, presentando una experiencia equivalente a cualquier formulario digital moderno.  
* Cumplimiento legal: la plataforma opera bajo la Ley N° 25506 (Firma Digital) y Ley N° 25326 (Protección de Datos Personales).

## **Presupuesto general**

| Concepto | Descripción |
| :---- | :---- |
| Infraestructura \- Testnet | Nodo RPC en Sepolia (Infura/Alchemy free tier) |
| Licencias y herramientas | Todas open source / free tier |
| Equipamiento | Hardware personal propio del equipo |
| Gas fees (Testnet) | Tokens de prueba gratuitos (faucet Sepolia) |
| Horas hombre | Costo de realizar el trabajo y desarrollar el producto, según la cantidad de personas que lo hagan. |

## **Riesgos generales**

| Riesgo | Causa → Efecto | Respuesta preliminar |
| :---- | :---- | :---- |
| R1 \- Planificación | Si el equipo subestima la complejidad del stack blockchain+backend+frontend, no se podrán cumplir las fechas de entrega académicas. | Realizar revisiones de avance quincenales y ajustar el alcance tempranamente. |
| R2 \- Capacitación técnica | Si algún integrante no adquiere las competencias en Solidity / ECC / OAuth 2.0 para el plazo requerido, la arquitectura central podría quedar sin implementar. | Asignar un plan de capacitación individual por área técnica desde el inicio del proyecto. |
| R3 \- Disponibilidad Testnet | Si la red Sepolia presenta inestabilidad o los faucets restringen tokens de prueba, el desarrollo y las demos podrían verse afectados. | Mantener entornos de prueba locales (Hardhat/Ganache) como respaldo. |
| R4 \- Barrera regulatoria | Si la institución piloto (CEUTI) no valida formalmente el uso del sistema, la demo real podría no concretarse dentro del plazo. | Planificar ejecución de demostración en un entorno simulado, que imite condiciones reales. |
| R5 \- Seguridad (SSO) | Si el sistema de autenticación institucional es vulnerado, se podrían generar pruebas de Merkle ilegítimas antes de la votación. | Implementar validación de estado del certificado en tiempo real y monitoreo de anomalías. |

## **Hitos principales**

| Hito | Descripción | Semana estimada |
| :---- | :---- | ----- |
| H1 \- Kick-off | Project Charter aprobado. Alcance definido. Repositorio Git inicializado. | Sem. 1-3 |
| H2 \- Gestión de interesados | Plan de gestión de interesados finalizado. | Sem. 4-6 |
| H3 \-  Alcance completo | Documento de alcance entregado: EDT, scope statement, supuestos, gestión de configuración. | Sem. 7-8 |
| H4 \- Cronograma | Elaboración y validación del cronograma del proyecto, incluyendo la definición de sprints, duración, hitos principales y calendarización de ceremonias Scrum. | Sem. 9 |
| H5 \- Riesgos identificados | Registro de riesgos completo. Plan de comunicaciones aprobado. | Sem. 10 |
| H6 \- Arquitectura base | Smart contracts desplegados en Testnet. Backend funcional. Árbol de Merkle operativo. | Sem. 11-17 |
| H7 \- MVP funcional | Flujo completo de votación E2E: autenticación → emisión → recibo → dashboard público. | Sem. 18-23 |
| H8 \- Demo piloto | Proceso electoral de prueba realizado en entorno CEUTI o simulado. Resultados auditados. | Sem. 24-28 |
| H9 \- Producto final | Plataforma completa. Código publicado open source. Documentación técnica entregada. | Sem. 29-32 |
| H10 \- Cierre | Documentación de tomos presentada. Presentación final ante la cátedra. Cierre del proyecto. | Sem. 33-34 |

## **Supuestos y restricciones** 

#### **Supuestos**

* La red Ethereum Testnet (Sepolia) estará disponible durante todo el período de desarrollo.  
* Podremos disponer del sistema de autenticación institucional e integrarlo via OAuth 2.0 de la institución piloto (CEUTI / UTN FRVM).  
* El equipo cuenta con dispositivos personales con conexión a internet adecuados para el desarrollo.  
* La cátedra mantendrá el cronograma de entregas publicado en el campus virtual sin modificaciones estructurales.  
* El marco legal vigente (Ley N° 25506 y Ley N° 25326\) se mantiene sin cambios sustanciales durante el proyecto.

#### **Restricciones** {#restricciones}

* El presupuesto está enfocado de manera tal que el único gasto sea en infraestructura y de manera mínima.  
* El despliegue de producción queda limitado a redes Testnet durante el ciclo académico; la migración a Mainnet excede el alcance del proyecto.  
* La plataforma no tiene alcance para procesos electorales gubernamentales con efectos jurídicos ante el Estado (requiere certificación normativa adicional).  
* Todo el stack tecnológico debe ser open source o de uso gratuito.