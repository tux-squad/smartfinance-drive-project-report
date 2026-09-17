# Capítulo IV: Product Design

## 4.1. Style Guidelines

### 4.1.1. General Style Guidelines

El sistema de diseño de SmartFinance Drive se ha construido para transmitir confianza, innovación y fluidez. Al ser una plataforma que maneja decisiones financieras importantes y un inventario de alto valor, el diseño visual debe equilibrar la formalidad del sector automotriz con la agilidad de una startup tecnológica.

**A. Branding y Logotipo**
El isotipo y logotipo reflejan la conexión digital entre la oferta y la demanda. Se emplean versiones monocromáticas (blanco) para fondos oscuros como el Hero de la landing page, y a color para fondos claros.
*   **Isotipo:** Silueta de un vehículo fusionada con nodos de red, representando la inmediatez de la conexión B2B y B2C.
*   **Logotipo (Wordmark):** Texto "SmartFinance" seguido de "*Drive*" en itálica, enfatizando el dinamismo.
![Logotipo SmartFinance Drive](assets/Chapter-4/logo.png)
![Logotipo con letras](assets/Chapter-4/Logo-letras.png)

**B. Tipografía (Typography)**
Se utiliza la familia tipográfica **Inter** de Google Fonts en pesos de 400, 500, 600, 700 y 800. Esta fuente *sans-serif* maximiza la legibilidad en interfaces digitales densas en datos (como catálogos de autos y calculadoras de crédito).
*   **Display / Hero:** `Inter Bold (700)` o `ExtraBold (800)` para los encabezados principales (ej. "Tu próximo auto está más cerca").
*   **Headings (H2, H3):** `Inter SemiBold (600)` para títulos de secciones modulares.
*   **Cuerpo (Body) y Metadatos:** `Inter Regular (400)` para descripciones largas y `Medium (500)` para etiquetas de UI y botones.
![Jerarquía Tipográfica](assets/Chapter-4/Letras.jpeg)

**C. Paleta de Colores (Color Palette)**
La paleta se divide en colores de confianza y colores de acción, aplicados a través de variables CSS para facilitar el mantenimiento y la consistencia temática.
![Paleta de Colores](assets/Chapter-4/colores-smartdrive.png)
*   **Primary Blue (`#1E56A0`) & Dark Blue (`#0D2149`):** Establecen la base visual de seguridad y profesionalismo. Utilizados en textos principales, fondos de sección y el pie de página.
*   **Teal / Cyan (`#00A896`):** Actúa como color de acento tecnológico (usado en la clase `liquid-glass--teal` y `badge--teal`). Representa las funciones de Inteligencia Artificial y validación.
*   **Orange / Warm (`#F4A261`):** Color de contraste para conversiones principales. Se aplica en botones de llamada a la acción primarios (clase `btn--warm` y `badge--orange`).
*   **Off-White (`#F8F9FA`):** Fondo base neutral que reduce la fatiga visual (usado en la variable `--bg-light` o similar).

**D. Micro-interacciones y Animaciones**
El diseño general integra interacciones fluidas mediante JavaScript nativo, diseñadas para usuarios con punteros precisos (mouse/trackpad):
*   **Custom Cursor:** Un cursor magnético compuesto por un punto (`data-cursor-dot`) y un anillo (`data-cursor-ring`) que reacciona de forma elástica al pasar sobre enlaces y botones.
*   **Magnetic Buttons:** Los botones principales (`data-magnetic`) se desplazan sutilmente hacia el cursor del usuario, mejorando la sensación táctil digital.
*   **Liquid Glass Glow:** Un efecto de iluminación dinámica en tarjetas y menús de navegación (`data-liquid-glass`) que sigue las coordenadas `X` e `Y` del puntero, otorgando un aspecto premium.

### 4.1.2. Web Style Guidelines

La interfaz web (incluyendo la Landing Page y futuras Web Apps) aplica un enfoque *Responsive* y prioriza la inmersión del usuario.
*   **Estructura Base (Reset & Variables):** Separación modular de estilos en archivos dedicados (`reset.css`, `variables.css`, `typography.css`, `components.css`) para garantizar la escalabilidad.
*   **Efectos de Scroll (Scroll Reveal):** Los elementos clave (títulos, tarjetas de beneficios) ingresan al *viewport* con animaciones escalonadas controladas por `IntersectionObserver` (`data-reveal`), manteniendo la atención del usuario a medida que navega hacia abajo.
*   **Parallax:** El fondo de la sección Hero (`data-parallax-bg`) se desplaza a una velocidad diferente al contenido, generando profundidad.
*   **Componentes Modulares:** Uso intensivo de carruseles arrastrables (`data-drag-track`), acordeones para preguntas frecuentes (`data-accordion`) y selectores de idioma (`lang-switch`) para maximizar el uso del espacio.

### 4.1.3. Mobile Style Guidelines

El ecosistema móvil demanda adaptaciones específicas para mantener la usabilidad sin comprometer el estilo visual de la marca.

#### 4.1.3.1. iOS Mobile Style Guidelines
*   **Navegación Táctil:** Reemplazo de los efectos de *hover* y cursores magnéticos (deshabilitados vía media queries táctiles) por *Tap Highlights* nativos.
*   **Componentes Modales:** Implementación de modales de pantalla inferior (Bottom Sheets) para la pre-evaluación crediticia externa, respetando las *Human Interface Guidelines* de Apple y evitando salidas disruptivas del flujo principal.
*   **Safe Areas:** Respeto estricto del *notch* superior y el indicador de inicio inferior en la estructura de vistas de la aplicación iOS.

#### 4.1.3.2. Android Mobile Style Guidelines
*   **Material Design 3:** Adopción de sombras modulares (Elevation) y efectos de ondas táctiles (Ripple effect) en listas de vehículos y botones de acción.
*   **Barra de Navegación (Bottom Navigation):** Controles fijos en la parte inferior para acceder rápidamente a: *Búsqueda, Mi Perfil, Recomendaciones IA*.
*   **Gestos:** Soporte total para gestos de deslizamiento horizontal (Swipe) en galerías de imágenes de los autos y para descartar tarjetas de recomendación de la IA.

---

## 4.2. Information Architecture

### 4.2.1. Organization Systems
El sistema de organización de SmartFinance Drive combina estructuras jerárquicas y secuenciales para guiar al usuario desde el descubrimiento inicial hasta la conversión.
*   **Landing Page (Single-Page Layout):** Estructura jerárquica guiada por el scroll. Se organiza en: `Hero (Inicio)` -> `Propuesta de Valor (Cómo funciona)` -> `Público Objetivo (Compradores & concesionarias)` -> `Modelo de Negocio (Membresías)` -> `Acerca de (Equipo)`.
*   **Organización Secuencial (Plataforma):** El flujo de recomendación asistida y la pre-evaluación crediticia se organizan paso a paso para reducir la carga cognitiva del usuario.
*   **Organización Visual por Pestañas (Pagers):** En secciones densas, como los segmentos objetivo, se utiliza un `segments-pager` que permite alternar visualmente entre "Demanda" y "Oferta B2B" sin recargar la vista.

### 4.2.2. Labeling Systems
Se emplea un lenguaje claro, enfocado en conversiones directas y con soporte de internacionalización (i18n).
*   **Navegación:** Etiquetas concisas en la cabecera: *Inicio, Cómo funciona, Compradores & concesionarias, Membresías, Equipo*.
*   **Botones de Acción (CTAs):** Se utilizan verbos imperativos claros para incitar la acción: *Explorar vehículos, Soy concesionaria, Afiliar mi concesionaria*.
*   **Etiquetas de Atributos (Badges):** Identificadores visuales rápidos como *Demanda, Oferta B2B, Vehículos nuevos, Vehículos usados*.

### 4.2.3. SEO Tags and Meta Tags
Para asegurar la indexación correcta y atraer tráfico orgánico, la Landing Page incluye un bloque robusto de metadatos optimizado.

```html
<!-- Primary Meta Tags -->
<title>SmartFinance Drive | Marketplace inteligente de vehículos</title>
<meta name="description" content="SmartFinance Drive conecta compradores y concesionarias con recomendaciones inteligentes, un catálogo unificado de vehículos nuevos y usados, y pre-evaluación crediticia externa.">
<!-- Etiqueta Viewport -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<!-- Open Graph / Social -->
<meta property="og:title" content="SmartFinance Drive | Marketplace inteligente de vehículos">
<meta property="og:description" content="Conectamos compradores con concesionarias de vehículos nuevos y usados en un solo lugar.">
```

### 4.2.4. Searching Systems

El sistema de búsqueda está diseñado fundamentalmente para el **Canal Virtual Directo**.

* **Filtros Globales:** Los usuarios pueden depurar el inventario unificado mediante filtros técnicos (condición, kilometraje, año, carrocería) y financieros (presupuesto, capacidad de cuota mensual).


* **Asistente IA (Búsqueda Guiada):** Actúa como un buscador alternativo conversacional. En lugar de campos de texto vacíos, ofrece sugerencias de marcas y modelos basados en inputs de estilo de vida ("auto familiar", "bajo consumo").



### 4.2.5. Navigation Systems

La navegación está optimizada para la retención y la accesibilidad en cualquier dispositivo.

* **Navegación Global (Sticky Header):** La etiqueta `<header data-site-header>` se mantiene fija en la parte superior. Al hacer scroll (`window.scrollY > 40`), altera su estado visual (`is-scrolled`) para reducir su tamaño y no interferir con la lectura.


* **Menú Lateral Móvil (Drawer):** Un `<aside class="drawer" data-drawer>` se despliega en resoluciones menores, acompañado de un telón de fondo (`data-drawer-backdrop`) para centrar el foco de atención, permitiendo cerrar el menú al hacer clic fuera.


* **Scroll Spy (Navegación contextual):** Mediante `IntersectionObserver`, el sistema detecta qué sección del sitio está visible en pantalla y actualiza automáticamente el estado activo (`site-header__link--active`) del enlace correspondiente en el menú superior.


* **Navegación Legal Modal:** Los términos y políticas de privacidad están accesibles mediante un cajón oculto (`<div class="legal-drawer" data-legal-drawer>`), evitando redirigir al usuario fuera de la página principal y perder la sesión.



---

## 4.3. Landing Page UI Design

En esta sección se traduce la arquitectura de la información y las decisiones de diseño en interfaces visuales para la página de aterrizaje (Landing Page) de SmartFinance Drive.

### 4.3.1. Landing Page Wireframe

*(Aquí se insertarán las imágenes explicadas de los wireframes estructurales (baja fidelidad) para Desktop y Mobile, mostrando la distribución de las secciones detalladas en el main.js y el index.html: Hero, Intro, Accordion, Slider de features, Outcomes y Team).*

### 4.3.2. Landing Page Mock-up

*(Aquí se insertarán las imágenes en alta fidelidad de la Landing Page, aplicando el Design System definido: tipografía Inter, paleta de colores azul/teal/naranja, y los componentes de UI).*

---

## 4.4. Mobile Applications UX/UI Design

### 4.4.1. Mobile Applications Wireframes

*(Aquí se incluirán los esquemas de baja fidelidad de la aplicación móvil obligatoria, priorizando las vistas del catálogo, simulador IA, y perfil).*

### 4.4.2. Mobile Applications Wireflow Diagrams

*(Aquí se incluirán los diagramas que muestran la conexión entre las diferentes pantallas (Wireframes) para los flujos principales de los User Goals, como la búsqueda de un auto o el inicio del simulador).*

### 4.4.3. Mobile Applications Mock-ups

*(Aquí se insertarán los diseños finales en alta fidelidad de la aplicación, reflejando las directrices de Material Design 3 e iOS HIG).*

### 4.4.4. Mobile Applications User Flow Diagrams

*(Aquí se presentarán los flujos de usuario detallados utilizando los Mock-ups, mostrando el happy path y los unhappy paths para tareas clave, como la solicitud de la pre-evaluación crediticia).*

---

## 4.5. Mobile Applications Prototyping

### 4.5.1. Android Mobile Applications Prototyping

*(Enlace/Captura del prototipo interactivo en Figma simulando la interacción en un dispositivo Android, demostrando el uso del bottom navigation bar y ripple effects).*

### 4.5.2. iOS Mobile Applications Prototyping

*(Enlace/Captura del prototipo interactivo simulando un entorno iOS, evidenciando el uso de modales (sheets) y navegación nativa de Apple).*

---

## 4.6. Web Applications UX/UI Design

### 4.6.1. Web Applications Wireframes

*(Esquemas de las vistas del Dashboard B2B para las concesionarias y el portal web de compradores).*

### 4.6.2. Web Applications Wireflow Diagrams

*(Diagrama de conexión entre los wireframes de la Web App).*

### 4.6.3. Web Applications Mock-ups

*(Diseños de alta fidelidad de la plataforma web, aplicando componentes modulares y el grid system).*

### 4.6.4. Web Applications User Flow Diagrams

*(Mapeo de los flujos de interacción completos utilizando los mock-ups de la Web App).*

---

## 4.7. Web Applications Prototyping

*(Enlace al video/prototipo navegable del panel web de SmartFinance Drive, evidenciando las decisiones de la arquitectura de la información y sistemas de navegación).*

---

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

*(Aquí se insertará el Modelo Entidad-Relación (ERD) o el esquema NoSQL que soportará el catálogo unificado, la persistencia de usuarios, el historial de las pre-evaluaciones y la configuración de las membresías B2B).*
