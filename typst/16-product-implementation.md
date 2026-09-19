# Capítulo V: Product Implementation

## 5.1. Software Configuration Management

### 5.1.1. Software Development Environment Configuration

En esta sección se presentan las principales herramientas utilizadas durante el desarrollo de **SmartFinance Drive**, organizadas según las actividades de UX/UI Design, arquitectura, modelado, gestión del producto y desarrollo de software.

#### Product UX/UI Design

Esta área comprende las actividades relacionadas con el análisis de usuarios, definición de experiencias, diseño de interfaces y validación de los flujos de interacción de SmartFinance Drive.

- **Canvas:** herramienta utilizada para desarrollar el **Lean UX Canvas**, permitiendo organizar el problema, los usuarios objetivo, las soluciones propuestas y las hipótesis que orientan el desarrollo del producto.

- **UxPressia:** plataforma utilizada para representar y analizar la experiencia de los usuarios. Se empleó para elaborar:
  - User Personas.
  - User Task Matrix.
  - User Journey Mapping.
  - Empathy Mapping.
  - Impact Mapping.

- **Miro:** herramienta colaborativa utilizada para representar visualmente los escenarios del producto. Se empleó principalmente para:
  - As-is Scenario Mapping.
  - To-Be Scenario Mapping.

- **Figma:** herramienta de diseño colaborativo utilizada para la elaboración de **Wireframes, Mock-ups y Prototypes**. Permitió representar las interfaces de SmartFinance Drive antes de su implementación y validar la estructura visual de las diferentes pantallas.

- **Overflow:** herramienta utilizada para desarrollar **Wireflows y User Flows**, permitiendo representar las rutas de navegación y las interacciones principales que puede realizar un usuario dentro de la plataforma.

#### Software Architecture & Modeling

Esta área comprende las herramientas utilizadas para definir y documentar la arquitectura y estructura interna de SmartFinance Drive.

- **DLS Editor / Structurizr:** herramientas utilizadas para la elaboración de los diagramas de arquitectura de software, incluyendo:
  - Software Architecture Context Diagram.
  - Software Architecture Container Diagrams.
  - Software Architecture Components Diagrams.

- **UML:** utilizado para representar los elementos relacionados con el diseño orientado a objetos y el diseño de la base de datos. Entre los principales artefactos desarrollados se encuentran:
  - Class Diagrams.
  - Class Dictionary.
  - Relational/Non-Relational Database Diagram.

#### Product Management

- **Trello:** herramienta utilizada para administrar el **Product Backlog**, organizar las historias de usuario y realizar el seguimiento de las actividades planificadas para los diferentes Sprints del proyecto.

#### Software Development

El desarrollo de SmartFinance Drive se divide principalmente en la **Landing Page, Frontend Web Application y Backend**, utilizando tecnologías específicas para cada componente.

- **Landing Page:**
  - **HTML5:** utilizado para estructurar el contenido de la página.
  - **CSS3:** utilizado para definir los estilos y presentación visual.
  - **JavaScript:** utilizado para implementar la interacción y comportamiento dinámico.
  - **Material Design:** utilizado como referencia para los principios visuales y de diseño de la interfaz.

- **Frontend Web Application:**
  - **Vue Framework:** utilizado como framework principal para el desarrollo de la aplicación web.
  - **HTML5:** utilizado para la estructura de las interfaces.
  - **CSS3:** utilizado para los estilos y diseño visual.
  - **JavaScript:** utilizado para implementar la lógica e interactividad del frontend.
  - **PrimeVue:** utilizado como biblioteca de componentes de interfaz de usuario.
  - **Material Design:** utilizado como referencia para mantener una interfaz consistente y orientada a la usabilidad.

- **Backend:**
  - **Next.js (App Router):** utilizado como framework principal para la implementación de los servicios y lógica del lado servidor.
  - **TypeScript:** utilizado como lenguaje principal para el desarrollo del backend, proporcionando tipado estático y mayor seguridad durante la implementación.
  - **Clean Architecture:** utilizada como patrón arquitectónico para separar responsabilidades y organizar la lógica del sistema.
  - **Server Actions:** utilizadas para ejecutar operaciones directamente en el servidor mediante las capacidades de Next.js.
  - **Route Handlers:** utilizados para implementar endpoints HTTP tradicionales, principalmente para integraciones y funcionalidades que requieren comunicación mediante API.

#### Database & Authentication

- **PostgreSQL:** sistema de gestión de bases de datos relacional utilizado para la persistencia de la información de SmartFinance Drive.

- **Prisma:** ORM utilizado para facilitar la interacción entre el backend y PostgreSQL, permitiendo trabajar con los datos mediante modelos y operaciones tipadas.

- **Supabase:** plataforma utilizada principalmente para la autenticación y gestión de sesiones de los usuarios. También se utiliza para almacenar información relacionada con los perfiles de usuario.

#### Development Environment

- **Git:** utilizado para el control de versiones del código fuente y el seguimiento de los cambios realizados durante el desarrollo.

- **GitHub:** plataforma utilizada para alojar los repositorios, gestionar el código fuente y facilitar la colaboración entre los integrantes del equipo.

- **IntelliJ IDEA:** entorno de desarrollo utilizado para trabajar principalmente con los componentes relacionados con el backend y la lógica de programación.

- **Antigravity IDE:** herramienta utilizada como apoyo durante las actividades de desarrollo y programación.

- **GitFlow Helper:** herramienta utilizada para facilitar la gestión del flujo de ramas basado en GitFlow.

### 5.1.2. Source Code Management

Para gestionar el código fuente de **SmartFinance Drive**, el equipo utiliza **Git** para el control de versiones y **GitHub** como plataforma de almacenamiento y colaboración.

**Enlace Organización tux-squad:** [https://github.com/tux-squad](https://github.com/tux-squad)

**Repositorios GitHub:**

* **Project Report:** [https://github.com/tux-squad/smartfinance-drive-project-report](https://github.com/tux-squad/smartfinance-drive-project-report)
* **Landing Page:** [https://github.com/tux-squad/smartfinance-drive-landing-page](https://github.com/tux-squad/smartfinance-drive-landing-page)
* **FrontEnd:** [https://github.com/tux-squad/smartfinance-drive-frontend](https://github.com/tux-squad/smartfinance-drive-frontend)
* **BackEnd:** [https://github.com/tux-squad/smartfinance-drive-backend](https://github.com/tux-squad/smartfinance-drive-backend)

#### GitFlow Workflow

El proyecto utiliza **GitFlow** para organizar el desarrollo mediante diferentes tipos de ramas:

| Rama | Uso |
| :--- | :--- |
| `main` | Versiones estables. |
| `develop` | Integración del desarrollo. |
| `feature/*` | Desarrollo de nuevas funcionalidades. |
| `release/*` | Preparación de nuevas versiones. |
| `hotfix/*` | Correcciones urgentes. |

Las ramas de funcionalidades siguen la estructura:

```text
feature/nombre-de-la-funcionalidad
```

#### Conventional Commits

Los commits siguen **Conventional Commits** para mantener un historial organizado:

| Tipo | Uso |
| :--- | :--- |
| `feat` | Nueva funcionalidad. |
| `fix` | Corrección de errores. |
| `docs` | Documentación. |
| `refactor` | Reestructuración del código. |
| `test` | Pruebas. |
| `chore` | Mantenimiento. |

## 5.2. Product Implementation & Deployment
Evidencias de la implementación del Landing Page, Web Frontend, API REST Backend y App Móvil.

## 5.3. Video About-the-Product
Enlace y presentación del video demostrativo del producto.
