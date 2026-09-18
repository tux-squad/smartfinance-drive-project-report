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
- **Teal / Cyan (`#00A896`):** Actúa como color de acento tecnológico (usado en la clase `liquid-glass--teal` y `badge--teal`). Representa las funciones de Inteligencia Artificial y validación.
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

La interfaz web (incluyendo la Landing Page y futuras Web Apps) aplica un enfoque *Responsive* y prioriza la inmersión del usuario.

- **Estructura Base (Reset & Variables):** Separación modular de estilos en archivos dedicados (`reset.css`, `variables.css`, `typography.css`, `components.css`) para garantizar la escalabilidad.
- **Efectos de Scroll (Scroll Reveal):** Los elementos clave (títulos, tarjetas de beneficios) ingresan al *viewport* con animaciones escalonadas controladas por `IntersectionObserver` (`data-reveal`), manteniendo la atención del usuario a medida que navega hacia abajo.
- **Parallax:** El fondo de la sección Hero (`data-parallax-bg`) se desplaza a una velocidad diferente al contenido, generando profundidad.
- **Componentes Modulares:** Uso intensivo de carruseles arrastrables (`data-drag-track`), acordeones para preguntas frecuentes (`data-accordion`) y selectores de idioma (`lang-switch`) para maximizar el uso del espacio.

### 4.1.3. Mobile Style Guidelines

El ecosistema móvil demanda adaptaciones específicas para mantener la usabilidad sin comprometer el estilo visual de la marca.

#### 4.1.3.1. iOS Mobile Style Guidelines

- **Navegación Táctil:** Reemplazo de los efectos de *hover* y cursores magnéticos (deshabilitados vía media queries táctiles) por *Tap Highlights* nativos.
- **Componentes Modales:** Implementación de modales de pantalla inferior (Bottom Sheets) para la pre-evaluación crediticia externa, respetando las *Human Interface Guidelines* de Apple y evitando salidas disruptivas del flujo principal.
- **Safe Areas:** Respeto estricto del *notch* superior y el indicador de inicio inferior en la estructura de vistas de la aplicación iOS.

#### 4.1.3.2. Android Mobile Style Guidelines

- **Material Design 3:** Adopción de sombras modulares (Elevation) y efectos de ondas táctiles (Ripple effect) en listas de vehículos y botones de acción.
- **Barra de Navegación (Bottom Navigation):** Controles fijos en la parte inferior para acceder rápidamente a: *Búsqueda, Mi Perfil, Recomendaciones IA*.
- **Gestos:** Soporte total para gestos de deslizamiento horizontal (Swipe) en galerías de imágenes de los autos y para descartar tarjetas de recomendación de la IA.

---

## 4.2. Information Architecture

En esta sección el equipo plantea las decisiones y el sustento que dirigen la manera en que se organizará el contenido en las experiencias web y móvil, abarcando tanto el Landing Page promocional como la Aplicación Web (Marketplace/B2B). Estas propuestas están estrictamente orientadas a que los visitantes (compradores y concesionarias) se adapten con facilidad a la funcionalidad de cada producto, minimicen su carga cognitiva y encuentren rápidamente lo que necesitan sin esfuerzo.

### 4.2.1. Organization Systems

Para garantizar que los usuarios encuentren la información adecuada en el momento preciso, SmartFinance Drive implementa los siguientes esquemas de organización visual y categorización de contenido:

**Organización visual del contenido:**

- **De forma jerárquica (Visual Hierarchy):** Se aplica intensivamente en el Dashboard B2B y en las fichas de detalle de vehículos de la aplicación. La información crítica (Precio del vehículo, Estado de pre-aprobación del lead) se ubica en la parte superior con tipografía de mayor peso, mientras que los datos secundarios (kilometraje, tracción, historial) se agrupan en niveles inferiores.
- **Organización secuencial (Step-by-step):** Se utiliza exclusivamente para procesos transaccionales complejos que requieren alta concentración, como el embudo de pre-evaluación crediticia y el registro o *onboarding* de una nueva concesionaria. Dividir estos procesos en pasos secuenciales reduce drásticamente la tasa de abandono.
- **Organización matricial:** Implementada en la Landing Page mediante el "Segments Pager". En lugar de crear una página extensa, se utiliza una matriz horizontal deslizable que permite al visitante interactuar y alternar entre los tres perfiles del mercado (Compradores, Concesionarias Nuevos, Concesionarias Usados) dentro de un mismo bloque visual de la pantalla.

**Esquemas de categorización:**

- **Según audiencia (Audience-based):** Es el pilar del Landing Page. El contenido se bifurca desde el Hero Section con llamados a la acción distintos ("Explorar vehículos" para la demanda vs. "Soy concesionaria" para la oferta B2B).
- **Por tópicos:** Utilizado en el motor de búsqueda y catálogo de la Web App, agrupando el inventario en categorías universales como SUVs, Sedanes, Pick-ups y Hatchbacks.
- **Alfabético:** Empleado estrictamente en los menús desplegables (dropdowns) de selección de Marcas y Modelos vehiculares para facilitar la ubicación rápida.
- **Cronológico:** Utilizado en el Panel B2B para listar los *Leads* (prospectos) recibidos, priorizando visualmente a los clientes más recientes.

### 4.2.2. Labeling Systems

Las etiquetas de la plataforma están diseñadas con el mínimo número de palabras posibles, utilizando terminología estandarizada para evitar curvas de aprendizaje y establecer asociaciones mentales directas.

- **Asociación de Negocio:** La etiqueta **"Membresías"** en la navegación asocia inmediatamente en la mente del usuario corporativo que encontrará los planes de precios, los beneficios B2B de la plataforma y el modelo de negocio, sin necesidad de usar títulos largos como "Planes para concesionarias".
- **Asociación Institucional:** La etiqueta **"Equipo"** agrupa los perfiles, roles y códigos de los seis estudiantes fundadores (tux-squad) encargados del desarrollo del sistema.
- **Llamados a la Acción (CTAs):** Se utilizan verbos imperativos directos. En la cabecera, **"Comenzar"** funciona como la entrada principal a la aplicación web. En el catálogo, se usarán etiquetas como **"Pre-evaluar Crédito"** (asociado al formulario financiero) y **"Agendar Test Drive"** (asociado al contacto físico).
- **Asociación Legal Oculta:** Las etiquetas **"Términos"** y **"Privacidad"** ubicadas en el pie de página abren un panel lateral superpuesto (*Legal Drawer*) que asocia los documentos normativos sin redirigir al usuario a una nueva pestaña ni abrumarlo con texto en la página principal.

### 4.2.3. SEO Tags and Meta Tags

Para asegurar la correcta indexación y posicionamiento orgánico en motores de búsqueda, se han definido las siguientes etiquetas estructuradas para los dos entornos principales del ecosistema digital.

**Sitio Web Estático (Landing Page)**

- **Title:** `SmartFinance Drive | Marketplace inteligente de vehículos`
- **Description:** `SmartFinance Drive conecta compradores y concesionarias con recomendaciones inteligentes, un catálogo unificado de vehículos nuevos y usados, y pre-evaluación crediticia externa.`
- **Keywords:** `marketplace automotriz, comprar auto peru, autos nuevos, autos usados, financiamiento vehicular, pre-evaluación crediticia, recomendador IA`
- **Author:** `tux-squad`

**Web Application (Catálogo y Panel B2B)**

- **Title:** `Catálogo Unificado de Vehículos | SmartFinance Drive`
- **Description:** `Explora el catálogo de vehículos nuevos y seminuevos. Descubre autos que se ajustan a tu presupuesto y obtén tu pre-aprobación crediticia 100% digital.`
- **Keywords:** `catálogo de autos, crédito vehicular online, autos financiados, simulador de cuotas vehiculares, gestión de leads automotriz`
- **Author:** `tux-squad`

### 4.2.4. Searching Systems

Dado el alto volumen de información que maneja un mercado unificado de vehículos, SmartFinance Drive provee herramientas de búsqueda robustas para evitar que el comprador se sienta abrumado o perdido.

- **Opciones de Búsqueda Ofrecidas:**
  - **Búsqueda Semántica (Recomendador IA):** El usuario no necesita conocer marcas o especificaciones técnicas. Ingresa un estilo de vida (ej. "Auto familiar seguro") y un límite de cuota mensual, y el sistema traduce esa intención en modelos específicos.
  - **Búsqueda Directa (Predictiva):** Una barra de búsqueda libre con autocompletado en tiempo real que sugiere marcas, modelos o concesionarias a medida que el usuario teclea (ej. al escribir "Yar", despliega "Toyota Yaris").
  - **Filtros Facetados (Faceted Search):** Los usuarios más experimentados contarán con un panel lateral en el catálogo para aplicar filtros acumulativos: *Condición* (Nuevo/Usado), *Presupuesto* (Rango de precios), *Año de fabricación*, *Transmisión* (Automática/Manual) y *Tipo de combustible*.
- **Visualización de Datos Tras la Búsqueda:** Los resultados se presentan en una cuadrícula (*Grid*) de tarjetas de vehículos (Cards). Cada tarjeta resalta visualmente la fotografía principal, la marca/modelo, el precio total y un cálculo estimado de la cuota mensual. Si no hay resultados exactos, el sistema sugiere automáticamente vehículos con características similares o precios ligeramente superiores.

### 4.2.5. Navigation Systems

El sistema de navegación define las acciones y técnicas que guían a los usuarios fluidamente desde su llegada al ecosistema hasta el cumplimiento de sus objetivos transaccionales.

- **Navegación del Landing Page:**
  - **Sticky Global Header:** Una barra superior persistente que acompaña al usuario al hacer scroll hacia abajo, permitiéndole saltar a diferentes anclas de la página (Inicio, Cómo funciona, Segmentos) sin tener que regresar manualmente arriba.
  - **Smooth Scrolling:** Los hipervínculos utilizan anclajes dinámicos que deslizan la pantalla suavemente hacia la sección de interés, calculando el margen exacto para no ocultar el título debajo de la cabecera fija.
  - **Mobile Drawer Menu:** En dispositivos móviles, la navegación se oculta tras un botón *hamburger* que despliega un panel superpuesto de pantalla completa, optimizando el espacio de lectura sin sacrificar acceso a las secciones.
- **Navegación de la Web Application:**
  - **Global Navigation:** Barra superior constante con acceso directo al Catálogo Unificado, Simulador IA y Perfil de Usuario.
  - **Local Navigation (B2B):** Las concesionarias interactúan a través de un menú lateral izquierdo (*Sidebar*) que les permite navegar rápidamente entre los sub-módulos de su entorno privado: Dashboard, Mi Inventario (Stock), Gestión de Leads y Configuración de Cuenta.
  - **Contextual Navigation (Breadcrumbs):** Para evitar que el comprador se desoriente en el catálogo, se implementan migas de pan en la parte superior de las fichas técnicas (ej. `Inicio > Autos Usados > Toyota > Yaris 2021`), permitiendo retroceder a categorías superiores con un solo clic.

---

## 4.3. Landing Page UI Design

### 4.3.1. Landing Page Wireframe

![smartfinance-drive-landing-wireframe](../assets/Chapter-4/smartfinance-drive-landing-wireframe.png)

### 4.3.2. Landing Page Mock-up

![smartfinance-drive-landing-mockup](../assets/Chapter-4/smartfinance-drive-landing-mockup.png)

## 4.4. Mobile Applications UX/UI Design

### 4.4.1. Mobile Applications Wireframes

![mobile-wireframe-1](../assets/Chapter-4/mobile-wireframe-1.png){width=45%}

![mobile-wireframe-2](../assets/Chapter-4/mobile-wireframe-2.png){width=45%}

![mobile-wireframe-3](../assets/Chapter-4/mobile-wireframe-3.png){width=45%}

![mobile-wireframe-4](../assets/Chapter-4/mobile-wireframe-4.png){width=45%}

![mobile-wireframe-5](../assets/Chapter-4/mobile-wireframe-5.png){width=45%}

![mobile-wireframe-6](../assets/Chapter-4/mobile-wireframe-6.png){width=45%}

![mobile-wireframe-7](../assets/Chapter-4/mobile-wireframe-7.png){width=45%}

![mobile-wireframe-8](../assets/Chapter-4/mobile-wireframe-8.png){width=45%}

![mobile-wireframe-9](../assets/Chapter-4/mobile-wireframe-9.png){width=45%}

![mobile-wireframe-10](../assets/Chapter-4/mobile-wireframe-10.png){width=45%}

![mobile-wireframe-11](../assets/Chapter-4/mobile-wireframe-11.png){width=45%}

![mobile-wireframe-12](../assets/Chapter-4/mobile-wireframe-12.png){width=45%}

![mobile-wireframe-13](../assets/Chapter-4/mobile-wireframe-13.png){width=45%}

![mobile-wireframe-14](../assets/Chapter-4/mobile-wireframe-14.png){width=45%}

![mobile-wireframe-15](../assets/Chapter-4/mobile-wireframe-15.png){width=45%}

![mobile-wireframe-16](../assets/Chapter-4/mobile-wireframe-16.png){width=45%}

![mobile-wireframe-17](../assets/Chapter-4/mobile-wireframe-17.png){width=45%}

![mobile-wireframe-18](../assets/Chapter-4/mobile-wireframe-18.png){width=45%}

![mobile-wireframe-19](../assets/Chapter-4/mobile-wireframe-19.png){width=45%}

![mobile-wireframe-20](../assets/Chapter-4/mobile-wireframe-20.png){width=45%}

![mobile-wireframe-21](../assets/Chapter-4/mobile-wireframe-21.png){width=45%}

![mobile-wireframe-22](../assets/Chapter-4/mobile-wireframe-22.png){width=45%}

![mobile-wireframe-23](../assets/Chapter-4/mobile-wireframe-23.png){width=45%}

![mobile-wireframe-24](../assets/Chapter-4/mobile-wireframe-24.png){width=45%}

![mobile-wireframe-25](../assets/Chapter-4/mobile-wireframe-25.png){width=45%}

![mobile-wireframe-26](../assets/Chapter-4/mobile-wireframe-26.png){width=45%}

### 4.4.2. Mobile Applications Wireflow Diagrams

![mobile-wireflow-X](../assets/Chapter-4/mobile-wireflow-X.png)

### 4.4.3. Mobile Applications Mock-ups

![mobile-mockups-1](../assets/Chapter-4/mobile-mockups-1.png){width=45%}

![mobile-mockups-2](../assets/Chapter-4/mobile-mockups-2.png){width=45%}

![mobile-mockups-3](../assets/Chapter-4/mobile-mockups-3.png){width=45%}

![mobile-mockups-4](../assets/Chapter-4/mobile-mockups-4.png){width=45%}

![mobile-mockups-5](../assets/Chapter-4/mobile-mockups-5.png){width=45%}

![mobile-mockups-6](../assets/Chapter-4/mobile-mockups-6.png){width=45%}

![mobile-mockups-7](../assets/Chapter-4/mobile-mockups-7.png){width=45%}

![mobile-mockups-8](../assets/Chapter-4/mobile-mockups-8.png){width=45%}

![mobile-mockups-9](../assets/Chapter-4/mobile-mockups-9.png){width=45%}

![mobile-mockups-10](../assets/Chapter-4/mobile-mockups-10.png){width=45%}

![mobile-mockups-11](../assets/Chapter-4/mobile-mockups-11.png){width=45%}

![mobile-mockups-12](../assets/Chapter-4/mobile-mockups-12.png){width=45%}

![mobile-mockups-13](../assets/Chapter-4/mobile-mockups-13.png){width=45%}

![mobile-mockups-14](../assets/Chapter-4/mobile-mockups-14.png){width=45%}

![mobile-mockups-15](../assets/Chapter-4/mobile-mockups-15.png){width=45%}

![mobile-mockups-16](../assets/Chapter-4/mobile-mockups-16.png){width=45%}

![mobile-mockups-17](../assets/Chapter-4/mobile-mockups-17.png){width=45%}

![mobile-mockups-18](../assets/Chapter-4/mobile-mockups-18.png){width=45%}

![mobile-mockups-19](../assets/Chapter-4/mobile-mockups-19.png){width=45%}

![mobile-mockups-20](../assets/Chapter-4/mobile-mockups-20.png){width=45%}

![mobile-mockups-21](../assets/Chapter-4/mobile-mockups-21.png){width=45%}

![mobile-mockups-22](../assets/Chapter-4/mobile-mockups-22.png){width=45%}

![mobile-mockups-23](../assets/Chapter-4/mobile-mockups-23.png){width=45%}

![mobile-mockups-24](../assets/Chapter-4/mobile-mockups-24.png){width=45%}

![mobile-mockups-25](../assets/Chapter-4/mobile-mockups-25.png){width=45%}

![mobile-mockups-26](../assets/Chapter-4/mobile-mockups-26.png){width=45%}

### 4.4.4. Mobile Applications User Flow Diagrams

![mobile-userflow-X](../assets/Chapter-4/mobile-userflow-X.png)

## 4.5. Mobile Applications Prototyping

### 4.5.1. Android Mobile Applications Prototyping

*(Enlace/Captura del prototipo interactivo en Figma simulando la interacción en un dispositivo Android).*

### 4.5.2. iOS Mobile Applications Prototyping

*(Enlace/Captura del prototipo interactivo simulando un entorno iOS).*

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

### 4.6.2. Web Applications Wireflow Diagrams

![webapp-wireflow-X](../assets/Chapter-4/webapp-wireflow-X.png)

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

### 4.6.4. Web Applications User Flow Diagrams

![webapp-userflow-X](../assets/Chapter-4/webapp-userflow-X.png)

## 4.7. Web Applications Prototyping

*(Enlace al video/prototipo navegable del panel web de SmartFinance Drive).*

## 4.8. Domain-Driven Software Architecture

El diseño de la arquitectura de software de SmartFinance Drive sigue los principios de Domain-Driven Design (DDD), garantizando que el modelo técnico refleje fielmente el contexto del negocio automotriz y financiero.

### 4.8.1. Software Architecture Context Diagram

*(Aquí se incluirá el diagrama C4 de Nivel 1 - Contexto. Mostrará a los actores (Compradores, Concesionarias) interactuando con el sistema SmartFinance Drive, y a este interactuando con sistemas externos (Entidades Financieras externas para la pre-evaluación crediticia)).*

### 4.8.2. Software Architecture Container Diagrams

*(Aquí se incluirá el diagrama C4 de Nivel 2 - Contenedores. Desglosará SmartFinance Drive en sus aplicaciones (Web App, Mobile App, Landing Page), el Gateway de API, los microservicios backend y las bases de datos).*

### 4.8.3. Software Architecture Components Diagrams

*(Aquí se incluirá el diagrama C4 de Nivel 3 - Componentes. Detallará la estructura interna de los contenedores más críticos, como el módulo de inventario o el simulador de inteligencia artificial).*

## 4.9. Software Object-Oriented Design

### 4.9.1. Class Diagrams

*(Aquí se documentarán los diagramas de clases UML para los principales Bounded Contexts identificados, detallando entidades, value objects y agregados).*

### 4.9.2. Class Dictionary

*(Tabla descriptiva de las clases principales representadas en los diagramas UML, definiendo sus atributos, métodos y responsabilidades dentro del dominio).*

## 4.10. Database Design

### 4.10.1. Relational/Non-Relational Database Diagram

*(Aquí se insertará el Modelo Entidad-Relación (ERD) o el esquema NoSQL que soportará el catálogo unificado).*
