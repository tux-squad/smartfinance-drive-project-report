# Capítulo IV: Product Design

## 4.1. Style Guidelines

### 4.1.1. General Style Guidelines

El sistema de diseño de SmartFinance Drive se ha construido para transmitir confianza, innovación y fluidez. Al ser una plataforma que maneja decisiones financieras importantes y un inventario de alto valor, el diseño visual debe equilibrar la formalidad del sector automotriz con la agilidad de una startup tecnológica.

**A. Branding y Logotipo**

El isotipo y logotipo reflejan la conexión digital entre la oferta y la demanda. Se emplean versiones monocromáticas (blanco) para fondos oscuros como el Hero de la landing page, y a color para fondos claros.

- **Isotipo:** Silueta de un vehículo fusionada con nodos de red, representando la inmediatez de la conexión B2B y B2C.
- **Logotipo (Wordmark):** Texto "SmartFinance" seguido de "*Drive*" en itálica, enfatizando el dinamismo.

```{=typst}
#v(0.5em)
#align(center)[
  #grid(
    columns: (auto, auto),
    gutter: 30pt,
    align: horizon + center,
    image("assets/Chapter-4/logo.png", height: 50pt),
    image("assets/Chapter-4/Logo-letras.png", height: 50pt)
  )
]
#v(0.5em)
```

**B. Tipografía (Typography)**

Se utiliza la familia tipográfica **Inter** de Google Fonts en pesos de 400, 500, 600, 700 y 800. Esta fuente *sans-serif* maximiza la legibilidad en interfaces digitales densas en datos (como catálogos de autos y calculadoras de crédito).

- **Display / Hero:** `Inter Bold (700)` o `ExtraBold (800)` para los encabezados principales (ej. "Tu próximo auto está más cerca").
- **Headings (H2, H3):** `Inter SemiBold (600)` para títulos de secciones modulares.
- **Cuerpo (Body) y Metadatos:** `Inter Regular (400)` para descripciones largas y `Medium (500)` para etiquetas de UI y botones.

```{=typst}
#v(0.5em)
#align(center)[
  #image("assets/Chapter-4/Letras.jpeg", width: 60%)
]
#v(0.5em)
```

**C. Paleta de Colores (Color Palette)**

La paleta se divide en colores de confianza y colores de acción, aplicados a través de variables CSS para facilitar el mantenimiento y la consistencia temática.

- **Primary Blue (`#1E56A0`) & Dark Blue (`#0D2149`):** Establecen la base visual de seguridad y profesionalismo. Utilizados en textos principales, fondos de sección y el pie de página.
- **Teal / Cyan (`#00A896`):** Actúa como color de acento tecnológico (usado en la clase `liquid-glass--teal` y `badge--teal`). Representa las funciones de Inteligencia Artificial y validación.
- **Orange / Warm (`#F4A261`):** Color de contraste para conversiones principales. Se aplica en botones de llamada a la acción primarios (clase `btn--warm` y `badge--orange`).
- **Off-White (`#F8F9FA`):** Fondo base neutral que reduce la fatiga visual (usado en la variable `--bg-light` o similar).

```{=typst}
#v(0.5em)
#align(center)[
  #image("assets/Chapter-4/colores-smartdrive.png", width: 60%)
]
#v(0.5em)
```

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

En esta sección se traducen la arquitectura de la información y las decisiones de diseño en interfaces visuales para la página de aterrizaje (Landing Page) de SmartFinance Drive. Para permitir una inspección detallada sin pérdidas de resolución ni saltos de página con títulos aislados, los diseños estructurales y de alta fidelidad se presentan divididos en dos partes correlativas.

### 4.3.1. Landing Page Wireframe

![smartfinance-drive-landing-wireframe-part1](assets/Chapter-4/smartfinance-drive-landing-wireframe-part1.png){width=65%}

![smartfinance-drive-landing-wireframe-part2](assets/Chapter-4/smartfinance-drive-landing-wireframe-part2.png){width=65%}

### 4.3.2. Landing Page Mock-up

![smartfinance-drive-landing-mockup-part1](assets/Chapter-4/smartfinance-drive-landing-mockup-part1.png){width=65%}

![smartfinance-drive-landing-mockup-part2](assets/Chapter-4/smartfinance-drive-landing-mockup-part2.png){width=65%}

## 4.4. Mobile Applications UX/UI Design

### 4.4.1. Mobile Applications Wireframes

![mobile-wireframe-1](assets/Chapter-4/mobile-wireframe-1.png){width=45%}

![mobile-wireframe-2](assets/Chapter-4/mobile-wireframe-2.png){width=45%}

![mobile-wireframe-3](assets/Chapter-4/mobile-wireframe-3.png){width=45%}

![mobile-wireframe-4](assets/Chapter-4/mobile-wireframe-4.png){width=45%}

![mobile-wireframe-5](assets/Chapter-4/mobile-wireframe-5.png){width=45%}

![mobile-wireframe-6](assets/Chapter-4/mobile-wireframe-6.png){width=45%}

![mobile-wireframe-7](assets/Chapter-4/mobile-wireframe-7.png){width=45%}

![mobile-wireframe-8](assets/Chapter-4/mobile-wireframe-8.png){width=45%}

![mobile-wireframe-9](assets/Chapter-4/mobile-wireframe-9.png){width=45%}

![mobile-wireframe-10](assets/Chapter-4/mobile-wireframe-10.png){width=45%}

![mobile-wireframe-11](assets/Chapter-4/mobile-wireframe-11.png){width=45%}

![mobile-wireframe-12](assets/Chapter-4/mobile-wireframe-12.png){width=45%}

![mobile-wireframe-13](assets/Chapter-4/mobile-wireframe-13.png){width=45%}

![mobile-wireframe-14](assets/Chapter-4/mobile-wireframe-14.png){width=45%}

![mobile-wireframe-15](assets/Chapter-4/mobile-wireframe-15.png){width=45%}

![mobile-wireframe-16](assets/Chapter-4/mobile-wireframe-16.png){width=45%}

![mobile-wireframe-17](assets/Chapter-4/mobile-wireframe-17.png){width=45%}

![mobile-wireframe-18](assets/Chapter-4/mobile-wireframe-18.png){width=45%}

![mobile-wireframe-19](assets/Chapter-4/mobile-wireframe-19.png){width=45%}

![mobile-wireframe-20](assets/Chapter-4/mobile-wireframe-20.png){width=45%}

![mobile-wireframe-21](assets/Chapter-4/mobile-wireframe-21.png){width=45%}

![mobile-wireframe-22](assets/Chapter-4/mobile-wireframe-22.png){width=45%}

![mobile-wireframe-23](assets/Chapter-4/mobile-wireframe-23.png){width=45%}

![mobile-wireframe-24](assets/Chapter-4/mobile-wireframe-24.png){width=45%}

![mobile-wireframe-25](assets/Chapter-4/mobile-wireframe-25.png){width=45%}

![mobile-wireframe-26](assets/Chapter-4/mobile-wireframe-26.png){width=45%}

### 4.4.2. Mobile Applications Wireflow Diagrams

Esta sección presenta los Wireflows propuestos para la aplicación móvil. Cada diagrama refleja un User Goal específico para los distintos User Personas, mostrando cómo la interacción en la pantalla táctil genera representaciones de nuevos estados en el flujo de la aplicación.

### Wireflow 1: Descubrimiento y Pre-evaluación Crediticia Móvil

![mobile-wireflow-1](assets/Chapter-4/mobile-wireflow-1.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Descubrir vehículos a través de recomendaciones personalizadas, comparar opciones y solicitar la pre-evaluación financiera desde su smartphone.

- **Explicación del Flujo y Estados UI:** El flujo inicia en la pantalla de "Bienvenida" del comprador, la cual exhibe recomendaciones iniciales basadas en el perfil. El usuario puede transitar hacia el "Asistente Inteligente", donde ingresa su presupuesto interactuando con la interfaz conversacional. A partir de las sugerencias, navega hacia la vista de "Detalle del Vehículo". Si desea contrastar opciones, activa el estado de "Comparar Vehículos", dividiendo la pantalla para evaluar dos unidades simultáneamente. Finalmente, al decidirse, avanza al formulario de "Pre-evaluación Crediticia", cambiando el estado de la aplicación para procesar sus datos de identidad y financieros.

### Wireflow 2: Monitoreo de Rendimiento y Creación de Campañas (B2B)

![mobile-wireflow-2](assets/Chapter-4/mobile-wireflow-2.png)

- **User Persona:** Valeria Rojas (Concesionaria de Autos Nuevos)

- **User Goal:** Revisar las métricas de captación de leads en tiempo real y aplicar bonos de descuento inmediatos a su inventario para acelerar ventas.

- **Explicación del Flujo y Estados UI:** El flujo comienza en el "Resumen Mensual" del panel de administración (Drive Admin), donde la concesionaria visualiza métricas clave como Prospectos IA e Interacciones Diarias. Desde allí, el usuario transita a la pantalla "Bono de Descuento" para configurar una campaña especial, ingresando el nombre y el monto del descuento. Al presionar "Crear y Aplicar Bono", el sistema genera un estado de vista previa en tarjeta. El flujo concluye actualizando la vista de "Inventario Activo", donde el vehículo seleccionado refleja el nuevo precio ajustado y la etiqueta de disponibilidad.

### Wireflow 3: Gestión de Inventario y Certificación de Seminuevos (B2B)

![mobile-wireflow-3](assets/Chapter-4/mobile-wireflow-3.png)

- **User Persona:** Roberto García (Concesionaria de Autos Usados)

- **User Goal:** Administrar el catálogo de seminuevos desde el patio de ventas, actualizar estados y registrar nuevas certificaciones de inspección.

- **Explicación del Flujo y Estados UI:** El flujo inicia en el módulo de "Gestión de Seminuevos", que muestra indicadores de rotación y calidad de inventario. El usuario navega hacia el "Inventario Activo", visualizando la lista completa de unidades publicadas. Al seleccionar una unidad para certificar, la aplicación transita al formulario de "Nueva Certificación", permitiendo registrar los detalles de la inspección mecánica y legal. Finalmente, tras confirmar la certificación, el sistema avanza a la pantalla de "Datos del Vehículo" para completar la publicación, alterando el estado de la unidad en la base de datos a "Certificado".

### 4.4.3. Mobile Applications Mock-ups

![mobile-mockups-1](assets/Chapter-4/mobile-mockups-1.png){width=45%}

![mobile-mockups-2](assets/Chapter-4/mobile-mockups-2.png){width=45%}

![mobile-mockups-3](assets/Chapter-4/mobile-mockups-3.png){width=45%}

![mobile-mockups-4](assets/Chapter-4/mobile-mockups-4.png){width=45%}

![mobile-mockups-5](assets/Chapter-4/mobile-mockups-5.png){width=45%}

![mobile-mockups-6](assets/Chapter-4/mobile-mockups-6.png){width=45%}

![mobile-mockups-7](assets/Chapter-4/mobile-mockups-7.png){width=45%}

![mobile-mockups-8](assets/Chapter-4/mobile-mockups-8.png){width=45%}

![mobile-mockups-9](assets/Chapter-4/mobile-mockups-9.png){width=45%}

![mobile-mockups-10](assets/Chapter-4/mobile-mockups-10.png){width=45%}

![mobile-mockups-11](assets/Chapter-4/mobile-mockups-11.png){width=45%}

![mobile-mockups-12](assets/Chapter-4/mobile-mockups-12.png){width=45%}

![mobile-mockups-13](assets/Chapter-4/mobile-mockups-13.png){width=45%}

![mobile-mockups-14](assets/Chapter-4/mobile-mockups-14.png){width=45%}

![mobile-mockups-15](assets/Chapter-4/mobile-mockups-15.png){width=45%}

![mobile-mockups-16](assets/Chapter-4/mobile-mockups-16.png){width=45%}

![mobile-mockups-17](assets/Chapter-4/mobile-mockups-17.png){width=45%}

![mobile-mockups-18](assets/Chapter-4/mobile-mockups-18.png){width=45%}

![mobile-mockups-19](assets/Chapter-4/mobile-mockups-19.png){width=45%}

![mobile-mockups-20](assets/Chapter-4/mobile-mockups-20.png){width=45%}

![mobile-mockups-21](assets/Chapter-4/mobile-mockups-21.png){width=45%}

![mobile-mockups-22](assets/Chapter-4/mobile-mockups-22.png){width=45%}

![mobile-mockups-23](assets/Chapter-4/mobile-mockups-23.png){width=45%}

![mobile-mockups-24](assets/Chapter-4/mobile-mockups-24.png){width=45%}

![mobile-mockups-25](assets/Chapter-4/mobile-mockups-25.png){width=45%}

![mobile-mockups-26](assets/Chapter-4/mobile-mockups-26.png){width=45%}

### 4.4.4. Mobile Applications User Flow Diagrams

Esta sección detalla los flujos de usuario (User Flows) adaptados a la interfaz de la aplicación móvil, garantizando coherencia lógica con la versión web pero optimizados para interacciones táctiles y pantallas reducidas.

### Mobile User Flow 1: Pre-evaluación Crediticia Móvil

![mobile-userflow-1](assets/Chapter-4/mobile-userflow-1.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Enviar la solicitud de crédito vehicular desde su dispositivo móvil.

- **Descripción del Happy Path:** El flujo inicia (nodo azul) en la vista móvil del detalle de la "Toyota RAV4 2024". El usuario abre el formulario táctil de solicitud e ingresa sus datos. El sistema procesa el primer nodo de decisión (rombo rojo) para validar campos obligatorios. Luego, el segundo nodo de decisión evalúa la respuesta de la entidad financiera. Al recibir la aprobación, la app móvil transita a una pantalla de confirmación exitosa con la credencial del perfil aprobado.

- **Descripción del Unhappy Path 1 (Error de formulario):** El primer rombo desvía el flujo si los datos están incompletos, recargando el formulario con alertas visuales requeridas.

- **Descripción del Unhappy Path 2 (Crédito denegado):** El segundo rombo desvía la experiencia hacia una vista móvil de error si la financiera rechaza la solicitud.

### Mobile User Flow 2: Gestión Móvil de Bonos y Campañas

![mobile-userflow-2](assets/Chapter-4/mobile-userflow-2.png)

- **User Persona:** Valeria Rojas (Concesionaria de Autos Nuevos)

- **User Goal:** Configurar rápidamente una campaña de descuento desde la app administrativa.

- **Descripción del Happy Path:** Desde el menú móvil, el administrador ingresa a la vista de "Campañas y Bonos". Tras completar los datos, el sistema procesa el primer rombo de decisión para validar el descuento. Acto seguido, un segundo rombo de decisión confirma la disponibilidad del auto en la base de datos. Al tener éxito, la app navega a la pantalla "Gestión de Inventario", confirmando la actualización del stock.

- **Descripción del Unhappy Path 1 (Monto excedido):** Si el primer rombo detecta un monto inválido, muestra un mensaje de alerta rojo en la misma vista móvil del formulario.

- **Descripción del Unhappy Path 2 (Error de stock):** Si el vehículo ya no está disponible en el segundo rombo, la app transita a la vista de inventario con un indicador de error destacado.

### Mobile User Flow 3: Atención de Prospectos Móvil

![mobile-userflow-3](assets/Chapter-4/mobile-userflow-3.png)

- **User Persona:** Roberto García (Concesionaria de Autos Usados)

- **User Goal:** Revisar notificaciones de leads y responder consultas en tiempo real.

- **Descripción del Happy Path:** El asesor inicia el flujo en la tarjeta móvil del prospecto "Carlos Mendoza". El primer rombo de decisión representa la evaluación de viabilidad del lead por parte del asesor. Al considerarlo apto, transita a la interfaz de "Bandeja de Entrada" de la app. En el chat, el segundo rombo de decisión espera la confirmación de la cita por parte del cliente. Con el acuerdo logrado, el flujo llega al nodo de éxito final.

- **Descripción del Unhappy Path 1 (Rechazo de Lead):** Si el asesor determina en el primer rombo que el prospecto no es apto, finaliza el flujo anticipadamente, archivando el registro.

- **Descripción del Unhappy Path 2 (Interacción fallida):** Si en el segundo rombo el cliente no da respuesta en el chat, el flujo termina en un nodo pendiente inferior, a la espera de seguimiento.

## 4.5. Mobile Applications Prototyping

### 4.5.1. Android Mobile Applications Prototyping

[https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20Android%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ea167f36b%2D6ab9%2D4b43%2Dac6d%2D5be3407131c0](https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20Android%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ea167f36b%2D6ab9%2D4b43%2Dac6d%2D5be3407131c0)

### 4.5.2. iOS Mobile Applications Prototyping

[https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20Iphone%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ee04382ee%2D4fe6%2D4860%2Daf80%2Dda7f7f9cfd64](https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20Iphone%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ee04382ee%2D4fe6%2D4860%2Daf80%2Dda7f7f9cfd64)

## 4.6. Web Applications UX/UI Design

### 4.6.1. Web Applications Wireframes

![webapp-wireframe-1](assets/Chapter-4/webapp-wireframe-1.png)

![webapp-wireframe-2](assets/Chapter-4/webapp-wireframe-2.png)

![webapp-wireframe-3](assets/Chapter-4/webapp-wireframe-3.png)

![webapp-wireframe-4](assets/Chapter-4/webapp-wireframe-4.png)

![webapp-wireframe-5](assets/Chapter-4/webapp-wireframe-5.png)

![webapp-wireframe-6](assets/Chapter-4/webapp-wireframe-6.png)

![webapp-wireframe-7](assets/Chapter-4/webapp-wireframe-7.png)

![webapp-wireframe-8](assets/Chapter-4/webapp-wireframe-8.png)

![webapp-wireframe-9](assets/Chapter-4/webapp-wireframe-9.png)

![webapp-wireframe-10](assets/Chapter-4/webapp-wireframe-10.png)

![webapp-wireframe-11](assets/Chapter-4/webapp-wireframe-11.png)

![webapp-wireframe-12](assets/Chapter-4/webapp-wireframe-12.png)

![webapp-wireframe-13](assets/Chapter-4/webapp-wireframe-13.png)

![webapp-wireframe-14](assets/Chapter-4/webapp-wireframe-14.png)

![webapp-wireframe-15](assets/Chapter-4/webapp-wireframe-15.png)

![webapp-wireframe-16](assets/Chapter-4/webapp-wireframe-16.png)

![webapp-wireframe-17](assets/Chapter-4/webapp-wireframe-17.png)

![webapp-wireframe-18](assets/Chapter-4/webapp-wireframe-18.png)

![webapp-wireframe-19](assets/Chapter-4/webapp-wireframe-19.png)

![webapp-wireframe-20](assets/Chapter-4/webapp-wireframe-20.png)

![webapp-wireframe-21](assets/Chapter-4/webapp-wireframe-21.png)

![webapp-wireframe-22](assets/Chapter-4/webapp-wireframe-22.png)

![webapp-wireframe-23](assets/Chapter-4/webapp-wireframe-23.png)

![webapp-wireframe-24](assets/Chapter-4/webapp-wireframe-24.png)

![webapp-wireframe-25](assets/Chapter-4/webapp-wireframe-25.png)

![webapp-wireframe-26](assets/Chapter-4/webapp-wireframe-26.png)

### 4.6.2. Web Applications Wireflow Diagrams

Esta sección presenta los Wireflows propuestos para la aplicación web. Los flujos ilustran cómo la interacción del usuario genera cambios de estado en la interfaz para cumplir sus objetivos principales.

### Wireflow 1: Búsqueda Multicanal y Solicitud de Pre-evaluación

![webapp-wireflow-1](assets/Chapter-4/webapp-wireflow-1.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Encontrar un vehículo financiable explorando diferentes rutas de descubrimiento (IA, Catálogo o Concesionaria directa) y completar el formulario de pre-evaluación crediticia.

- **Explicación del Flujo y Estados UI:**

  El flujo centraliza las tres vías principales que tiene el comprador para llegar a la ficha de un vehículo. Partiendo de la vista de inicio del Panel de Comprador (extremo izquierdo), el usuario puede tomar tres rutas de navegación:

  * **Vía IA (Arriba):** Ingresa a la interfaz de "Consulta IA", interactúa en el chat ingresando su presupuesto y recibe una recomendación directa que transita a la ficha del vehículo.

  * **Vía Catálogo General (Centro):** Ingresa a "Vehículos a buscar", utiliza los filtros estructurados (Condición, Rango de Precio) y selecciona una unidad específica del catálogo unificado.

  * **Vía Concesionaria Aliada (Abajo):** Ingresa al directorio de agencias, transita al portal privado de una concesionaria específica (ej. EuroMotors) y selecciona un vehículo de su inventario particular.

  Independientemente de la ruta elegida, todas convergen en un estado común: la vista de **Detalle del Vehículo** (la pantalla central más grande). Aquí el usuario revisa las fotos, el precio y el simulador de cuotas. Finalmente, al hacer clic en la acción principal, el estado de la interfaz cambia superponiendo el **Modal de Solicitud de Pre-evaluación Crediticia** (extremo derecho), donde el flujo culmina con el ingreso de datos para enviar a la entidad bancaria.

### Wireflow 2: Panel de Rendimiento y Gestión de Bonos B2B

![webapp-wireflow-2](assets/Chapter-4/webapp-wireflow-2.png)

- **User Persona:** Valeria Rojas (Concesionaria de Autos Nuevos)

- **User Goal:** Analizar el rendimiento comercial en pantalla grande y aplicar estrategias de precios (campañas) sobre unidades específicas.

- **Explicación del Flujo y Estados UI:** El flujo arranca en el "Resumen de Rendimiento" del Dashboard B2B, mostrando gráficas de interacciones y prospectos en un periodo determinado. El gerente navega hacia el "Inventario Activo", donde se listan los vehículos disponibles en formato de tabla de datos. Desde esta vista, selecciona una unidad y transita al módulo de "Campañas y Bonos", donde un formulario le permite configurar un descuento. Al guardar los cambios, la interfaz cambia de estado mostrando un modal o pantalla de confirmación de publicación exitosa, actualizando el precio público del vehículo.

### Wireflow 3: Administración de Equipo de Ventas y Asignaciones

![webapp-wireflow-3](assets/Chapter-4/webapp-wireflow-3.png)

- **User Persona:** Administrador de Concesionaria / Gerente Comercial

- **User Goal:** Monitorear el desempeño del equipo de ventas, registrar nuevos asesores y reasignar prospectos para optimizar la tasa de cierre.

- **Explicación del Flujo y Estados UI:** El flujo inicia en el panel general, desde donde el administrador accede a la sección "Control de Asesores" o "Equipo de Ventas". La interfaz presenta una lista de los ejecutivos registrados junto con sus métricas operativas. Al seleccionar la acción de editar sobre un perfil, la vista cambia a un formulario de "Edición de Asesor" donde se pueden modificar roles o reasignar carteras de leads. Al guardar, el flujo finaliza confirmando la acción y reflejando el nuevo estado organizativo de la agencia en el sistema.

### 4.6.3. Web Applications Mock-ups

![webapp-mockups-1](assets/Chapter-4/webapp-mockups-1.png)

![webapp-mockups-2](assets/Chapter-4/webapp-mockups-2.png)

![webapp-mockups-3](assets/Chapter-4/webapp-mockups-3.png)

![webapp-mockups-4](assets/Chapter-4/webapp-mockups-4.png)

![webapp-mockups-5](assets/Chapter-4/webapp-mockups-5.png)

![webapp-mockups-6](assets/Chapter-4/webapp-mockups-6.png)

![webapp-mockups-7](assets/Chapter-4/webapp-mockups-7.png)

![webapp-mockups-8](assets/Chapter-4/webapp-mockups-8.png)

![webapp-mockups-9](assets/Chapter-4/webapp-mockups-9.png)

![webapp-mockups-10](assets/Chapter-4/webapp-mockups-10.png)

![webapp-mockups-11](assets/Chapter-4/webapp-mockups-11.png)

![webapp-mockups-12](assets/Chapter-4/webapp-mockups-12.png)

![webapp-mockups-13](assets/Chapter-4/webapp-mockups-13.png)

![webapp-mockups-14](assets/Chapter-4/webapp-mockups-14.png)

![webapp-mockups-15](assets/Chapter-4/webapp-mockups-15.png)

![webapp-mockups-16](assets/Chapter-4/webapp-mockups-16.png)

![webapp-mockups-17](assets/Chapter-4/webapp-mockups-17.png)

![webapp-mockups-18](assets/Chapter-4/webapp-mockups-18.png)

![webapp-mockups-19](assets/Chapter-4/webapp-mockups-19.png)

![webapp-mockups-20](assets/Chapter-4/webapp-mockups-20.png)

![webapp-mockups-21](assets/Chapter-4/webapp-mockups-21.png)

![webapp-mockups-22](assets/Chapter-4/webapp-mockups-22.png)

![webapp-mockups-23](assets/Chapter-4/webapp-mockups-23.png)

![webapp-mockups-24](assets/Chapter-4/webapp-mockups-24.png)

![webapp-mockups-25](assets/Chapter-4/webapp-mockups-25.png)

![webapp-mockups-26](assets/Chapter-4/webapp-mockups-26.png)

### 4.6.4. Web Applications User Flow Diagrams

Esta sección presenta la propuesta de User Flows para la aplicación web. Se ha considerado un User Flow para cada objetivo principal, incluyendo los mock-ups de las pantallas, la ruta esperada (Happy Path) y las rutas alternativas de error (Unhappy Paths) dictadas por los nodos de decisión del sistema.

### Web User Flow 1: Solicitud de Pre-evaluación Crediticia

![webapp-userflow-1](assets/Chapter-4/webapp-userflow-1.png)

- **User Persona:** Carlos Mendoza (Comprador Interesado)

- **User Goal:** Solicitar la pre-evaluación financiera para un vehículo específico.

- **Descripción del Happy Path:** El flujo inicia (nodo azul) en la vista de detalle del vehículo. El usuario ingresa al formulario de pre-evaluación crediticia y llena sus datos financieros. El sistema valida la información en el primer nodo de decisión (rombo rojo). Tras pasar esta validación local, el flujo avanza a un segundo nodo de decisión (rombo rojo) donde se evalúa la aprobación de la entidad bancaria externa. Al ser aprobado, el flujo transita a una pantalla de éxito, culminando la ruta ideal en el nodo azul final.

- **Descripción del Unhappy Path 1 (Error de datos):** En el primer rombo de decisión, si el usuario ingresa datos inválidos o falta información, el sistema interrumpe la ruta principal y despliega un error visual en el mismo formulario.

- **Descripción del Unhappy Path 2 (Rechazo crediticio):** Si el banco deniega el perfil en el segundo rombo de decisión, el sistema desvía al usuario hacia una vista alternativa que informa el rechazo del crédito.

### Web User Flow 2: Aplicación de Campañas y Bonos

![webapp-userflow-2](assets/Chapter-4/webapp-userflow-2.png)

- **User Persona:** Valeria Rojas (Concesionaria de Autos Nuevos)

- **User Goal:** Crear un bono de descuento y aplicarlo a un vehículo disponible.

- **Descripción del Happy Path:** El usuario parte del nodo azul inicial e ingresa a la pantalla de "Campañas y Bonos". Completa el formulario del bono y el sistema entra al primer rombo de decisión para validar si el monto ingresado es permitido por las reglas de negocio. Al validarlo, pasa a un segundo rombo de decisión para verificar si el vehículo objetivo sigue en estado disponible. Con ambas validaciones superadas, el flujo llega a la vista de "Gestión de Inventario", mostrando la tabla actualizada con éxito.

- **Descripción del Unhappy Path 1 (Monto inválido):** Si el monto del bono falla la validación en el primer rombo, el sistema despliega un mensaje de error rojo sobre el mismo formulario de campañas.

- **Descripción del Unhappy Path 2 (Vehículo no disponible):** Si la validación de inventario en el segundo rombo falla, la interfaz muestra una pantalla de error indicando que la unidad ya no admite modificaciones.

### Web User Flow 3: Gestión y Atención de Prospectos

![webapp-userflow-3](assets/Chapter-4/webapp-userflow-3.png)

- **User Persona:** Roberto García (Concesionaria de Autos Usados)

- **User Goal:** Evaluar la viabilidad de un prospecto y contactarlo para agendar una cita.

- **Descripción del Happy Path:** El gerente comercial inicia en el detalle del prospecto "Carlos Mendoza". En el primer rombo de decisión, el gerente evalúa si el perfil del comprador es viable. Al determinar que sí, transita a la "Bandeja de Entrada" (Mensajes) para contactar al cliente. Durante la conversación, un segundo rombo de decisión evalúa si el cliente confirma la disponibilidad para la cita. Al recibir respuesta afirmativa, el flujo termina exitosamente en la confirmación.

- **Descripción del Unhappy Path 1 (Lead descartado):** Si en el primer rombo el perfil financiero del prospecto no es apto, el flujo se desvía hacia el final, descartando el contacto.

- **Descripción del Unhappy Path 2 (Sin respuesta):** Si el cliente no confirma la cita en el segundo rombo, el flujo se pausa derivando a un estado alternativo pendiente.

## 4.7. Web Applications Prototyping

[https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20WebApp%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ede73efa3%2Deae7%2D4cf7%2D8c90%2Dc09d17c6b910](https://upcedupe-my.sharepoint.com/personal/u20231b120_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20231b120%5Fupc%5Fedu%5Fpe%2FDocuments%2FVideos%5FDise%C3%B1odeExperimentos%2FPrototipo%20WebApp%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ede73efa3%2Deae7%2D4cf7%2D8c90%2Dc09d17c6b910)

## 4.8. Domain-Driven Software Architecture

A continuación se presenta la documentación detallada de la arquitectura de software basada en el modelo C4 y en los principios de Domain-Driven Design (DDD).

### 4.8.1. Software Architecture Context Diagram

El diagrama de contexto (Nivel 1) ilustra la plataforma SmartFinance Drive como el sistema central que conecta la oferta y la demanda del sector automotriz. En este nivel se identifican las interacciones principales con los actores y sistemas externos:

![Context Diagram](assets/Chapter-4/ContextDiagram.png)

- **Comprador Interesado**: Usuario final que busca vehículos, recibe recomendaciones de inteligencia artificial y solicita pre-evaluaciones crediticias.

- **Concesionaria**: Cliente corporativo que publica su inventario de vehículos nuevos o usados, atiende a los prospectos (leads) y gestiona el pago de sus membresías B2B.

- **Super Administrador**: Actor encargado de gestionar la configuración global de la plataforma, administrar usuarios, entidades financieras y definir los planes de negocio.

- **Servicios SUNAT (Externo)**: Sistema gubernamental utilizado para la validación de números de RUC, estado y condición de las empresas.

- **Entidades Financieras (Externo)**: Bancos aliados que proveen las tasas de referencia (TEA/TCEA) y ejecutan la validación externa de las pre-aprobaciones crediticias.

- **Stripe (Externo)**: Pasarela de pagos encargada de procesar los cobros de las suscripciones B2B y la facturación de las concesionarias.

---

### 4.8.2. Software Architecture Container Diagrams

El diagrama de contenedores (Nivel 2) desglosa el sistema SmartFinance Drive en sus aplicaciones principales y componentes de almacenamiento de datos. El sistema se estructura de la siguiente manera:

![Container Diagram](assets/Chapter-4/ContainerDiagram.png)

- **Landing Page**: Aplicación web estática (HTML/CSS/JS) orientada a la presentación del producto y conversión de visitantes.

- **Web Application**: Frontend tipo SPA desarrollado en Vue.js, que proporciona las interfaces para el catálogo de compradores, el panel B2B de concesionarias y el backoffice administrativo.

- **Mobile App**: Aplicación móvil nativa para iOS y Android, enfocada en la búsqueda ágil de autos para el comprador y la gestión en patio para el vendedor.

- **Backend API**: Implementado como un monolito modular basado en Java Spring Boot y Next.js. Este contenedor centraliza toda la lógica de negocio estructurada en 8 Bounded Contexts independientes.

- **Base de Datos**: Sistema de gestión de bases de datos relacional PostgreSQL, encargado de almacenar de forma persistente la información de usuarios, simulaciones, inventario y facturación de todos los contextos.

---

### 4.8.3. Software Architecture Components Diagrams

En el Nivel 3, se realiza un acercamiento a la estructura interna del Backend API. Al seguir los principios de Clean Architecture, cada Bounded Context se desglosa en cuatro capas principales: Interfaces (Controladores REST), Application (Casos de Uso), Domain (Reglas de negocio y Agregados) e Infrastructure (Adaptadores de persistencia y clientes externos).

#### Component Diagram: IAM Context

El contexto de Identidad y Gestión de Accesos (IAM) aísla completamente la seguridad de los datos operativos.

![Component Diagram IAM](assets/Chapter-4/ComponentDiagram_IAM.png)

- **Responsabilidad**: Gestiona la autenticación de usuarios, registro, manejo de sesiones y emisión de tokens de seguridad JWT.

- **Componentes clave**: Implementa el agregado principal `User`, expone controladores para login y recuperación de contraseñas, y maneja la persistencia de credenciales y tokens revocados en la base de datos.

#### Component Diagram: Profiles Context

El contexto Profiles separa los datos demográficos de las credenciales de acceso.

![Component Diagram Profiles](assets/Chapter-4/ComponentDiagram_Profiles.png)

- **Responsabilidad**: Gestión de la información personal, laboral y socioeconómica del cliente (nombres, teléfono, DNI y nivel de ingresos mensuales).

- **Componentes clave**: Orquesta la actualización de los perfiles mediante el agregado `Profile` y los adapta para su persistencia, sirviendo de base para la evaluación de riesgo crediticio.

#### Component Diagram: Catalog Context

El contexto Catalog administra de manera aislada la oferta de vehículos.

![Component Diagram Catalog](assets/Chapter-4/ComponentDiagram_Catalog.png)

- **Responsabilidad**: Gestión del catálogo unificado de vehículos disponibles, incluyendo características técnicas, precios, estado (nuevo/usado) e integración de imágenes.

- **Componentes clave**: Utiliza el agregado `Vehicle` para centralizar la información que luego será consumida por el motor de simulaciones para evitar alteraciones de precio desde el frontend.

#### Component Diagram: Partners Context

El contexto Partners administra las variables macroeconómicas y los aliados de la plataforma.

![Component Diagram Partners](assets/Chapter-4/ComponentDiagram_Partners.png)

- **Responsabilidad**: Administración de entidades bancarias asociadas, sus rangos de tasas (TEA/TCEA), comisiones de seguros y la integración con servicios gubernamentales.

- **Componentes clave**: Administra los agregados `FinancialEntity` y `RateBenchmark`, y utiliza la capa de infraestructura para realizar llamadas HTTP externas a la API de SUNAT.

#### Component Diagram: Financing Context

El contexto Financing representa el Core Domain de la plataforma.

![Component Diagram Financing](assets/Chapter-4/ComponentDiagram_Financing.png)

- **Responsabilidad**: Orquesta la creación de planes de financiamiento, genera cronogramas de cuotas aplicando el método francés y calcula indicadores como VAN, TIR y TCEA.

- **Componentes clave**: El servicio de dominio `FinancingPlanBuilder` ejecuta los algoritmos matemáticos, y el agregado `Simulation` encapsula los periodos de pago generados para su persistencia en la base de datos.

#### Component Diagram: Scoring Context

El contexto Scoring se encarga del análisis de viabilidad crediticia.

![Component Diagram Scoring](assets/Chapter-4/ComponentDiagram_Scoring.png)

- **Responsabilidad**: Evalúa la capacidad de endeudamiento cruzando la cuota proyectada con los ingresos del usuario para calcular el Ratio de Cobertura de Deuda (DTI).

- **Componentes clave**: Asigna un nivel de riesgo crediticio (Risk Tier) que se comunica directamente con el contexto de financiamiento para ajustar automáticamente la tasa de interés ofrecida.

#### Component Diagram: Projections Context

El contexto Projections añade la capa de innovación para las decisiones inteligentes.

![Component Diagram Projections](assets/Chapter-4/ComponentDiagram_Projections.png)

- **Responsabilidad**: Estima la depreciación técnica y comercial del vehículo a lo largo del tiempo (2, 3 o 5 años).

- **Componentes clave**: A través del agregado `DepreciationProjection`, contrasta la curva de valor del vehículo contra la cuota balón del crédito para aconsejar al usuario sobre la rentabilidad de su compra.

#### Component Diagram: Billing Context

El contexto Billing gestiona la monetización y modelo de negocio de SmartFinance Drive.

![Component Diagram Billing](assets/Chapter-4/ComponentDiagram_Billing.png)

- **Responsabilidad**: Control de los planes de suscripción B2B (SaaS), facturación, y cobro de membresías a las concesionarias.

- **Componentes clave**: Maneja los agregados `Subscription`, `Plan` e `Invoice`. Su capa de infraestructura integra el SDK de Stripe para la generación de checkouts de pago y la escucha asíncrona de webhooks.

## 4.9 Software Object-Oriented Design

### 4.9.1 Class Diagram

El siguiente diagrama de clases general representa la estructura orientada a objetos de toda la plataforma SmartFinance. Se modelan las entidades principales del dominio y sus interacciones, promoviendo una separación clara de responsabilidades bajo el enfoque de Domain-Driven Design (DDD).

![General Class Diagram](assets/Chapter-4/oopgeneral.png "Diagrama de Clases General")

#### Bounded Context: Identity & Security

Este diagrama representa el contexto de Identity & Security, el cual centraliza la autenticación, autorización y administración de usuarios del sistema. En este contexto, el Aggregate Root es `User`, el cual contiene la información de acceso y sus vínculos directos con los roles del sistema (`Role`). Además, se gestionan los tokens revocados (`RevokedToken`) para garantizar la integridad y seguridad de las sesiones activas. El diseño separa claramente las responsabilidades de identidad de la información personal del usuario.

![Class diagram identity](assets/Chapter-4/oop1.png "Identity & Security")

#### Bounded Context: Profile

El contexto Profile encapsula todo lo relacionado con la representación y datos demográficos de los usuarios en el sistema. El Aggregate Root es `Profile`, que contiene la información no sensible y de contacto (nombres, teléfono, país), así como datos críticos para el negocio como ingresos mensuales y estado laboral. Este diseño permite a los usuarios gestionar su identidad financiera y es el punto de integración principal con los módulos de evaluación crediticia.

![Class diagram profile](assets/Chapter-4/oop2.png "Profile")

#### Bounded Context: Subscriptions & Billing

El diagrama de clases presentado pertenece al contexto de Subscriptions & Billing, el cual representa el núcleo de las funcionalidades relacionadas con la gestión de planes SaaS y facturación. El Aggregate Root principal es `Subscription`, que vincula a un usuario con un `Plan` específico. La entidad `Invoice` encapsula los datos relacionados con el cobro, montos y fechas de pago. Este diseño refleja un enfoque modular preparado para integraciones con gateways de pago externos (como Stripe) mediante capas de infraestructura.

![Class diagram subscriptions](assets/Chapter-4/oop3.png "Subscriptions & Billing")

#### Bounded Context: Vehicle Catalog

Este esquema representa la lógica del contexto de Vehicle Catalog. La clase principal es `Vehicle`, que almacena los detalles técnicos, de marca, modelo, año de fabricación y precio de los automóviles disponibles para financiamiento. Su diseño flexible permite gestionar de manera eficiente el catálogo que los usuarios explorarán antes de realizar una cotización.

![Class diagram vehicle catalog](assets/Chapter-4/oop4.png "Vehicle Catalog")

#### Bounded Context: Financial Configuration

Este diagrama enfoca su diseño en la parametrización del mercado a través del contexto Financial Configuration. El Aggregate Root es `FinancialEntity`, representando a los bancos, cajas o instituciones de crédito. Se relaciona con `RateBenchmark`, que modela las tasas de referencia (TEA, TCEA), tipos de interés y reglas de negocio vigentes que dictan las condiciones de financiamiento en la plataforma.

![Class diagram financial config](assets/Chapter-4/oop5.png "Financial Configuration")

#### Bounded Context: Simulation

Este esquema representa el contexto Simulation, el motor matemático y central del sistema. El Aggregate Root es `Simulation`, que encapsula todas las variables ingresadas por el usuario (cuota inicial, plazo, tasa seleccionada, monto financiado). Se compone de múltiples instancias de `SimulationPaymentPeriod`, las cuales modelan el detalle individual de cada cuota del cronograma de pagos (amortización, interés, seguros y saldos).

![Class diagram simulation](assets/Chapter-4/oop6.png "Simulation")

#### Bounded Context: Planning

El contexto de Planning aborda la proyección y viabilidad de las decisiones del usuario. Modela clases analíticas como `CreditScore`, que evalúa la capacidad de endeudamiento, ratio DTI (Debt-to-Income) y el nivel de riesgo del perfil frente a una simulación; y `DepreciationProjection`, que encapsula el comportamiento del valor del vehículo a lo largo del tiempo, permitiendo generar recomendaciones estratégicas al usuario.

![Class diagram planning](assets/Chapter-4/oop7.png "Planning")

### 4.9.2 Class Dictionary

| Entidad | Descripción |
| :--- | :--- |
| **User** | Entidad raíz de seguridad que representa a cualquier persona que interactúa con la plataforma, almacenando sus credenciales de acceso y estado de cuenta. |
| **Role** | Define los permisos y el nivel de acceso asignado a un usuario dentro del sistema (ej. Cliente, Administrador). |
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
| **DepreciationProjection** | Análisis predictivo de la pérdida de valor de un vehículo en el tiempo, utilizado para aconsejar al usuario sobre la rentabilidad de su inversión a mediano y largo plazo. |

## 4.10 Database Design

### 4.10.1 Database Diagram

![Database diagram general](assets/Chapter-4/dbgeneral.png "Diagrama de base de datos general")

#### Bounded Context: Identity & Security

Este esquema representa la lógica del contexto de identidad y seguridad de SmartFinance. La tabla `users` almacena las credenciales de acceso y controles de bloqueo de los usuarios. Se apoya en las tablas `roles` y `user_roles` para la gestión de permisos, mientras que `revoked_tokens` maneja la invalidación de sesiones por seguridad.

![Database diagram identity](assets/Chapter-4/db1.png "Identity & Security")

#### Bounded Context: Profile

Este esquema representa el contexto de gestión de clientes. La tabla `profiles` concentra toda la información personal, financiera (ingresos mensuales) y laboral del usuario, la cual es indispensable para perfilar al cliente antes de una evaluación crediticia.

![Database diagram profile](assets/Chapter-4/db2.png "Profile")

#### Bounded Context: Subscriptions & Billing

Este esquema controla el modelo de negocio SaaS de la plataforma. La tabla `plans` define los límites de simulaciones y vehículos por paquete. La tabla `subscriptions` vincula al usuario con un plan activo usando los identificadores de Stripe, y la tabla `invoices` registra el historial de facturación y cobros.

![Database diagram subscriptions](assets/Chapter-4/db3.png "Subscriptions & Billing")

#### Bounded Context: Vehicle Catalog

Este esquema aísla la gestión del inventario automotriz. La tabla `vehicles` centraliza los datos técnicos, año de fabricación, marca, condición y precio del vehículo a financiar, estableciendo además su vínculo con una entidad financiera.

![Database diagram vehicle catalog](assets/Chapter-4/db4.png "Vehicle Catalog")

#### Bounded Context: Financial Configuration

Este esquema administra los parámetros macroeconómicos del sistema. La tabla `financial_entities` registra los bancos o financieras disponibles, mientras que `financial_entity_rate_benchmarks` almacena el historial de tasas referenciales aplicables a los créditos.

![Database diagram financial config](assets/Chapter-4/db5.png "Financial Configuration")

#### Bounded Context: Simulation

Este esquema define el núcleo de cálculo del sistema. La tabla `simulations` concentra todas las variables del crédito (TEA, TCEA, cuota inicial, seguros y montos a financiar). La tabla `simulation_payment_periods` desglosa el cronograma mes a mes, separando el capital, interés y los seguros aplicados en cada cuota.

![Database diagram simulation](assets/Chapter-4/db6.png "Simulation")

#### Bounded Context: Planning

Este esquema se enfoca en el análisis predictivo y la viabilidad del crédito. La tabla `credit_scores` evalúa el riesgo financiero del perfil asociado a una simulación particular, determinando ratios de deuda e ingresos. La tabla `depreciation_projections` planifica el valor futuro del vehículo, calculando la depreciación anual para ofrecer acciones recomendadas al cliente.

![Database diagram planning](assets/Chapter-4/db7.png "Planning")
