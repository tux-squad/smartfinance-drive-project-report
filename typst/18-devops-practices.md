# Capítulo VII: DevOps Practices

Este capítulo describe las prácticas de integración, entrega y despliegue de **SmartFinance Drive**. El proceso DevOps busca que los cambios de código se integren de manera controlada, se verifiquen mediante compilaciones y pruebas, y se publiquen en las plataformas correspondientes. El alcance comprende los servicios backend, la aplicación web, la landing page y la aplicación móvil Android.

Los repositorios del proyecto se encuentran en la organización `tux-squad`.

| Producto | Repositorio | Tecnologías principales | Plataforma de despliegue o distribución |
|---|---|---|---|
| Backend Services | [smartfinance-drive-platform](https://github.com/tux-squad/smartfinance-drive-platform) | Java 26, Spring Boot, Maven, PostgreSQL y Flyway | Render mediante Docker |
| Web Application | [smartfinance-drive-webapp](https://github.com/tux-squad/smartfinance-drive-webapp) | Vue.js, TypeScript y Vite | Vercel |
| Landing Page | [smartfinance-drive-landingpage](https://github.com/tux-squad/smartfinance-drive-landingpage) | HTML5, CSS3 y JavaScript | Vercel |
| Native Mobile Application | [smartfinance-drive-mobile-app](https://github.com/tux-squad/smartfinance-drive-mobile-app) | Kotlin, Jetpack Compose y Gradle | APK de Android para distribución interna |

La arquitectura de despliegue separa el servidor de la API y la base de datos: **Render aloja el backend**, mientras que **Aiven proporciona el servicio administrado de PostgreSQL**. La aplicación web y la landing page se publican de forma independiente en Vercel. La aplicación móvil se compila como APK para su instalación en dispositivos Android.

El equipo utiliza GitFlow (`main`, `develop`, `feature/*`, `release/*` y `hotfix/*`) y Conventional Commits, de acuerdo con la estrategia de trabajo descrita en la sección 5.1.2.

---

## 7.1. Continuous Integration

La integración continua (*Continuous Integration*, CI) consiste en incorporar cambios pequeños y frecuentes al repositorio compartido y verificar cada cambio mediante compilaciones y pruebas automatizadas. En SmartFinance Drive, el objetivo es detectar errores antes de integrar una funcionalidad y evitar que problemas de compilación, pruebas o dependencias lleguen a las etapas de entrega.

### 7.1.1. Tools and Practices

**Herramientas**

| Herramienta | Tipo | Uso en SmartFinance Drive |
|---|---|---|
| Git y GitHub | Control de versiones | Mantienen el historial del código, las ramas de trabajo y las solicitudes de integración (*Pull Requests*). |
| GitHub Actions | Automatización CI/CD | Ejecuta los flujos de compilación, pruebas y verificaciones definidos para los repositorios. |
| Maven Wrapper (`mvnw`) | Construcción del backend | Permite ejecutar Maven con una versión controlada desde el propio repositorio. |
| JUnit Jupiter y Mockito | Pruebas unitarias | Verifican la lógica de entidades y servicios de dominio, aislando dependencias cuando corresponde. |
| Spring MockMvc y Spring Security Test | Pruebas de integración | Permiten comprobar el comportamiento de controladores HTTP y las reglas de autenticación y autorización. |
| Cucumber y Gherkin | Pruebas BDD | Expresan escenarios de comportamiento y criterios de aceptación de forma legible. |
| Swagger UI y Postman | Pruebas de sistema | Permiten ejecutar solicitudes contra la API y validar flujos funcionales completos. |
| OWASP Dependency-Check | Análisis de seguridad | Examina dependencias en busca de vulnerabilidades conocidas cuando se ejecuta como parte de la construcción Maven. |
| Node.js, npm y Vite | Construcción web | Instalan dependencias y generan la versión de producción de la aplicación Vue. |
| Gradle y Android SDK | Construcción móvil | Compilan la aplicación Android y generan el APK. |
| Docker | Contenerización | Empaqueta el backend y su entorno de ejecución en una imagen reproducible. |
| Flyway | Versionado de base de datos | Administra las migraciones del esquema de PostgreSQL. |

**Prácticas de integración**

- **Ramas de corta duración.** Cada funcionalidad se desarrolla en una rama `feature/*` y se propone para integración mediante un Pull Request hacia `develop`.
- **Verificaciones por cambio.** Los flujos de integración se ejecutan ante cambios relevantes en las ramas de trabajo y ante Pull Requests dirigidos a las ramas compartidas.
- **Revisión de código.** Los Pull Requests deben ser revisados por otro integrante del equipo antes de integrarse, siguiendo el proceso de revisión de la sección 6.2.2.
- **Protección de ramas principales.** La integración en `develop` y `main` debe realizarse mediante Pull Requests y con las verificaciones requeridas satisfactorias.
- **Conventional Commits.** Los prefijos `feat`, `fix`, `docs`, `refactor`, `test` y `chore` permiten identificar el propósito de cada cambio.
- **Construcciones reproducibles.** Maven Wrapper, `package-lock.json` y Gradle Wrapper ayudan a mantener versiones consistentes de herramientas y dependencias.
- **Gestión segura de secretos.** Las claves de JWT, Stripe, Cloudinary, SMTP, Firebase y otros servicios externos no deben almacenarse en el código fuente. Los repositorios pueden incluir archivos de ejemplo como `.env.example`, mientras que los valores reales se administran mediante variables de entorno y secretos de las plataformas correspondientes.

### 7.1.2. Build & Test Suite Pipeline Components

El pipeline de integración continua se organiza en etapas. Si una verificación obligatoria falla, la ejecución se considera fallida y el cambio debe corregirse antes de continuar con su integración.

**Backend Services (`smartfinance-drive-platform`)**

| Etapa | Acción | Comando o componente | Resultado esperado |
|---|---|---|---|
| 1. Checkout | Obtener el código de la rama o del Pull Request. | `actions/checkout` | Código disponible en el entorno de ejecución. |
| 2. Configuración | Preparar Java y la caché de Maven. | `actions/setup-java` con Java 26 y caché Maven | Entorno de construcción preparado. |
| 3. Compilación y pruebas | Compilar, ejecutar las pruebas configuradas y empaquetar el proyecto. | `./mvnw -B verify` | Construcción satisfactoria y reportes de pruebas generados. |
| 4. Análisis de dependencias | Revisar dependencias en busca de vulnerabilidades conocidas. | OWASP Dependency-Check integrado en Maven | Reporte de análisis disponible para revisión. |
| 5. Conservación de resultados | Conservar reportes y el artefacto generado cuando el flujo lo configure. | Artefactos de GitHub Actions | Resultados accesibles desde la ejecución del workflow. |

La ejecución de `./mvnw -B verify` constituye el punto central de validación del backend. Las pruebas se organizan en las siguientes suites, relacionadas con la estrategia de pruebas descrita en la sección 6.1.

| Suite | Sección relacionada | Alcance | Forma de ejecución |
|---|---|---|---|
| Pruebas unitarias | 6.1.1 | Entidades, objetos de valor y lógica de dominio de los contextos principales, como IAM, Catalog, Financing y Scoring. | Automatizada mediante Maven. |
| Pruebas de integración de controladores | 6.1.2 | Controladores HTTP, autenticación y autorización, incluidas respuestas como `401 Unauthorized` y `403 Forbidden` cuando corresponda. | Automatizada mediante Maven y las herramientas de prueba de Spring. |
| Pruebas BDD con Cucumber | 6.1.3 | Escenarios de comportamiento expresados en archivos `.feature`. | Automatizada cuando la suite BDD está integrada en la construcción Maven. |
| Pruebas de sistema | 6.1.4 | Casos ST-01 a ST-18 y flujos funcionales de la API. | Ejecución con Swagger UI o Postman contra la aplicación en ejecución. |

Las pruebas de sistema realizadas con Swagger UI o Postman complementan las pruebas automatizadas: no se consideran parte de la ejecución de Maven salvo que se integren expresamente como pruebas automatizadas.

**Web Application (`smartfinance-drive-webapp`)**

| Etapa | Acción | Comando o componente | Resultado esperado |
|---|---|---|---|
| 1. Checkout | Obtener el código. | `actions/checkout` | Código disponible. |
| 2. Configuración | Preparar Node.js y la caché de npm. | `actions/setup-node` | Entorno Node.js listo. |
| 3. Instalación | Instalar las dependencias declaradas en el archivo de bloqueo. | `npm ci` | Dependencias instaladas de forma reproducible. |
| 4. Compilación | Construir la aplicación Vue. | `npm run build` | Archivos de producción generados en `dist/`. |

La compilación verifica que la aplicación pueda construirse para producción. Las pruebas de componentes y las comprobaciones estáticas forman parte del pipeline cuando sus comandos están definidos en el repositorio.

**Landing Page (`smartfinance-drive-landingpage`)**

La landing page utiliza HTML5, CSS3 y JavaScript, por lo que no requiere un proceso de compilación como el de la aplicación Vue. La validación consiste en revisar los cambios del sitio y comprobar la correcta carga de sus archivos y recursos. La publicación de los archivos estáticos se realiza mediante Vercel.

**Native Mobile Application (`smartfinance-drive-mobile-app`)**

| Etapa | Acción | Comando o componente | Resultado esperado |
|---|---|---|---|
| 1. Configuración | Preparar Java y Android SDK. | `actions/setup-java` y entorno Android | Entorno listo para compilar. |
| 2. Compilación | Generar la aplicación Android. | `./gradlew assembleDebug` | APK de depuración generado. |
| 3. Pruebas unitarias | Ejecutar las pruebas JVM configuradas en el proyecto. | `./gradlew testDebugUnitTest` | Resultado de las pruebas unitarias disponible. |

El APK de depuración permite comprobar la instalación y el funcionamiento de la aplicación durante el desarrollo. La distribución interna del archivo se describe en la sección 7.3.2.

---

## 7.2. Continuous Delivery

La entrega continua (*Continuous Delivery*, CD) mantiene el software en un estado que permita preparar una publicación después de superar las verificaciones correspondientes. En SmartFinance Drive, la entrega se apoya en la integración continua, la revisión de Pull Requests, las vistas previas de Vercel y la validación funcional de las versiones candidatas.

### 7.2.1. Tools and Practices

**Herramientas**

- **GitHub Actions:** ejecuta las verificaciones automatizadas y conserva los resultados de las construcciones.
- **GitHub Pull Requests:** permite revisar los cambios antes de integrarlos en las ramas compartidas.
- **Vercel Preview Deployments:** ofrece vistas previas de los cambios de la aplicación web y de la landing page asociados a Pull Requests, cuando la integración con Vercel está habilitada.
- **Docker y `render.yaml`:** describen la construcción y la configuración del servicio backend en Render.
- **Flyway:** registra las migraciones del esquema de PostgreSQL para mantener la evolución de la base de datos bajo control de versiones.
- **Aiven:** proporciona PostgreSQL como servicio administrado para el backend.
- **Jira:** permite organizar las tareas del Sprint y registrar su estado.

**Prácticas de entrega**

- **Integración controlada.** Los cambios pasan por un Pull Request y las verificaciones de CI antes de incorporarse a `develop`.
- **Estabilización de versiones.** Las ramas `release/x.y.z` se utilizan para preparar una versión y concentrar las correcciones necesarias antes de su publicación.
- **Validación previa.** Las vistas previas de Vercel permiten revisar cambios de interfaz antes de integrarlos en la versión principal.
- **Aprobación antes de producción.** La integración de una versión de lanzamiento en `main` debe contar con revisión y aprobación de un integrante distinto del autor, de acuerdo con el flujo de trabajo del equipo.
- **Validación funcional.** Los casos de sistema ST-01 a ST-18 se ejecutan con Swagger UI o Postman para comprobar los flujos definidos en la sección 6.1.4.
- **Migraciones controladas.** Flyway administra los cambios del esquema de PostgreSQL; Hibernate utiliza `DDL_AUTO=validate` para comprobar la correspondencia del esquema sin modificarlo automáticamente.
- **Recuperación de versiones.** Si una publicación presenta problemas, se puede restaurar una versión anterior desde Render o Vercel, o revertir el cambio mediante `git revert`, según el origen del problema.

### 7.2.2. Stages Deployment Pipeline Components

El flujo de entrega de SmartFinance Drive sigue estas etapas:

| Etapa | Disparador | Actividad | Criterio de salida |
|---|---|---|---|
| 1. Integración inicial | `push` o apertura de Pull Request | Ejecutar las verificaciones de CI correspondientes al repositorio. | Compilación y verificaciones obligatorias satisfactorias. |
| 2. Revisión previa | Pull Request abierto | Revisar el código y, en los proyectos web, comprobar la vista previa de Vercel cuando esté disponible. | Cambios revisados y observaciones resueltas. |
| 3. Integración | Aprobación del Pull Request | Incorporar el cambio a `develop`. | Revisión aprobada y CI satisfactorio. |
| 4. Preparación de versión | Creación de `release/x.y.z` | Estabilizar la versión y revisar los resultados de construcción y análisis de dependencias. | Versión candidata preparada para validación. |
| 5. Validación funcional | Versión candidata disponible | Ejecutar los casos de sistema ST-01 a ST-18 con Swagger UI o Postman. | Resultados conformes con los criterios de aceptación. |
| 6. Aprobación de publicación | Pull Request de `release/x.y.z` hacia `main` | Revisar y aprobar la integración de la versión. | Versión autorizada para publicarse. |

La aprobación del Pull Request constituye el control humano previo a la publicación. El despliegue posterior se realiza según la configuración de cada plataforma y repositorio.

---

## 7.3. Continuous Deployment

El despliegue continuo (*Continuous Deployment*) automatiza la publicación de los cambios que superan las condiciones establecidas para la rama de producción. En SmartFinance Drive, Render gestiona el despliegue del backend, Vercel publica los proyectos web y la aplicación móvil se distribuye como un APK de Android.

### 7.3.1. Tools and Practices

**Herramientas**

| Herramienta o servicio | Componente | Función |
|---|---|---|
| Render | Backend Services | Construye y ejecuta el servicio backend a partir de la configuración del repositorio y su `Dockerfile`. |
| Aiven PostgreSQL | Base de datos | Aloja la base de datos PostgreSQL administrada, a la que el backend se conecta mediante variables de entorno. |
| Vercel | Web Application y Landing Page | Construye y publica los proyectos web, y distribuye sus archivos mediante su infraestructura de entrega de contenido. |
| Docker | Backend Services | Proporciona una imagen de ejecución reproducible para el servidor de la API. |
| Flyway | Base de datos | Aplica las migraciones versionadas del esquema durante el arranque de la aplicación, de acuerdo con la configuración del backend. |
| Variables de entorno y secretos | Todos los componentes | Separan la configuración y las credenciales del código fuente. |
| Gradle | Native Mobile Application | Compila la aplicación Android y genera el APK para distribución interna. |

**Prácticas de despliegue**

- **Publicación desde la rama principal.** Los cambios aprobados que llegan a `main` pueden activar el despliegue automático configurado en Render y Vercel.
- **Construcción del backend mediante Docker.** Render utiliza el `Dockerfile` para construir la imagen y ejecutar la API.
- **Base de datos administrada.** El backend se conecta a Aiven PostgreSQL mediante la configuración de conexión proporcionada por variables de entorno. Las credenciales no se guardan en el repositorio.
- **Infraestructura declarativa.** La configuración del servicio backend se mantiene en `render.yaml`, mientras que la configuración de conexión a Aiven se administra como configuración del entorno.
- **Migraciones bajo control de versiones.** Flyway aplica las migraciones del esquema; `DDL_AUTO=validate` permite que Hibernate valide la estructura existente sin realizar cambios automáticos.
- **Protección de secretos.** Las claves de JWT y las credenciales de servicios externos se administran fuera del código fuente.
- **Recuperación ante fallos.** Los despliegues anteriores disponibles en Render y Vercel permiten restaurar una versión estable. Los cambios de código también pueden revertirse mediante `git revert`.
- **Versionado semántico.** Las versiones de publicación se identifican con etiquetas Git del formato `vMAJOR.MINOR.PATCH`, por ejemplo, `v1.2.0`.

### 7.3.2. Production Deployment Pipeline Components

**Backend Services: Render**

El flujo de despliegue del backend está compuesto por las siguientes etapas:

1. **Detección del cambio.** Una integración aprobada llega a la rama `main` del repositorio `smartfinance-drive-platform`.
2. **Construcción de la imagen.** Render obtiene el código y ejecuta el `Dockerfile`, que empaqueta la aplicación en una imagen de contenedor.
3. **Preparación de la ejecución.** El contenedor inicia con las variables de entorno configuradas para el servicio, incluida la conexión a PostgreSQL en Aiven y los parámetros de seguridad de la API.
4. **Migración del esquema.** Flyway aplica las migraciones pendientes definidas por el proyecto. Hibernate valida el esquema con `DDL_AUTO=validate`.
5. **Inicio del servicio.** Render ejecuta la aplicación Spring Boot y expone la API en la dirección de producción.
6. **Comprobación funcional.** La disponibilidad del servicio puede comprobarse mediante la documentación Swagger UI y solicitudes a los endpoints de la API.

La API de producción se encuentra en:

- **Backend API:** [https://smartfinance-drive-platform.onrender.com](https://smartfinance-drive-platform.onrender.com)
- **Swagger UI:** [https://smartfinance-drive-platform.onrender.com/swagger-ui/index.html](https://smartfinance-drive-platform.onrender.com/swagger-ui/index.html)

**Base de datos: Aiven PostgreSQL**

Aiven proporciona el servicio PostgreSQL utilizado por el backend de SmartFinance Drive. Render ejecuta la API y se conecta a la base de datos mediante los parámetros de conexión configurados en las variables de entorno del servicio.

La separación entre la API y la base de datos permite administrar de forma independiente el entorno de ejecución de la aplicación y el servicio de persistencia. Las credenciales de conexión se mantienen fuera del repositorio y las modificaciones del esquema se controlan mediante migraciones Flyway.

**Web Application: Vercel**

El despliegue de la aplicación web se realiza mediante Vercel:

1. **Detección del cambio.** Vercel detecta los cambios integrados en la rama configurada para producción del repositorio `smartfinance-drive-webapp`.
2. **Instalación.** Se instalan las dependencias del proyecto con npm.
3. **Compilación.** Vite ejecuta `npm run build` y genera los archivos de producción en `dist/`.
4. **Publicación.** Vercel publica los archivos generados y los distribuye mediante su infraestructura.
5. **Enrutamiento de la aplicación.** La configuración de Vercel debe dirigir las rutas de la aplicación de una sola página hacia su punto de entrada para que Vue Router gestione la navegación interna.

La aplicación web está disponible en:

- **Web Application:** [https://smartfinance-drive-webapp.vercel.app/](https://smartfinance-drive-webapp.vercel.app/)

**Landing Page: Vercel**

La landing page es un sitio estático construido con HTML5, CSS3 y JavaScript. Su flujo de publicación comprende la detección de los cambios en el repositorio, la publicación de los archivos estáticos y su distribución a través de Vercel.

La landing page está disponible en:

- **Landing Page:** [https://smartfinance-drive-landingpage.vercel.app/](https://smartfinance-drive-landingpage.vercel.app/)

**Native Mobile Application: APK de Android**

La aplicación móvil se compila con Gradle y se empaqueta como un APK de Android. El archivo generado se utiliza para instalar la aplicación en los dispositivos del equipo y realizar validaciones internas. Este mecanismo permite distribuir una versión instalable sin depender de una publicación en una tienda de aplicaciones.

**Resumen de entornos de producción**

| Componente | Plataforma | Dirección o mecanismo de acceso |
|---|---|---|
| Backend API | Render | [https://smartfinance-drive-platform.onrender.com](https://smartfinance-drive-platform.onrender.com) |
| Documentación de la API | Render | [https://smartfinance-drive-platform.onrender.com/swagger-ui/index.html](https://smartfinance-drive-platform.onrender.com/swagger-ui/index.html) |
| Base de datos PostgreSQL | Aiven | Acceso desde el backend mediante variables de entorno y credenciales privadas. |
| Web Application | Vercel | [https://smartfinance-drive-webapp.vercel.app/](https://smartfinance-drive-webapp.vercel.app/) |
| Landing Page | Vercel | [https://smartfinance-drive-landingpage.vercel.app/](https://smartfinance-drive-landingpage.vercel.app/) |
| Native Mobile Application | Distribución interna | APK generado mediante Gradle para instalación en dispositivos Android. |

En conjunto, las prácticas de integración continua, entrega continua y despliegue continuo permiten mantener un flujo controlado desde el cambio de código hasta la publicación. GitHub y GitHub Actions apoyan la integración y la verificación; los Pull Requests establecen el control de revisión; Render y Aiven proporcionan el entorno de la API y su base de datos; Vercel publica las interfaces web; y Gradle genera el paquete instalable de Android.

```{=typst}
#pagebreak()
```
