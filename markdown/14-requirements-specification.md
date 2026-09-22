# Capítulo III: Requirements Specification

## 3.1. To-Be Scenario Mapping

**Segmento 1: Compradores interesados**

![to-be-scenario-mapping-segmento-1](../assets/Chapter-3/to-be-scenario-mapping-segmento-1.png)

**Segmento 2: Concesionarias de vehículos nuevos**

![to-be-scenario-mapping-segmento-2](../assets/Chapter-3/to-be-scenario-mapping-segmento-2.png)

**Segmento 3: Concesionarias de vehículos usados**

![to-be-scenario-mapping-segmento-3](../assets/Chapter-3/to-be-scenario-mapping-segmento-3.png)

* **Enlace interactivo del tablero en Miro:** [https://miro.com/app/board/uXjVHpkhWe4=/?share_link_id=221895309503](https://miro.com/app/board/uXjVHpkhWe4=/?share_link_id=221895309503)

## 3.2. User Stories

En esta sección se definen los requisitos funcionales, no funcionales y técnicos de SmartFinance Drive mediante un conjunto estructurado de Epics y User Stories. La redacción contempla los tres segmentos objetivo (Compradores, Concesionarias de nuevos y Concesionarias de usados), así como las historias técnicas necesarias para la viabilidad de la plataforma.

| **US-01** | **Visualizar módulos funcionales de la plataforma** |
| :--- | :--- |
| **User** | Visitante |
| **Priority** | Alta |
| **Epic** | Landing Page |
| **Description** | Como visitante, deseo visualizar las funcionalidades principales del producto para entender cómo me ayudará a buscar o vender un vehículo. |
| **Acceptance Criteria** | **Dado** que un visitante accede a la página de aterrizaje,<br>**Cuando** navega por la sección de funcionalidades,<br>**Entonces** el sistema despliega la información sobre el mercado unificado, el embudo dual, el recomendador IA y el panel B2B. |

<br>

| **US-02** | **Consultar planes de membresía B2B** |
| :--- | :--- |
| **User** | Visitante Gerente Comercial |
| **Priority** | Alta |
| **Epic** | Landing Page |
| **Description** | Como visitante gerente comercial, deseo consultar los planes de suscripción para evaluar los beneficios de afiliar mi concesionaria a la plataforma. |
| **Acceptance Criteria** | **Dado** que un representante de concesionaria explora la plataforma,<br>**Cuando** consulta la sección de modelo de negocio,<br>**Entonces** el sistema detalla las características y costos del Plan Concesionaria Nueva y del Plan Concesionaria Usada. |

<br>

| **US-03** | **Cambiar el idioma de la interfaz estática** |
| :--- | :--- |
| **User** | Visitante Internacional |
| **Priority** | Media |
| **Epic** | i18n |
| **Description** | Como visitante internacional, deseo cambiar el idioma de la página para leer el contenido corporativo en mi idioma de preferencia. |
| **Acceptance Criteria** | **Dado** que un visitante se encuentra en cualquier sección de la página,<br>**Cuando** selecciona un idioma distinto en el control de preferencias (ES/EN),<br>**Entonces** el sistema actualiza todos los textos estáticos al idioma seleccionado. |

<br>

| **US-04** | **Navegación fluida mediante menú interactivo** |
| :--- | :--- |
| **User** | Visitante |
| **Priority** | Alta |
| **Epic** | Landing Page |
| **Description** | Como visitante, deseo utilizar un menú de navegación para saltar directamente a la sección de mi interés sin perder el contexto de la página. |
| **Acceptance Criteria** | **Dado** que un visitante interactúa con el menú superior,<br>**Cuando** selecciona un enlace de navegación,<br>**Entonces** el sistema realiza un desplazamiento suave hasta la sección correspondiente. |

<br>

| **US-05** | **Registro de nueva cuenta para comprador** |
| :--- | :--- |
| **User** | Comprador interesado |
| **Priority** | Alta |
| **Epic** | Cuentas |
| **Description** | Como comprador interesado, deseo registrarme en la plataforma creando una cuenta segura para poder guardar mis preferencias y solicitar pre-evaluaciones. |
| **Acceptance Criteria** | **Dado** que un visitante desea registrarse como comprador,<br>**Cuando** envía el formulario con un correo válido y una contraseña segura,<br>**Entonces** el sistema crea la cuenta y envía un enlace de verificación al correo. |

<br>

| **US-06** | **Inicio de sesión para compradores** |
| :--- | :--- |
| **User** | Comprador interesado |
| **Priority** | Alta |
| **Epic** | Cuentas |
| **Description** | Como comprador registrado, deseo iniciar sesión en mi cuenta para continuar con la búsqueda de mi vehículo y visualizar mis opciones guardadas. |
| **Acceptance Criteria** | **Dado** que un comprador posee una cuenta activa,<br>**Cuando** ingresa sus credenciales correctas en la vista de acceso,<br>**Entonces** el sistema lo autentica y lo redirige al catálogo de vehículos. |

<br>

| **US-07** | **Inicio de sesión para concesionarias** |
| :--- | :--- |
| **User** | Gerente Comercial |
| **Priority** | Alta |
| **Epic** | Cuentas |
| **Description** | Como gerente comercial de una concesionaria, deseo iniciar sesión en mi portal B2B para gestionar mi inventario y atender a los prospectos. |
| **Acceptance Criteria** | **Dado** que una concesionaria cuenta con una suscripción corporativa,<br>**Cuando** el gerente comercial ingresa su usuario y contraseña,<br>**Entonces** el sistema valida el acceso y lo redirige al entorno B2B. |

<br>

| **US-08** | **Explorar catálogo unificado de vehículos** |
| :--- | :--- |
| **User** | Comprador interesado |
| **Priority** | Alta |
| **Epic** | Catálogo |
| **Description** | Como comprador interesado, deseo visualizar un catálogo general de vehículos nuevos y usados para conocer la oferta disponible en el mercado. |
| **Acceptance Criteria** | **Dado** que un comprador accede a la sección de exploración,<br>**Cuando** el sistema carga la vista principal,<br>**Entonces** se despliega una lista paginada de vehículos disponibles con fotografía, marca, modelo, año y precio. |

<br>

| **US-09** | **Visualizar Dashboard de métricas comerciales** |
| :--- | :--- |
| **User** | Gerente Comercial |
| **Priority** | Alta |
| **Epic** | Gestión B2B |
| **Description** | Como gerente comercial, deseo visualizar un panel resumen (Dashboard) al ingresar a mi cuenta para monitorear el rendimiento de mis publicaciones y prospectos. |
| **Acceptance Criteria** | **Dado** que un gerente comercial inicia sesión exitosamente,<br>**Cuando** carga la pantalla de inicio del portal,<br>**Entonces** el sistema despliega un panel con indicadores de vehículos activos, prospectos (leads) del mes y alertas pendientes. |

<br>

| **US-10** | **Visualizar ficha detallada del vehículo** |
| :--- | :--- |
| **User** | Comprador interesado |
| **Priority** | Alta |
| **Epic** | Catálogo |
| **Description** | Como comprador interesado, deseo revisar las especificaciones completas de un vehículo para analizar sus características técnicas antes de solicitar pre-evaluación crediticia. |
| **Acceptance Criteria** | **Dado** que un comprador navega por el catálogo de vehículos,<br>**Cuando** selecciona una unidad específica,<br>**Entonces** el sistema carga una vista detallada con kilometraje, transmisión, galería y datos de la concesionaria. |

<br>

| **TS-01** | **Implementar lógica de internacionalización (i18n)** |
| :--- | :--- |
| **User** | Developer |
| **Priority** | Alta |
| **Epic** | Frontend & UI |
| **Description** | Como desarrollador, deseo implementar un script para el cambio de idioma estático que actualice los textos utilizando atributos de datos sin recargar la página. |
| **Acceptance Criteria** | **Dado** que se requiere soportar los idiomas inglés y español,<br>**Cuando** el usuario acciona el control de cambio de idioma,<br>**Entonces** el sistema localiza todas las etiquetas con atributos de traducción y reemplaza su contenido instantáneamente. |

## 3.3. Product Backlog

En esta sección se presenta el Product Backlog priorizado del proyecto. Siguiendo las directrices del curso, el orden de los elementos se ha determinado estrictamente por el valor que aportan al negocio, colocando en las primeras posiciones las historias relacionadas con el sitio web estático (Landing Page) para asegurar su inclusión desde el primer sprint. Asimismo, se ha evitado el anti-patrón de colocar las historias de seguridad o autenticación al inicio, priorizando antes la visualización del catálogo y la propuesta de valor.

A continuación, se detalla la tabla de estimación utilizando la escala de Story Points (1, 2, 3, 5, 8).

| # Orden | User Story Id | Título | Descripción | Story Points |
| :---: | :---: | :--- | :--- | :---: |
| 1 | US-01 | Visualizar módulos funcionales de la plataforma | Como visitante, deseo visualizar las funcionalidades principales del producto para entender cómo me ayudará a buscar o vender un vehículo. | 2 |
| 2 | US-02 | Consultar planes de membresía B2B | Como visitante gerente comercial, deseo consultar los planes de suscripción para evaluar los beneficios de afiliar mi concesionaria a la plataforma. | 2 |
| 3 | US-04 | Navegación fluida mediante menú interactivo | Como visitante, deseo utilizar un menú de navegación para saltar directamente a la sección de mi interés sin perder el contexto de la página. | 1 |
| 4 | US-08 | Explorar catálogo unificado de vehículos | Como comprador interesado, deseo visualizar un catálogo general de vehículos nuevos y usados para conocer la oferta disponible en el mercado. | 5 |
| 5 | US-10 | Visualizar ficha detallada del vehículo | Como comprador interesado, deseo revisar las especificaciones completas de un vehículo para analizar sus características técnicas antes de solicitar una pre-evaluación crediticia. | 3 |
| 6 | US-09 | Visualizar Dashboard de métricas comerciales | Como gerente comercial, deseo visualizar un panel resumen (Dashboard) al ingresar a mi cuenta para monitorear el rendimiento de mis publicaciones y prospectos. | 5 |
| 7 | US-05 | Registro de nueva cuenta para comprador | Como comprador interesado, deseo registrarme en la plataforma creando una cuenta segura para poder guardar mis preferencias y solicitar pre-evaluaciones. | 3 |
| 8 | US-06 | Inicio de sesión para compradores | Como comprador registrado, deseo iniciar sesión en mi cuenta para continuar con la búsqueda de mi vehículo y visualizar mis opciones guardadas. | 2 |
| 9 | US-07 | Inicio de sesión para concesionarias | Como gerente comercial de una concesionaria, deseo iniciar sesión en mi portal B2B para gestionar mi inventario y atender a los prospectos. | 2 |
| 10 | TS-01 | Implementar lógica de internacionalización (i18n) | Como desarrollador, deseo implementar un script para el cambio de idioma estático que actualice los textos utilizando atributos de datos sin necesidad de recargar la página web. | 3 |
| 11 | US-03 | Cambiar el idioma de la interfaz estática | Como visitante internacional, deseo cambiar el idioma de la página para leer el contenido corporativo en mi idioma de preferencia. | 1 |

**Evidencia de Product Backlog gestionado en Trello:**

![ProductBacklog-Trello](../assets/Chapter-3/productbacklog-trello.png)

**Enlace público del Product Backlog:**  
[Tablero de Product Backlog en Trello](https://trello.com/invite/b/68cef3b9540a3e849e12d1e2/ATTI55e37783ca94033bfa115ee21378ce0d092EEDDF/smartfinance-drive)

## 3.4. Impact Mapping

En esta sección el equipo explica y presenta el Impact Mapping para el modelo de negocio digital de SmartFinance Drive, elaborado en la herramienta UXPressia. Para su desarrollo, tomamos como base las fichas de los User Personas elaboradas previamente.

El proceso inició con la definición de un objetivo de negocio principal (Business Goal) estructurado bajo criterios SMART para asegurar su medición. A partir de esta meta general, el mapa se ramifica respondiendo a las siguientes interrogantes estratégicas:

* **Actors/Personas:** ¿Quiénes nos ayudarán a lograr la meta? (Alineados directamente con nuestros tres segmentos objetivo).

* **Impacts:** ¿Qué tendrían que hacer o cómo esperamos que cambien su comportamiento para ayudar a lograr la meta?

* **Deliverables:** ¿Qué podemos hacer o construir como negocio digital para provocar esos impactos?

* **User Stories:** ¿Cuáles son las historias de usuario específicas ("Como... deseo... para...") que permitirán al equipo técnico construir los entregables identificados?

A continuación, se presenta la captura del mapa estructurado con todos sus componentes consolidados.

![Impact-Mapping](../assets/Chapter-3/impact-map.png)
