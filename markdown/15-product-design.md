# Capítulo IV: Product Design

## 4.1. Style Guidelines

### 4.1.1. General Style Guidelines

El sistema de diseño de SmartFinance Drive se ha construido para transmitir confianza, innovación y fluidez. Al ser una plataforma que maneja decisiones financieras importantes y un inventario de alto valor, el diseño visual debe equilibrar la formalidad del sector automotriz con la agilidad de una startup tecnológica.

**A. Branding y Logotipo**

El isotipo y logotipo reflejan la conexión digital entre la oferta y la demanda. Se emplean versiones monocromáticas (blanco) para fondos oscuros como el Hero de la landing page, y a color para fondos claros.

- **Isotipo:** Silueta de un vehículo fusionada con nodos de red, representando la inmediatez de la conexión B2B y B2C.
- **Logotipo (Wordmark):** Texto "SmartFinance" seguido de "*Drive*" en itálica, enfatizando el dinamismo.

<p align="center">
  <img src="../assets/Chapter-4/logo.png" alt="Logotipo SmartFinance Drive" height="70" />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <img src="../assets/Chapter-4/Logo-letras.png" alt="Logotipo con letras" height="70" />
</p>

**B. Tipografía (Typography)**

Se utiliza la familia tipográfica **Inter** de Google Fonts en pesos de 400, 500, 600, 700 y 800. Esta fuente *sans-serif* maximiza la legibilidad en interfaces digitales densas en datos (como catálogos de autos y calculadoras de crédito).

- **Display / Hero:** `Inter Bold (700)` o `ExtraBold (800)` para los encabezados principales (ej. "Tu próximo auto está más cerca").
- **Headings (H2, H3):** `Inter SemiBold (600)` para títulos de secciones modulares.
- **Cuerpo (Body) y Metadatos:** `Inter Regular (400)` para descripciones largas y `Medium (500)` para etiquetas de UI y botones.

<p align="center">
  <img src="../assets/Chapter-4/Letras.jpeg" alt="Jerarquía Tipográfica" width="60%" />
</p>

**C. Paleta de Colores (Color Palette)**

La paleta se divide en colores de confianza y colores de acción, aplicados a través de variables CSS para facilitar el mantenimiento y la consistencia temática.

- **Primary Blue (`#1E56A0`) & Dark Blue (`#0D2149`):** Establecen la base visual de seguridad y profesionalismo. Utilizados en textos principales, fondos de sección y el pie de página.
- **Teal / Cyan (`#00A896`):** Actúa como color de acento tecnológico (usado en la clase `liquid-glass--teal` y `badge--teal`). Representa los estados de validación y confirmación, como el RUC verificado, la evaluación aprobada o la simulación guardada.
- **Orange / Warm (`#F4A261`):** Color de contraste para conversiones principales. Se aplica en botones de llamada a la acción primarios (clase `btn--warm` y `badge--orange`).
- **Off-White (`#F8F9FA`):** Fondo base neutral que reduce la fatiga visual (usado en la variable `--bg-light` o similar).

<p align="center">
  <img src="../assets/Chapter-4/colores-smartdrive.png" alt="Paleta de Colores" width="60%" />
</p>

**D. Micro-interacciones y Animaciones**

El diseño general integra interacciones fluidas mediante JavaScript nativo, diseñadas para usuarios con punteros precisos (mouse/trackpad):

- **Custom Cursor:** Un cursor magnético compuesto por un punto (`data-cursor-dot`) y un anillo (`data-cursor-ring`) que reacciona de forma elástica al pasar sobre enlaces y botones.
- **Magnetic Buttons:** Los botones principales (`data-magnetic`) se desplazan sutilmente hacia el cursor del usuario, mejorando la sensación táctil digital.
- **Liquid Glass Glow:** Un efecto de iluminación dinámica en tarjetas y menús de navegación (`data-liquid-glass`) que sigue las coordenadas `X` e `Y` del puntero, otorgando un aspecto premium.

### 4.1.2. Web Style Guidelines

La interfaz web (incluyendo la Landing Page y la Web Application desarrollada en Vue.js) aplica un enfoque *Responsive* y prioriza la inmersión del usuario.

- **Estructura Base (Reset & Variables):** Separación modular de estilos en archivos dedicados (`reset.css`, `variables.css`, `typography.css`, `components.css`) para garantizar la escalabilidad.
- **Efectos de Scroll (Scroll Reveal):** Los elementos clave (títulos, tarjetas de beneficios) ingresan al *viewport* con animaciones escalonadas controladas por `IntersectionObserver` (`data-reveal`), manteniendo la atención del usuario a medida que navega hacia abajo.
- **Parallax:** El fondo de la sección Hero (`data-parallax-bg`) se desplaza a una velocidad diferente al contenido, generando profundidad.
- **Componentes Modulares:** Uso intensivo de carruseles arrastrables (`data-drag-track`), acordeones para preguntas frecuentes (`data-accordion`) y selectores de idioma (`lang-switch`) para maximizar el uso del espacio.

### 4.1.3. Mobile Style Guidelines

El alcance de la aplicación móvil es Android y se centra en el inicio de sesión y la mensajería entre clientes, concesionarias y entidades financieras. Las adaptaciones específicas mantienen la usabilidad sin comprometer el estilo visual de la marca.

#### 4.1.3.1. iOS Mobile Style Guidelines

- **Alcance:** La aplicación móvil se desarrolla únicamente para Android; los lineamientos de estilo móviles se definen en la sección siguiente.

#### 4.1.3.2. Android Mobile Style Guidelines

- **Material Design 3:** Adopción de sombras modulares (Elevation) y efectos de ondas táctiles (Ripple effect) en la lista de conversaciones y en los botones de acción.
- **Barra de Navegación (Bottom Navigation):** Controles fijos en la parte inferior para acceder rápidamente a: *Chats, Nuevo chat, Perfil / Cerrar sesión*.
- **Gestos:** Soporte de gestos de desplazamiento vertical en la bandeja de conversaciones y en el historial de mensajes de cada chat.

---

## 4.2. Information Architecture

En esta sección el equipo plantea las decisiones y el sustento que dirigen la manera en que se organizará el contenido en las experiencias web y móvil, abarcando tanto el Landing Page promocional como la Aplicación Web (Marketplace B2B2C). Estas propuestas están estrictamente orientadas a que los visitantes (compradores, concesionarias y entidades financieras) se adapten con facilidad a la funcionalidad de cada producto, minimicen su carga cognitiva y encuentren rápidamente lo que necesitan sin esfuerzo.

### 4.2.1. Organization Systems

Para garantizar que los usuarios encuentren la información adecuada en el momento preciso, SmartFinance Drive implementa los siguientes esquemas de organización visual y categorización de contenido:

**Organización visual del contenido:**

- **De forma jerárquica (Visual Hierarchy):** Se aplica intensivamente en el panel de la concesionaria y en las fichas de detalle de vehículos de la aplicación. La información crítica (precio y condición del vehículo) se ubica en la parte superior con tipografía de mayor peso, mientras que los datos secundarios (kilometraje, tracción, historial) se agrupan en niveles inferiores.
- **Organización secuencial (Step-by-step):** Se utiliza exclusivamente para procesos transaccionales complejos que requieren alta concentración, como el flujo de pre-evaluación de riesgo crediticio y simulación de crédito, y la solicitud de rol de una nueva concesionaria o entidad financiera con validación de RUC. Dividir estos procesos en pasos secuenciales reduce drásticamente la tasa de abandono.
- **Organización matricial:** Implementada en la Landing Page mediante el "Segments Pager". En lugar de crear una página extensa, se utiliza una matriz horizontal deslizable que permite al visitante interactuar y alternar entre los tres perfiles del mercado (Compradores, Concesionarias Nuevos, Concesionarias Usados) dentro de un mismo bloque visual de la pantalla.

**Esquemas de categorización:**

- **Según audiencia (Audience-based):** Es el pilar del Landing Page. El contenido se bifurca desde el Hero Section con llamados a la acción distintos ("Explorar vehículos" para la demanda vs. "Soy concesionaria" para la oferta B2B).
- **Por tópicos:** Utilizado en el motor de búsqueda y catálogo de la Web App, agrupando el inventario en categorías universales como SUVs, Sedanes, Pick-ups y Hatchbacks.
- **Alfabético:** Empleado estrictamente en los menús desplegables (dropdowns) de selección de Marcas y Modelos vehiculares para facilitar la ubicación rápida.
- **Cronológico:** Utilizado en el historial de simulaciones del cliente, en la bandeja de solicitudes de la entidad financiera y en la lista de clientes que simularon sobre los vehículos de la concesionaria, priorizando visualmente los registros más recientes.

### 4.2.2. Labeling Systems

Las etiquetas de la plataforma están diseñadas con el mínimo número de palabras posibles, utilizando terminología estandarizada para evitar curvas de aprendizaje y establecer asociaciones mentales directas.

- **Asociación de Negocio:** La etiqueta **"Membresías"** en la navegación asocia inmediatamente en la mente del usuario corporativo que encontrará los planes de precios, los beneficios B2B de la plataforma y el modelo de negocio, sin necesidad de usar títulos largos como "Planes para concesionarias".
- **Asociación Institucional:** La etiqueta **"Equipo"** agrupa los perfiles, roles y códigos de los seis estudiantes fundadores (tux-squad) encargados del desarrollo del sistema.
- **Llamados a la Acción (CTAs):** Se utilizan verbos imperativos directos. En la cabecera, **"Comenzar"** funciona como la entrada principal a la aplicación web. En el catálogo, se usarán etiquetas como **"Pre-evaluar Crédito"** (asociado a la pre-evaluación de riesgo crediticio), **"Simular Crédito"** (asociado a la simulación) y **"Ver contacto"** (asociado a los datos de contacto de la concesionaria).
- **Asociación Legal Oculta:** Las etiquetas **"Términos"** y **"Privacidad"** ubicadas en el pie de página abren un panel lateral superpuesto (*Legal Drawer*) que asocia los documentos normativos sin redirigir al usuario a una nueva pestaña ni abrumarlo con texto en la página principal.

### 4.2.3. SEO Tags and Meta Tags

Para asegurar la correcta indexación y posicionamiento orgánico en motores de búsqueda, se han definido las siguientes etiquetas estructuradas para los dos entornos principales del ecosistema digital.

**Sitio Web Estático (Landing Page)**

- **Title:** `SmartFinance Drive | Marketplace de vehículos con financiamiento`
- **Description:** `SmartFinance Drive conecta compradores, concesionarias y entidades financieras con un catálogo unificado de vehículos nuevos y usados, comparación de entidades financieras y simulación de crédito vehicular.`
- **Keywords:** `marketplace automotriz, comprar auto peru, autos nuevos, autos usados, financiamiento vehicular, pre-evaluación crediticia, simulador de crédito vehicular`
- **Author:** `tux-squad`

**Web Application (Catálogo y Panel B2B)**

- **Title:** `Catálogo Unificado de Vehículos | SmartFinance Drive`
- **Description:** `Explora el catálogo de vehículos nuevos y usados, compáralos y simula tu crédito vehicular con distintas entidades financieras.`
- **Keywords:** `catálogo de autos, crédito vehicular online, autos financiados, simulador de cuotas vehiculares, comparador de entidades financieras`
- **Author:** `tux-squad`

### 4.2.4. Searching Systems

Dado el alto volumen de información que maneja un mercado unificado de vehículos, SmartFinance Drive provee herramientas de búsqueda robustas para evitar que el comprador se sienta abrumado o perdido.

- **Opciones de Búsqueda Ofrecidas:**
  - **Búsqueda Directa:** Una barra de búsqueda libre en el catálogo que permite ubicar vehículos por marca o modelo.
  - **Filtros Facetados (Faceted Search):** Los usuarios cuentan con un panel lateral en el catálogo para aplicar filtros acumulativos: *Marca*, *Precio máximo*, *Año de fabricación*, *Condición* (Nuevo/Usado) y *Concesionaria*.
- **Visualización de Datos Tras la Búsqueda:** Los resultados se presentan en una cuadrícula (*Grid*) de tarjetas de vehículos (Cards). Cada tarjeta resalta visualmente la fotografía principal, la marca/modelo, la condición y el precio del vehículo.

### 4.2.5. Navigation Systems

El sistema de navegación define las acciones y técnicas que guían a los usuarios fluidamente desde su llegada al ecosistema hasta el cumplimiento de sus objetivos transaccionales.

- **Navegación del Landing Page:**
  - **Sticky Global Header:** Una barra superior persistente que acompaña al usuario al hacer scroll hacia abajo, permitiéndole saltar a diferentes anclas de la página (Inicio, Cómo funciona, Segmentos) sin tener que regresar manualmente arriba.
  - **Smooth Scrolling:** Los hipervínculos utilizan anclajes dinámicos que deslizan la pantalla suavemente hacia la sección de interés, calculando el margen exacto para no ocultar el título debajo de la cabecera fija.
  - **Mobile Drawer Menu:** En dispositivos móviles, la navegación se oculta tras un botón *hamburger* que despliega un panel superpuesto de pantalla completa, optimizando el espacio de lectura sin sacrificar acceso a las secciones.
- **Navegación de la Web Application:**
  - **Global Navigation:** Barra superior constante con acceso directo al Catálogo, el Comparador, Financiamiento (entidades financieras, pre-evaluación, simulaciones y depreciación) y Mi panel, cuyo contenido varía según el rol del usuario (cliente, concesionaria, entidad financiera o administrador).
  - **Local Navigation (B2B):** Las concesionarias interactúan a través de un menú lateral izquierdo (*Sidebar*) que les permite navegar rápidamente entre los sub-módulos de su entorno privado: Mi Inventario (publicar, editar, listar y estado de stock), Estadísticas, Membresía y Configuración de Cuenta. Las entidades financieras acceden desde su panel a la bandeja de solicitudes asignadas y a la evaluación de cada expediente.
  - **Contextual Navigation (Breadcrumbs):** Para evitar que el comprador se desoriente en el catálogo, se implementan migas de pan en la parte superior de las fichas técnicas (ej. `Inicio > Autos Usados > Toyota > Yaris 2021`), permitiendo retroceder a categorías superiores con un solo clic.

---

## 4.3. Landing Page UI Design

En esta sección se traducen la arquitectura de la información y las decisiones de diseño en interfaces visuales para la página de aterrizaje (Landing Page) de SmartFinance Drive. Para permitir una inspección detallada sin pérdidas de resolución ni saltos de página con títulos aislados, los diseños estructurales y de alta fidelidad se presentan divididos en dos partes correlativas.

### 4.3.1. Landing Page Wireframe

![smartfinance-drive-landing-wireframe-part1](../assets/Chapter-4/smartfinance-drive-landing-wireframe-part1.png){width=65%}

![smartfinance-drive-landing-wireframe-part2](../assets/Chapter-4/smartfinance-drive-landing-wireframe-part2.png){width=65%}

### 4.3.2. Landing Page Mock-up

![smartfinance-drive-landing-mockup-part1](../assets/Chapter-4/smartfinance-drive-landing-mockup-part1.png)

![smartfinance-drive-landing-mockup-part2](../assets/Chapter-4/smartfinance-drive-landing-mockup-part2.png)

## 4.4. Mobile Applications UX/UI Design

### 4.4.1. Mobile Applications Wireframes

![mobile-wireframe-1](../assets/Chapter-4/mobile-wireframe-1.png)

![mobile-wireframe-2](../assets/Chapter-4/mobile-wireframe-2.png)

![mobile-wireframe-3](../assets/Chapter-4/mobile-wireframe-3.png)

![mobile-wireframe-4](../assets/Chapter-4/mobile-wireframe-4.png)

![mobile-wireframe-5](../assets/Chapter-4/mobile-wireframe-5.png)

![mobile-wireframe-6](../assets/Chapter-4/mobile-wireframe-6.png)

![mobile-wireframe-7](../assets/Chapter-4/mobile-wireframe-7.png)

![mobile-wireframe-8](../assets/Chapter-4/mobile-wireframe-8.png)

![mobile-wireframe-9](../assets/Chapter-4/mobile-wireframe-9.png)

![mobile-wireframe-10](../assets/Chapter-4/mobile-wireframe-10.png)

![mobile-wireframe-11](../assets/Chapter-4/mobile-wireframe-11.png)

![mobile-wireframe-12](../assets/Chapter-4/mobile-wireframe-12.png)

![mobile-wireframe-13](../assets/Chapter-4/mobile-wireframe-13.png)

![mobile-wireframe-14](../assets/Chapter-4/mobile-wireframe-14.png)

![mobile-wireframe-15](../assets/Chapter-4/mobile-wireframe-15.png)

![mobile-wireframe-16](../assets/Chapter-4/mobile-wireframe-16.png)

![mobile-wireframe-17](../assets/Chapter-4/mobile-wireframe-17.png)

![mobile-wireframe-18](../assets/Chapter-4/mobile-wireframe-18.png)

![mobile-wireframe-19](../assets/Chapter-4/mobile-wireframe-19.png)

![mobile-wireframe-20](../assets/Chapter-4/mobile-wireframe-20.png)

![mobile-wireframe-21](../assets/Chapter-4/mobile-wireframe-21.png)

![mobile-wireframe-22](../assets/Chapter-4/mobile-wireframe-22.png)

![mobile-wireframe-23](../assets/Chapter-4/mobile-wireframe-23.png)

![mobile-wireframe-24](../assets/Chapter-4/mobile-wireframe-24.png)

![mobile-wireframe-25](../assets/Chapter-4/mobile-wireframe-25.png)

![mobile-wireframe-26](../assets/Chapter-4/mobile-wireframe-26.png)

* **Enlace interactivo de Wireframes Móviles en Figma:** [https://www.figma.com/design/IsJBORA34fGF5Yn55ItYDy/SmartFinance-Drive?node-id=43-2&p=f&t=1a39oiBBrjhbTbCe-0](https://www.figma.com/design/IsJBORA34fGF5Yn55ItYDy/SmartFinance-Drive?node-id=43-2&p=f&t=1a39oiBBrjhbTbCe-0)

### 4.4.2. Mobile Applications Wireflow Diagrams

Esta sección presenta los Wireflows propuestos para la aplicación móvil Android, cuyo alcance es el inicio de sesión y la mensajería. Cada diagrama refleja un User Goal específico para los distintos User Personas, mostrando cómo la interacción en la pantalla táctil genera representaciones de nuevos estados en el flujo de la aplicación.

**Wireflow 1 (Mobile): Inicio de Sesión y Bandeja de Chats**

![mobile-wireflow-1](../assets/Chapter-4/mobile-wireflow-1.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Iniciar sesión desde su smartphone, revisar sus conversaciones activas e identificar los mensajes no leídos.

- **Explicación del Flujo y Estados UI:** El flujo inicia en la pantalla de "Inicio de Sesión", donde el usuario ingresa sus credenciales. Al autenticarse, la aplicación transita a la "Bandeja de Chats", que lista las conversaciones activas e indica con un contador las que tienen mensajes no leídos. Al seleccionar una conversación, se abre la vista de "Chat" con el historial de mensajes, desde la cual el usuario puede redactar y enviar un nuevo mensaje. Desde el menú de perfil puede cerrar sesión y regresar a la pantalla de inicio de sesión.

**Wireflow 2 (Mobile): Nuevo Chat con Concesionaria o Entidad Financiera**

![mobile-wireflow-2](../assets/Chapter-4/mobile-wireflow-2.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Iniciar una conversación con una concesionaria o con la entidad financiera que evalúa su crédito y enviar su primera consulta.

- **Explicación del Flujo y Estados UI:** El flujo comienza en la "Bandeja de Chats", desde donde el usuario presiona "Nuevo chat". La aplicación presenta la selección del interlocutor, que puede ser una concesionaria o la entidad financiera que evalúa su crédito. Tras elegir al interlocutor, se abre la vista de "Chat" sin mensajes previos. Al enviar el primer mensaje, la conversación queda registrada y se refleja como una nueva entrada en la "Bandeja de Chats".

**Wireflow 3 (Mobile): Respuesta de Mensajes como Concesionaria**

![mobile-wireflow-3](../assets/Chapter-4/mobile-wireflow-3.png)

- **User Persona:** Valeria Rojas (Concesionaria de Autos Nuevos)

- **User Goal:** Atender desde su smartphone las consultas recibidas de los clientes y responderlas.

- **Explicación del Flujo y Estados UI:** El flujo inicia en la "Bandeja de Chats" de la concesionaria, donde las conversaciones con mensajes pendientes se destacan mediante el indicador de no leídos. Al abrir una conversación, la aplicación muestra el historial de mensajes del cliente. La concesionaria redacta su respuesta y la envía, tras lo cual el mensaje se agrega al historial y el indicador de no leídos de esa conversación se actualiza. El mismo flujo aplica a la entidad financiera cuando responde a los clientes cuyo crédito evalúa.

* **Enlace interactivo de Wireflows Móviles en Overflow:** [https://overflow.io/s/JPKMSWFD](https://overflow.io/s/JPKMSWFD)

### 4.4.3. Mobile Applications Mock-ups

![mobile-mockups-1](../assets/Chapter-4/mobile-mockups-1.png)

![mobile-mockups-2](../assets/Chapter-4/mobile-mockups-2.png)

![mobile-mockups-3](../assets/Chapter-4/mobile-mockups-3.png)

![mobile-mockups-4](../assets/Chapter-4/mobile-mockups-4.png)

![mobile-mockups-5](../assets/Chapter-4/mobile-mockups-5.png)

![mobile-mockups-6](../assets/Chapter-4/mobile-mockups-6.png)

![mobile-mockups-7](../assets/Chapter-4/mobile-mockups-7.png)

![mobile-mockups-8](../assets/Chapter-4/mobile-mockups-8.png)

![mobile-mockups-9](../assets/Chapter-4/mobile-mockups-9.png)

![mobile-mockups-10](../assets/Chapter-4/mobile-mockups-10.png)

![mobile-mockups-11](../assets/Chapter-4/mobile-mockups-11.png)

![mobile-mockups-12](../assets/Chapter-4/mobile-mockups-12.png)

![mobile-mockups-13](../assets/Chapter-4/mobile-mockups-13.png)

![mobile-mockups-14](../assets/Chapter-4/mobile-mockups-14.png)

![mobile-mockups-15](../assets/Chapter-4/mobile-mockups-15.png)

![mobile-mockups-16](../assets/Chapter-4/mobile-mockups-16.png)

![mobile-mockups-17](../assets/Chapter-4/mobile-mockups-17.png)

![mobile-mockups-18](../assets/Chapter-4/mobile-mockups-18.png)

![mobile-mockups-19](../assets/Chapter-4/mobile-mockups-19.png)

![mobile-mockups-20](../assets/Chapter-4/mobile-mockups-20.png)

![mobile-mockups-21](../assets/Chapter-4/mobile-mockups-21.png)

![mobile-mockups-22](../assets/Chapter-4/mobile-mockups-22.png)

![mobile-mockups-23](../assets/Chapter-4/mobile-mockups-23.png)

![mobile-mockups-24](../assets/Chapter-4/mobile-mockups-24.png)

![mobile-mockups-25](../assets/Chapter-4/mobile-mockups-25.png)

![mobile-mockups-26](../assets/Chapter-4/mobile-mockups-26.png)

* **Enlace interactivo de Mockups Móviles en Figma:** [https://www.figma.com/design/IsJBORA34fGF5Yn55ItYDy/SmartFinance-Drive?node-id=43-2&p=f&t=1a39oiBBrjhbTbCe-0](https://www.figma.com/design/IsJBORA34fGF5Yn55ItYDy/SmartFinance-Drive?node-id=43-2&p=f&t=1a39oiBBrjhbTbCe-0)

### 4.4.4. Mobile Applications User Flow Diagrams

Esta sección detalla los flujos de usuario (User Flows) de la aplicación móvil, enfocados en el inicio de sesión y la mensajería, y optimizados para interacciones táctiles y pantallas reducidas.

**Mobile User Flow 1 (Mobile): Inicio de Sesión y Bandeja de Chats**

![mobile-userflow-1](../assets/Chapter-4/mobile-userflow-1.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Iniciar sesión en la aplicación móvil y acceder a sus conversaciones.

- **Explicación del Flujo, Decisiones y Errores:** El flujo comienza en la pantalla "Inicio de Sesión", donde el usuario ingresa sus credenciales y presiona "Ingresar". Un nodo de decisión valida las credenciales:
  - **Happy Path:** Si las credenciales son válidas, la app navega a la "Bandeja de Chats", donde se listan las conversaciones activas con su indicador de mensajes no leídos.
  - **Unhappy Path:** Si las credenciales no son válidas, la app permanece en la pantalla de inicio de sesión y muestra un mensaje de error para que el usuario corrija sus datos.

**Mobile User Flow 2 (Mobile): Nuevo Chat con Concesionaria o Entidad Financiera**

![mobile-userflow-2](../assets/Chapter-4/mobile-userflow-2.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Iniciar una conversación con una concesionaria o con la entidad financiera que evalúa su crédito y enviar un mensaje.

- **Explicación del Flujo, Decisiones y Errores:** Desde la "Bandeja de Chats", el usuario presiona "Nuevo chat", selecciona el tipo de interlocutor (concesionaria o entidad financiera) y elige al destinatario. Redacta su mensaje y presiona "Enviar". El sistema evalúa:
  - **Happy Path:** Si el mensaje se envía correctamente, la conversación se crea, el mensaje aparece en el historial del chat y la conversación se agrega a la "Bandeja de Chats".
  - **Unhappy Path:** Si el mensaje no puede enviarse, la app lo señala como no enviado y permite al usuario reintentar el envío.

**Mobile User Flow 3 (Mobile): Respuesta de Mensajes**

![mobile-userflow-3](../assets/Chapter-4/mobile-userflow-3.png)

- **User Persona:** Roberto García (Concesionaria de Autos Usados)

- **User Goal:** Revisar los mensajes no leídos de sus clientes y responderlos.

- **Descripción del Happy Path:** El usuario inicia el flujo en la "Bandeja de Chats", donde identifica las conversaciones con mensajes no leídos. El primer nodo de decisión evalúa si existe una conversación pendiente. Al haberla, transita al chat, donde revisa el historial de mensajes. En el segundo nodo de decisión, el usuario redacta y envía su respuesta; con el envío exitoso, el mensaje queda registrado en el historial y el flujo llega al nodo de éxito final. El mismo flujo aplica a la entidad financiera al responder a los clientes cuyo crédito evalúa.

- **Descripción del Unhappy Path 1 (Sin conversaciones pendientes):** Si en el primer nodo de decisión no existen conversaciones con mensajes no leídos, el flujo finaliza anticipadamente mostrando la bandeja sin pendientes.

- **Descripción del Unhappy Path 2 (Envío fallido):** Si en el segundo nodo de decisión el mensaje no puede enviarse, la app lo señala como no enviado y permite reintentar el envío.

* **Enlace interactivo de User Flows Móviles en Overflow:** [https://overflow.io/s/JPKMSWFD](https://overflow.io/s/JPKMSWFD)

## 4.5. Mobile Applications Prototyping

### 4.5.1. Android Mobile Applications Prototyping

[https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20Android%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ea167f36b%2D6ab9%2D4b43%2Dac6d%2D5be3407131c0](https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20Android%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ea167f36b%2D6ab9%2D4b43%2Dac6d%2D5be3407131c0)

### 4.5.2. iOS Mobile Applications Prototyping

[https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20Iphone%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ee04382ee%2D4fe6%2D4860%2Daf80%2Dda7f7f9cfd64](https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20Iphone%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ee04382ee%2D4fe6%2D4860%2Daf80%2Dda7f7f9cfd64)

## 4.6. Web Applications UX/UI Design

### 4.6.1. Web Applications Wireframes

![webapp-wireframe-1](../assets/Chapter-4/webapp-wireframe-1.png)

![webapp-wireframe-2](../assets/Chapter-4/webapp-wireframe-2.png)

![webapp-wireframe-3](../assets/Chapter-4/webapp-wireframe-3.png)

![webapp-wireframe-4](../assets/Chapter-4/webapp-wireframe-4.png)

![webapp-wireframe-5](../assets/Chapter-4/webapp-wireframe-5.png)

![webapp-wireframe-6](../assets/Chapter-4/webapp-wireframe-6.png)

![webapp-wireframe-7](../assets/Chapter-4/webapp-wireframe-7.png)

![webapp-wireframe-8](../assets/Chapter-4/webapp-wireframe-8.png)

![webapp-wireframe-9](../assets/Chapter-4/webapp-wireframe-9.png)

![webapp-wireframe-10](../assets/Chapter-4/webapp-wireframe-10.png)

![webapp-wireframe-11](../assets/Chapter-4/webapp-wireframe-11.png)

![webapp-wireframe-12](../assets/Chapter-4/webapp-wireframe-12.png)

![webapp-wireframe-13](../assets/Chapter-4/webapp-wireframe-13.png)

![webapp-wireframe-14](../assets/Chapter-4/webapp-wireframe-14.png)

![webapp-wireframe-15](../assets/Chapter-4/webapp-wireframe-15.png)

![webapp-wireframe-16](../assets/Chapter-4/webapp-wireframe-16.png)

![webapp-wireframe-17](../assets/Chapter-4/webapp-wireframe-17.png)

![webapp-wireframe-18](../assets/Chapter-4/webapp-wireframe-18.png)

![webapp-wireframe-19](../assets/Chapter-4/webapp-wireframe-19.png)

![webapp-wireframe-20](../assets/Chapter-4/webapp-wireframe-20.png)

![webapp-wireframe-21](../assets/Chapter-4/webapp-wireframe-21.png)

![webapp-wireframe-22](../assets/Chapter-4/webapp-wireframe-22.png)

![webapp-wireframe-23](../assets/Chapter-4/webapp-wireframe-23.png)

![webapp-wireframe-24](../assets/Chapter-4/webapp-wireframe-24.png)

![webapp-wireframe-25](../assets/Chapter-4/webapp-wireframe-25.png)

![webapp-wireframe-26](../assets/Chapter-4/webapp-wireframe-26.png)

* **Enlace interactivo de Wireframes Web en Figma:** [https://www.figma.com/design/IsJBORA34fGF5Yn55ItYDy/SmartFinance-Drive?node-id=43-2&p=f&t=1a39oiBBrjhbTbCe-0](https://www.figma.com/design/IsJBORA34fGF5Yn55ItYDy/SmartFinance-Drive?node-id=43-2&p=f&t=1a39oiBBrjhbTbCe-0)

### 4.6.2. Web Applications Wireflow Diagrams

Esta sección presenta los Wireflows propuestos para la aplicación web. Los flujos ilustran cómo la interacción del usuario genera cambios de estado en la interfaz para cumplir sus objetivos principales.

**Wireflow 1 (Web): Búsqueda, Comparación, Pre-evaluación y Simulación**

![webapp-wireflow-1](../assets/Chapter-4/webapp-wireflow-1.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Explorar el catálogo mediante filtros, comparar vehículos, obtener su pre-evaluación de riesgo crediticio y simular el crédito con varias entidades financieras para enviarlo a evaluación.

- **Explicación del Flujo y Estados UI:** El flujo comienza en la "Página de Inicio Web", desde donde el usuario accede al catálogo. Al aplicar filtros por marca, precio máximo, año, condición o concesionaria, la plataforma actualiza dinámicamente la grilla de vehículos disponibles. El usuario hace clic en una tarjeta para abrir la "Ficha Técnica Completa", donde visualiza las especificaciones y el simulador de cuotas, y puede añadir el vehículo al comparador (máximo 2 unidades). Al presionar "Pre-evaluar Crédito", el sistema presenta el resultado de la pre-evaluación de riesgo (score, DTI y Risk Tier). Desde allí, el usuario crea la simulación de crédito, compara las cotizaciones de distintas entidades financieras y envía la simulación elegida a evaluación, tras lo cual se despliega el estado de "Confirmación de Envío".

**Wireflow 2 (Web): Publicación de Vehículo y Estadísticas de la Concesionaria**

![webapp-wireflow-2](../assets/Chapter-4/webapp-wireflow-2.png)

- **User Persona:** Valeria Rojas (Concesionaria de Autos Nuevos)

- **User Goal:** Publicar un vehículo en el catálogo y consultar las estadísticas y los datos de contacto de los clientes que simularon sobre sus unidades.

- **Explicación del Flujo y Estados UI:** El usuario inicia sesión y accede a "Mi panel", desde donde navega a "Mi Inventario" mediante la barra lateral. Al accionar el botón "Publicar vehículo", el sistema abre el formulario con los datos técnicos y las imágenes de la unidad. Tras guardar, la tabla de inventario se recarga reflejando el vehículo publicado y su estado de stock. Desde la sección "Estadísticas", la concesionaria consulta las vistas y simulaciones por vehículo y accede a los datos de contacto de los clientes que simularon sobre sus unidades.

**Wireflow 3 (Web): Bandeja de la Entidad Financiera y Evaluación de Solicitudes**

![webapp-wireflow-3](../assets/Chapter-4/webapp-wireflow-3.png)

- **User Persona:** Entidad Financiera

- **User Goal:** Revisar las solicitudes asignadas y emitir la evaluación oficial de cada simulación.

- **Explicación del Flujo y Estados UI:** El flujo inicia en "Mi panel" de la entidad financiera, desde donde accede a la "Bandeja de Solicitudes", que lista las simulaciones asignadas. Al seleccionar una solicitud, la vista cambia al "Detalle del Expediente" del cliente. Desde allí, la entidad registra su evaluación como aprobada o rechazada junto con sus notas. Al guardar, el flujo finaliza confirmando la acción, actualizando el estado de la solicitud en la bandeja y notificando por correo al cliente.

* **Enlace interactivo de Wireflows Web en Overflow:** [https://overflow.io/s/JPKMSWFD](https://overflow.io/s/JPKMSWFD)

### 4.6.3. Web Applications Mock-ups

![webapp-mockups-1](../assets/Chapter-4/webapp-mockups-1.png)

![webapp-mockups-2](../assets/Chapter-4/webapp-mockups-2.png)

![webapp-mockups-3](../assets/Chapter-4/webapp-mockups-3.png)

![webapp-mockups-4](../assets/Chapter-4/webapp-mockups-4.png)

![webapp-mockups-5](../assets/Chapter-4/webapp-mockups-5.png)

![webapp-mockups-6](../assets/Chapter-4/webapp-mockups-6.png)

![webapp-mockups-7](../assets/Chapter-4/webapp-mockups-7.png)

![webapp-mockups-8](../assets/Chapter-4/webapp-mockups-8.png)

![webapp-mockups-9](../assets/Chapter-4/webapp-mockups-9.png)

![webapp-mockups-10](../assets/Chapter-4/webapp-mockups-10.png)

![webapp-mockups-11](../assets/Chapter-4/webapp-mockups-11.png)

![webapp-mockups-12](../assets/Chapter-4/webapp-mockups-12.png)

![webapp-mockups-13](../assets/Chapter-4/webapp-mockups-13.png)

![webapp-mockups-14](../assets/Chapter-4/webapp-mockups-14.png)

![webapp-mockups-15](../assets/Chapter-4/webapp-mockups-15.png)

![webapp-mockups-16](../assets/Chapter-4/webapp-mockups-16.png)

![webapp-mockups-17](../assets/Chapter-4/webapp-mockups-17.png)

![webapp-mockups-18](../assets/Chapter-4/webapp-mockups-18.png)

![webapp-mockups-19](../assets/Chapter-4/webapp-mockups-19.png)

![webapp-mockups-20](../assets/Chapter-4/webapp-mockups-20.png)

![webapp-mockups-21](../assets/Chapter-4/webapp-mockups-21.png)

![webapp-mockups-22](../assets/Chapter-4/webapp-mockups-22.png)

![webapp-mockups-23](../assets/Chapter-4/webapp-mockups-23.png)

![webapp-mockups-24](../assets/Chapter-4/webapp-mockups-24.png)

![webapp-mockups-25](../assets/Chapter-4/webapp-mockups-25.png)

![webapp-mockups-26](../assets/Chapter-4/webapp-mockups-26.png)

* **Enlace interactivo de Mockups Web en Figma:** [https://www.figma.com/design/IsJBORA34fGF5Yn55ItYDy/SmartFinance-Drive?node-id=43-2&p=f&t=1a39oiBBrjhbTbCe-0](https://www.figma.com/design/IsJBORA34fGF5Yn55ItYDy/SmartFinance-Drive?node-id=43-2&p=f&t=1a39oiBBrjhbTbCe-0)

### 4.6.4. Web Applications User Flow Diagrams

Esta sección presenta la propuesta de User Flows para la aplicación web. Se ha considerado un User Flow para cada objetivo principal, incluyendo los mock-ups de las pantallas, la ruta esperada (Happy Path) y las rutas alternativas de error (Unhappy Paths) dictadas por los nodos de decisión del sistema.

**User Flow 1 (Web): Pre-evaluación de Riesgo y Simulación Multi-banco**

![webapp-userflow-1](../assets/Chapter-4/webapp-userflow-1.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Obtener la pre-evaluación de riesgo crediticio para una unidad específica, simular el crédito con varias entidades financieras y enviarlo a evaluación.

- **Explicación del Flujo, Decisiones y Errores:** Desde la ficha del vehículo, el usuario hace clic en "Pre-evaluar Crédito". El sistema valida si el usuario ha iniciado sesión; de lo contrario, abre el modal de autenticación. Una vez autenticado, el sistema verifica que el perfil socioeconómico esté registrado:
  - **Happy Path:** Si el perfil está completo, la plataforma genera la pre-evaluación de riesgo (score, DTI y Risk Tier). El usuario crea la simulación, compara las cotizaciones de las entidades financieras y envía la simulación elegida a evaluación de la entidad.
  - **Unhappy Path:** Si el perfil socioeconómico no está registrado, el sistema redirige al usuario a completarlo antes de continuar. Si la pre-evaluación indica un nivel de riesgo alto por capacidad de endeudamiento insuficiente, el sistema muestra el resultado y permite ajustar la cuota inicial, el plazo o explorar vehículos de menor valor.

**User Flow 2 (Web): Publicación de Vehículo**

![webapp-userflow-2](../assets/Chapter-4/webapp-userflow-2.png)

- **User Persona:** Valeria Rojas (Concesionaria de Autos Nuevos)

- **User Goal:** Publicar un vehículo en el catálogo para exponer su inventario a los compradores.

- **Explicación del Flujo, Decisiones y Errores:** Desde "Mi Inventario", la concesionaria hace clic en "Publicar vehículo". El sistema verifica que la concesionaria cuente con una membresía activa:
  - **Happy Path:** Si la membresía está activa y los datos e imágenes del vehículo son válidos, el sistema publica la unidad, que pasa a aparecer en el catálogo público y en el listado de vehículos publicados de la concesionaria.
  - **Unhappy Path:** Si la concesionaria no cuenta con una membresía activa, el sistema la redirige a la selección de membresía. Si faltan datos obligatorios del vehículo, el sistema señala los campos incompletos y no permite publicar hasta corregirlos.

**User Flow 3 (Web): Evaluación de Solicitudes por la Entidad Financiera**

![webapp-userflow-3](../assets/Chapter-4/webapp-userflow-3.png)

- **User Persona:** Entidad Financiera

- **User Goal:** Revisar una solicitud asignada y emitir la evaluación oficial de la simulación.

- **Descripción del Happy Path:** La entidad financiera inicia en la "Bandeja de Solicitudes". En el primer nodo de decisión se verifica si existen solicitudes asignadas. Al haberlas, selecciona una y accede al detalle del expediente del cliente. En el segundo nodo de decisión, la entidad emite su evaluación como aprobada junto con sus notas, el sistema notifica al cliente por correo y el flujo termina exitosamente en la confirmación.

- **Descripción del Unhappy Path 1 (Sin solicitudes asignadas):** Si en el primer nodo de decisión no existen solicitudes asignadas, el flujo finaliza mostrando la bandeja vacía.

- **Descripción del Unhappy Path 2 (Solicitud rechazada):** Si en el segundo nodo de decisión la entidad rechaza la solicitud, registra sus notas, el sistema notifica el resultado al cliente por correo y el flujo finaliza con la solicitud en estado rechazado.

* **Enlace interactivo de User Flows Web en Overflow:** [https://overflow.io/s/JPKMSWFD](https://overflow.io/s/JPKMSWFD)

## 4.7. Web Applications Prototyping

[https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20WebApp%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ede73efa3%2Deae7%2D4cf7%2D8c90%2Dc09d17c6b910](https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20WebApp%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ede73efa3%2Deae7%2D4cf7%2D8c90%2Dc09d17c6b910)

## 4.8. Domain-Driven Software Architecture

A continuación se presenta la documentación detallada de la arquitectura de software basada en el modelo C4 y en los principios de Domain-Driven Design (DDD).

* **Código DSL de la Arquitectura C4 en el repositorio:** [https://github.com/tux-squad/smartfinance-drive-project-report/blob/main/assets/software_architecture_diagrams.dls](https://github.com/tux-squad/smartfinance-drive-project-report/blob/main/assets/software_architecture_diagrams.dls)

### 4.8.1. Software Architecture Context Diagram

El diagrama de contexto (Nivel 1) ilustra la plataforma SmartFinance Drive como el sistema central que conecta la oferta y la demanda del sector automotriz. En este nivel se identifican las interacciones principales con los actores y sistemas externos:

![Context Diagram](../assets/Chapter-4/ContextDiagram.png)

- **Cliente (Comprador Interesado)**: Usuario final que busca y compara vehículos, compara entidades financieras, genera su pre-evaluación de riesgo crediticio, simula créditos y se comunica por mensajería con concesionarias y entidades financieras.

- **Concesionaria**: Cliente corporativo que publica su inventario de vehículos nuevos o usados, consulta las estadísticas de sus vehículos y los datos de contacto de los clientes que simularon, responde mensajes y gestiona el pago de sus membresías B2B.

- **Entidad Financiera**: Rol de usuario registrado en la plataforma que recibe las simulaciones asignadas, emite la evaluación oficial (aprobada o rechazada con notas) y responde mensajes de los clientes.

- **Super Administrador**: Actor encargado de gestionar la configuración global de la plataforma y administrar usuarios y roles.

- **Servicios SUNAT (Externo)**: Sistema gubernamental utilizado para la validación de números de RUC, estado y condición de las empresas.

- **Brevo (Externo)**: Servicio de correo transaccional utilizado para la verificación de correo y las notificaciones de resultado de evaluación.

- **Stripe (Externo)**: Pasarela de pagos encargada de procesar los cobros de las suscripciones B2B y la facturación de las concesionarias.

---

### 4.8.2. Software Architecture Container Diagrams

El diagrama de contenedores (Nivel 2) desglosa el sistema SmartFinance Drive en sus aplicaciones principales y componentes de almacenamiento de datos. El sistema se estructura de la siguiente manera:

![Container Diagram](../assets/Chapter-4/ContainerDiagram.png)

- **Landing Page**: Aplicación web estática (HTML/CSS/JS) orientada a la presentación del producto y conversión de visitantes.

- **Web Application**: Frontend tipo SPA desarrollado en Vue.js, que proporciona las interfaces para todos los roles: el catálogo y las herramientas de financiamiento del cliente, el panel de concesionarias, la bandeja de entidades financieras y la administración de roles.

- **Mobile App**: Aplicación móvil nativa para Android (Kotlin y Jetpack Compose), enfocada en el inicio de sesión y la mensajería entre clientes, concesionarias y entidades financieras.

- **Backend API**: Implementado como un monolito modular basado en Java Spring Boot. Este contenedor centraliza toda la lógica de negocio estructurada en 8 Bounded Contexts independientes: IAM, Profiles, Catalog, Partners, Financing, Scoring, Projections y Billing.

- **Base de Datos**: Sistema de gestión de bases de datos relacional PostgreSQL, encargado de almacenar de forma persistente la información de usuarios, simulaciones, inventario y facturación de todos los contextos.

---

### 4.8.3. Software Architecture Components Diagrams

En el Nivel 3, se realiza un acercamiento a la estructura interna del Backend API. Al seguir los principios de Clean Architecture, cada Bounded Context se desglosa en cuatro capas principales: Interfaces (Controladores REST), Application (Casos de Uso), Domain (Reglas de negocio y Agregados) e Infrastructure (Adaptadores de persistencia y clientes externos).

**Component Diagram: IAM Context**

El contexto IAM encapsula la lógica de autenticación, autorización y control de acceso del sistema.

![Component Diagram IAM](../assets/Chapter-4/ComponentDiagram_IAM.png)

- **Responsabilidad**: Gestión del ciclo de vida de identidades, tokens JWT, revocaciones y roles (Cliente, Concesionaria, Entidad Financiera, Administrador).

- **Componentes clave**: El servicio de dominio `AuthenticationService` coordina la emisión y validación de credenciales a través del adaptador de persistencia en PostgreSQL.

**Component Diagram: Profiles Context**

El contexto Profiles gestiona la información demográfica, de contacto y el historial operativo de los usuarios.

![Component Diagram Profiles](../assets/Chapter-4/ComponentDiagram_Profiles.png)

- **Responsabilidad**: Administración de perfiles individuales de clientes y perfiles corporativos de concesionarias y entidades financieras.

- **Componentes clave**: Implementa validaciones de completitud de perfil necesarias para desbloquear la funcionalidad de pre-evaluación crediticia.

**Component Diagram: Catalog Context**

El contexto Catalog gestiona el inventario completo de vehículos nuevos y usados.

![Component Diagram Catalog](../assets/Chapter-4/ComponentDiagram_Catalog.png)

- **Responsabilidad**: Mantenimiento de especificaciones técnicas, precios, imágenes, kilometraje y estado de disponibilidad de cada vehículo publicado.

- **Componentes clave**: Expone adaptadores de búsqueda optimizados para consultas de alta velocidad y filtrado por múltiples atributos.

**Component Diagram: Partners Context**

El contexto Partners centraliza las integraciones con concesionarias y entidades financieras registradas en la plataforma.

![Component Diagram Partners](../assets/Chapter-4/ComponentDiagram_Partners.png)

- **Responsabilidad**: Administración de entidades bancarias asociadas, sus rangos de tasas (TEA/TCEA), comisiones de seguros y la integración con servicios gubernamentales.

- **Componentes clave**: Administra los agregados `FinancialEntity` y `RateBenchmark`, y utiliza la capa de infraestructura para realizar llamadas HTTP externas a la API de SUNAT.

**Component Diagram: Financing Context**

El contexto Financing representa el Core Domain de la plataforma.

![Component Diagram Financing](../assets/Chapter-4/ComponentDiagram_Financing.png)

- **Responsabilidad**: Orquesta la creación de planes de financiamiento, genera cronogramas de cuotas aplicando el método francés y calcula indicadores como VAN, TIR y TCEA.

- **Componentes clave**: El servicio de dominio `FinancingPlanBuilder` ejecuta los algoritmos matemáticos, y el agregado `Simulation` encapsula los periodos de pago generados para su persistencia en la base de datos.

**Component Diagram: Scoring Context**

El contexto Scoring se encarga del análisis de viabilidad crediticia.

![Component Diagram Scoring](../assets/Chapter-4/ComponentDiagram_Scoring.png)

- **Responsabilidad**: Evalúa la capacidad de endeudamiento cruzando la cuota proyectada con los ingresos del usuario para calcular el Ratio de Cobertura de Deuda (DTI).

- **Componentes clave**: Asigna un nivel de riesgo crediticio (Risk Tier) que se comunica directamente con el contexto de financiamiento para ajustar automáticamente la tasa de interés ofrecida.

**Component Diagram: Projections Context**

El contexto Projections gestiona la proyección de depreciación para apoyar la decisión de compra.

![Component Diagram Projections](../assets/Chapter-4/ComponentDiagram_Projections.png)

- **Responsabilidad**: Estima la depreciación técnica y comercial del vehículo a lo largo del tiempo (2, 3 o 5 años).

- **Componentes clave**: A través del agregado `DepreciationProjection`, contrasta la curva de valor del vehículo contra la cuota balón del crédito para informar al usuario sobre la conveniencia de su compra.

**Component Diagram: Billing Context**

El contexto Billing gestiona la monetización y modelo de negocio de SmartFinance Drive.

![Component Diagram Billing](../assets/Chapter-4/ComponentDiagram_Billing.png)

- **Responsabilidad**: Control de los planes de suscripción B2B (SaaS), facturación, y cobro de membresías a las concesionarias.

- **Componentes clave**: Maneja los agregados `Subscription`, `Plan` e `Invoice`. Su capa de infraestructura integra el SDK de Stripe para la generación de checkouts de pago y la escucha asíncrona de webhooks.

## 4.9. Software Object-Oriented Design

### 4.9.1. Class Diagrams

El siguiente diagrama de clases general representa la estructura orientada a objetos de toda la plataforma SmartFinance. Se modelan las entidades principales del dominio y sus interacciones, promoviendo una separación clara de responsabilidades bajo el enfoque de Domain-Driven Design (DDD).

![General Class Diagram](../assets/Chapter-4/oopgeneral.png "Diagrama de Clases General")

**Bounded Context: Identity & Security**

Este diagrama representa el contexto de Identity & Security, el cual centraliza la autenticación, autorización y administración de usuarios del sistema. En este contexto, el Aggregate Root es `User`, el cual contiene la información de acceso y sus vínculos directos con los roles del sistema (`Role`). Además, se gestionan los tokens revocados (`RevokedToken`) para garantizar la integridad y seguridad de las sesiones activas. El diseño separa claramente las responsabilidades de identidad de la información personal del usuario.

![Class diagram identity](../assets/Chapter-4/oop1.png "Identity & Security")

**Bounded Context: Profile**

El contexto Profile encapsula todo lo relacionado con la representación y datos demográficos de los usuarios en el sistema. El Aggregate Root es `Profile`, que contiene la información no sensible y de contacto (nombres, teléfono, país), así como datos críticos para el negocio como ingresos mensuales y estado laboral. Este diseño permite a los usuarios gestionar su identidad financiera y es el punto de integración principal con los módulos de evaluación crediticia.

![Class diagram profile](../assets/Chapter-4/oop2.png "Profile")

**Bounded Context: Subscriptions & Billing**

El diagrama de clases presentado pertenece al contexto de Subscriptions & Billing, el cual representa el núcleo de las funcionalidades relacionadas con la gestión de planes SaaS y facturación. El Aggregate Root principal es `Subscription`, que vincula a un usuario con un `Plan` específico. La entidad `Invoice` encapsula los datos relacionados con el cobro, montos y fechas de pago. Este diseño refleja un enfoque modular preparado para integraciones con gateways de pago externos (como Stripe) mediante capas de infraestructura.

![Class diagram subscriptions](../assets/Chapter-4/oop3.png "Subscriptions & Billing")

**Bounded Context: Vehicle Catalog**

Este esquema representa la lógica del contexto de Vehicle Catalog. La clase principal es `Vehicle`, que almacena los detalles técnicos, de marca, modelo, año de fabricación y precio de los automóviles disponibles para financiamiento. Su diseño flexible permite gestionar de manera eficiente el catálogo que los usuarios explorarán antes de realizar una cotización.

![Class diagram vehicle catalog](../assets/Chapter-4/oop4.png "Vehicle Catalog")

**Bounded Context: Financial Configuration**

Este diagrama enfoca su diseño en la parametrización del mercado a través del contexto Financial Configuration. El Aggregate Root es `FinancialEntity`, representando a los bancos, cajas o instituciones de crédito. Se relaciona con `RateBenchmark`, que modela las tasas de referencia (TEA, TCEA), tipos de interés y reglas de negocio vigentes que dictan las condiciones de financiamiento en la plataforma.

![Class diagram financial config](../assets/Chapter-4/oop5.png "Financial Configuration")

**Bounded Context: Simulation**

Este esquema representa el contexto Simulation, el motor matemático y central del sistema. El Aggregate Root es `Simulation`, que encapsula todas las variables ingresadas por el usuario (cuota inicial, plazo, tasa seleccionada, monto financiado). Se compone de múltiples instancias de `SimulationPaymentPeriod`, las cuales modelan el detalle individual de cada cuota del cronograma de pagos (amortización, interés, seguros y saldos).

![Class diagram simulation](../assets/Chapter-4/oop6.png "Simulation")

**Bounded Context: Planning**

El contexto de Planning aborda la proyección y viabilidad de las decisiones del usuario. Modela clases analíticas como `CreditScore`, que evalúa la capacidad de endeudamiento, ratio DTI (Debt-to-Income) y el nivel de riesgo del perfil frente a una simulación; y `DepreciationProjection`, que encapsula el comportamiento del valor del vehículo a lo largo del tiempo, permitiendo contrastarlo con la cuota balón del crédito.

![Class diagram planning](../assets/Chapter-4/oop7.png "Planning")

### 4.9.2. Class Dictionary

| Entidad | Descripción |
| :--- | :--- |
| **User** | Entidad raíz de seguridad que representa a cualquier persona que interactúa con la plataforma, almacenando sus credenciales de acceso y estado de cuenta. |
| **Role** | Define los permisos y el nivel de acceso asignado a un usuario dentro del sistema (ej. Cliente, Concesionario, Entidad Financiera, Administrador). |
| **RevokedToken** | Entidad de seguridad utilizada para llevar el registro de tokens de sesión que han sido invalidados o han expirado. |
| **Profile** | Contiene la información personal, laboral y financiera detallada del usuario, fundamental para la evaluación de perfiles crediticios. |
| **SunatRuc** | Entidad de apoyo (o Value Object) utilizada para consultar y verificar información tributaria y empresarial conectada al usuario. |
| **Plan** | Define los paquetes de suscripción disponibles en la plataforma, estableciendo límites operativos (ej. simulaciones máximas) y precios. |
| **Subscription** | Representa el contrato activo o inactivo de un usuario con un plan específico, gestionando su ciclo de facturación. |
| **Invoice** | Documento que registra los detalles de facturación, montos y el estado de los pagos recurrentes generados por una suscripción. |
| **Vehicle** | Representa un automóvil disponible en el catálogo, detallando sus características físicas, estado, año de fabricación y precio de mercado. |
| **VehiclePage** | Objeto que agrupa una lista paginada de vehículos para optimizar las consultas y búsquedas del catálogo en el frontend. |
| **FinancialEntity** | Representa a un banco, caja o institución financiera aliada que provee las tasas y condiciones para los créditos vehiculares. |
| **RateBenchmark** | Encapsula las tasas referenciales (TEA, TCEA) y condiciones macroeconómicas dictadas por una entidad financiera en un periodo de tiempo. |
| **Simulation** | Representa un escenario de crédito vehicular generado por el usuario, consolidando el vehículo, la entidad financiera elegida, plazos y montos totales. |
| **SimulationPaymentPeriod** | Modela el detalle individual de cada cuota dentro del cronograma de pagos de una simulación (desglose de interés, amortización de capital, seguros y saldos). |
| **CreditScore** | Evaluación de riesgo financiero calculada para un perfil específico, indicando métricas clave como el ratio deuda-ingreso (DTI) para determinar viabilidad. |
| **DepreciationProjection** | Proyección de la pérdida de valor de un vehículo en el tiempo, utilizada para informar al usuario sobre su inversión a mediano y largo plazo. |

## 4.10. Database Design

### 4.10.1. Relational/Non-Relational Database Diagram

![Database diagram general](../assets/Chapter-4/dbgeneral.png "Diagrama de base de datos general")

**Bounded Context: Identity & Security**

Este esquema representa la lógica del contexto de identidad y seguridad de SmartFinance. La tabla `users` almacena las credenciales de acceso y controles de bloqueo de los usuarios. Se apoya en las tablas `roles` y `user_roles` para la gestión de permisos, mientras que `revoked_tokens` maneja la invalidación de sesiones por seguridad.

![Database diagram identity](../assets/Chapter-4/db1.png "Identity & Security")

**Bounded Context: Profile**

Este esquema representa el contexto de gestión de clientes. La tabla `profiles` concentra toda la información personal, financiera (ingresos mensuales) y laboral del usuario, la cual es indispensable para perfilar al cliente antes de una evaluación crediticia.

![Database diagram profile](../assets/Chapter-4/db2.png "Profile")

**Bounded Context: Subscriptions & Billing**

Este esquema controla el modelo de negocio SaaS de la plataforma. La tabla `plans` define los límites de simulaciones y vehículos por paquete. La tabla `subscriptions` vincula al usuario con un plan activo usando los identificadores de Stripe, y la tabla `invoices` registra el historial de facturación y cobros.

![Database diagram subscriptions](../assets/Chapter-4/db3.png "Subscriptions & Billing")

**Bounded Context: Vehicle Catalog**

Este esquema aísla la gestión del inventario automotriz. La tabla `vehicles` centraliza los datos técnicos, año de fabricación, marca, condición y precio del vehículo a financiar, estableciendo además su vínculo con una entidad financiera.

![Database diagram vehicle catalog](../assets/Chapter-4/db4.png "Vehicle Catalog")

**Bounded Context: Financial Configuration**

Este esquema administra los parámetros macroeconómicos del sistema. La tabla `financial_entities` registra los bancos o financieras disponibles, mientras que `financial_entity_rate_benchmarks` almacena el historial de tasas referenciales aplicables a los créditos.

![Database diagram financial config](../assets/Chapter-4/db5.png "Financial Configuration")

**Bounded Context: Simulation**

Este esquema define el núcleo de cálculo del sistema. La tabla `simulations` concentra todas las variables del crédito (TEA, TCEA, cuota inicial, seguros y montos a financiar). La tabla `simulation_payment_periods` desglosa el cronograma mes a mes, separando el capital, interés y los seguros aplicados en cada cuota.

![Database diagram simulation](../assets/Chapter-4/db6.png "Simulation")

**Bounded Context: Planning**

Este esquema se enfoca en el análisis de la viabilidad del crédito y la proyección del valor del vehículo. La tabla `credit_scores` evalúa el riesgo financiero del perfil asociado a una simulación particular, determinando ratios de deuda e ingresos. La tabla `depreciation_projections` proyecta el valor futuro del vehículo, calculando la depreciación anual.

![Database diagram planning](../assets/Chapter-4/db7.png "Planning")
