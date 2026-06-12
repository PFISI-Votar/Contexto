

*INGENIERÍA EN SISTEMAS DE INFORMACIÓN*  
*Quinto año*

CÁTEDRA:  
Proyecto Final \- Ingeniería en Sistemas de Información

**Definición del alcance de proyecto**

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
*20 de Abril de 2026*

# **ÍNDICE** {#índice}

[**ÍNDICE	2**](#índice)

[**HISTORIAL DE REVISIONES	3**](#historial-de-revisiones)

[**DESARROLLO	4**](#desarrollo)

[**Contexto y entorno de aplicación	4**](#contexto-y-entorno-de-aplicación)

[Selección del ámbito	4](#selección-del-ámbito)

[Estudio del ámbito/organización	4](#estudio-del-ámbito/organización)

[Diagnóstico del sistema de información actual	5](#diagnóstico-del-sistema-de-información-actual)

[**Planteamiento del problema y antecedentes	6**](#planteamiento-del-problema-y-antecedentes)

[Identificación de problemas y necesidades	6](#identificación-de-problemas-y-necesidades)

[► Vulnerabilidad en terminales y redes de comunicación	6](#►-vulnerabilidad-en-terminales-y-redes-de-comunicación)

[► Conflicto entre privacidad y autenticación	6](#►-conflicto-entre-privacidad-y-autenticación)

[► Falta de verificabilidad extremo a extremo (E2E)	6](#►-falta-de-verificabilidad-extremo-a-extremo-\(e2e\))

[► Riesgo de coerción y compra de votos	6](#►-riesgo-de-coerción-y-compra-de-votos)

[► Centralización y manipulación de resultados	7](#►-centralización-y-manipulación-de-resultados)

[► Brecha de usabilidad y exclusión digital	7](#►-brecha-de-usabilidad-y-exclusión-digital)

[Antecedentes	7](#antecedentes)

[**Análisis estratégico y de viabilidad	9**](#análisis-estratégico-y-de-viabilidad)

[Análisis FODA	9](#análisis-foda)

[► Fortalezas	9](#►-fortalezas)

[► Oportunidades	10](#►-oportunidades)

[► Debilidades	10](#►-debilidades)

[► Amenazas	10](#►-amenazas)

[Estudio de factibilidad	11](#estudio-de-factibilidad)

[► Factibilidad técnica	11](#►-factibilidad-técnica)

[► Factibilidad operativa	11](#►-factibilidad-operativa)

[► Factibilidad económica	12](#►-factibilidad-económica)

[► Conclusión del estudio de factibilidad	13](#►-conclusión-del-estudio-de-factibilidad)

[**Definiciones	13**](#definiciones)

[Reglas de negocio	13](#reglas-de-negocio)

[► Regulaciones que pueden afectarnos	16](#►-regulaciones-que-pueden-afectarnos)

[Propuesta de investigación/capacitación	17](#propuesta-de-investigación/capacitación)

[**BIBLIOGRAFÍA	18**](#bibliografía)

# 

# **HISTORIAL DE REVISIONES** {#historial-de-revisiones}

| Versión | Fecha | Autor / es | Descripción |
| :---: | :---: | :---: | ----- |
| *1.0.0* | *14/04/26* | *Ignacio Mosconi* | Creación inicial del documento. Planteo de títulos a completar. Formato general del documento |
| *1.1.0* | *14/04/26* | *Valentino Terreno* | Título “Descripción” completado.  |
| *1.2.0* | *14/04/26* | *Bruno Lucarelli* | Antecedentes, Análisis de Factibilidad, Regulaciones que pueden afectarnos |
| *1.3.0* | *15/04/26* | *Alejo Liendo* | Título “¿Dónde va a desarrollarse el proyecto actual?” completado. |
| *1.3.1* | *15/04/26* | *Ignacio Mosconi* | Corrección y chequeo de redacción del título “¿Dónde va a desarrollarse el proyecto actual?” |
| *1.4.0* | *16/04/26* | *Alejo Liendo* | Títulos “Ciclo de vida del proyecto” y “Enfoque de desarrollos” completados. |
| *1.5.0* | *16/04/26* | *Gastón Magni* | Reestructuración de títulos y subtítulos, más reglas de negocio. |
| *1.6.0* | *17/04/26* | *Gastón Magni* | Estudio de factibilidad y propuestas de investigación/capacitación. |
| *1.7.0* | *19/04/26* | *Gastón Magni* | Identificación de problemas y necesidades |
| *1.8.0* | *19/04/26* | *Alejo Liendo* | Estudio del ámbito/organización, Diagnóstico del sistema de información actual |
| *1.8.1* | *19/04/26* | *Valentino Terreno* | Formateo de encabezados y pies de página. Justificación de párrafos. Revisión y corrección de los siguientes títulos: Selección de ámbito, Estudio de ámbito/organización, Diagnóstico del sistema de información actual, Identificación de problemas y necesidades, Antecedentes, Análisis FODA, Estudio de factibilidad, Reglas de negocio, Propuesta de investigación/capacitación. |
| *1.8.2* | *20/04/26* | *Ignacio Mosconi* | Revisión general y correcciones de redacción y formato a lo largo de todo el documento. |
| *2.1.0* | *27/04/26* | *Valentino Terreno* | Modificación del documento en base a la revisión de la cátedra. Eliminación de título Consigna y descripción del título Historial de versiones. Corrección de errores de ortografía. Creación de título Bibliografía |

# 

# **DESARROLLO** {#desarrollo}

## **Contexto y entorno de aplicación** {#contexto-y-entorno-de-aplicación}

### Selección del ámbito {#selección-del-ámbito}

El proyecto “**VOTAR**” se enmarca en el **ámbito de la gobernanza digital y los sistemas de votación electrónica, específicamente orientado a elecciones de pequeña y mediana escala**. El sector abarca cualquier organización, pública o privada, que requiera modernizar sus procesos de elecciones mediante estándares elevados de seguridad criptográfica, transparencia e inmutabilidad.

Los contextos de aplicación que cubre la plataforma incluyen:

* **Institucional:** Elecciones de centros de estudiantes, consejos directivos o cuerpos de gobierno universitario.  
* **Empresariales:** Votaciones internas en empresas para elecciones organizacionales o de representantes gremiales.  
* **Sector público:** Procesos participativos en organismos gubernamentales o municipales.  
* **Organizaciones civiles:** Asambleas, cooperativas, sindicatos u otras entidades que requieran elecciones formales.

Como caso de aplicación concreto y representativo, el proyecto toma como ejemplo las elecciones del Centro de Estudiantes (CEUTI) de la Universidad Tecnológica Nacional \- Facultad Regional Villa María (UTN FRVM). Este entorno real permite demostrar la capacidad del sistema para digitalizar el escrutinio, eliminando la dependencia de métodos manuales y proporcionando a cada elector una garantía matemática de la integridad de su voto.

### Estudio del ámbito/organización {#estudio-del-ámbito/organización}

El estudio del ámbito consiste en el análisis del entorno social, legal y operativo donde se insertará la solución tecnológica. Este análisis es fundamental para identificar las restricciones, los actores clave y los procesos actuales que el proyecto pretende optimizar.

Dado que la solución es de naturaleza **genérica y adaptable**, el estudio del ámbito se articula particularmente en un nivel general:

* Todo proceso electoral implica la existencia de un padrón (conjunto de votantes habilitados), listas o candidatos y una autoridad electoral que gestiona y valida los comicios.  
* Los procesos pueden variar en escala (decenas a miles de votantes), en la modalidad de autenticación (credenciales institucionales, DNI, correo, entre otros) y en la estructura de las listas (uninominales, plurinominales, por agrupaciones).  
* La plataforma contempla esta variabilidad mediante una arquitectura híbrida: núcleo **blockchain** inmutable, más capas de backend y frontend configurables por institución.

Una organización se entiende como un sistema social coordinado, con objetivos definidos y una estructura específica. Al estudiar la organización, el equipo de proyecto debe comprender su estructura jerárquica, sus procesos internos y las normativas que rigen su funcionamiento, transformando el contexto institucional en requerimientos técnicos precisos.

Este tipo de organizaciones (ya sean académicas, civiles o corporativas) suelen enfrentar desafíos comunes, como la logística de la presencialidad, los costos operativos de los métodos tradicionales y la dificultad para realizar auditorías externas de manera ágil. Por lo tanto, el ámbito de aplicación demanda una solución técnica capaz de adaptarse a diferentes normativas internas, aportando una capa de seguridad criptográfica que asegura la transparencia en el escrutinio.

Para aterrizar estos conceptos en requisitos técnicos reales, se considera como un escenario de validación posible el entorno del **Centro de Estudiantes (CEUTI)**. Este caso de uso permite contrastar la arquitectura del sistema con una dinámica institucional real, utilizando sus protocolos de validación de identidad como modelo para demostrar la transparencia y viabilidad de la solución en el campo.

### Diagnóstico del sistema de información actual {#diagnóstico-del-sistema-de-información-actual}

Los sistemas de votación actuales, tanto los procesos tradicionales en papel como los sistemas electrónicos centralizados, presentan un conjunto de limitaciones estructurales que “VOTAR” busca resolver:

*→ Problemas de transparencia y trazabilidad:* 

Tanto el modelo analógico (papel) como en sistemas digitales centralizados, **el procesamiento de la información carece de trazabilidad de extremo a extremo**. Actualmente, el escrutinio se comporta como una **caja negra**: el dato ingresa, pero el proceso de transformación y contenido no es auditable en tiempo real por actores externos. Esto genera una dependencia crítica de la confianza en los intermediarios, ya que no existe un mecanismo técnico que permita verificación independiente y descentralizada de los resultados.

*→ Vulnerabilidades de integridad:*

La arquitectura de información actual se basa mayoritariamente en bases de datos centralizadas. Desde la perspectiva de la seguridad, esto representa un **punto único de fallo**. Cualquier entidad con acceso privilegiado al servidor central tiene la capacidad técnica de alterar, suprimir o duplicar registros sin dejar huella inmutable (algunos ejemplos de riesgos son la alteración de resultados, el doble voto, la supresión de sufragios válidos). Esta vulnerabilidad estructural compromete la integridad del sistema ante ataques externos o manipulaciones internas, haciendo que la legitimidad del proceso sea difícil de garantizar matemáticamente. 

*→ Tensión entre anonimato y auditabilidad:*

Existe una limitación técnica en la relación entre el anonimato y la auditabilidad. En sistemas actuales, es prácticamente imposible que un votante obtenga una **confirmación de que su voto fue efectivamente contabilizado** sin comprometer el secreto del sufragio. Esta falta de herramientas de verificación individual impide que el sistema sea verdaderamente transparente para el usuario final, manteniendo la duda sobre la persistencia del dato una vez emitido.

## **Planteamiento del problema y antecedentes** {#planteamiento-del-problema-y-antecedentes}

### Identificación de problemas y necesidades {#identificación-de-problemas-y-necesidades}

Los sistemas de votación actuales, tanto los procesos tradicionales en papel como los sistemas electrónicos centralizados, presentan un conjunto de falencias estructurales que generan inseguridad tecnológica, falta de transparencia e imposibilidad de auditoría ciudadana independiente. A continuación, se detallan los problemas centrales detectados y las necesidades de información que el proyecto busca cubrir en respuesta a cada uno:

#### ► **Vulnerabilidad en terminales y redes de comunicación** {#►-vulnerabilidad-en-terminales-y-redes-de-comunicación}

Los dispositivos personales de los votantes (teléfonos o computadoras) pueden estar comprometidos por malware capaz de interceptar o modificar el voto antes de su envío, sin que el elector lo perciba. Adicionalmente, la transmisión de datos por redes públicas expone la información a ataques de intermediario (*man-in-the-middle*), interceptación y denegación de servicio (DoS). Esto genera la necesidad de implementar canales de comunicación seguros y mecanismos de verificación que permitan al votante confirmar la integridad de su sufragio independientemente del estado de su dispositivo.

#### ► **Conflicto entre privacidad y autenticación** {#►-conflicto-entre-privacidad-y-autenticación}

Existe un problema criptográfico estándar asociado a la naturaleza de este tipo de sistemas: el sistema debe identificar de forma inequívoca al elector para garantizar su legitimidad e impedir el doble voto, pero simultáneamente debe ser incapaz de vincular esa identidad con el contenido del sufragio emitido. Esto genera la necesidad de una arquitectura de autenticación híbrida que separe criptográficamente la identidad del votante del registro de su voto.

#### ► **Falta de verificabilidad extremo a extremo (E2E)** {#►-falta-de-verificabilidad-extremo-a-extremo-(e2e)}

En los sistemas vigentes, el elector pierde todo control sobre su voto en el momento en que lo emite. No existe mecanismo que le permita confirmar que su sufragio fue registrado, ni que fue contabilizado tal como fue registrado. Esta opacidad genera una dependencia de confianza ciega en los operadores del sistema. 

#### ► **Riesgo de coerción y compra de votos** {#►-riesgo-de-coerción-y-compra-de-votos}

En entornos de votación remota y no supervisada, un actor externo puede obligar al votante a votar por una opción determinada frente a la pantalla, o instrumentar la técnica del "voto en cadena" para verificar la decisión antes de liberarlo. La necesidad identificada es neutralizar la efectividad de estas prácticas mediante la implementación del voto múltiple: un mecanismo por el cual el votante puede emitir su sufragio más de una vez durante el período electoral, siendo únicamente el último voto registrado el que se computa en el escrutinio final.

#### ► **Centralización y manipulación de resultados** {#►-centralización-y-manipulación-de-resultados}

La dependencia de bases de datos centralizadas y opacas controladas por una única entidad constituye el vector de ataque más crítico de los sistemas actuales. Un actor con acceso privilegiado, interno o externo, puede manipular registros, suprimir sufragios válidos o alterar resultados sin dejar evidencia detectable. Esto genera la necesidad de reemplazar el modelo centralizado por una infraestructura inmutable y descentralizada.

#### ► **Brecha de usabilidad y exclusión digital** {#►-brecha-de-usabilidad-y-exclusión-digital}

Los sistemas que incorporan tecnología avanzada frecuentemente presentan interfaces complejas que elevan la barrera de participación y excluyen a sectores con menor familiaridad tecnológica. Una curva de aprendizaje elevada reduce la participación y genera desconfianza en el proceso, independientemente de la robustez técnica del sistema. La necesidad identificada es diseñar interfaces intuitivas que abstraigan la complejidad criptográfica subyacente, presentando al votante una experiencia equivalente a la de cualquier formulario digital moderno y fomentando la inclusión de todos los sectores demográficos.

En síntesis, las necesidades de información que el proyecto busca cubrir son: autenticación segura con desvinculación criptográfica de identidad, registro inmutable de votos en infraestructura descentralizada, verificación individual mediante recibo criptográfico con E2E, escrutinio público en tiempo real, gestión segura del padrón electoral y una interfaz accesible que garantice la inclusión de todos los participantes.

### Antecedentes {#antecedentes}

A continuación, se especifican proyectos y/o productos ya existentes en el mercado, y que comparten características similares a lo propuesto en el presente informe:

[![][image1]](https://voatz.com/)

Ecosistema de votación respaldado por tecnología DLT/blockchain, empleado en múltiples elecciones gubernamentales de Estados Unidos. 

Este producto comparte con el nuestro la premisa fundamental de mitigar vulnerabilidades y transicionar lejos de los servidores centralizados opacos.

A nivel de arquitectura, el sistema basa su funcionamiento en la convergencia de tres pilares tecnológicos: el uso de dispositivos móviles (smartphones) como terminales de votación, un sistema de verificación de identidad biométrica, y una infraestructura de *blockchain* permisionada o privada. Para acceder al sistema, el elector debe superar un proceso de validación que requiere fotografiar un documento de identidad oficial y grabar un video *selfie*; la plataforma utiliza software de reconocimiento facial de terceros para comparar ambos elementos y autorizar la emisión del voto.

[![][image2]](https://www.agora.vote/)

Plataforma de votación digital desarrollada por una empresa de tecnología suiza, reconocida principalmente por haber implementado una prueba piloto basada en *blockchain* durante las elecciones presidenciales de Sierra Leona en 2018\.

A nivel de arquitectura técnica, el sistema operó inicialmente sobre una red *blockchain* permisionada (de acceso restringido) para el registro y contabilización de los sufragios. Para mitigar los riesgos de centralización propios de una red privada, la plataforma incorporaba un mecanismo de anclaje de datos que consistía en copiar periódicamente el estado de su libro mayor (*ledger*) a la cadena de bloques pública de Bitcoin, buscando asegurar la inmutabilidad definitiva de los resultados.

Para proteger el secreto del voto, las primeras versiones del protocolo empleaban un enfoque criptográfico basado en redes de mezcla (*mixnets*), el cual ofuscaba el rastro de las transacciones para desvincular la identidad del elector de su decisión.

[![][image3]](https://followmyvote.com/)

Desarrollada por la organización homónima, esta plataforma tiene como objetivo modernizar los procesos electorales trasladando la experiencia del sufragio físico a un entorno digital, permitiendo a los electores emitir su voto a través de dispositivos personales como computadoras, teléfonos inteligentes o tabletas.

A nivel de arquitectura y flujo operativo, el sistema requiere que el elector descargue una aplicación cliente que funciona como una "cabina de votación" virtual (*voting booth*). El proceso de sufragio inicia con una etapa de verificación de identidad; una vez que un registrador valida los datos del usuario, este genera un Número de Identificación Personal (PIN) acoplado a una firma criptográfica. Utilizando esta credencial, el elector solicita la boleta digital que le corresponde y, tras realizar su selección, la plataforma empaqueta y envía el voto de forma segura a una urna basada en un registro descentralizado. Al confirmar la transacción, el sistema otorga al votante un recibo o clave criptográfica que sirve como comprobante de participación. Esta infraestructura tecnológica busca asegurar la inmutabilidad de los datos, garantizando que el voto no pueda ser alterado ni eliminado una vez registrado.

Una de las características operativas más distintivas de este sistema es que, si la entidad organizadora lo permite, faculta al elector para reingresar a la plataforma y modificar su voto múltiples veces durante el periodo electoral, hasta el momento exacto en que se decreta el cierre de los comicios. En materia de escrutinio, Follow My Vote aprovecha la naturaleza de la *blockchain* para habilitar una auditoría pública exhaustiva. El diseño permite a cualquier ciudadano u observador contar los votos e inspeccionar los resultados directamente desde el registro público, eliminando la dependencia de conteos cerrados por parte de las autoridades oficiales. Paralelamente, el elector puede utilizar su recibo criptográfico para rastrear su transacción en la red pública y confirmar matemáticamente que su elección fue contabilizada correctamente, manteniendo su identidad civil separada de la decisión registrada.

## **Análisis estratégico y de viabilidad** {#análisis-estratégico-y-de-viabilidad}

### Análisis FODA {#análisis-foda}

La incorporación de un análisis FODA constituye una herramienta estratégica fundamental para evaluar la factibilidad integral del proyecto VOTAR. Al estructurar el ecosistema del proyecto en dimensiones internas (fortalezas tecnológicas y debilidades operativas) y externas (oportunidades de mercado y amenazas regulatorias), este análisis permite transicionar de una propuesta puramente técnica a un modelo de implementación realista y sustentable. 

#### ► **Fortalezas** {#►-fortalezas}

* Arquitectura de privacidad criptográfica: La implementación de una autenticación híbrida que desvincula la identidad real del usuario (validada vía SSO) de la dirección criptográfica (billetera efímera) garantiza el anonimato absoluto del sufragio.

* Eficiencia en el procesamiento de datos: El uso de Árboles de Merkle para la gestión del padrón electoral permite validar el derecho al voto sin exponer públicamente la identidad del resto de los participantes ni saturar la red *blockchain* con datos innecesarios.

* Inmutabilidad y automatización: La delegación de la lógica del ciclo de vida electoral (apertura, cierre y conteo) a contratos inteligentes elimina la dependencia de autoridades centrales durante el escrutinio, garantizando que las reglas operativas no puedan ser alteradas.

* Escrutinio público y trazable: A diferencia de los sistemas de *"caja negra"*, el *Dashboard* conectado a los eventos (*logs*) de los contratos inteligentes provee una auditoría matemática en tiempo real para cualquier ciudadano.

* Abstracción de la complejidad Web3: El diseño del *frontend* elimina la fricción tecnológica para el usuario final, ocultando la firma de transacciones y el manejo de criptografía detrás de una *"Boleta Única Digital"* intuitiva.

* Escalabilidad a modelos híbridos: El prototipo desarrollado para elecciones de pequeña o mediana escala puede servir como base demostrativa para futuras licitaciones o adopciones a nivel municipal o provincial.

* Transparencia y auditabilidad mediante código abierto (Open Source): La naturaleza abierta del código fuente permite que expertos, organizaciones civiles y los propios votantes inspeccionen y verifiquen la integridad de los algoritmos utilizados. Esto elimina la opacidad de los sistemas tradicionales, garantizando la ausencia de "*backdoors*" o funciones ocultas, lo que eleva radicalmente la confianza técnica y ética en el sistema de votación.

#### ► **Oportunidades** {#►-oportunidades}

* Demanda creciente de transparencia institucional: Existe una necesidad latente en organismos gubernamentales, universidades y sindicatos por transicionar hacia sistemas auditables que mitiguen vectores de ataque internos.

* Auge de Organizaciones Autónomas Descentralizadas (DAOs): El ecosistema Web3 requiere constantemente infraestructuras de gobernanza robustas, representando un nicho de mercado primario altamente receptivo a esta solución.

* Optimización de costos operativos a mediano y largo plazo: la digitalización del proceso electoral permite reducir gastos asociados a impresión de boletas, logística de distribución, almacenamiento y escrutinio manual. Si bien requiere una inversión inicial significativa en infraestructura tecnológica y seguridad, el sistema puede generar eficiencias económicas sostenibles en el tiempo.

#### ► **Debilidades** {#►-debilidades}

* Dependencia de la seguridad del SSO centralizado: Si el sistema de autenticación de la institución (OAuth 2.0) es vulnerado, un atacante podría generar pruebas de Merkle legítimas para identidades comprometidas antes de que el usuario real emita su voto.

* Limitaciones del entorno de pruebas (Testnet): El despliegue inicial está proyectado sobre redes *Testnet* (como Sepolia). Transicionar a un entorno de producción (*Mainnet*) introducirá costos operativos variables (tarifas de *gas*) que la institución organizadora deberá subsidiar para mantener la gratuidad del voto.

* Complejidad del stack tecnológico: Mantener una arquitectura que requiere sincronizar bases de datos relacionales tradicionales con el estado de la *blockchain* exige un alto nivel de especialización técnica y dificulta el mantenimiento a largo plazo.

* Vulnerabilidad del entorno local: Dado que la billetera efímera se genera localmente en el navegador del votante, la presencia de *malware* en el dispositivo personal podría interceptar la transacción antes de ser enviada a la red.

#### ► **Amenazas** {#►-amenazas}

* Resistencia institucional y barreras regulatorias: La falta de marcos legales claros respecto a la validez jurídica del voto electrónico mediante *blockchain* puede frenar la adopción por parte de entidades estatales tradicionales.

* Ataques de denegación de servicio (DDoS) al servidor central: Aunque la *blockchain* es resiliente, el servidor *backend* responsable de generar las pruebas de Merkle es un punto único de fallo que podría ser atacado para impedir que los votantes obtengan la autorización necesaria para interactuar con el contrato.

### Estudio de factibilidad {#estudio-de-factibilidad}

El estudio de factibilidad evalúa la viabilidad del proyecto VOTAR desde tres dimensiones complementarias: técnica, operativa y económica. El objetivo es determinar si el sistema propuesto puede ser construido, puesto en operación y sostenido en el tiempo, identificando las principales fortalezas y obstáculos en cada dimensión.

#### ► **Factibilidad técnica** {#►-factibilidad-técnica}

Desde el punto de vista tecnológico, el proyecto es viable, aunque requiere una arquitectura de complejidad considerable que el equipo deberá abordar de forma iterativa.

La base criptográfica del sistema es sólida y se sustenta en protocolos de amplio uso en la industria. La generación de billeteras efímeras mediante Criptografía de Curva Elíptica (ECC), combinada con el uso de Árboles de Merkle para la gestión del padrón, garantiza que la identidad del votante pueda desvincularse del sufragio sin exponer información personal en la red pública. Estas tecnologías se encuentran maduras y cuentan con implementaciones de referencia en ecosistemas como Ethereum.

La elección de la red blockchain es un factor determinante para la viabilidad técnica. La plataforma operará inicialmente sobre redes de prueba (Testnet como Sepolia), lo que elimina los costos de transacción durante el desarrollo y permite validar la lógica de los contratos inteligentes en un entorno controlado. Redes de segunda generación como Ethereum son técnicamente capaces de procesar el volumen de transacciones esperado para elecciones de pequeña y mediana escala, el segmento objetivo del proyecto.

La verificabilidad de extremo a extremo (E2E) es técnicamente alcanzable con el diseño propuesto. El recibo criptográfico que se emite a cada votante le permite confirmar matemáticamente que su sufragio fue incluido en el cómputo global, y el Dashboard Público conectado a los eventos del contrato inteligente habilita una auditoría abierta en tiempo real para cualquier observador.

El principal obstáculo técnico identificado es la vulnerabilidad del entorno local del votante. Dado que la billetera efímera se genera en el navegador del usuario, la presencia de malware en el dispositivo podría comprometer la transacción antes de su envío a la red. Esta limitación es inherente a cualquier sistema de votación remota y no es exclusiva de esta arquitectura; su mitigación requiere comunicación clara hacia los usuarios y, en instancias críticas, el uso de terminales controladas por la institución organizadora.

Adicionalmente, el stack tecnológico completo, que integra un backend relacional tradicional, la infraestructura blockchain y el frontend, exige un nivel de especialización técnica alto, representando un desafío significativo para el equipo durante la etapa de desarrollo.

#### ► **Factibilidad operativa** {#►-factibilidad-operativa}

La operación del sistema es viable en cualquier organización que cuente con un padrón de participantes definido y un mecanismo de autenticación institucional existente, ya sea un directorio corporativo, un sistema académico, un registro de socios o cualquier otra fuente de identidad integrable vía protocolos estándar como OAuth 2.0. Esta condición es prácticamente universal en los contextos objetivo de la plataforma: universidades, empresas, sindicatos, cooperativas y organismos públicos de escala media.

La separación de roles definida en las reglas de negocio, autoridad electoral, votante y observador, es operativamente clara y no requiere estructuras organizacionales complejas para su gestión. El Panel de Administración centraliza las tareas de configuración de los comicios y gestión del padrón, mientras que el Dashboard Público opera de forma autónoma sin intervención continua por parte de la institución.

De acuerdo con la revisión sistemática de **Jafar et al. (2021)**, la implementación de sistemas de votación electrónica enfrenta obstáculos que trascienden lo tecnológico, situando a la carencia de marcos legales claros como una de las barreras críticas para su adopción. En el contexto argentino, ante la falta de una normativa específica para el sufragio estatal mediante *blockchain*, la plataforma encuentra su fundamento jurídico en la **Ley N° 25.506 de Firma Digital**. Esta ley permite alcanzar los requisitos de "no repudio" y "autenticidad" que el paper identifica como esenciales, al otorgar a la firma digital una equivalencia funcional con la manuscrita y una presunción de integridad sobre los documentos electrónicos. Tal como sugiere el estudio internacional respecto a la viabilidad actual de estas tecnologías en entornos controlados, este respaldo jurídico posiciona a la plataforma como una solución válida para procesos de escala intermedia \-asambleas de cooperativas, elecciones estudiantiles o votaciones corporativas- sin requerir reformas normativas inmediatas. No obstante, la expansión hacia comicios municipales o sindicales con efectos ante el Estado permanece supeditada a superar los desafíos de escalabilidad y certificación técnica que la literatura científica aún señala como áreas en desarrollo.

Adicionalmente, la usabilidad de la interfaz es un factor operativo crítico transversal a todos los contextos de uso. Una curva de aprendizaje elevada reduciría la participación y generaría desconfianza en el proceso, independientemente de la robustez técnica del sistema. Por este motivo, el diseño de la Boleta Única Digital (BUD) prioriza la abstracción de la complejidad criptográfica, presentando al votante una experiencia equivalente a la de cualquier formulario digital moderno. La confianza de los participantes en el sistema es, en última instancia, un requisito operativo tan importante como cualquier componente técnico.

Como caso de aplicación inicial tentativa y validación del sistema en un entorno real y acotado, el proyecto podría tomar como referencia las elecciones del Centro de Estudiantes (CEUTI) de UTN FRVM, donde la institución ya cuenta con padrón de alumnos y sistemas de autenticación integrables, lo que reduce significativamente la complejidad del primer despliegue.

#### ► **Factibilidad económica** {#►-factibilidad-económica}

En términos económicos, el proyecto presenta un perfil de costos inicial moderado y un potencial de reducción de gastos operativos sostenido a mediano y largo plazo para cualquier organización que lo adopte.

Los sistemas de votación tradicionales implican costos recurrentes y significativos en cada proceso electoral: impresión y distribución de boletas físicas, contratación de personal para la fiscalización y el escrutinio manual, logística de transporte y almacenamiento de documentación. Una plataforma digital como VOTAR reemplaza estos gastos por una inversión inicial de implementación que, una vez absorbida, se amortiza a lo largo de múltiples procesos electorales sobre la misma infraestructura. Esta eficiencia se vuelve más pronunciada cuanto mayor es la frecuencia con la que la institución organiza comicios.

La adopción de un modelo de Código Abierto (Open Source) maximiza el valor económico del proyecto a escala global. Distintas organizaciones pueden tomar el código base, adaptarlo a sus necesidades particulares y contribuir mejoras a la comunidad, diluyendo los costos de investigación y desarrollo sin incurrir en licencias privativas. Esto es especialmente relevante para organizaciones con presupuestos acotados, cooperativas, sindicatos, municipios pequeños, centros estudiantiles, que hoy dependen de soluciones propietarias costosas o de métodos manuales con altos costos operativos ocultos.

El único escenario de costo variable significativo se presenta al migrar del entorno de pruebas (Testnet) a producción (Mainnet), donde cada transacción de voto incurre en una tarifa de red (gas fee) que la institución organizadora deberá cubrir para mantener la gratuidad del proceso para el votante. Sin embargo, para elecciones de pequeña y mediana escala, el segmento objetivo del proyecto, este costo es considerablemente menor al de los métodos tradicionales equivalentes, y puede reducirse aún más mediante la elección de redes blockchain de bajo costo operativo en el momento del despliegue productivo.

#### ► **Conclusión del estudio de factibilidad** {#►-conclusión-del-estudio-de-factibilidad}

El proyecto VOTAR es técnica y económicamente viable para cualquier organización que requiera llevar adelante procesos electorales formales con necesidades de transparencia, integridad y auditabilidad. La factibilidad operativa es sólida en el segmento de elecciones no gubernamentales de pequeña y mediana escala, cooperativas, universidades, empresas, sindicatos, organizaciones civiles, y cuenta con respaldo jurídico a través de la Ley N° 25506 de Firma Digital, que equipara el acto de sufragar digitalmente a una firma manuscrita y le otorga plena fuerza probatoria en dichos contextos. La limitación regulatoria se acota únicamente a los comicios con efectos jurídicos plenos ante el Estado, para los cuales se requerirá en el futuro un proceso de certificación y adaptación normativa específica.

La estrategia de adopción progresiva es la vía más adecuada para el crecimiento del sistema: comenzar en contextos controlados y no gubernamentales permite demostrar el valor de la plataforma, construir confianza institucional y acumular evidencia técnica que siente las bases para futuras certificaciones regulatorias. El modelo de Código Abierto refuerza esta trayectoria, ya que facilita la inspección independiente del sistema y su adopción sin barreras económicas por parte de organizaciones de distinta escala y naturaleza.

## **Definiciones** {#definiciones}

### Reglas de negocio {#reglas-de-negocio}

Las siguientes reglas son genéricas al dominio de la votación electrónica y no dependen de ninguna organización específica. Se aplican a cualquier instancia de uso de la plataforma.

| Regla | Descripción  |
| :---: | ----- |
| Cantidad de votantes | El sistema debe contar con un padrón electoral definido antes del inicio del proceso. Solo los votantes incluidos en dicho padrón están habilitados para emitir su sufragio. |
| Unicidad del voto | Cada votante habilitado puede emitir su sufragio una o más veces durante el período electoral activo; sin embargo, únicamente el último voto registrado será computado en el escrutinio final. |
| Voto en blanco | El sistema debe contemplar la opción de voto en blanco como una alternativa válida y contabilizable dentro del cómputo general de sufragios. |
| Voto anulado | El sistema debe definir las condiciones bajo las cuales un voto se considera nulo (ej. emisión fuera de término, error en el proceso de firma criptográfica, entre otros). Los votos anulados deben registrarse y contabilizarse de forma separada, sin afectar el cómputo de votos válidos. |
| Autorizaciones | El sistema distingue roles con permisos diferenciados: autoridad electoral (configuración de comicios, gestión del padrón, generación de reportes), votante (emisión del sufragio) y observador (acceso de sólo lectura al dashboard público de escrutinio). Ningún rol puede operar fuera de sus permisos asignados. |
| Bajas y sucesiones | Una lista no puede darse de baja una vez que ha sido oficialmente registrada y asignada al proceso electoral. Cualquier modificación posterior al cierre de la inscripción queda inhabilitada para preservar la integridad de los comicios.  |
| Mínimo de candidatos | Cada lista debe cumplir con un mínimo de candidatos definido por la configuración del proceso electoral antes de poder ser registrada. Las listas que no alcancen dicho mínimo no podrán participar. |
| Inmutabilidad | Todo voto registrado en la blockchain es inmutable. No puede ser modificado ni eliminado por ningún actor, incluidas las autoridades electorales. |
| Recibo criptográfico | Cada votante recibe un recibo criptográfico al finalizar la emisión de su sufragio, que le permite verificar matemáticamente que su voto fue procesado e incluido en el cómputo global, preservando el secreto de su elección. |
| Desvinculación de identidad | Tras la autenticación inicial, el sistema desvincula criptográficamente al votante de su identidad real antes de registrar el sufragio, garantizando el secreto del voto en todo momento. |
| Escrutinio público | El conteo de votos debe estar disponible para cualquier ciudadano u observador independiente en tiempo real, sin necesidad de autenticación. Ningún actor del sistema puede restringir o demorar el acceso a esta información. |
| Resultados en tiempo real | A medida que se registran sufragios en la blockchain, los totales parciales deben reflejarse de forma inmediata en el dashboard público. No se admiten períodos de opacidad durante el proceso de votación. |
| Auditabilidad del proceso | Toda transacción registrada en la blockchain (emisión de voto, generación de recibo) debe ser auditable por cualquier observador externo. El sistema no puede operar como "caja negra" en ninguna etapa del proceso electoral. |
| Verificación individual | Cada votante tiene el derecho de verificar, mediante su recibo criptográfico, que su voto fue procesado e incluido en el cómputo global. Esta verificación debe ser posible en cualquier momento posterior a la emisión del sufragio. |
| Publicidad del padrón | La cantidad total de votantes habilitados debe ser información pública y accesible antes del inicio del proceso, permitiendo contrastar el número de sufragios emitidos con el universo electoral. |
| Publicidad de las listas | Las listas y candidatos registrados deben estar disponibles públicamente desde el momento de su oficialización, sin posibilidad de modificación una vez iniciado el proceso electoral. |

#### ► **Regulaciones que pueden afectarnos** {#►-regulaciones-que-pueden-afectarnos}

*Ley N° 25326: Protección de Datos Personales y Privacidad*

Esta es la regulación con mayor impacto técnico sobre el diseño del sistema. La legislación argentina (al igual que el RGPD en Europa) establece principios estrictos sobre el tratamiento de datos personales, el consentimiento informado y los derechos de los titulares.

* **Desafío técnico-legal (derecho al olvido):** La ley otorga a los ciudadanos el derecho a solicitar la supresión de sus datos personales. Esto entra en conflicto directo con la naturaleza inmutable de la *blockchain*, donde los datos no pueden ser borrados.

La arquitectura de VOTAR aborda esta regulación de forma nativa mediante la *disociación de datos*. Al utilizar un sistema de Autenticación Híbrida y Árboles de Merkle, la *blockchain* nunca almacena datos en texto plano (como el DNI o el nombre completo), sino únicamente pruebas criptográficas (hashes) y el registro de la interacción de una Billetera Efímera anónima. De esta forma, el sistema cumple con la normativa al no exponer Información de Identificación Personal (PII) en la red pública.

*Ley N° 25506: Ley de Firma Digital y Documento Electrónico* 

Para que los resultados arrojados por los *smart contracts* de VOTAR tengan validez vinculante con las máximas garantías legales, el acto de sufragar se instrumentará mediante Firma Digital. A diferencia de la firma electrónica simple, la firma digital garantiza legalmente la autoría e integridad de cada voto, otorgándole idéntico valor que una firma manuscrita y plena fuerza probatoria. Bajo este esquema, se presume que cada sufragio pertenece al titular del certificado y que no ha sido alterado desde su emisión.

Para su implementación, la plataforma se integrará exclusivamente con certificados emitidos por Certificadores Licenciados reconocidos por la autoridad nacional, verificando en tiempo real su vigencia y estado de revocación, garantizando así que únicamente usuarios autorizados con credenciales válidas puedan participar en el proceso.

Finalmente, la plataforma adoptará medidas estrictas de conservación y auditoría que aseguren la inalterabilidad y consultabilidad futura de los registros. Al optar por firma digital en lugar de electrónica, las instituciones que utilicen VOTAR quedan automáticamente amparadas por el marco legal vigente, sin necesidad de acuerdos previos de aceptación mutua.

*Normativas Electorales e Institucionales*

De acuerdo al entorno donde se implemente el producto, el sistema debe acatar leyes específicas que rigen los procesos democráticos.

* **Estatutos Universitarios y Ley de Educación Superior (N° 24.521):** Para implementar VOTAR en centros de estudiantes o consejos directivos, el software debe cumplir con las exigencias de transparencia, secreto del voto y auditoría de fiscales que exijan los estatutos propios de la Universidad Tecnológica Nacional (o la institución de destino).

* **Ley de Asociaciones Sindicales (N° 23.551):** En caso de orientar el producto a elecciones gremiales, el Ministerio de Trabajo exige estándares rigurosos para la aprobación de los comicios. El *Dashboard* de escrutinio público de VOTAR es una herramienta clave para satisfacer los requerimientos de los veedores del ministerio.

*Normativas de Infraestructura Crítica*

Al gestionar un proceso de alta criticidad como una elección, el *backend* del sistema (que procesa el padrón y genera el Árbol de Merkle) puede ser considerado infraestructura crítica para la institución. Es probable que la plataforma deba ajustarse a las normativas y estándares internacionales de seguridad de la información como la familia ISO/SEC 27000 o las directrices de la Dirección Nacional de Ciberseguridad.

### Propuesta de investigación/capacitación {#propuesta-de-investigación/capacitación}

Para el desarrollo del proyecto, el equipo deberá profundizar en las siguientes áreas técnicas y legales, varias de las cuales requieren experimentación práctica dado el nivel de especificidad que demanda la arquitectura propuesta.

* **Tecnología blockchain y selección de red.** Evaluar las características de distintas redes en términos de rendimiento, costo operativo (gas fees) y descentralización para fundamentar la elección de la red de producción. El despliegue inicial sobre Sepolia requiere familiarizarse con las herramientas del ecosistema: nodos, exploradores de bloques y entornos de prueba.  
* **Smart contracts con Solidity.** Capacitarse en el desarrollo de contratos que gestionen el ciclo de vida electoral completo, con foco en la gestión de eventos (logs) que alimentan el Dashboard Público, la optimización de gas y las metodologías de auditoría para garantizar que la lógica electoral no pueda ser explotada una vez desplegada.  
* **Criptografía aplicada al voto anónimo.** Investigar la generación de billeteras efímeras mediante ECC, la construcción de Árboles de Merkle para la gestión del padrón y el diseño del recibo criptográfico que permite al votante verificar su sufragio sin comprometer su identidad.  
* **Autenticación e integración institucional.** Estudiar la implementación de OAuth 2.0 y OpenID Connect de forma tal que la identidad validada institucionalmente no quede expuesta en la capa blockchain, garantizando la separación criptográfica entre autenticación y emisión del voto.  
* **Desarrollo full-stack orientado a Web3.** Investigar la integración entre frontend y contratos inteligentes mediante ethers.js o web3.js, y los patrones de sincronización entre bases de datos relacionales y el estado de la blockchain para la construcción de la BUD, el Panel de Administración y el Dashboard Público.  
* **Marco legal aplicable.** Revisar la Ley de Firma Digital, la Ley de Protección de Datos Personales y las normativas institucionales según el contexto de despliegue, para asegurar que las decisiones de diseño técnico sean coherentes con los marcos legales vigentes.

# **BIBLIOGRAFÍA** {#bibliografía}

* [Shah, S. I. H., Ahmed, A., Mushtaq, M., Shah, S. F., & Kim, D.-S. (2021). Blockchain for electronic voting system—Review and open research challenges. *Applied Sciences*, *11*(17), 8226\.](https://doi.org/10.3390/app11178226)   
* [Ley N° 25.506. (2001, 14 de diciembre). Ley de Firma Digital. Honorable Congreso de la Nación Argentina.](http://servicios.infoleg.gob.ar/infolegInternet/anexos/70000-74999/70749/norma.htm)  
  * [Texto actualizado de la norma](https://servicios.infoleg.gob.ar/infolegInternet/anexos/70000-74999/70749/texact.htm)  
* [Voatz. (s. f.). *Voatz: Mobile Voting & Election Platform*.](https://voatz.com/)   
* [Agora. (s. f.). *Agora: The Future of Voting*.](https://www.agora.vote/)   
* [Follow My Vote. (s. f.). *The Secure Mobile Voting Platform Of The Future*.](https://followmyvote.com/)   
* [Ethereum Foundation. (s. f.). *Solidity Documentation*.](https://docs.soliditylang.org/en/latest/)   
* [Ley N° 11.672. (1932, 31 de diciembre). Complementaria Permanente de Presupuesto (t.o. 2014). Honorable Congreso de la Nación Argentina.](http://servicios.infoleg.gob.ar/infolegInternet/anexos/25000-29999/25394/texact.htm)  
* [Ley N° 19.550. (1972, 3 de abril). Ley General de Sociedades (t.o. 1984). Honorable Congreso de la Nación Argentina.](http://servicios.infoleg.gob.ar/infolegInternet/anexos/20000-24999/20993/texact.htm)   
* [Ley N° 20.337. (1973, 2 de mayo). Ley de Cooperativas. Honorable Congreso de la Nación Argentina.](http://servicios.infoleg.gob.ar/infolegInternet/anexos/60000-64999/64790/texact.htm)   
* [Hardt, D. (Ed.). (2012, octubre). *The OAuth 2.0 Authorization Framework* (RFC 6749). Internet Engineering Task Force.](https://datatracker.ietf.org/doc/html/rfc6749)

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAARwAAABgCAYAAADPY83uAAAgvElEQVR4Xu1dCXQc1ZUtSd2SWpstYRuSgSE5yZzJyUxOcsIMxjbeWIzBu6VWb1ptMDuHHAhhNbGJV9nWYi3eZBvskGRIQrZJSAhkYchAYEhCICEhC5AAMbYly63eqrr6zXu/urpraUktqbokwb/nPEtWV1f9qvr//vfef+99ATg4ODhsgmD8AwcHB0euwAmHg4PDNnDC4eDgsA2ccDg4OGwDJxwODg7bwAmHg4PDNnDC4eDgsA2ccDg4OGwDJxwODg7bwAmHg4PDNnDC4eDgsA2ccDg4OGwDJxwODg7bwAmHg4PDNnDC4eDgsA2ccDg4OGwDJxwODg7bwAmHg4PDNnDC4eDgsA2ccHKEhPqPTL9Ius84OD6omLSEQ2OVDVqEnEj/PjUggxiPwMwFdbDqlvuNH3JwfGBhP+FoyIP9lMIgQhR/F9kfSBeI478R/Blmx/azn9Hk3xVdQYa4rPwf4iH9CSeAmVLaTFyCV9/rh6oFASi/8iYIRrlmw8GhRU4JJ5FIJMc/DTwZ5Lio/BaPQigOcHvvd8BZ3wuFNZ0w098LQk0HCJ79INTuhXyvWYTadvZ5nrsdnHh8ibcbSht7YckdbdA3oJBWXA7BQCiMFycCk7ENSjtyggTZSzLEYjE4gQzpWtQAMy+9Di645kaIx+Mgy8ye4uDgSCKnhEOIJyQcl1G46u5uyHf3QH6gC/JriVi6wendA8VuJBA/fubtggJPFwi+Lva7kWxSpIOfO7ydqf8XeTrBEUAi8rVBAZ5P8PWA0LwfPuZ7AHkuysgmVwMf9Sw4iz8r560B19wAnLtsPZRcsho/GDQeysHBARYTjiRJbGZPiBH4WR9Aia8dXL5OEOr3gRDYB8Xe3UgqZhKxUgQfirsD8jxIajWtUFLXDa76/dD21B+RfwaMTR41iLzoHsnMm76wHmZefi3MvKKJ/X7BFdU5IzcOjvcDLCEc0mIIERyEwoqNUFC3D7UN0jqG1lTsFCeSneBug7xAG7iu/wYEsZ0xSYQISrZIEQl+13HR5TDjsmth2oI6JudduQFmzVvB/EqKt4mDgyMTxkw4ql9EEsPwce+DINQ9jCTTCkV1vaYBP5lEWLNL8QWt3QWf2bAdzkajWVHEwKAMn1jqRqKpg3+66iZGNK7ZPii7tAme/9Mb5JgyfoWDg8OAURMOEQ3TZ0In4MM190Bx0xEo8rZBYV2PaXBPZsnzdILT04q/tzNtLBx8y3iryqIX3m80LkHZwgYovcST0mrKL/WDa+56OPrDp5IrbJxwODhGQtaEk1rpQfPp7kefQw1hJzi9O00DeapJsW8f5NV2Q2Ftl/6GEVIkCuvvvgc+tHRDimhUqbjMDwMxol5awOfg4MgGWROOKAO8gz+Fa7ZA/spdpoE71URAonH696KW047M0sccwal7DUcgEkat5pJqqFjkM5CNH6oWNkHD3dvSD2ecYBqjssKeFnIvTaowHtHURtJ1ExA2HMdhB0L0T2wQqNdqRYzHtIdNOmRFOIPBPrhu/9NQ4J/c/plspMBHS/D4c00rnKK4QTmaIptoNAxiNAZR1OYqr1hv0mqYKTUP5aIllq5GUSdxBbqgyIemXl07E6EBf67rUgIbJxDEeZIkw2MvngRnbU+qfST51dvhLLckJwSR8CALycj3tOnkhy+TWjB5MSzhyHIQZ7AoCFdvNA3cqSgFvg4ovXYPlF69FWeHAeabUUHjJhQfhE8tb4aqxY1QMT+gIxrXgnqYNt8Ds+as0H3PCkgxEXZ8700obDATetd/v2g83FYQ3VFEd6G/G0rr96ef5bo2EJZvxE6f/Uofh3VIyMrEaOwvT746BQknjvpyIi7Dyf6z4Aykg+ymrrRDYeAQTKs7jm8qhBqNYZAk4hAWY1A2Zx2ce7lZq2EyrwZmLXSDLMVTYQBWIoTU/q/NtISvaGCqFKxtUdSMHFxzJLDlATECQs39pmda7O80Hs5hI95XhEPT/RtRgBmBXigKbDPd1JSTpv+C6zq+ghrbQCodQUVMToAcHYSq2WugdAFpNX4z2aBUXnkThOhrlCqh+b5VIA0rFh6A4ob9aFql45eEVZvAUb0HgiH7o5eleAJm3/MNJJyDpmf625P9xsM5bMT7gnBUX8Z7QRHyaPXG05HyeUxFKfZ2QVF1qxJnM0ROVUiSwDG3CSrnZyYaVc5deiM8//rbzHeT6TzjRUxMsKz4354WoaBG75R3uHfCawP2O2cHpUEQ/NQP0lpucfVO+MxtvRORI8uhwfuCcCAWAQhjJ8NBKvj2mG5mKkmepw1Klm8kr7DuFlVEZAlNI0Azyg/li/T+mszih+mLG1EjAujrH3+KxJCQovCxBn24gbC6HYQrPs9y5VnMT46hkmqx54DpuQr+HpYVzzGxeF8QjiyGkGimrkZDQis9Bb5OeJfUmoSyuqy7R4l8MDKcFeNQeFENIxNyEpsJJrNULrkBzZ+opatUeihLzQL5znwUmKjcF92TsGona3+uQabjy0FgIQOp63t6IL+2E07k/vIcWWDqE44cR1W+BQoaHzHdxFSQwgD5GVATqN6FwxUHrZh5Fqa/0lJ4OZJH2TxjjE0WsqgJps+tZsuSucRfByRwoVmrvcdSXw/8OSwq5kwObZq42AfCyjTZkBQEsF8svR81vDgkYkHjV8YOg6lLZiUrLTJZkYjrHn26BEuuJqDMmPKEQ/GyxsZPJaEs9Pmf70YtbQBEMg2HQD/O0OVL0omXY5U9j37HeGpLEYEBKF+7Gxy+ttQ9OnwdUOil1aEQDMGn4wNqfbQa5ly/H/KqdyvPFTUrlnm/dC9+NjY/kjooEzI1mtJAosxL3vnTP8BHfRtBoHIlaMIL/la4sGkrdD3zR4VQ2Uim78hMK6X/yiadNTdgZU0SSkgAPRPSaiGGbX7yNTjf+wC2uQ0ntw7ID/SAd8dX4JfvkGZKoECC5KQwnDYoK7WhVKG7y6S90kqh9jhVIBpS4nAM4+CpP/zddKzue0iYdF/s97hs+jyXQhOJoESMIvN4zfb6VBAh0MYihlufeAnMBpQeoVgUqhY2QMW84R3E2Yhwkdt4ektBDnwSoTod+6JK2eovME3DalA62O1H/4ddg4iGPd+1LVDUdAhInwvL2QchKoOHZn2JDcGKpbeBy9MFheSE9ncyMd6XUZys9lE3tuU4VFx9Bxt8dD525/LYyG84MI5j2pYIp/72D/gX/2alnTUUVNejmJUZ2pmS2m4oa34Y++MBFsn+3F9Opk+sAd3Fe1GJ3ZsqTn87lNWb02vO4He1x6lSWNsOxbXmZ1hct890rFaeQFuZClFGxQg43ObPcyY17VDu3gICMTcxJc0uxsZPdilq6GQlJ87ElHzvoVaP1KFZOd9rIo6xix+efuZ/FRMghwhi46kwmfa+yal/7MW/mDryuCGjVuXv0F3L4dkN0zw7jEcOC9Ys1GKWbToGxf5uKK4/rDunsvrZyQqxOfxKQTamReEgYhGz3jTh6d63t40dV7PpEbxAP0ikkJH2NMR7Hw3oDFTs9t7DT0BF42FGGsbrU1sVokTTvbYVJ2mljdRW1l7PAcir1U8QQjVOEGvug5ikRLSz5GcpBmSU6s6Pz7nIs8vYLGyTzO7ZKNSWTM9I1UiHkh+/dhoVtQFmkglEpIbvWy1UXI9qVK287xC7d2EwGoHiVeOLtaF6M0phLbVa3yiFOpxb7zMYTmiZll52oacbp4sBkOThNZvwYAycF12egTTGJxWX3cjUxFyCBkKBexucU2eeEKwsiREaeAcH0X5w1qZXJwXUHAXvg0l9OAuEIkypmYVtLaqnAZsmSlYfCbUbh6eFve+iAJptHjJLOpkmI6zejuREJgoNpA4oqzsI+Whm0Tum0AxGTJp7J3L69G3tFEg1PveJSENfhuWbHsb27QdHdUu6zdinne7DaMa24TtoR8LrUYixZgcQ6UxvaGVVK/M9aA7W4eeBY1BK6R+kwSEhKZUsk+0NdMLMhha83imKgQARzVfd+xyCcETsACqhacWFk62QQeOiSdh4rFa++/rbSNUDzBZwrXkITGNxDEJ1rwR8ZwX15nitQvdRqPIdBDl2ht2PEIxEwdlw1HTgaMThOwClnnYoqN4zJnE07ssYXDaUsIJanoOom1EHp1lD/5K0oCqEF85ZAoWz06UlrJKqxfU2pC5GISSdRkKml6t/DlUrbzcePGasuP+rILBrpInf2djJfHtUsCw7YDv9W6G0+QAjCKaxJM9VWnuA1Ura+Piv8JYoaDCqsCnFJmjOT74MhUbRHAmF4Oq2R8DlP6gM7OS51Fnc4UMtY8XOlHk1lpXDCH5lRjNqLowA9dqdq6aLXftX9BDkIMt5Y6ZiMtQiFXFBtyApmjRpMe/iz0JfC7ZPo+0gKRXU7oIi1J5iSDaDwaj+fQ5BOAz0fIwSJ6fxoP4cKE++/Ib5WI3E6Cdrt+K/sQIxnHQjiTBUbnjU1B7hmo34kMkCUR6WsPX7L0KRf3yqVTnOQg89/qLy1Mcgrd99AWcy8ww+lBRih2YuRHp4w4A6B+XOTp9fB2WG3CgrpGKuGyrnrjZe1nJE0GS8+5EnTc8hDzvw1597ZVykR2ka8UQMz2WeLc+/bis7ZqSBTGkw9z76DAjLNkNpk8GkuLoFLrh5P8TRjJBgEJQobcUBPBxSZhJ2kRODSpE0Yel9SDDb9eev2Y3aRRfs+/nrShB5lghjCzqe/D2ebwsUGtJ3nEgU/3Zzu1LiSDNAR2ozIUGrWGQ20X/we786HYWKpkOQh4SpEmVBUy8cf+2M/nkPRzgZMJlWqYhwSimxW+NTKsMx+vHGHTAQI7s3fawgeKgQ+SFTw0clpE569zPHouqrHw2oE158+3ZmKpnOrZGSANrvD/WykPsoq0UzPORoAj687BYTUVglRSiuhc3Gy1oO6vdk+s6+rQeEtfqZXqjeCvLg0KtyI6EfR7Lg7tGVgy3y0zW6INg/QueNI9WJp+Ej/s1Q1qBfwi/27oC8K++CqByB6BDBl9lCTSWhd069y9WM16AVIs31CuoOw6c+dxRC4RGCMqUQymlwrngA+73+HMLyL0GpbxuSWxzkiEVlHrDpyOfw1llgpXfz16Jp6VX8KdprT0XCiURFGESWd9buVu4Nr0+mcrGvHS6o28a4wOhfE6jUpuC2ppCWo+74mNQ0tUnGTpsStKtpp4Z/v6WDpQCw7wxnRzHIqNk0QPEc600pVarm+aBkXp3xwrlDIpo0e9LPpmDdAajwt+DATqr7WUJ9fvue+rWpWmNJYzf0sYN0XzHhDHa4Cz33M/+MYs8n+4G/By6/YwfTTkY4xZgQkiKw+1u/wOumzXDFxOqAz9y813i4DtSe8/2bWLVH7QRXWt8DX/k1DlbSuhnGR5IZIYZwQA7hOphihCPLEpygycpQt5x2TilCwqHnl6k3CtRZTGw7RnE0H2fqaSRy2nid7CCSg6yb7bqgPW+Vpw1meh9SekuWPfhjV9WbCMJqqVwQQFOtXolrkCyaEYdBSOqHZ/rjSAjkfFVKWQgBytzuZqajulqXDagzkC5AdXcKGxStiYiHstXv2f8ttjoyHKR4hJk5s/wPm/rBj/4QyuluqXReogXPtsdMzuSCwG52TDRD8xWSjcJMw3dIbuz9ueaY3ECMnmRbJjkaDqGmOrU1HOo/ZM4WN6dN6MLavTBr9RdhuPAUwdhgK+TWw08br5MVZDkEH12ver+Vc9Gs9clraVl26JvQguUBIfuWjCWKeIxCCyV2gO5NRBWWHOzGZdvS678KA0EKcMgWYahqPKY7h+DeDY5V24H21Rqxclx8EFy0slitMYPJibvsQegPjWDWWAXURgqrt4GwglaNkm2gIML6AxCXMni28EXRDKxoZMn+5WlhK56xTMdbjDg+M3qHp0R8h2sNftMpQjhUXQHtTfaM1WuSaU8/Xet72KoaBWkOhZwQTnn9cXq69FSM1xsRYqQPOwAts7Wz+JPzcfYdXYa2iKaOByoXNZiIIVdiF+GooD1GBR+ZBJpO69sDJas3jahWsGBfxBeOPIHvSd/pBf+OrC0JOo3xvVPMCcSV5U+7EELNkvYe07bDWdOKGqe5fMZfQ+Y2uzYcQ20szFYz7UIkAsznqWvLJCccdfzRNET7vDncmooG1x2GshtxzIvMEB8WjHBUhrJKaDmUcm9GmCMzgrK4pVicqWuO2u3MVswG6gNZ0nQrFC/KXB7Uailf0AAV831s8Ili9ubMeEGxti++dRpNILNpcGKEiVpKROCEJANpkdrSI7S98vQ1LRCOZacl3XXkJ6ZrUx2fkQjPcoiDaHJ/0dD/WuDpP5u1LNeKe01t/ueGLymzto2ISmeA9ghRgvGSY2+SE44khlgYAEVTU86l8pzblMjx6i1Zv3fBgWq04E0HO1klQn0vq+tCMQcjLatmwk2HfsI6U7ZQ7leGEnISz7dHu5k+uwbOuazJ0BL7IFRvNj/3VWpxd/MzV6g7jB3FXMo0391iOHp4lHvMDv6ub/8u235nGQZZ3Kxec3G628BRbR68JV5zm+NSxFwBMsdQo6PZTrRuJWdtshNOhCKTq/UTXFGAVk0fZCEPzJbKAoKwvBVcvvEF/mUSJ5INmUR/AnIwZteYcQEvUXLxKhMp5FJKFjdCyaJ1xpbYhtgAmp+1qNr60+otaS0f8j3AMuKNoIFVuL4Vj0kfT6teDv/eLD1kaRTWmXO8KGcqGYFiI2Rl5tW2pWYPC0Q1QnDrUyxIWEKqlGk9JffIQw210JN8jpOUcEhXoEL5eb79Ot8X+evKrrln1Jq9MO/eY2i7W19si7bWpZ+F674MCdFsT1sN6jJlc82kkEspvWQFTJuzxtgU+4A3/Tb+KKrdpH/+a1vh+b+YS0iQsVRAvgN/miyEtQ/Bx+86xGIqRgMa1MZ33ieLo1qatwYSiMxE1LQF21aC6r4RxhUtEnJw0j7xEwHB343mSDLgdZISTjD4bjJ1oUsX2Ces2pP0e5k16eEghBISaMPZrRbSdD65YTuI8ciYggJHAi0zEs69ZBnzpxhJIZcy49JaOPb9pwwtshdSPAxlhjwrwX8AZt7yOMhUBiKhZJ0ThBpzvJVQd1gpvTBKVLq3ms71iZuPAAWW2grsUt/7c7+uHa7AJlh692HjkVCg2XVClW8+9yYoBSDsAw1Uilsm5zYl4rK2TELCoXYKlEPWmNYMiSQL0DSVIqeMh2cFgRiKZkRjw60SMqvy3HvhB6++AeEcFHGhJDhS5amY1vSF1qcvDCfll9/IwronEqS1nMAB4/QeYCEE9Mwp6ZIqH356fRcrYxGMS1CwhpILNQF+1R3s3bwbVDrvaPH6GfOKj1DXk8ybsRMiK9WgbYeDKghkmNsadz1mbjMeS5ncdoKSPB797T+Y0zi1S8ckIhzyi9Ezca41V/8sWLUDaOuosc4rQjh6En7ZH4WCOmtXqowieA7jA7J+yVRGzenCpfY4ibVSuaAe5q7xpTSsCUOCjIoENLf9WJf2QEK+mSdeDUE8EmR1bbSfUSKlf+tjwFTiMYQvhPtPmN7xrFrKYJdBsjCLfTjQYsRbgwkoa/yyvq81HmOanRGUM8Y+1xCUsKYDtjx7gq2O2oVwZABKmw3+pElEOJGzfawUiEtb1xwnq1Ikx/7+dyEezb4ukhECxcvQq8lb9zVT460UKkgkVONs0j/GKOShgB2raI79hPOhNXeypMXsUvpyDypzdV7NdijU1EGmok6Ftb2sVEK+W5++4Kw7AuHxrM6gZnfZ1q+xolrqOamcA2Vw50KTzYjIWywATVtSg4plfe0n/wesqqAB9Ka6XjoF5evTiyTkayQtQ5ZGjiEZN5AkaKwtuWuXeYKfBIRzNkJVCBOsb0xfp2jLlPFOfqa8mn3AMvwRsdjoNWIVqRKjb8bIl6NvfC7kMlY8ySIg2RTP8UHV5fbE3WhltmeDsTUTikHUKsLhPnBk2L1TK4KvB2f4buiLiuPf6yrxOgheffY2iWP1LhbtPYZoiOyQjJspMWSms2vfcIz5rIYKxaBwrfxr9RoRey41O4Fom5VvyBEkZJt/ADnu2ydXpHGy7Gik/xT2jd2p2jl0vlLUkqnU7Xtn+rJd+R4WKcKJhlHdrNvHiiQZb8JKEdYiU0qZO8OogSqykQhyLdMXNILjP6tBjWqZbPjmb/5ueuZaKag/BM/+zZrnL0fjMBBPpIpmpa5DBanqaWJRnpEF/ZRBPU8oGEWi61F2tlDvq47KdKJJJw4/+1LMyGA0xswqSgjW9c2VbfDKySBEJLqSde+XzkaazWdvP4Ym3BAxbxNIOGGycuQQlKLWpatGgMToCByFkJxdMGg2MOxLdRqEFeZgMiuF9qgW3C2WlOZ8s/+siRByLTMW3wCnqQ54MrJ5soFiUooberCzmBcCaMVBqNkz6pibkRATQ6hyd7NBLNQo16VsbBrQX37+TZbYmnpaGXwrI0M1XKPwhWM/Zdnoag0bMuNYZLv3IB4WGlKzMSIYJ9Kh4u1dismJ53LUtrEqfRU1dwG5TllxsHFClMJwCrlrelM6S1yob4WKeoNDdgIJR0bNWFit7y+sds+qB5OaanbPNBvoCEeUgvhKRShs7IFyTXKW5YIP+1VWRY1e6OhvRh3sH7n6ehMh5ErK59VB2ZxaePLZl9g+5JMakZOQ591ieu5U1S4eO6PuKWAdaLtkmiHdd0PBukd0OV6k+ZAJt/Shb8Bg5AwbgOqMr7TC/P7Vz1Whgf/pm6ikJhXjTg8Muo6r/iBOkvdDPBphNYmzBZWlTUiDjKgY8bjTM3veaqXUqbD8HpYKEpZo5/ekzpPcPUIBtV3T/gS5aSi3RDmGFo5J6xKSGwoWB8iUaoXK5qMwICoO7JRMAOGwYYT3ZwyLoYliOk4YMigThVVC0Gs4rFCSDNseewE7ZzLkOgci1LWCsKEHYtEgSKOMVCSoiXYU5WskhlxJycVrYMbsZUDbhkix7Dv2hCAyCD94xWxazfLtATYY1LdvGWilC7UGMQgt3/4RODV1jShHi7KxST134eCmfc9cno3wekRiX6PEScqApx1FZTSRWZh8JKqU6VxyJzjqkBD8bazyP51LW1Ceoqq/9/v34FRYWYgYLkvZDOVYmsF/8V44WYNZfVZdSua7t4NV68tvPA5V7i/i8JPZNkT0+FgpVGpvgv4axybHoS8hwdGfvQIu1A7IEc1qNJNZUqP4mor9aFItuT9ZqC67IupDYbyEQ/4YOR4FV+MhNiloS9SU1D8MN23cD0sffBSWfelxS2TJJloRNRIOguV54CN84Piz4MALUxFr402NV5TEzDacQbbBWSkKFHxIS6mD+BCyETEuwScWu2HapfbE3ZB2c84la/HhhCatKaUFi6vBgVxONnntFhZCL9R2okViw0oMgjYJfPhlEa9pqFWDZMEKk3uooHq3Unjfk9QsSKPwKkW0aOeGvLXtUEx/12bEJ6Ws6TAs73wJif+0bvYcK5R3GoYt330BCtYqbVajktnuDG7aZaIDimilL0Aai1Io3Yn356ilz3YxTYYGLcU/adtK5p+wuhv++XoqgUEXQxEzpGPYTDiyPABlSOLFzeZFBtplgVY4jX8fjxABE0yEQ4iLygrDn1D5MFb0slJIRRZqFHYtXr0Zpi28DqYvpAC+4aV0rhfOWZT7Aluq3NHZyzpK3AKb3hYkm3l2oJ9FEufXbMXGn4Wx+U9GDxrAdKWzaD5RYuU0NINcAWVAamNgshUqh1CEpOlYvZNpQrTZnHVuzDTCoqLhR3FCy/PsZBG1tFsDbT5obNNw4iIn+gqqpLkV3qEHEcIJIJouAzuabWKGwlgJh7pGRBJZ3aOKgLntuRLSRgkZCUcFNS7Yd5IRg/EE1grVvlEC1WiTuqoF9mguI8mFy2+Fr//i95DJzzAlQEGJNKvGiSwnyAxMsMVmpaOfPQW/OwVQ6tnOInwFH4q3FZy+HqbJkHZDsyv5Zgr8vXhcC7xBkdB0HlnZvdO6taPhQVo+mVtSKAIvnKA271BWxrC9NAlTW6nwPO1YIniVFbLCVZvhriNPMlKUJXX3CYK+/7BdREMUrUuFRhSJSHR09nfHzk2ToOYcJCNNiYPBfnYVSrJVfGT67+dK1HYNSzgqKIW/sPmrqG7mzq/DhO3vcwBKVt4HM+YHoHL++HfIHIuULGyG85bcwGJbpirXTE6QuzrpO2Gmu/I3tr9WQlRMQVC2wAU2GkYaPjaAmqZxRiv14JNtJZ8Ri6qm6OqkK54RI+80QyErwmGh6rEgXHlXN3OumYKWLBRalqRlSlegB8qoro1NfhqSsgWNUDLHDc7/WAm0LErLgWriIwcHx/iRFeEQKFpdqb4XZlX9KflPoF0UM5CGFcLUa1Rhy1ZuZsF20xY1mQjCSqG9q2YtvZWF+1M9X9LqODg4rEXWhKOCZnzaPI2I55wbDqccgeo+y1YL7bhYWNsFpVd8jlXyq1hoEfEsamAJmKVz/FB5WROLraEcESuDnDg4OPQYNeGoUMskvh0MQ+lqcqh1skS4kTazG6tQKcYy9y6oWuCDciSMijHupEnF1aluDknZvFVwCg3vM2dzXyCMg4NjHISjhRwdZBGZM666E4Tq7SDU7WU5WRTebiSO8QidT6CNxK64E7UTd9YFtyoXKURDvxddGoCSTy1WVhK4NsPBYSssIRx1zYvCPKIJqh8nMWKYrqmda4lQQBirOEZRq0hA85pN5JJR0BRzfLaGZeoSx5BZqMTvccLh4LAT1hCOARTqLceiLAUhKg3Ced6tkN/wMBRfcy8UZ4gcHZtQZGonlC26DqoWN6bIheJ4iudSUKAfzrn4GhaZLJMjeBKssHJwfNCRE8IxgqWyJZTyPWJQhD1P/AaEVTvR9OqFosYjSoi4l4ILu1iWc6bauyQufzsUobnm9B2BotqDqEXtYYmBroZOmHnpeth8+OtKiSA5pXSxn1MhHYGD44MAWwjHhGSSHQuiSohKjFdSFIYgHckcrQhxiX2H7eWdOjZDBC3nFw6OSYmJIRwODo4PJDjhcHBw2AZOOBwcHLaBEw4HB4dt4ITDwcFhGzjhcHBw2AZOOBwcHLaBEw4HB4dt4ITDwcFhGzjhcHBw2AZOOBwcHLaBEw4HB4dt4ITDwcFhGzjhcHBw2AZOOBwcHLaBEw4HB4dt4ITDwcFhGzjhcHBw2AZOOBwcHLaBEw4HB4dt+H8VATBM18R+IwAAAABJRU5ErkJggg==>

[image2]: <data:image/png;base64,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>

[image3]: <data:image/png;base64,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>