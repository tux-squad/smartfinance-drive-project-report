```{=typst}
#align(center)[
  #v(0.5cm)
  #image("assets/Chapter-1/upc_logo.png", width: 130pt)
  #v(1em)
  #text(size: 15pt, weight: "bold", fill: rgb("#1e3a8a"))[Universidad Peruana de Ciencias Aplicadas]
  
  #text(size: 12pt, fill: rgb("#334155"))[Carrera de Ingeniería de Software]

  #v(1em)

  #text(size: 13pt, weight: "bold", fill: rgb("#b91c1c"))[1ASI0732 -- Diseño de Experimentos de Ingeniería de Software]

  #text(size: 11pt)[*Sección / NRC:* 9104]

  #v(1.5em)

  #rect(width: 100%, fill: rgb("#f8fafc"), stroke: 1pt + rgb("#1e3a8a"), radius: 6pt, inset: 14pt)[
    #text(size: 20pt, weight: "bold", fill: rgb("#1e3a8a"))[Informe del Trabajo Final]
  ]

  #v(1.2em)

  #grid(
    columns: (1fr, 1fr),
    gutter: 20pt,
    align: (left, left),
    [
      #text(weight: "bold", fill: rgb("#1e3a8a"))[Docente:] Noriega Melendez, Julio Manuel \
      #text(weight: "bold", fill: rgb("#1e3a8a"))[Startup:] tux-squad
    ],
    [
      #text(weight: "bold", fill: rgb("#1e3a8a"))[Producto:] SmartFinance Drive \
      #text(weight: "bold", fill: rgb("#1e3a8a"))[Sección/NRC:] 9104
    ]
  )

  #v(1.2em)

  #text(size: 12pt, weight: "bold", fill: rgb("#1e3a8a"))[Relación de Integrantes]
  #v(0.4em)
  #table(
    columns: (110pt, 1fr),
    align: (center, left),
    table.header([Código], [Apellidos y Nombres]),
    [U202113229], [Castillo Yataco, Mauricio Sebastian],
    [U20231B120], [Cotrina Siclla, Sofia Alessandra],
    [U202312912], [Jonseck Choque, Oliver],
    [U202419485], [Machacca Soto, Aldo Jeanfranco],
    [U202316687], [Paucar Zenteno, Jesús Fernando],
  )

  #v(1.5cm)

  #text(size: 11pt, weight: "bold", fill: rgb("#64748b"))[Período 202620 -- Setiembre 2026]
]
#pagebreak()
```
# Registro de versiones del informe

| Versión | Fecha | Autor | Descripción de modificación |
| --- | --- | --- | --- |
| 0.1.0 | 9/9/26 | \@iamandreek | docs: agregar estructura inicial de la documentación |

```{=typst}
#pagebreak()
```
# Project Report Collaboration Insights

Sección para registrar los insights de colaboración, métricas de trabajo en equipo e iteraciones de los informes del proyecto **SmartFinance Drive**.

```{=typst}
#pagebreak()
```
# Student Outcome

El desarrollo de este informe y proyecto contribuye al logro de los siguientes **Student Outcomes** de la carrera de Ingeniería de Software en la UPC:

| Criterio | Descripción | Aporte en el Proyecto |
| :--- | :--- | :--- |
| **ABET - Student Outcome 1** | Capacidad de identificar, formular y resolver problemas complejos de ingeniería aplicando principios de ingeniería, ciencia y matemáticas. | Aplicación de metodologías de diseño de experimentos y arquitectura de software para SmartFinance Drive. |

```{=typst}
#pagebreak()
```
```{=typst}
#outline(
  title: [Contenido],
  indent: 1.5em,
  depth: 4
)
#pagebreak()
```
# Capítulo I: Introducción

## 1.1. Startup Profile

### 1.1.1. Descripción de la Startup

**tux-squad** es una startup enfocada en el desarrollo de soluciones digitales avanzadas e innovadoras para la gestión financiera y análisis de datos en el sector automotriz y de movilidad urbana.

### 1.1.2. Perfiles de integrantes del equipo

```{=typst}
#v(0.5em)
#grid(
  columns: (1fr),
  gutter: 1.2em,

  rect(
    width: 100%,
    fill: rgb("#f8fafc"),
    stroke: 0.6pt + rgb("#cbd5e1"),
    radius: 6pt,
    inset: 12pt,
    [
      #text(size: 12pt, weight: "bold", fill: rgb("#1e3a8a"))[Castillo Yataco, Mauricio Sebastian]
      #h(1fr)
      #text(size: 9.5pt, fill: rgb("#b91c1c"), weight: "bold")[U202113229 (\@M4uricioCastillo)] \
      #text(size: 9pt, style: "italic", fill: rgb("#64748b"))[Backend Developer / Software Engineer]
    ]
  ),

  rect(
    width: 100%,
    fill: rgb("#f8fafc"),
    stroke: 0.6pt + rgb("#cbd5e1"),
    radius: 6pt,
    inset: 12pt,
    [
      #text(size: 12pt, weight: "bold", fill: rgb("#1e3a8a"))[Cotrina Siclla, Sofia Alessandra]
      #h(1fr)
      #text(size: 9.5pt, fill: rgb("#b91c1c"), weight: "bold")[U20231B120 (\@CotrinaAlessandra)] \
      #text(size: 9pt, style: "italic", fill: rgb("#64748b"))[UX/UI Designer / Frontend Specialist]
    ]
  ),

  rect(
    width: 100%,
    fill: rgb("#f8fafc"),
    stroke: 0.6pt + rgb("#cbd5e1"),
    radius: 6pt,
    inset: 12pt,
    [
      #text(size: 12pt, weight: "bold", fill: rgb("#1e3a8a"))[Jonseck Choque, Oliver]
      #h(1fr)
      #text(size: 9.5pt, fill: rgb("#b91c1c"), weight: "bold")[U202312912 (\@Olizzy-upc)] \
      #text(size: 9pt, style: "italic", fill: rgb("#64748b"))[DevOps Engineer / QA Analyst]
    ]
  ),

  rect(
    width: 100%,
    fill: rgb("#f8fafc"),
    stroke: 0.6pt + rgb("#cbd5e1"),
    radius: 6pt,
    inset: 12pt,
    [
      #text(size: 12pt, weight: "bold", fill: rgb("#1e3a8a"))[Machacca Soto, Aldo Jeanfranco]
      #h(1fr)
      #text(size: 9.5pt, fill: rgb("#b91c1c"), weight: "bold")[U202419485 (\@IamAndreek)] \
      #text(size: 9pt, style: "italic", fill: rgb("#64748b"))[Full Stack Developer / Software Architect]
    ]
  ),

  rect(
    width: 100%,
    fill: rgb("#f8fafc"),
    stroke: 0.6pt + rgb("#cbd5e1"),
    radius: 6pt,
    inset: 12pt,
    [
      #text(size: 12pt, weight: "bold", fill: rgb("#1e3a8a"))[Paucar Zenteno, Jesús Fernando]
      #h(1fr)
      #text(size: 9.5pt, fill: rgb("#b91c1c"), weight: "bold")[U202316687 (\@AbraamAcostae)] \
      #text(size: 9pt, style: "italic", fill: rgb("#64748b"))[Data Engineer / Data Analyst]
    ]
  )
)

#pagebreak()
```
## 1.2. Solution Profile

**SmartFinance Drive** es una plataforma integral diseñada para optimizar y automatizar la gestión financiera personal y corporativa relacionada con flotas vehiculares y transporte.

### 1.2.1. Antecedentes y problemática

#### 1.2.1.1. What
La falta de herramientas especializadas para el seguimiento de costos operativos, combustible, mantenimiento y retorno de inversión en vehículos.

#### 1.2.1.2. When
Ocurre diariamente durante la operación de vehículos individuales y flotas comerciales.

#### 1.2.1.3. Where
En el mercado local y regional de transporte y finanzas personales/empresariales.

#### 1.2.1.4. Who
Conductores independientes, empresas de logística y gestores de flotas vehiculares.

#### 1.2.1.5. Why
Debido a la dispersión de gastos en recibos físicos, falta de categorización inteligente y ausencia de proyecciones analíticas.

#### 1.2.1.6. How
A través de un sistema centralizado Web y Móvil impulsado por análisis de datos e inteligencia financiera.

#### 1.2.1.7. How much
Pérdidas estimadas del 15% al 25% del presupuesto operativo por falta de optimización y gastos invisibles.

### 1.2.2. Lean UX Process

#### 1.2.2.1. Lean UX Problem Statements
Se ha identificado que los usuarios carecen de visibilidad en tiempo real sobre sus costos de rendimiento por kilómetro.

#### 1.2.2.2. Lean UX Assumptions
* Los usuarios desean registrar gastos de combustible de manera rápida y automatizada.
* Las empresas prefieren reportes consolidados exportables en PDF/Excel.

#### 1.2.2.3. Lean UX Hypothesis Statements
Creemos que al ofrecer un panel de control intuitivo con categorización automática de gastos vehiculares, lograremos incrementar la retención de usuarios en un 30%.

#### 1.2.2.4. Lean UX Canvas
*(Lienzo de Lean UX disponible en los anexos y recursos de diseño).*
## 1.3. Segmentos objetivo

1. **Conductores Particulares y de Apps de Movilidad:** Personas que buscan controlar el gasto diario de combustible y mantenimiento preventivo de su vehículo personal o de trabajo.
2. **Pequeñas y Medianas Empresas (PyMEs) con Flotas Vehiculares:** Empresas que requieren supervisar múltiples unidades, asignar presupuestos y auditar gastos operativos.
# Capítulo II: Requirements Elicitation & Analysis

## 2.1. Competidores

### 2.1.1. Análisis competitivo

| Competidor | Fortalezas | Debilidades | Oportunidad para SmartFinance Drive |
| :--- | :--- | :--- | :--- |
| **Drivvo** | Seguimiento de gastos y recordatorios. | Interfaz anticuada y reportes limitados. | Interfaz moderna con analítica avanzada. |
| **Simply Auto** | Buen control de mantenimiento. | Curva de aprendizaje alta. | Proceso de onboarding guiado y simplificado. |

### 2.1.2. Estrategias y tácticas frente a competidores

* Enfoque en la experiencia de usuario (UX) intuitiva con dashboard interactivo.
* Automatización de reportes mediante algoritmos de predicción de gastos.
## 2.2. Entrevistas

### 2.2.1. Diseño de entrevistas
Preguntas estructuradas dirigidas a validar dolores principales en el registro de gastos vehiculares.

### 2.2.2. Registro de entrevistas
Detalle de las sesiones realizadas con representantes de los segmentos objetivo.

### 2.2.3. Análisis de entrevistas
Síntesis de los hallazgos clave obtenidos durante las entrevistas de exploración.
## 2.3. Needfinding

### 2.3.1. User Personas
Fichas descriptivas de los usuarios arquetipo del sistema.

### 2.3.2. User Task Matrix
Matriz de frecuencia y relevancia de tareas principales por tipo de usuario.

### 2.3.3. User Journey Mapping
Mapa de experiencia del usuario identificando puntos de dolor y oportunidades de mejora.

### 2.3.4. Empathy Mapping
Mapa de empatía (Qué piensa, qué ve, qué oye, qué dice y hace).

### 2.3.5. As-is Scenario Mapping
Mapeo de la situación actual sin la solución SmartFinance Drive.
## 2.4. Ubiquitous Language

Glosario de términos y conceptos del dominio de gestión financiera y automotriz utilizados en la plataforma:

* **Vehículo / Unidad:** Objeto principal de seguimiento de gastos.
* **Gasto Operativo:** Desembolso financiero ligado al funcionamiento directo (combustible, peajes).
* **Mantenimiento Preventivo:** Servicio programado para conservar la unidad en óptimas condiciones.
* **Score de Eficiencia:** Métrica calculada en función al costo por kilómetro recorrido.
# Capítulo III: Requirements Specification

## 3.1. To-Be Scenario Mapping
Mapeo del escenario futuro deseado con la solución integrada.

## 3.2. User Stories
Historias de usuario priorizadas con sus respectivos criterios de aceptación.

## 3.3. Product Backlog
Backlog general del producto clasificado por épicas y prioridades.

## 3.4. Impact Mapping
Mapa de impactos conectando metas de negocio con los actores y entregables.
# Capítulo IV: Product Design

## 4.1. Style Guidelines
Guías de estilo visual para la aplicación Web y Móvil (paleta de colores, tipografías, componentes).

## 4.2. Information Architecture
Sistemas de organización, etiquetado, navegación y SEO.

## 4.3. Landing Page UI Design
Wireframes y Mock-ups de la página de aterrizaje del producto.

## 4.4. Mobile Applications UX/UI Design
Diseño de la aplicación móvil (wireframes, wireflows y mock-ups).

## 4.5. Mobile Applications Prototyping
Prototipo interactivo de las aplicaciones Android e iOS.

## 4.6. Web Applications UX/UI Design
Diseño de interfaz de usuario de la plataforma web.

## 4.7. Web Applications Prototyping
Prototipo ejecutable de la plataforma web.

## 4.8. Domain-Driven Software Architecture
Diagramas de contexto, contenedores y componentes basados en C4 model y DDD.

## 4.9. Software Object-Oriented Design
Diagrama de clases y diccionario de entidades del dominio.

## 4.10. Database Design
Diseño lógico y físico del modelo de datos relacional y no relacional.
# Capítulo V: Product Implementation

## 5.1. Software Configuration Management
Configuración del entorno de desarrollo, gestión de código fuente (Gitflow) y guías de estilo.

## 5.2. Product Implementation & Deployment
Evidencias de la implementación del Landing Page, Web Frontend, API REST Backend y App Móvil.

## 5.3. Video About-the-Product
Enlace y presentación del video demostrativo del producto.
# Capítulo VI: Product Verification & Validation

## 6.1. Testing Suites & Validation
Pruebas unitarias, de integración, BDD y pruebas de sistema.

## 6.2. Static testing & Verification
Análisis estático de código, estándares de calidad y revisiones.

## 6.3. Validation Interviews
Entrevistas de validación con usuarios finales y evaluación por heurísticas.

## 6.4. Auditoría de Experiencias de Usuario
Informe de auditorías UX realizadas y recibidas entre equipos.
# Capítulo VII: DevOps Practices

## 7.1. Continuous Integration
Pipelines de automatización de compilación y ejecución de tests (GitHub Actions).

## 7.2. Continuous Delivery
Pipelines de despliegue continuo en entornos de staging.

## 7.3. Continuous Deployment
Despliegue automatizado a producción en entornos cloud.

## 7.4. Continuous Monitoring
Herramientas y componentes para monitoreo de métricas, alertas y notificaciones.
# Capítulo VIII: Experiment-Driven Development

## 8.1. Experiment Planning
Identificación de supuestos, lagunas de conocimiento, backlog de preguntas y fichas de experimentos.

## 8.2. Experiment Design
Formulación de hipótesis, métricas de negocio, condiciones y plan de analítica web/móvil.

## 8.3. Experimentation
Ejecución de experimentos, desarrollo de historias de usuario To-Be y validación.

## 8.4. Experiment Aftermath & Analysis
Interpretación de resultados y repriorización del backlog de preguntas.

## 8.5. Continuous Learning
Flujo de aprendizaje e insumos de las sesiones de retroalimentación.

## 8.6. To-Be Software Platform Pre-launch
Video de lanzamiento e integración del Gees Framework.
# Matriz de Evaluación Ética y de Impacto

Análisis del impacto ético, privacidad de datos financieros de los usuarios y responsabilidad social en la implementación de **SmartFinance Drive**.

| Dimensión | Consideraciones | Acciones Mitigantes |
| :--- | :--- | :--- |
| **Privacidad de datos** | Manejo de información financiera confidencial. | Encriptación de datos en tránsito y reposo. |
| **Transparencia** | Algoritmos de recomendación de ahorro. | Explicabilidad en los cálculos de proyecciones. |
# Conclusiones y Recomendaciones

## Conclusiones
* La solución **SmartFinance Drive** responde a las necesidades identificadas en los segmentos objetivo mediante una plataforma modular e intuitiva.
* Las prácticas de Experiment-Driven Development permitieron validar de manera ágil los supuestos clave antes del desarrollo a escala.

## Recomendaciones
* Continuar con la expansión de integraciones bancarias automáticas.
* Mantener la batería de pruebas y monitoreo continuo en el pipeline CI/CD.

## Videos del Proyecto
* **Video App Validation:** [Enlace a video]
* **Video About-the-Team:** [Enlace a video]
# Bibliografía

1. Gothelf, J., & Seiden, J. (2021). *Lean UX: Designing Great Products with Agile Teams*. O'Reilly Media.
2. Evans, E. (2004). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley.
3. Humble, J., & Farley, D. (2010). *Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation*. Addison-Wesley.

---

# Anexos

* **Anexo A:** Evidencias de artefactos UX/UI.
* **Anexo B:** Guías de configuración de entorno.
