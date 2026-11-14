# Conclusiones y Recomendaciones

## Conclusiones

Al cierre del presente informe, el equipo **tux-squad** ha implementado SmartFinance Drive como un marketplace B2B2C de vehículos nuevos y usados con financiamiento, cuyo alcance está definido por las historias de usuario US-01 a US-22 (incluyendo las historias de captación y presentación de la Landing Page US-01 a US-04). La aplicación web (Web) concentra la funcionalidad para los cuatro roles de la plataforma (cliente, concesionario, entidad financiera y administrador), mientras que la aplicación móvil Android (Mobile) permite a los usuarios acceder al catálogo, consultar detalles de vehículos, realizar simulaciones y gestionar su perfil. A partir del trabajo realizado en los Sprints 1 y 2 y de las pruebas documentadas, se presentan las siguientes conclusiones.

* **Presentación del producto (Landing):** La Landing Page (US-01 a US-04), desplegada de forma estática en Vercel, comunica la propuesta de valor a las dos audiencias de la plataforma, compradores y concesionarias, y presenta los planes de membresía B2B. Con ello se establece un primer punto de contacto con el visitante y un acceso directo al registro.

* **Catálogo y exploración de vehículos (Web / Backend):** Se implementaron el catálogo con búsqueda y filtros (US-16, US-17), el detalle del vehículo (US-18) y la publicación, edición, eliminación y listado de vehículos por parte de la concesionaria (US-11, US-12, US-13, US-14, US-15). El backend en Spring Boot con PostgreSQL y migraciones Flyway sostiene esta funcionalidad, lo que confirma la viabilidad de exponer el inventario de las concesionarias en un catálogo unificado.

* **Financiamiento y simulación de crédito (Web / Backend):** La plataforma integra la simulación de crédito vehicular mediante el método francés (US-19, SP-01), con cuota, TCEA, TIR, VAN, cálculo de ratios crediticios y cronograma de pagos, permitiendo consultar (US-20) y gestionar las simulaciones guardadas (US-21). Estas capacidades permiten al cliente comparar alternativas de financiamiento antes de tomar una decisión de compra, sin que la plataforma apruebe créditos: la decisión final corresponde a la entidad financiera.

* **Evaluación por la entidad financiera (Web / Backend):** El flujo de evaluación oficial de las simulaciones por parte de la entidad financiera registrada (US-22), con resultado aprobado o rechazado y notas, y su verificación mediante RUC (SUNAT/CIIU), diferencian a SmartFinance Drive de un simple simulador y distribuyen con claridad las responsabilidades: la plataforma estima el riesgo y la entidad financiera decide.

* **Membresías y valor para la concesionaria (Web / Backend):** Los planes de membresía para concesionarias (US-03), junto con el control del inventario (US-11) y la interacción comercial para prospectos calificados, sustentan el modelo de negocio basado en la exposición del inventario y en información útil para la gestión comercial.

* **Aplicación móvil (Mobile):** La aplicación Android desarrollada en Kotlin con Jetpack Compose permite a los usuarios explorar vehículos, consultar detalles técnicos y de financiamiento, y gestionar su perfil desde dispositivos móviles, asegurando una experiencia ágil y responsiva.

* **Calidad y entrega continua (Backend / DevOps):** La estrategia de pruebas del Capítulo VI (pruebas unitarias, de integración, BDD y de sistema) y las prácticas de integración y despliegue del Capítulo VII, apoyadas en GitHub Actions, Render y Vercel, brindan trazabilidad entre las historias de usuario, el código y los entornos de ejecución.

* **Aspectos pendientes:** Aún deben completarse la ejecución y el registro de resultados de las pruebas de sistema (ST-01 a ST-18) y la validación de las historias de la aplicación móvil en su propio cliente. Asimismo, parte de los registros de los Sprint Reviews y Retrospectives del Sprint 2 se encuentra por completar.

**Conclusiones (Avance al Hito 3)**

* **Validación empírica mediante Experiment-Driven Development:** La estructuración y ejecución de las fases de planificación, diseño, experimentación, análisis y aprendizaje continuo permitieron contrastar las hipótesis de negocio de SmartFinance Drive con evidencia real en los entornos web y móvil, demostrando que la integración de filtros guiados por presupuesto y la pre-evaluación crediticia reducen significativamente la fricción en la toma de decisiones del comprador.

* **Madurez operativa con prácticas DevOps integrales:** La incorporación del monitoreo continuo (Continuous Monitoring, alertas y notificaciones) junto con los pipelines de CI/CD garantiza la disponibilidad, observabilidad y rápida detección de incidencias en producción, asegurando una experiencia confiable para compradores y concesionarias.

* **Evolución iterativa centrada en el usuario:** Las 9 entrevistas adicionales de validación realizadas en este ciclo, sumadas a las evaluaciones heurísticas y auditorías UX, permitieron identificar cuellos de botella en la navegación y convertir los hallazgos directamente en historias de usuario To-Be priorizadas para mejorar la usabilidad y conversión de la plataforma.

## Recomendaciones

Considerando el estado actual del producto, se establecen las siguientes recomendaciones realistas para los próximos ciclos del proyecto:

* **Completar la validación de extremo a extremo:** Ejecutar los casos de sistema ST-01 a ST-18 sobre una versión candidata, registrar los resultados obtenidos y ampliar progresivamente la cobertura hacia las historias de la aplicación web que aún no cuentan con casos automatizados, como el ordenamiento y búsqueda avanzada (US-17), la comparación de cotizaciones multi-banco (US-19) y la gestión de simulaciones (US-20).

* **Reforzar la evaluación de solicitudes:** Consolidar el flujo de evaluación de la entidad financiera (US-22) y la notificación por correo del resultado (SP-02, TS-03), verificando los tiempos de entrega y el manejo de errores del servicio de correo transaccional.

* **Validar con usuarios reales:** Realizar sesiones de prueba de usabilidad con clientes, concesionarias y entidades financieras sobre los flujos de simulación, publicación de vehículos y evaluación, a fin de contrastar las hipótesis del proceso Lean UX con el comportamiento observado.

* **Optimizar la experiencia móvil:** Continuar ampliando la cobertura de pruebas y optimizar el rendimiento de la aplicación Android en la navegación del catálogo y la visualización de fichas de vehículos.

* **Fortalecer la seguridad y la observabilidad:** Mantener la gestión de secretos fuera del código fuente, revisar periódicamente las reglas de autorización por rol y habilitar monitoreo de los servicios desplegados en Render para detectar fallos tempranamente.

* **Mantener la separación de entornos de despliegue:** La Landing Page debe permanecer desplegada de forma estática en Vercel, mientras que la aplicación web debe seguir optimizando el manejo de tokens (JWT) y del estado global (Pinia) para proteger las rutas privadas.
