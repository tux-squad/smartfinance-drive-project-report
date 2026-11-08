# Conclusiones y Recomendaciones

## Conclusiones

Al cierre del presente informe, el equipo **tux-squad** ha implementado SmartFinance Drive como un marketplace B2B2C de vehículos nuevos y usados con financiamiento, cuyo alcance está definido por las historias de usuario US01 a US49 y por las historias de la Landing Page (LP-01 a LP-04). La aplicación web (Web) concentra la funcionalidad para los cuatro roles de la plataforma (cliente, concesionario, entidad financiera y administrador), mientras que la aplicación móvil Android (Mobile) se limita al inicio y cierre de sesión y a la mensajería (US40 a US49). A partir del trabajo realizado en los Sprints 1 y 2 y de las pruebas documentadas, se presentan las siguientes conclusiones.

* **Presentación del producto (Landing):** La Landing Page (LP-01 a LP-04), desplegada de forma estática en Vercel, comunica la propuesta de valor a las dos audiencias de la plataforma, compradores y concesionarias, y presenta los planes de membresía B2B. Con ello se establece un primer punto de contacto con el visitante y un acceso directo al registro.

* **Catálogo y exploración de vehículos (Web / Backend):** Se implementaron el catálogo con búsqueda y filtros (US08), el detalle del vehículo (US09) y la publicación, edición, eliminación y listado de vehículos por parte de la concesionaria (US10, US11, US12, US36). El backend en Spring Boot con PostgreSQL y migraciones Flyway sostiene esta funcionalidad, lo que confirma la viabilidad de exponer el inventario de las concesionarias en un catálogo unificado.

* **Financiamiento y simulación de crédito (Web / Backend):** La plataforma integra la pre-evaluación de riesgo crediticio (US15), basada en el score, el indicador DTI y el nivel de riesgo A/B/C, y la simulación de crédito mediante el método francés (US17), con cuota, TCEA, TIR, VAN y cronograma de pagos. Estas capacidades permiten al cliente comparar alternativas de financiamiento antes de tomar una decisión de compra, sin que la plataforma apruebe créditos: la decisión final corresponde a la entidad financiera.

* **Evaluación por la entidad financiera (Web / Backend):** El flujo de evaluación oficial de las simulaciones por parte de la entidad financiera registrada (US22), con resultado aprobado o rechazado y notas, y su verificación mediante RUC (SUNAT/CIIU), diferencian a SmartFinance Drive de un simple simulador y distribuyen con claridad las responsabilidades: la plataforma estima el riesgo y la entidad financiera decide.

* **Membresías y valor para la concesionaria (Web / Backend):** La membresía obligatoria para concesionarias mediante Stripe (US28), junto con las estadísticas de vistas y simulaciones por vehículo (US29) y los datos de contacto de los clientes que simularon sobre sus vehículos (US39), sustentan el modelo de negocio basado en la exposición del inventario y en información útil para la gestión comercial.

* **Mensajería móvil (Mobile):** La aplicación Android desarrollada en Kotlin con Jetpack Compose acota su alcance a la autenticación y a la mensajería entre clientes, concesionarias y entidades financieras (US40 a US49). Este recorte permite que cada canal cumpla un propósito definido: la web para la operación completa del marketplace y el móvil para la comunicación directa.

* **Calidad y entrega continua (Backend / DevOps):** La estrategia de pruebas del Capítulo VI (pruebas unitarias, de integración, BDD y de sistema) y las prácticas de integración y despliegue del Capítulo VII, apoyadas en GitHub Actions, Render y Vercel, brindan trazabilidad entre las historias de usuario, el código y los entornos de ejecución.

* **Aspectos pendientes:** Aún deben completarse la ejecución y el registro de resultados de las pruebas de sistema (ST-01 a ST-18) y la validación de las historias de la aplicación móvil en su propio cliente. Asimismo, parte de los registros de los Sprint Reviews y Retrospectives del Sprint 2 se encuentra por completar.

## Recomendaciones

Considerando el estado actual del producto, se establecen las siguientes recomendaciones realistas para los próximos ciclos del proyecto:

* **Completar la validación de extremo a extremo:** Ejecutar los casos de sistema ST-01 a ST-18 sobre una versión candidata, registrar los resultados obtenidos y ampliar progresivamente la cobertura hacia las historias de la aplicación web que aún no cuentan con casos automatizados, como el comparador de vehículos (US24), la comparación de cotizaciones multi-banco (US19) y la proyección de depreciación (US16).

* **Reforzar la evaluación de solicitudes:** Consolidar el flujo de la bandeja de la entidad financiera (US34, US35) y la notificación por correo del resultado (US23), verificando los tiempos de entrega y el manejo de errores del servicio de correo transaccional.

* **Validar con usuarios reales:** Realizar sesiones de prueba de usabilidad con clientes, concesionarias y entidades financieras sobre los flujos de simulación, publicación de vehículos y evaluación, a fin de contrastar las hipótesis del proceso Lean UX con el comportamiento observado.

* **Consolidar la mensajería móvil:** Completar y probar los flujos de chat con la concesionaria y con la entidad financiera, la respuesta de cada parte y el indicador de mensajes no leídos (US42 a US49), manteniendo la aplicación móvil enfocada en este alcance.

* **Fortalecer la seguridad y la observabilidad:** Mantener la gestión de secretos fuera del código fuente, revisar periódicamente las reglas de autorización por rol y habilitar monitoreo de los servicios desplegados en Render para detectar fallos tempranamente.

* **Mantener la separación de entornos de despliegue:** La Landing Page debe permanecer desplegada de forma estática en Vercel, mientras que la aplicación web debe seguir optimizando el manejo de tokens (JWT) y del estado global (Pinia) para proteger las rutas privadas.
