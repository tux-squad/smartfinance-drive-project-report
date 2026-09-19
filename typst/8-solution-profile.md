## 1.2. Solution Profile

**SmartFinance Drive** es una solución digital desarrollada por **tux-squad**, orientada a facilitar el proceso de búsqueda y adquisición de vehículos nuevos y usados. La plataforma conecta a compradores con concesionarias mediante un marketplace digital, incorporando recomendaciones inteligentes, búsqueda de vehículos y acceso a alternativas de evaluación crediticia mediante entidades financieras externas.

La solución busca reducir el tiempo y esfuerzo que los compradores invierten en identificar un vehículo adecuado, considerando factores como sus necesidades, estilo de vida y presupuesto. Asimismo, proporciona a las concesionarias un canal digital para promocionar su inventario y conectar con potenciales compradores.

### 1.2.1. Antecedentes y Problemática

#### 1.2.1.1. What – ¿Qué problema existe?
Existe una dificultad para conectar eficientemente las necesidades de los compradores con la oferta disponible de las concesionarias. Los compradores deben invertir tiempo en buscar y comparar alternativas, mientras que las concesionarias necesitan mecanismos que faciliten el contacto con potenciales clientes.

#### 1.2.1.2. When – ¿Cuándo ocurre?
El problema aparece durante las etapas de búsqueda y evaluación de alternativas, especialmente cuando el usuario no tiene claro qué vehículo elegir o necesita comparar diferentes opciones antes de tomar una decisión de compra.

En el caso de las concesionarias, el problema se presenta durante la comercialización de los vehículos disponibles y cuando necesitan incrementar la exposición de su inventario ante potenciales compradores.

#### 1.2.1.3. Where – ¿Dónde ocurre?
El problema se presenta principalmente durante el proceso de búsqueda, comparación y adquisición de vehículos, especialmente cuando el comprador debe consultar diferentes concesionarias y fuentes de información para encontrar una alternativa adecuada.

#### 1.2.1.4. Who – ¿Quiénes?
Los principales involucrados son:

- Compradores interesados en adquirir vehículos nuevos o usados.
- Concesionarias de autos nuevos que buscan comercializar sus vehículos disponibles.
- Concesionarias de autos usados que buscan comercializar y rotar su inventario.

#### 1.2.1.5. Why – ¿Por qué ocurre?
Ocurre debido a la cantidad de alternativas disponibles en el mercado, la dispersión de la información entre diferentes concesionarias y la dificultad de relacionar las características de cada vehículo con las necesidades y presupuesto específicos de cada comprador.

#### 1.2.1.6. How – ¿Cómo se manifiesta?
Se manifiesta mediante procesos de búsqueda prolongados, comparación manual de alternativas, incertidumbre en la selección del vehículo y dificultades para avanzar desde la identificación de una alternativa hasta el proceso de financiamiento y compra.

Para las concesionarias, se manifiesta en la necesidad de encontrar canales adicionales que permitan incrementar la exposición de sus vehículos y generar oportunidades de venta.

#### 1.2.1.7. How Much – ¿Cuánto impacto genera?
El problema genera costos de tiempo y esfuerzo para los compradores y puede afectar la velocidad con la que las concesionarias logran convertir su inventario disponible en ventas. Además, los vehículos representan activos cuyo valor puede disminuir con el tiempo, especialmente en el caso de los vehículos usados y de las unidades nuevas que permanecen durante periodos prolongados en inventario.

### 1.2.2. Lean UX Process

#### 1.2.2.1. Lean UX Problem Statements
El proceso actual de búsqueda y comercialización de vehículos es ineficiente y fragmentado. Los compradores deben navegar entre múltiples plataformas desconectadas para encontrar un auto que se ajuste a sus necesidades, estilo de vida y presupuesto, mientras que los concesionarios (tanto de autos nuevos como usados) enfrentan dificultades para centralizar su inventario y captar oportunidades de contacto con prospectos cualificados.

Hemos observado que las soluciones actuales no integran eficazmente la oferta de vehículos nuevos y usados en un solo lugar ni facilitan la recomendación personalizada, lo que genera alta fricción en la toma de decisiones del comprador y una baja tasa de conversión de leads para los concesionarios.

**¿Cómo podríamos** centralizar la oferta disponible de concesionarios de autos nuevos y usados y personalizar el proceso de recomendación para los compradores, de modo que reduzcamos la fricción en el descubrimiento del vehículo ideal y mejoremos la conexión con oportunidades comerciales cualificadas?

Sabremos que la solución es exitosa cuando observemos:

- **Reducción del 35%** en el tiempo promedio requerido por los compradores para identificar alternativas de vehículos que se ajusten a su presupuesto y perfil.
- **Incremento del 25%** en la tasa de conversión de prospectos cualificados generados para los concesionarios.
- **Puntuación de satisfacción del cliente (NPS)** superior a 50 puntos en la experiencia global de búsqueda.

#### 1.2.2.2. Lean UX Assumptions

**Business Assumptions**

- Creemos que los compradores de vehículos enfrentan fricción al buscar opciones que se ajusten a su presupuesto debido a la fragmentación de la oferta digital.
- Creemos que los concesionarios de autos nuevos necesitan un canal digital para captar prospectos cualificados sin depender únicamente del tráfico físico en salón.
- Creemos que los concesionarios de autos usados sufren por altos costos de publicación y baja confianza del comprador en la condición del vehículo.
- Creemos que ambos tipos de concesionarios pagarán una membresía recurrente si la plataforma genera contactos comerciales de alta conversión.
- Creemos que un modelo de negocio B2B por suscripción (*SaaS/Marketplace*) respaldará la viabilidad financiera de la plataforma.

**Business Outcome Assumptions**

- **O01 (Autos Nuevos):** Lograr una tasa de conversión del **15%** en la transición de prospectos cualificados hacia el agendamiento de pruebas de manejo (*test drive*) para concesionarios de vehículos nuevos.
- **O02 (Autos Usados):** Reducir en un **30%** el tiempo promedio de rotación del inventario publicado por concesionarios de vehículos usados.
- **O03 (Monetización B2B):** Mantener una tasa de retención mensual de membresías (*Churn Rate* < **5%**) combinada entre concesionarios de autos nuevos y usados.

**User Assumptions**

- **Compradores Interesados:**
    - Necesitan comparar vehículos nuevos y usados dentro de una misma plataforma según su presupuesto.
    - Aquellos sin conocimiento técnico valoran la orientación guiada sobre qué auto se adapta a su estilo de vida.
    - Los compradores decididos priorizan la velocidad de filtrado y contacto directo con el concesionario.
- **Concesionarios de Autos Nuevos:**
    - Necesitan posicionar modelos específicos del año e incentivar promociones de marca/financiamiento de fábrica.
    - Valoran recibir prospectos (*leads*) altamente cualificados y con intención de compra inmediata para sus equipos de ventas.
- **Concesionarios de Autos Usados:**
    - Necesitan acelerar la rotación de inventario heterogéneo (variedad de marcas, años y kilometrajes).
    - Necesitan transmitir transparencia sobre la condición y precio del vehículo para ganar la confianza del comprador.

**User Outcome Assumptions**

- **Compradores Interesados:** Reducción del **40%** en el tiempo invertido en la fase de filtrado y comparación de vehículos.
- **Concesionarios de Autos Nuevos:** Incremento del **20%** en la tasa de cierre de ventas a partir de los contactos recibidos por la plataforma.
- **Concesionarios de Autos Usados:** Aumento del **35%** en la visibilidad e interacción (*leads* por vehículo) de su inventario publicado.

**Feature Assumptions**

- **FA01 - Marketplace Integrado con Filtro por Tipo de Vehículo:** Creemos que unificar la oferta de autos nuevos y usados en un catálogo estructurado para compradores activos permitirá simplificar la comparación. Sabremos que es correcto cuando la tasa de clics de detalle (*CTR*) desde las búsquedas sea superior al **25%**.
- **FA02 - Asistente de Recomendación IA:** Creemos que un asistente interactivo para compradores indecisos logrará sugerir tanto autos nuevos como usados según presupuesto y estilo de vida. Sabremos que es correcto cuando el **50%** de los usuarios que inician el asistente guarden al menos una opción recomendada.
- **FA03 - Perfil de Inventario Específico para Usados vs. Nuevos:** Creemos que adaptar la ficha del vehículo (detallando kilometraje y condición para usados; versiones y promociones para nuevos) para los compradores logrará aumentar la confianza. Sabremos que es correcto cuando la conversión a solicitud de contacto aumente un **18%**.
- **FA04 - Embudo Dual de Navegación (Retail vs. Directo):** Creemos que ofrecer una ruta guiada (Retail) y una ruta rápida (Directa) para los dos perfiles de compradores logrará maximizar la retención. Sabremos que es correcto si la tasa de abandono durante la búsqueda se mantiene por debajo del **15%**.
- **FA05 - Pre-evaluación Crediticia Externa:** Creemos que integrar la pre-aprobación financiera con entidades externas para compradores interesados acortará el ciclo de decisión. Sabremos que es correcto cuando el **30%** de las solicitudes enviadas a los concesionarios incluyan perfil financiero validado.
- **FA06 - Panel de Gestión y Membresías B2B:** Creemos que un portal de administración de inventario con analítica diferenciada para concesionarios de nuevos y usados justificará el cobro del plan. Sabremos que es correcto si el **80%** de los concesionarios renueva su suscripción tras el periodo de prueba.

#### 1.2.2.3. Lean UX Hypothesis Statements

A continuación se presentan las hipótesis priorizadas del proyecto SmartFinance Drive:

##### Hypothesis Statement 1: Recomendador Asistido para Compradores Exploradores
**Declaración:**
Creemos que incrementaremos la retención y reduciremos la tasa de abandono en la fase de descubrimiento inicial si los compradores indecisos/exploradores obtienen recomendaciones personalizadas de vehículos nuevos y usados a través de un asistente interactivo guiado según su presupuesto mensual y estilo de vida.

**Criterio de Validación:**
Sabremos que tuvimos éxito cuando observemos que:

- Al menos el 50% de los usuarios que inician el asistente interactivo completan el flujo y guardan o solicitan cotización de al menos una de las alternativas sugeridas.
- El tiempo promedio invertido en encontrar opciones viables se reduzca en un 35% en comparación con la búsqueda tradicional por filtros genéricos.

##### Hypothesis Statement 2: Canal Virtual Directo y Pre-evaluación Crediticia Externa
**Declaración:**
Creemos que incrementaremos la tasa de conversión a leads comerciales cualificados para las concesionarias si los compradores decididos pueden filtrar directamente el catálogo unificado y solicitar una pre-evaluación de viabilidad crediticia a entidades financieras externas de manera transparente y sin intermediación bancaria directa de la plataforma.

**Criterio de Validación:**
Sabremos que tuvimos éxito cuando observemos que:

- El 30% de las solicitudes de contacto enviadas a las concesionarias incluyan un perfil financiero pre-evaluado y validado por la entidad externa.
- La tasa de conversión de prospecto a agendamiento de visita o prueba de manejo (*test drive*) alcance al menos un 15%.

##### Hypothesis Statement 3: Membresía B2B y Aceleración de Rotación de Inventario (Autos Usados)
**Declaración:**
Creemos que lograremos la sostenibilidad financiera del marketplace mediante el cobro de suscripciones recurrentes si los concesionarios de autos usados obtienen un panel de gestión que incrementa la visibilidad de sus unidades y conecta prospectos de alta intención para mitigar la devaluación acelerada de su inventario estancado.

**Criterio de Validación:**
Sabremos que tuvimos éxito cuando observemos que:

- El tiempo promedio de permanencia/rotación del inventario publicado en la plataforma se reduzca en un 30% en un plazo de 60 días.
- Al menos el 80% de los concesionarios afiliados renueven su membresía mensual tras el periodo de prueba piloto (manteniendo un *Churn Rate B2B* mensual inferior al 5%).

##### Hypothesis Statement 4: Conversión de Prospectos Cualificados para Concesionarias de Nuevos
**Declaración:**
Creemos que incrementaremos la atracción y afiliación continua de distribuidores autorizados de vehículos nuevos si los concesionarios de autos nuevos reciben contactos con intención de compra verificada y capacidad crediticia pre-evaluada, disminuyendo su costo de prospección física en salón de ventas.

**Criterio de Validación:**
Sabremos que tuvimos éxito cuando observemos que:

- La tasa de cierre de ventas por prospecto recibido a través de SmartFinance Drive aumente en un 20% frente a otros canales digitales de captación.
- Los concesionarios publiquen y mantengan activo más del 70% de su stock disponible en la plataforma.

#### 1.2.2.4. Lean UX Canvas

![LeanUxCanvas](assets/Chapter-1/LeanUXCanvas-Smartfinance-drive.png)

* **Enlace interactivo del Lean UX Canvas:** [https://canva.link/g1n16bn2clawb90](https://canva.link/g1n16bn2clawb90)
