# Part III: Experiment-Driven Lifecycle

# Capítulo VIII: Experiment-Driven Development

## 8.1. Experiment Planning

En esta sección se define **qué se investigará, por qué importa y qué experimentos se ejecutarán** sobre SmartFinance Drive. El punto de partida es el estado actual del producto (web y móvil) y el conocimiento acumulado en los capítulos I a VII: las 9 entrevistas (2.2), los User Personas (2.3), las hipótesis de Lean UX (1.2.2) y las User Stories vigentes (3.2).

### 8.1.1. As-Is Summary

SmartFinance Drive es un marketplace B2B2C de vehículos nuevos y usados con financiamiento, que conecta a clientes, concesionarias y entidades financieras. La aplicación web ya cubre el flujo principal para los cuatro roles de la plataforma: registro y solicitud de rol validando el RUC, catálogo con búsqueda, filtros y comparador de vehículos, comparador de entidades financieras, pre-evaluación de riesgo crediticio (score, DTI y Risk Tier), simulación de crédito con método francés (cuota, TCEA, TIR y VAN), comparación de cotizaciones multi-banco, proyección de depreciación, evaluación oficial de las simulaciones por la entidad financiera, membresías B2B y panel de estadísticas para la concesionaria. La aplicación móvil Android cubre el inicio y cierre de sesión, la exploración del catálogo vehicular con fichas técnicas, la simulación de créditos y el perfil del comprador.

No obstante, la plataforma aún no ha medido el comportamiento real de sus usuarios ni ha validado con ellos las funciones que la diferencian de NeoAuto y Autocosmos, por lo que la decisión de qué mejorar o ampliar descansa en suposiciones.

**Problemas identificados:**

* **Sin línea base de uso del cliente (Web):** Solo existen estadísticas para la concesionaria (vistas y simulaciones por vehículo); no se mide el recorrido del cliente entre búsqueda, detalle, pre-evaluación, simulación y envío a evaluación, ni dónde abandona.
* **Pre-evaluación que exige datos sensibles (Web):** El cliente debe ingresar ingresos y deudas antes de simular su crédito, y se desconoce cuántos clientes lo completan o abandonan por desconfianza.
* **Comparación de entidades sin validar (Web):** El cuadro comparativo multi-banco existe, pero no se sabe si cambia la decisión del cliente ni si aumenta los envíos a evaluación.
* **Valor de la membresía sin validar (Web):** Las concesionarias deben seleccionar un plan antes de operar, pero no existe evidencia de que estén dispuestas a pagar ni de que usen las estadísticas y los datos de contacto de los clientes que simularon.
* **Gestión del inventario sin validar (Web):** Las concesionarias cuentan con funcionalidades para publicar, consultar, editar y eliminar vehículos, pero no se ha evaluado si pueden completar estas operaciones de forma autónoma, sencilla y sin errores.
* **Adopción móvil sin medir (Mobile):** La app móvil cubre catálogo y simulación para compradores, pero aún no se mide la retención ni la tasa de conversión desde la búsqueda móvil hacia el guardado de simulaciones; las cuentas de concesionaria y entidad financiera se gestionan desde la web.

**Objetivos de mejora:**

* **Reducir la fricción de la evaluación crediticia:** Lograr que al menos 50% de los clientes que inician la pre-evaluación completen y guarden una simulación.
* **Aumentar los envíos a evaluación:** Alcanzar que 30% de las simulaciones guardadas se envíen a la entidad financiera y reciban una evaluación oficial.
* **Validar la monetización B2B:** Confirmar que las concesionarias pagan y renuevan la membresía (retención ≥ 80% y churn mensual < 5%).
* **Demostrar valor a la concesionaria:** Medir si las estadísticas por vehículo y los datos de contacto de los clientes se traducen en acciones (ajuste de precio y contacto).
* **Facilitar la gestión del inventario:** Lograr que al menos el 80% de las tareas de publicación, consulta, edición y eliminación de vehículos se completen correctamente y sin asistencia.
  
### 8.1.2. Raw Material: Assumptions, Knowledge Gaps, Ideas, Claims

**Assumptions (Suposiciones):**

* **Disposición a compartir datos financieros:** Se asume que los clientes ingresarán sus ingresos y deudas en la plataforma para conocer su capacidad de endeudamiento antes de simular.
* **Valor de la comparación multi-banco:** Se asume que ver la cuota, la TCEA y el VAN de varias entidades en un solo cuadro ayuda al cliente a decidir y a enviar su simulación.
* **Pago de la membresía:** Se asume que las concesionarias de vehículos nuevos y usados pagarán una membresía mensual si la plataforma les genera visibilidad y clientes interesados.
* **Uso de las estadísticas:** Se asume que las concesionarias ajustarán precios y contactarán a los clientes a partir de las vistas y simulaciones por vehículo.
* **Autonomía en la gestión del inventario:** Se asume que las concesionarias podrán administrar sus publicaciones desde el panel web sin depender del soporte del equipo de SmartFinance Drive.
* **Uso móvil para simulación:** Se asume que los compradores valoran explorar el catálogo y calcular cuotas desde el smartphone antes de visitar la concesionaria.

**Knowledge Gaps (Brechas de conocimiento):**

* Se desconoce cuánto tiempo tarda hoy un cliente en encontrar una alternativa viable y cuántos abandonan antes de simular, por lo que no existe línea base para demostrar la reducción de 35%.
* Carecemos de evidencia sobre la disposición de pago y el precio aceptable de la membresía, ya que las entrevistas no exploraron este punto.
* No sabemos si el Risk Tier calculado por la plataforma anticipa la evaluación oficial de la entidad financiera.
* Se desconoce si las concesionarias pueden publicar, consultar, editar y eliminar vehículos de manera autónoma, cuánto tiempo les toma cada operación y qué errores encuentran durante el proceso.

**Ideas:**

* **Pre-evaluación previa a la simulación:** Mostrar la capacidad máxima de endeudamiento antes de simular y precargar la cuota máxima en el simulador.
* **Envío desde el comparador multi-banco:** Permitir guardar y enviar a evaluación la oferta elegida directamente desde el cuadro comparativo.
* **Piloto de membresía:** Ofrecer un periodo de prueba de 30 días y un botón "Solicitar demo" en la sección de planes de la Landing Page.
* **Resumen de estadísticas:** Enviar a la concesionaria un resumen semanal de vistas, simulaciones y clientes interesados por vehículo.
* **Prueba de gestión del inventario:** Evaluar con concesionarias las tareas de publicación, consulta, edición y eliminación de vehículos desde el panel web.

### 8.1.3. Experiment-Ready Questions

| Question | Confidence | Risk | Impact | Interest | Total Score |
| --- | --- | --- | --- | --- | --- |
| ¿Aumentará la cantidad de clientes que guardan una simulación si ven su **capacidad máxima de endeudamiento (pre-evaluación)** antes de simular? | 7 | 8 | 9 | 8 | **32** |
| ¿Aumentarán los envíos a evaluación de la entidad financiera si el cliente puede **comparar cotizaciones multi-banco** y enviar la oferta elegida desde el mismo cuadro? | 7 | 7 | 9 | 8 | **31** |
| ¿Están las concesionarias dispuestas a **pagar una membresía mensual** y a iniciar un piloto con la propuesta actual? | 5 | 9 | 9 | 7 | **30** |
| ¿Podrán las concesionarias **gestionar autónomamente sus vehículos publicados** (publicar, consultar, editar y eliminar) desde el panel web? | 7 | 6 | 8 | 8 | **29** |
| ¿Actuarán las concesionarias sobre las **estadísticas por vehículo y los datos de contacto** de los clientes que simularon, ajustando precios y contactándolos? | 6 | 7 | 8 | 7 | **28** |

### 8.1.4. Question Backlog

| Prioridad (1,2,3,5,8) | Pregunta |
| --- | --- |
| 8 | ¿Aumentará la cantidad de clientes que guardan una simulación si ven su capacidad máxima de endeudamiento (pre-evaluación) antes de simular? |
| 5 | ¿Aumentarán los envíos a evaluación de la entidad financiera si el cliente puede comparar cotizaciones multi-banco y enviar la oferta elegida desde el mismo cuadro? |
| 5 | ¿Están las concesionarias dispuestas a pagar una membresía mensual y a iniciar un piloto con la propuesta actual? |
| 3 | ¿Actuarán las concesionarias sobre las estadísticas por vehículo y los datos de contacto de los clientes que simularon, ajustando precios y contactándolos? |
| 3 | ¿Podrán las concesionarias gestionar autónomamente sus vehículos publicados (publicar, consultar, editar y eliminar) desde el panel web? |

**Claims (Afirmaciones):**

* Una pre-evaluación previa reducirá el abandono y permitirá que al menos 50% de los clientes que la inician guarden una simulación.
* Las concesionarias pagarán la membresía solo si las estadísticas y los contactos les permiten reducir el tiempo de rotación de su inventario.
* Un panel web claro y consistente permitirá que las concesionarias administren sus publicaciones de vehículos sin asistencia y mantengan actualizado el catálogo.

### 8.1.5. Experiment Cards

| Question | ¿Aumentará la cantidad de clientes que guardan una simulación si ven su capacidad máxima de endeudamiento (pre-evaluación) antes de simular? (Web) |
| --- | --- |
| **Why** | Los 3 compradores entrevistados valoran conocer sus opciones de crédito antes de decidir, pero la pre-evaluación exige ingresar ingresos y deudas. Si el cliente no completa ese paso, no llega a simular ni a enviar su solicitud, y la plataforma pierde el recorrido que justifica su propuesta de valor. |
| **What** | Comparar con 10 a 15 clientes, en sesión moderada y con orden alternado, dos recorridos en la web: simular directamente un crédito y generar primero la pre-evaluación (US15), que muestra el score, el Risk Tier y la capacidad máxima de endeudamiento y precarga la cuota máxima en el simulador (US17). Se registra quién completa cada paso, cuánto tarda y qué datos se resisten a ingresar. |
| **Hypothesis** | Se espera que al menos el 50% de los clientes que inician la pre-evaluación completen y guarden una simulación y que el tiempo para llegar a una simulación viable se reduzca en 35% frente al recorrido sin pre-evaluación. |

| Question | ¿Aumentarán los envíos a evaluación de la entidad financiera si el cliente puede comparar cotizaciones multi-banco y enviar la oferta elegida desde el mismo cuadro? (Web) |
| --- | --- |
| **Why** | Los compradores entrevistados dedican tiempo a comparar opciones de financiamiento y piden información crediticia. El comparador y simulador multi-banco (US-19) existe, pero el cliente debe volver a simular para enviar la oferta, lo que puede cortar el recorrido antes de la evaluación oficial. |
| **What** | Comparar con 15 a 20 clientes, en sesión moderada, la versión actual del cuadro multi-banco con una versión que permite guardar y enviar a evaluación la oferta elegida desde el mismo cuadro, y medir la proporción de participantes que envía su simulación y el tiempo hasta hacerlo. |
| **Hypothesis** | Se espera que al menos el 30% de las simulaciones guardadas se envíen a evaluación de una entidad financiera con la versión nueva y que la proporción de clientes que envían su simulación aumente en 25% frente a la versión actual. |

| Question | ¿Están las concesionarias dispuestas a pagar una membresía mensual y a iniciar un piloto con la propuesta actual? (Web) |
| --- | --- |
| **Why** | La sostenibilidad del negocio (retención ≥ 80% y churn < 5%) depende de que las concesionarias paguen. Las entrevistas validaron el problema de rotación y exposición del inventario, pero no la disposición de pago, y Stripe, los planes y la selección de membresía (US-03) ya existen en el producto. |
| **What** | Agregar un botón "Solicitar demo" con formulario breve en la sección de planes de la Landing Page (*fake door*) con dos o tres niveles de precio, y realizar entrevistas de 20 minutos con 6 concesionarias (3 de nuevos y 3 de usados) para probar los precios y ofrecer un piloto de 30 días. |
| **Hypothesis** | Se espera que al menos el 50% de las concesionarias entrevistadas acepten un piloto de 30 días y que una de cada tres deje una solicitud de demo o contratación tras ver el precio. |

| Question | ¿Actuarán las concesionarias sobre las estadísticas por vehículo y los datos de contacto de los clientes que simularon, ajustando precios y contactándolos? (Web) |
| --- | --- |
| **Why** | Las concesionarias de usados buscan rotar su inventario y las de nuevos reducir su costo de prospección. El panel de métricas de la concesionaria (US-11) y los datos de contacto de prospectos son el principal beneficio de la membresía, pero no sabemos si generan acciones. |
| **What** | Entregar durante 3 semanas a 4 a 6 concesionarias, con un resumen semanal por correo armado por el equipo, las vistas y simulaciones por vehículo y los clientes que simularon sobre sus unidades. Al final se registra cuántas ajustaron un precio, contactaron a un cliente o marcaron un vehículo como vendido. |
| **Hypothesis** | Se espera que al menos el 70% de las concesionarias participantes actúen sobre al menos un vehiculo cada semana y que el número de simulaciones por vehículo publicado aumente en 20% frente a la semana previa al piloto. |

| Question | ¿Podrán las concesionarias gestionar autónomamente sus vehículos publicados (publicar, consultar, editar y eliminar) desde el panel web? (Web) |
| --- | --- |
| **Why** | Las concesionarias necesitan mantener actualizado su inventario para ofrecer vehículos disponibles a los clientes. SmartFinance Drive contempla las operaciones de publicación (US-13), consulta del inventario (US-11), edición (US-14) y eliminación (US-15), pero aún no se ha validado si los concesionarios pueden completar estas tareas de forma autónoma, sencilla y sin errores. Una experiencia poco intuitiva podría dificultar la actualización del catálogo y provocar que los clientes encuentren información desactualizada. |
| **What** | Realizar una prueba de usabilidad moderada con entre 6 y 8 concesionarias. Cada participante deberá publicar un vehículo, consultar sus vehículos publicados, modificar el precio de uno de ellos y eliminar un vehículo propio. Se registrará si cada tarea se completa correctamente y sin asistencia, el tiempo empleado y los errores cometidos durante cada operación. |
| **Hypothesis** | Se espera que al menos el 80% de las tareas asignadas se completen correctamente y sin asistencia del moderador, y que al menos el 70% de las concesionarias participantes complete las cuatro operaciones del flujo de gestión de inventario. |

## 8.2. Experiment Design

### 8.2.1. Hypotheses

| Atributo | Detalle de la Hipótesis: Experimento 1 (Pre-evaluación previa a la simulación) |
| --- | --- |
| **Question** | ¿Aumentará la cantidad de clientes que guardan una simulación si ven su capacidad máxima de endeudamiento (pre-evaluación) antes de simular? |
| **Belief** | Creemos que mostrar al cliente su score, su Risk Tier y su capacidad máxima de endeudamiento, y precargar la cuota máxima en el simulador, reducirá la incertidumbre sobre qué crédito puede obtener y evitará que abandone antes de completar una simulación viable. |
| **Hypothesis** | Al menos el 50% de los clientes que inician la pre-evaluación completarán y guardarán una simulación. Como métrica secundaria, el tiempo necesario para llegar a una simulación viable se reducirá en 35% frente al recorrido sin pre-evaluación. |
| **Null Hypothesis** | Menos del 50% de los clientes que inician la pre-evaluación completarán y guardarán una simulación, o el tiempo para llegar a una simulación viable no se reducirá frente al recorrido sin pre-evaluación, ya sea porque el cliente abandona al tener que ingresar sus ingresos y deudas o porque el paso adicional no aporta valor. |

| Atributo | Detalle de la Hipótesis: Experimento 2 (Envío desde el comparador multi-banco) |
| --- | --- |
| **Question** | ¿Aumentarán los envíos a evaluación de la entidad financiera si el cliente puede comparar cotizaciones multi-banco y enviar la oferta elegida desde el mismo cuadro? |
| **Belief** | Creemos que permitir guardar y enviar a evaluación la oferta elegida directamente desde el cuadro comparativo eliminará la necesidad de volver a simular, y evitará que el cliente abandone el recorrido justo antes de la evaluación oficial. |
| **Hypothesis** | Al menos el 30% de las simulaciones guardadas se enviarán a evaluación de una entidad financiera con la versión nueva del cuadro, y la proporción de clientes que envían su simulación aumentará en 25% frente a la versión actual. |
| **Null Hypothesis** | Menos del 30% de las simulaciones guardadas se enviarán a evaluación con la versión nueva, y la proporción de clientes que envían su simulación no aumentará en 25% respecto de la versión actual del cuadro multi-banco. |

| Atributo | Detalle de la Hipótesis: Experimento 3 (Disposición de pago de la membresía) |
| --- | --- |
| **Question** | ¿Están las concesionarias dispuestas a pagar una membresía mensual y a iniciar un piloto con la propuesta actual? |
| **Belief** | Creemos que las concesionarias de vehículos nuevos y usados, que mostraron problemas de rotación y exposición de su inventario en las entrevistas, pagarán una membresía mensual si perciben que la plataforma les genera visibilidad y clientes interesados. |
| **Hypothesis** | Al menos el 50% de las concesionarias entrevistadas (3 de 6) aceptarán un piloto de 30 días, y una de cada tres dejará una solicitud de demo o contratación tras ver el precio. |
| **Null Hypothesis** | Menos del 50% de las concesionarias entrevistadas (menos de 3 de 6) aceptarán el piloto de 30 días, o menos de una de cada tres dejará una solicitud de demo o contratación tras ver el precio. |

| Atributo | Detalle de la Hipótesis: Experimento 4 (Uso de estadísticas y datos de contacto) |
| --- | --- |
| **Question** | ¿Actuarán las concesionarias sobre las estadísticas por vehículo y los datos de contacto de los clientes que simularon, ajustando precios y contactándolos? |
| **Belief** | Creemos que recibir cada semana las vistas, las simulaciones y los clientes interesados por vehículo permitirá a las concesionarias tomar decisiones concretas (ajustar un precio, contactar a un cliente o marcar un vehículo como vendido) para rotar su inventario y reducir su costo de prospección. |
| **Hypothesis** | Al menos el 70% de las concesionarias participantes actuarán sobre al menos un vehículo cada semana, y el número de simulaciones por vehículo publicado aumentará en 20% frente a la semana previa al piloto. |
| **Null Hypothesis** | Menos del 70% de las concesionarias participantes actuarán sobre al menos un vehículo cada semana, o el número de simulaciones por vehículo publicado no aumentará en 20% respecto de la semana previa al piloto. |

| Atributo | Detalle de la Hipótesis: Experimento 5 (Gestión autónoma del inventario de vehículos) |
| --- | --- |
| **Question** | ¿Podrán las concesionarias gestionar autónomamente sus vehículos publicados (publicar, consultar, editar y eliminar) desde el panel web? |
| **Belief** | Creemos que un panel web claro y consistente permitirá a las concesionarias administrar sus publicaciones sin depender del soporte del equipo de SmartFinance Drive, manteniendo actualizado el catálogo para los clientes. |
| **Hypothesis** | Al menos el 80% de las tareas asignadas se completarán correctamente y sin asistencia del moderador, y al menos el 70% de las concesionarias participantes completará las cuatro operaciones del flujo de gestión de inventario. |
| **Null Hypothesis** | Menos del 80% de las tareas asignadas se completarán correctamente y sin asistencia, o menos del 70% de las concesionarias participantes completará las cuatro operaciones de gestión de inventario. |
### 8.2.2. Domain Business Metrics

Para evitar que las decisiones sobre SmartFinance Drive se fundamenten en métricas irrelevantes o de vanidad, cada hipótesis de 8.2.1 se vincula con una métrica primaria (P) y, cuando corresponde, una secundaria (S), que miden decisiones concretas del cliente o de la concesionaria (guardar, enviar, aceptar, actuar o responder). Las métricas aquí definidas constituyen los únicos indicadores autorizados para evaluar las condiciones de las *Experiment Cards*.

| Exp. | Nombre de la Métrica | Descripción y Justificación | Fórmula de Cálculo | Técnica de Recolección | Meta Deseada |
| --- | --- | --- | --- | --- | --- |
| **1 (P)** | **Tasa de Guardado de Simulación tras Pre-evaluación** | Mide cuántos clientes que inician la pre-evaluación logran completar el recorrido y guardar una simulación. Refleja si pedir ingresos y deudas genera abandono o confianza. | `(Clientes que guardan una simulación / Clientes que inician la pre-evaluación) * 100` | Eventos de inicio de pre-evaluación y de simulación guardada registrados en la web y consolidados desde la base de datos; observación moderada de las sesiones. | **≥ 50.0%** |
| **1 (S)** | **Tiempo hasta Simulación Viable** | Mide la rapidez con la que el cliente llega a una simulación guardada. Es la línea base que hoy no existe y sustenta la reducción de 35%. | `Promedio de (marca de tiempo de simulación guardada − marca de tiempo de inicio del recorrido)`; reducción = `((T_sin − T_con) / T_sin) * 100` | Marcas de tiempo por sesión moderada, comparando el recorrido directo con el recorrido con pre-evaluación (orden alternado). | **Reducción ≥ 35.0%** |
| **2 (P)** | **Tasa de Envío a Evaluación** | Representa el avance real hacia la evaluación oficial de la entidad financiera. Indica si el cuadro multi-banco convierte la comparación en una acción. | `(Simulaciones enviadas a evaluación / Simulaciones guardadas) * 100` | Registros en la base de datos de simulaciones guardadas y de solicitudes enviadas a la entidad financiera, por versión (actual vs. nueva). | **≥ 30.0%** |
| **2 (S)** | **Variación de Clientes que Envían su Simulación** | Compara la proporción de clientes que envían su simulación con la versión nueva frente a la versión actual del cuadro. | `((P_nueva − P_actual) / P_actual) * 100`, donde P es la proporción de participantes que envían | Observación moderada con 15 a 20 clientes, registrando quién envía y en cuánto tiempo, para cada versión. | **≥ +25.0%** |
| **3 (P)** | **Tasa de Aceptación del Piloto** | Valida la disposición de pago de las concesionarias, principal supuesto de sostenibilidad del negocio B2B. | `(Concesionarias que aceptan el piloto de 30 días / Concesionarias entrevistadas) * 100` | Registro estructurado de las 6 entrevistas de 20 minutos (3 de nuevos y 3 de usados), con el resultado de cada oferta de piloto. | **≥ 50.0% (3 de 6)** |
| **3 (S)** | **Tasa de Solicitud de Demo o Contratación** | Mide la intención de compra tras ver el precio, mediante el *fake door* de la Landing Page y las entrevistas. | `(Solicitudes de demo o contratación / Concesionarias que vieron el precio) * 100` | Envíos del formulario "Solicitar demo" en la sección de planes de la Landing Page y registro de las entrevistas. | **≥ 33.0% (1 de cada 3)** |
| **4 (P)** | **Tasa de Acción Semanal de la Concesionaria** | Mide si las estadísticas y los datos de contacto generan acciones (ajustar precio, contactar cliente o marcar vendido), que es el valor principal de la membresía. | `(Concesionarias con al menos una acción sobre un vehículo en la semana / Concesionarias participantes) * 100` | Registro semanal de acciones en la base de datos (cambio de precio, contacto, marcado como vendido) y verificación en el cierre de la tercera semana. | **≥ 70.0%** |
| **4 (S)** | **Variación de Simulaciones por Vehículo Publicado** | Mide si las acciones de la concesionaria se traducen en mayor interés del cliente en sus unidades. | `((Simulaciones por vehículo en semana de piloto − Simulaciones por vehículo en semana previa) / Simulaciones por vehículo en semana previa) * 100` | Conteo de simulaciones por vehículo desde el panel de métricas de la concesionaria (US-11), comparando la semana previa con cada semana del piloto. | **≥ +20.0%** |
| **5 (P)** | **Tasa de Tareas Completadas sin Asistencia** | Mide la proporción de operaciones de inventario que las concesionarias completan correctamente sin intervención del moderador. | `(Tareas completadas correctamente y sin asistencia / Total de tareas asignadas) * 100` | Lista de verificación completada durante las sesiones moderadas; se registra el resultado de las cuatro tareas de cada participante. | **≥ 80.0%** |
| **5 (S)** | **Tasa de Concesionarias que Completan el Flujo Completo** | Mide qué proporción de participantes logra publicar, consultar, editar y eliminar un vehículo sin asistencia. | `(Concesionarias que completan las cuatro tareas / Total de concesionarias participantes) * 100` | Registro de resultados por participante en las sesiones de usabilidad moderadas. | **≥ 70.0%** |

### 8.2.3. Measures

Las variables cuantitativas empleadas para contrastar las hipótesis corresponden a los datos crudos recolectados en las sesiones moderadas, los pilotos y las entrevistas:

* **Clientes que inician la pre-evaluación, clientes que guardan una simulación y tiempo hasta la simulación guardada (con y sin pre-evaluación):** Datos base para la Tasa de Guardado de Simulación y la reducción del tiempo hasta una simulación viable.
* **Simulaciones guardadas, simulaciones enviadas a evaluación y participantes que envían, por versión del cuadro multi-banco:** Datos utilizados para calcular la Tasa de Envío a Evaluación y su variación frente a la versión actual.
* **Concesionarias entrevistadas, que aceptan el piloto y que dejan solicitud de demo tras ver el precio:** Datos para la Tasa de Aceptación del Piloto y la Tasa de Solicitud de Demo o Contratación.
* **Acciones semanales por concesionaria (ajuste de precio, contacto, vehículo vendido) y simulaciones por vehículo publicado:** Datos para la Tasa de Acción Semanal y la variación de simulaciones por vehículo.
* **Tareas de publicación, consulta, edición y eliminación completadas, asistencia requerida, errores y tiempos por tarea:** Datos para la Tasa de Tareas Completadas sin Asistencia y la Tasa de Concesionarias que Completan el Flujo Completo.

### 8.2.4. Conditions

* **Condición Experimental (Grupo Expuesto):** Segmento de clientes y concesionarias que usa las funcionalidades nuevas de SmartFinance Drive: la pre-evaluación previa a la simulación con cuota máxima precargada, el envío a evaluación desde el cuadro multi-banco, el piloto de membresía con el botón "Solicitar demo", y el resumen semanal de estadísticas por vehículo. Para el experimento 5, concesionarias que realizan las cuatro tareas de gestión de inventario desde el panel web: publicar un vehículo (US-13), consultar sus vehículos publicados (US-11), editar el precio de un vehículo propio (US-14) y eliminar un vehículo propio (US-15). Para los experimentos 1 a 4, se mantienen las condiciones experimentales descritas en sus respectivas hipótesis.
* **Condición de Control (Grupo Base):** Segmento que usa la versión actual de la plataforma, en la que el cliente simula directamente sin pre-evaluación, debe volver a simular para enviar su oferta desde el cuadro multi-banco, la concesionaria opera sin resumen de estadísticas (línea base de la semana previa) y no existe un piloto de membresía. En los experimentos 3 y 5, que son pruebas de validación sin control paralelo, el resultado se compara contra el umbral definido en sus respectivas hipótesis.

### 8.2.5. Scale Calculations and Decisions

Para controlar el azar en la evaluación de los experimentos, se establecen los siguientes parámetros:

* **Nivel de Significación (α):** **5%**, para limitar los falsos positivos (error Tipo I).
* **Potencia Estadística (1 − β):** **80%**, para limitar los falsos negativos (error Tipo II).
* **Efecto Mínimo Detectable (MDE):** **10 puntos porcentuales** sobre la línea base. Dado que las muestras son pequeñas (6 a 20 participantes), los experimentos se consideran exploratorios y la decisión de escalar se basa en los umbrales de la matriz, no en pruebas de significancia.

| Factor | Scale Calculation y Decision (Métricas e Hipótesis) | 1. Desfavorable (Sin cambios) | 2. Aceptable (Progreso mínimo) | 3. Ideal (Meta del experimento) | 4. Excelente (Decisión: Escalar) |
| --- | --- | --- | --- | --- | --- |
| **Experimento 1: Pre-evaluación previa a la simulación** | Creemos que mostrar la capacidad máxima de endeudamiento antes de simular reducirá el abandono. Sabremos que esto es cierto cuando el 50% de quienes inician la pre-evaluación guarden una simulación. | Menos del 30%. | Entre 30% y 49%. | **50%.** | Más del 65%. (X) |
| **Experimento 2: Envío desde el comparador multi-banco** | Creemos que enviar la oferta elegida desde el mismo cuadro aumentará los envíos a evaluación. Sabremos que esto es cierto cuando el 30% de las simulaciones guardadas se envíen. | Menos del 15%. | Entre 15% y 29%. | **30%.** | Más del 40%. (X) |
| **Experimento 3: Disposición de pago de la membresía** | Creemos que las concesionarias pagarán por la membresía si perciben visibilidad y clientes interesados. Sabremos que esto es cierto cuando el 50% acepte el piloto de 30 días. | Menos de 2 de 6 (< 33%). | 2 de 6 (33%). | **3 de 6 (50%).** | 4 o más de 6 (≥ 67%). (X) |
| **Experimento 4: Uso de estadísticas y datos de contacto** | Creemos que el resumen semanal llevará a las concesionarias a actuar sobre sus vehículos. Sabremos que esto es cierto cuando el 70% actúe cada semana. | Menos del 40%. | Entre 40% y 69%. | **70%.** | Más del 85%. (X) |
| **Experimento 5: Gestión autónoma del inventario de vehículos** | Creemos que las concesionarias podrán administrar sus publicaciones sin asistencia. Sabremos que esto es cierto cuando al menos el 80% de las tareas se complete correctamente y sin ayuda. | Menos del 60%. | Entre 60% y 79%. | **80%.** | Más del 90%. (X) |

### 8.2.6. Methods Selection

| Herramienta | Precio | Capacidad de Análisis | Sencillez | Ventajas para SmartFinance Drive |
| --- | --- | --- | --- | --- |
| **Google Lighthouse** | Acceso gratuito. | Auditorías automatizadas de rendimiento, accesibilidad y buenas prácticas de la versión web. | Ejecución sencilla desde Chrome DevTools. | Verifica que la pre-evaluación, el simulador y el cuadro multi-banco carguen con rapidez en el celular, para que la lentitud técnica no se confunda con abandono por desconfianza. |
| **Google Analytics 4** | Acceso gratuito. | Rastreo de eventos personalizados y de embudos de conversión en la web. | Nivel de aprendizaje moderado. | Permite medir el recorrido del cliente (pre-evaluación, simulación guardada y envío a evaluación) y calcular la Tasa de Guardado y la Tasa de Envío a Evaluación. |
| **Registros del backend (base de datos propia)** | Incluido en la infraestructura existente. | Conteo exacto de simulaciones, envíos a evaluación, acciones de concesionarias y registros de cambios en publicaciones. | Consultas directas sin configuración adicional. | Es la fuente más confiable para las métricas de los experimentos 2, 4 y 5, incluidos los registros de publicación, edición y eliminación de vehículos. |

### 8.2.7. Data Analytics: Goals, KPIs and Metrics Selection

Dado que SmartFinance Drive se usa principalmente desde el celular, la calidad técnica de la web es una condición necesaria para que el abandono medido en los experimentos se deba a la propuesta y no a fallas técnicas. Se ejecutó una auditoría con Google Lighthouse en perfil móvil emulado (4G lento) sobre la pantalla pública de inicio de sesión:

* **Ruta bajo evaluación:** `https://smartfinance-drive-webapp.vercel.app/` (Perfil Móvil)
* **Performance (Rendimiento):** 97/100. FCP y LCP de 1.5 s, TBT de 110 ms y CLS de 0.001, dentro del rango óptimo.
* **Accessibility (Accesibilidad):** 88/100. Se detectaron contraste insuficiente y ausencia de un *main landmark*, puntos que se corregirán.
* **Best Practices (Buenas Prácticas):** 100/100. Cumple las verificaciones de seguridad y compatibilidad evaluadas.
* **SEO:** 91/100. Solo se identificó la falta de meta descripción.

### 8.2.8. Web and Mobile Tracking Plan.

Para SmartFinance Drive, el objetivo del plan de seguimiento es medir el comportamiento real de compradores y concesionarias en la aplicación web (Vue.js), la Landing Page y la aplicación móvil Android, de modo que las cinco hipótesis de 8.2.1 se evalúen con datos y no con suposiciones. Hoy solo existen estadísticas por vehículo para la concesionaria; no se mide el recorrido del cliente entre búsqueda, detalle, pre-evaluación, simulación y envío a evaluación (ver 8.1.1). Este plan cubre ese vacío.

El plan se ejecuta en dos etapas, igual que las condiciones de 8.2.4:

1. **Implementación inicial (línea base):** se instrumenta la plataforma *antes* de activar las funcionalidades nuevas, para obtener la línea base (recorrido directo sin pre-evaluación, cuadro multi-banco actual y semana previa al piloto de concesionarias).
2. **Seguimiento continuo:** se activan las funcionalidades experimentales y se compara contra la línea base con los mismos eventos, las mismas fórmulas y la misma fuente de datos.

**Principios del plan**

- **Una sola definición por métrica.** Cada evento se vincula con una métrica de 8.2.2 (P = primaria, S = secundaria). Si un evento no alimenta ninguna métrica, no se registra (se evitan métricas de vanidad).
- **Doble fuente.** Los eventos de producto se guardan en la base de datos propia (fuente oficial, tabla `experiment_events`) y los eventos de navegación web se espejan en Google Analytics 4. Si ambas fuentes difieren, prevalece la base de datos.
- **Sin datos sensibles en analítica.** Los ingresos, deudas, DNI, RUC y correos **nunca** se envían como parámetros de eventos ni a GA4. Solo se envían categorías derivadas (por ejemplo, `risk_tier` y rango de DTI). Esto respeta la Ley N.° 29733 de Protección de Datos Personales y la responsabilidad ética declarada en el Student Outcome 4.
- **Identificadores seudonimizados.** `user_hash` es un hash con sal del `userId`; los eventos de visitantes anónimos usan `anonymous_id` (cookie de primera parte) y solo se activan tras aceptar el aviso de cookies.
- **Variante explícita.** Cada evento de los experimentos 1 y 2 lleva `variant` (`control` o `treatment`), asignada por el moderador o por paridad del código de participante, con orden alternado.

**Herramientas**

| Herramienta | Plataforma | Uso en el plan |
|---|---|---|
| Google Analytics 4 | Web y Landing Page | Embudos de navegación, eventos personalizados, DebugView para validar la instrumentación. |
| Tabla `experiment_events` (PostgreSQL en Aiven) | Backend | Fuente oficial de eventos de producto; se llena desde `POST /api/v1/analytics/events` y desde los servicios del backend. |
| Capa `EventTracker` (Kotlin) | Android | Envía los eventos móviles al mismo endpoint del backend (sin SDK de terceros, para mantener un solo almacén). |
| Brevo | Backend | Registro de envío del resumen semanal (Experimento 4). |
| Google Lighthouse | Web | Verifica que la lentitud técnica no se confunda con abandono (ver 8.2.7). |
| Hoja de verificación de sesiones moderadas | Manual | Registro de tareas, asistencia y errores del Experimento 5, y marcas de tiempo del Experimento 1. |

**Estructura común de todo evento**

| Campo | Descripción |
|---|---|
| `event_name` | Nombre en `snake_case` (catálogo siguiente). |
| `occurred_at` | Marca de tiempo UTC. |
| `platform` | `web`, `landing` o `android`. |
| `user_hash` / `anonymous_id` | Identificador seudonimizado. |
| `role` | `buyer`, `dealer`, `financial_entity` o `visitor`. |
| `session_id` | Identificador de sesión o de recorrido. |
| `variant` | `control` o `treatment` (cuando aplica). |
| `properties` | Objeto JSON con los parámetros específicos del evento. |

**Catálogo de eventos**

**Experimento 1: Pre-evaluación previa a la simulación**

| Evento | Plataforma | Se dispara cuando | Parámetros | Métrica |
|---|---|---|---|---|
| `journey_started` | web | El comprador abre el simulador o la pre-evaluación desde una ficha de vehículo. | `vehicle_id`, `entry_point` | 1 (S) línea de inicio |
| `preeval_started` | web | El comprador abre el formulario de pre-evaluación. | `vehicle_id` | 1 (P) denominador |
| `preeval_completed` | web | La pre-evaluación devuelve score y capacidad máxima. | `risk_tier`, `dti_bucket` (≤30 / 30–45 / >45), `elapsed_seconds` | 1 (P) |
| `preeval_abandoned` | web | El comprador sale del formulario sin completarlo. | `last_field_touched` (solo nombre del campo) | 1 (P) diagnóstico |
| `simulation_started` | web, android | El comprador inicia una simulación. | `vehicle_id`, `prefilled_max_installment` (bool) | 1 (S) |
| `simulation_saved` | web, android | El comprador guarda una simulación. | `simulation_id`, `term_months`, `elapsed_seconds` desde `journey_started` | 1 (P) numerador, 1 (S), 2 (P) denominador |

**Experimento 2: Envío desde el comparador multi-banco**

| Evento | Plataforma | Se dispara cuando | Parámetros | Métrica |
|---|---|---|---|---|
| `comparison_viewed` | web | Se muestra el cuadro de cotizaciones multi-banco. | `bank_count`, `simulation_id` | 2 (S) |
| `simulation_submitted` | web | La simulación se envía a evaluación de una entidad financiera. | `simulation_id`, `financial_entity_id`, `origin` (`comparison_table` o `simulation_detail`), `elapsed_seconds` | 2 (P) numerador, 2 (S) |
| `evaluation_result_viewed` | web, android | El comprador ve el resultado oficial. | `status` (`approved` o `rejected`) | Seguimiento |

**Experimento 3: Disposición de pago de la membresía**

| Evento | Plataforma | Se dispara cuando | Parámetros | Métrica |
|---|---|---|---|---|
| `pricing_viewed` | landing | La sección de planes entra en el viewport. | `plan_tier_shown` | 3 (S) denominador |
| `demo_requested` | landing | Se envía el formulario "Solicitar demo". | `dealer_type` (`new` o `used`), `plan_tier` (`basic`, `standard`, `premium`) | 3 (S) numerador |
| `pilot_offer_result` | manual | Resultado de cada entrevista de 20 minutos. | `dealer_type`, `accepted` (bool), `price_tested` | 3 (P) |

**Experimento 4: Uso de estadísticas y datos de contacto**

| Evento | Plataforma | Se dispara cuando | Parámetros | Métrica |
|---|---|---|---|---|
| `weekly_summary_sent` | backend | Se envía el resumen semanal por correo. | `dealer_id_hash`, `week_id`, `vehicle_count` | 4 (P) control de entrega |
| `dealer_price_changed` | web | La concesionaria modifica el precio de un vehículo. | `vehicle_id`, `delta_percent` | 4 (P) |
| `dealer_lead_contacted` | web | La concesionaria contacta a un cliente que simuló. | `vehicle_id`, `channel` (`email`, `phone`, `whatsapp`) | 4 (P) |
| `dealer_vehicle_marked_sold` | web | La concesionaria marca un vehículo como vendido. | `vehicle_id`, `days_on_lot` | 4 (P) |
| `vehicle_simulations_count` | backend | Corte semanal por vehículo (agregado). | `vehicle_id`, `week_id`, `simulations` | 4 (S) |

**Experimento 5: Gestión autónoma del inventario**

| Evento | Plataforma | Se dispara cuando | Parámetros | Métrica |
|---|---|---|---|---|
| `inventory_task_started` | web | Se inicia publicar, consultar, editar o eliminar. | `task` (`publish`, `list`, `edit`, `delete`) | 5 (P) |
| `inventory_task_completed` | web | La operación termina correctamente. | `task`, `duration_seconds`, `error_count` | 5 (P), 5 (S) |
| `inventory_task_error` | web | El backend o la validación rechazan la operación. | `task`, `error_code` | 5 (P) diagnóstico |
| `inventory_task_assisted` | manual | El moderador interviene (registro en la hoja de verificación). | `task`, `reason` | 5 (P), 5 (S) |

**Eventos transversales móviles (adopción móvil, brecha de 8.1.1)**

| Evento | Plataforma | Se dispara cuando | Parámetros |
|---|---|---|---|
| `app_opened` | android | Se abre la aplicación. | `app_version`, `is_returning` |
| `catalog_searched` | android | Se aplica una búsqueda o filtro. | `filters_used` (lista de nombres de filtro) |
| `vehicle_detail_viewed` | android | Se abre la ficha de un vehículo. | `vehicle_id` |

**Fórmulas de cálculo desde los eventos**

| Métrica (8.2.2) | Cálculo sobre `experiment_events` |
|---|---|
| 1 (P) Tasa de Guardado tras Pre-evaluación | `COUNT(DISTINCT session_id) con simulation_saved` ÷ `COUNT(DISTINCT session_id) con preeval_started` × 100 |
| 1 (S) Tiempo hasta Simulación Viable | Promedio de `elapsed_seconds` en `simulation_saved`, por `variant`; reducción = (T_control − T_treatment) ÷ T_control × 100 |
| 2 (P) Tasa de Envío a Evaluación | `COUNT(simulation_submitted)` ÷ `COUNT(simulation_saved)` × 100, por versión del cuadro |
| 2 (S) Variación de clientes que envían | (P_nueva − P_actual) ÷ P_actual × 100, con P = participantes que envían ÷ participantes de la sesión |
| 3 (P) Tasa de Aceptación del Piloto | `pilot_offer_result.accepted = true` ÷ concesionarias entrevistadas × 100 |
| 3 (S) Tasa de Solicitud de Demo | `COUNT(demo_requested)` ÷ `COUNT(pricing_viewed)` (concesionarias únicas) × 100 |
| 4 (P) Tasa de Acción Semanal | Concesionarias con ≥1 evento `dealer_*` en la semana ÷ concesionarias participantes × 100 |
| 4 (S) Variación de simulaciones por vehículo | (Sim/veh. semana de piloto − Sim/veh. semana previa) ÷ semana previa × 100 |
| 5 (P) Tareas sin asistencia | Tareas con `inventory_task_completed` y sin `inventory_task_assisted` ÷ tareas asignadas × 100 |
| 5 (S) Flujo completo | Concesionarias con las 4 tareas completadas sin asistencia ÷ participantes × 100 |

**Etapa 1: Implementación inicial**

- **Recopilación:** número de usuarios activos, duración de sesión, recorrido búsqueda → detalle → simulación → guardado, y uso actual del cuadro multi-banco (versión de control).
- **Línea base de concesionarias:** simulaciones por vehículo de la semana previa al piloto, tomadas del panel de métricas (US-11).
- **Validación de la instrumentación (criterio de salida):** antes de abrir las sesiones con participantes se ejecutan 5 recorridos internos completos y se comprueba en GA4 DebugView y en `experiment_events` que cada evento del catálogo aparece una sola vez, con sus parámetros y sin datos sensibles.

**Etapa 2: Seguimiento continuo**

- **Métricas casi en tiempo real:** consultas sobre `experiment_events` (vista `v_experiment_funnel`) y reportes de GA4.
- **Segmentación:** por rol (comprador, concesionaria de nuevos, concesionaria de usados), por plataforma (web o Android) y por variante.
- **Retención:** el comprador que vuelve a la app móvil en 7 días (`app_opened` con `is_returning = true`) y la concesionaria que mantiene acciones semanales durante las 3 semanas del piloto.
- **Informes:** un reporte semanal del equipo con las métricas primarias y secundarias, contrastadas con la escala de 8.2.5, y las decisiones (escalar, iterar o descartar) alimentan la toma de decisiones del equipo y la evolución del backlog de experimentos.

**Plan de control de calidad de los datos**

| Riesgo | Control |
|---|---|
| Eventos duplicados por recargas del navegador | Idempotencia por `session_id` + `event_name` + `occurred_at` (segundo) en el backend. |
| Fuga de datos personales | Lista blanca de propiedades en el endpoint; todo campo fuera de la lista se descarta y se registra una advertencia. |
| Muestras pequeñas (6 a 20 participantes) | Los resultados se tratan como exploratorios (ver 8.2.5); se reportan conteos absolutos junto con los porcentajes. |
| Lentitud técnica confundida con abandono | Auditoría Lighthouse antes y durante el experimento (8.2.7). |

---

## 8.3. Experimentation

### 8.3.1. To-Be User Stories.

Las To-Be User Stories traducen los cinco experimentos de 8.2.1 en funcionalidades concretas y en la instrumentación necesaria para medirlos. Para no colisionar con el Capítulo III (US-01 a US-22), usan el prefijo **UA** (*user stories de aprendizaje*), igual que el proyecto de referencia. Los escenarios usan el mismo formato Dado/Cuando/Entonces del Capítulo III. **Cabe señalar que todas las User Stories planteadas para los experimentos están dirigidas a la versión Web de la plataforma (Landing Page y Aplicación Web Vue.js soportadas por el backend RESTful en Spring Boot)**, concentrando la validación experimental y las interacciones de los usuarios en el ecosistema web.

| Epic ID | Epic | Experimento | Historias |
|---|---|---|---|
| EX01 | Pre-evaluación y simulación guiada | 1 | UA-01, UA-02, UA-03 |
| EX02 | Envío a evaluación desde el comparador multi-banco | 2 | UA-04, UA-05 |
| EX03 | Validación de la membresía B2B | 3 | UA-06 |
| EX04 | Insights accionables para concesionarias | 4 | UA-07, UA-08, UA-09 |
| EX05 | Gestión autónoma del inventario | 5 | UA-10 |
| EX06 | Instrumentación y analítica | 1 a 5 | UA-11, UA-12, UA-13, UA-14 |

**UA-01 — Ver la capacidad máxima de endeudamiento antes de simular**

| Campo | Detalle |
|---|---|
| User | Comprador |
| Priority | Alta |
| Epic | EX01 |
| Description | Como Comprador, quiero ver mi score, mi nivel de riesgo y mi capacidad máxima de endeudamiento antes de simular un crédito, para saber qué cuota puedo asumir sin probar varias simulaciones. |
| Acceptance Criteria | **Escenario 1 — Pre-evaluación exitosa.** Dado que el comprador tiene sesión activa y está en la ficha de un vehículo, cuando ingresa sus ingresos mensuales y deudas y solicita la pre-evaluación, entonces la plataforma muestra su score, su Risk Tier y su cuota máxima mensual. <br> **Escenario 2 — Datos inválidos.** Dado que el comprador completa el formulario, cuando ingresa ingresos en cero o valores negativos, entonces la plataforma indica los campos a corregir y no calcula. <br> **Escenario 3 — Transparencia de datos.** Dado que el comprador va a ingresar datos financieros, cuando abre el formulario, entonces ve para qué se usan sus datos y que la decisión final corresponde a la entidad financiera. |

**UA-02 — Precargar la cuota máxima en el simulador**

| Campo | Detalle |
|---|---|
| User | Comprador |
| Priority | Alta |
| Epic | EX01 |
| Description | Como Comprador, quiero que el simulador use mi cuota máxima como punto de partida, para llegar más rápido a una simulación viable. |
| Acceptance Criteria | **Escenario 1 — Precarga.** Dado que el comprador completó la pre-evaluación, cuando abre el simulador de crédito, entonces el campo de cuota máxima aparece precargado y editable. <br> **Escenario 2 — Sin pre-evaluación.** Dado que el comprador no realizó la pre-evaluación, cuando abre el simulador, entonces el flujo funciona como la versión actual (grupo de control). |

**UA-03 — Guardar la simulación y registrar el recorrido**

| Campo | Detalle |
|---|---|
| User | Comprador |
| Priority | Alta |
| Epic | EX01 |
| Description | Como Comprador, quiero guardar mi simulación desde la web o desde la app móvil, para retomarla después y compararla con otras. |
| Acceptance Criteria | **Escenario 1 — Guardado exitoso.** Dado que el comprador calculó una simulación, cuando presiona "Guardar", entonces la plataforma la almacena con la fecha y hora y la muestra en su historial. <br> **Escenario 2 — Medición del recorrido.** Dado que la simulación se guardó, cuando el sistema registra el evento, entonces incluye el tiempo transcurrido desde el inicio del recorrido y la variante, sin datos personales. |

**UA-04 — Enviar a evaluación desde el cuadro multi-banco**

| Campo | Detalle |
|---|---|
| User | Comprador |
| Priority | Alta |
| Epic | EX02 |
| Description | Como Comprador, quiero guardar y enviar a evaluación la oferta que elegí directamente desde el cuadro comparativo, para no volver a simular. |
| Acceptance Criteria | **Escenario 1 — Envío exitoso.** Dado que el comprador compara cotizaciones de varias entidades, cuando selecciona una oferta y presiona "Enviar a evaluación", entonces la plataforma guarda la simulación y crea la solicitud para la entidad elegida. <br> **Escenario 2 — Falla del envío.** Dado que el comprador intenta enviar, cuando ocurre un error de conexión o de validación, entonces la plataforma muestra un mensaje claro y conserva la simulación guardada. <br> **Escenario 3 — Versión de control.** Dado que el comprador está en la versión actual, cuando quiere enviar una oferta, entonces debe volver a simular (flujo base de comparación). |

**UA-05 — Confirmación y estado de la solicitud enviada**

| Campo | Detalle |
|---|---|
| User | Comprador |
| Priority | Media |
| Epic | EX02 |
| Description | Como Comprador, quiero ver una confirmación y el estado de mi solicitud, para saber que la entidad financiera la recibió. |
| Acceptance Criteria | **Escenario 1 — Confirmación.** Dado que el comprador envió su simulación, cuando el envío termina, entonces la plataforma muestra el resumen y la entidad destinataria. <br> **Escenario 2 — Consulta posterior.** Dado que existe una solicitud enviada, cuando el comprador abre su historial, entonces ve el estado actual (pendiente, aprobada o rechazada). |

**UA-06 — Solicitar una demo desde los planes de membresía (Landing Page)**

| Campo | Detalle |
|---|---|
| User | Visitante (concesionaria) |
| Priority | Alta |
| Epic | EX03 |
| Description | Como representante de una concesionaria, quiero solicitar una demo desde la sección de planes, para evaluar el piloto de 30 días antes de contratar. |
| Acceptance Criteria | **Escenario 1 — Solicitud de demo.** Dado que el visitante ve los planes con sus precios, cuando presiona "Solicitar demo" y completa nombre, tipo de concesionaria, correo y plan de interés, entonces la plataforma registra la solicitud y muestra un mensaje de agradecimiento. <br> **Escenario 2 — Datos incompletos.** Dado que el visitante envía el formulario, cuando omite campos obligatorios o usa un correo inválido, entonces la plataforma indica qué corregir. <br> **Escenario 3 — Transparencia.** Dado que el visitante solicita la demo, cuando completa el formulario, entonces se le informa que se trata de un piloto y que aún no se realiza ningún cobro. |

**UA-07 — Recibir un resumen semanal de estadísticas por vehículo**

| Campo | Detalle |
|---|---|
| User | Concesionaria |
| Priority | Alta |
| Epic | EX04 |
| Description | Como Concesionaria, quiero recibir cada semana por correo las vistas, simulaciones y clientes interesados por vehículo, para decidir qué precio ajustar o a quién contactar. |
| Acceptance Criteria | **Escenario 1 — Envío semanal.** Dado que la concesionaria participa en el piloto, cuando se cumple el corte semanal, entonces recibe un correo con vistas, simulaciones y clientes interesados por cada vehículo publicado. <br> **Escenario 2 — Sin actividad.** Dado que un vehículo no tuvo actividad, cuando se arma el resumen, entonces aparece indicado como "sin actividad". <br> **Escenario 3 — Falla del correo.** Dado que el servicio de correo falla, cuando se intenta enviar, entonces el sistema registra el error y permite reenviar. |

**UA-08 — Registrar las acciones de la concesionaria sobre un vehículo**

| Campo | Detalle |
|---|---|
| User | Concesionaria |
| Priority | Alta |
| Epic | EX04 |
| Description | Como Concesionaria, quiero ajustar el precio de un vehículo, contactar a un cliente o marcar un vehículo como vendido desde el panel, para actuar sobre lo que muestran las estadísticas. |
| Acceptance Criteria | **Escenario 1 — Ajuste de precio.** Dado que la concesionaria ve las estadísticas de un vehículo, cuando modifica su precio y guarda, entonces el catálogo se actualiza y la acción queda registrada. <br> **Escenario 2 — Marcar como vendido.** Dado que un vehículo fue vendido, cuando la concesionaria lo marca como vendido, entonces deja de mostrarse en el catálogo público y se registran los días en patio. <br> **Escenario 3 — Datos inválidos.** Dado que la concesionaria edita un precio, cuando ingresa un valor fuera de rango, entonces la plataforma lo rechaza y muestra el error. |

**UA-09 — Contactar a un cliente que simuló sobre un vehículo**

| Campo | Detalle |
|---|---|
| User | Concesionaria |
| Priority | Media |
| Epic | EX04 |
| Description | Como Concesionaria, quiero ver qué clientes simularon un crédito sobre mis vehículos y contactarlos, para convertir ese interés en una visita o prueba de manejo. |
| Acceptance Criteria | **Escenario 1 — Lista de interesados.** Dado que existen simulaciones sobre un vehículo, cuando la concesionaria abre el detalle de estadísticas, entonces ve la lista de clientes que consintieron compartir su contacto. <br> **Escenario 2 — Consentimiento.** Dado que un cliente no autorizó compartir sus datos, cuando se arma la lista, entonces su contacto no se muestra. <br> **Escenario 3 — Contacto.** Dado que la concesionaria ve un cliente interesado, cuando presiona "Contactar", entonces se abre el canal elegido y la acción se registra. |

**UA-10 — Gestionar el inventario con confirmaciones y mensajes claros**

| Campo | Detalle |
|---|---|
| User | Concesionaria |
| Priority | Media |
| Epic | EX05 |
| Description | Como Concesionaria, quiero publicar, consultar, editar y eliminar vehículos con confirmaciones y mensajes de error claros, para completar estas tareas sin pedir ayuda al equipo. |
| Acceptance Criteria | **Escenario 1 — Confirmación de operación.** Dado que la concesionaria completa una operación de inventario, cuando termina, entonces la plataforma muestra un mensaje de éxito visible. <br> **Escenario 2 — Eliminación segura.** Dado que la concesionaria elimina un vehículo, cuando presiona "Eliminar", entonces la plataforma pide confirmación antes de ejecutar la baja. <br> **Escenario 3 — Error comprensible.** Dado que la operación falla por datos inválidos, cuando la plataforma rechaza el cambio, entonces indica el campo y el motivo. |

**UA-11 — Registrar eventos de navegación en la web y la Landing Page**

| Campo | Detalle |
|---|---|
| User | Developer |
| Priority | Alta |
| Epic | EX06 |
| Description | Como Developer, quiero registrar los eventos del catálogo definido en 8.2.8 en la web y la Landing Page, para calcular los embudos de los experimentos. |
| Acceptance Criteria | **Escenario 1 — Evento enviado.** Dado que el usuario aceptó el aviso de cookies, cuando realiza una acción del catálogo, entonces se envía el evento con sus parámetros a GA4 y al backend. <br> **Escenario 2 — Sin consentimiento.** Dado que el usuario no aceptó el aviso, cuando navega, entonces no se envían eventos de visitantes anónimos. <br> **Escenario 3 — Sin datos sensibles.** Dado que el evento incluye parámetros, cuando se envía, entonces no contiene ingresos, deudas, DNI, RUC ni correos. |

**UA-12 — Almacenar los eventos del experimento en el backend**

| Campo | Detalle |
|---|---|
| User | Developer |
| Priority | Alta |
| Epic | EX06 |
| Description | Como Developer, quiero un endpoint y una tabla para almacenar los eventos de producto, para disponer de una fuente oficial y consultable de las métricas. |
| Acceptance Criteria | **Escenario 1 — Registro exitoso.** Dado que el cliente envía un evento válido, cuando el backend lo recibe, entonces lo almacena en `experiment_events` y responde 202 Accepted. <br> **Escenario 2 — Evento inválido.** Dado que el evento tiene un nombre fuera del catálogo o propiedades no permitidas, cuando el backend lo valida, entonces responde 400 y no lo almacena. <br> **Escenario 3 — Idempotencia.** Dado que el mismo evento llega dos veces, cuando el backend lo procesa, entonces lo registra una sola vez. |

**UA-13 — Registrar eventos en la aplicación móvil**

| Campo | Detalle |
|---|---|
| User | Developer |
| Priority | Media |
| Epic | EX06 |
| Description | Como Developer, quiero que la aplicación Android registre los eventos móviles del catálogo, para medir retención y conversión desde la búsqueda móvil hasta el guardado de simulaciones. |
| Acceptance Criteria | **Escenario 1 — Evento móvil.** Dado que el comprador usa la app, cuando abre el catálogo, ve un vehículo o guarda una simulación, entonces la app envía el evento correspondiente al backend. <br> **Escenario 2 — Sin conexión.** Dado que el dispositivo no tiene conexión, cuando ocurre un evento, entonces la app lo guarda localmente y lo envía al recuperar la conexión. |

**UA-14 — Consultar y exportar las métricas del experimento**

| Campo | Detalle |
|---|---|
| User | Developer / Equipo |
| Priority | Media |
| Epic | EX06 |
| Description | Como integrante del equipo, quiero consultar y exportar las métricas de 8.2.2 desde los eventos almacenados, para analizar los resultados y preparar la sesión de shareback. |
| Acceptance Criteria | **Escenario 1 — Consulta del embudo.** Dado que existen eventos almacenados, cuando se ejecuta la consulta del experimento, entonces se obtienen los conteos y porcentajes por variante. <br> **Escenario 2 — Exportación.** Dado que se requiere el análisis, cuando se exporta, entonces se genera un archivo CSV sin identificadores personales. |

---

### 8.3.2. To-Be Product Backlog

El orden prioriza primero la instrumentación (sin ella no hay línea base), luego los experimentos según el puntaje del Question Backlog (8.1.4). La escala es 1, 2, 3, 5 y 8.

| # Orden | User Story ID | Título | Experimento | Story Points |
|---|---|---|---|---|
| 1 | UA-12 | Almacenar los eventos del experimento en el backend | 1 a 5 | 5 |
| 2 | UA-11 | Registrar eventos de navegación en la web y la Landing Page | 1 a 5 | 3 |
| 3 | UA-01 | Ver la capacidad máxima de endeudamiento antes de simular | 1 | 5 |
| 4 | UA-02 | Precargar la cuota máxima en el simulador | 1 | 3 |
| 5 | UA-03 | Guardar la simulación y registrar el recorrido | 1 | 3 |
| 6 | UA-04 | Enviar a evaluación desde el cuadro multi-banco | 2 | 5 |
| 7 | UA-05 | Confirmación y estado de la solicitud enviada | 2 | 2 |
| 8 | UA-06 | Solicitar una demo desde los planes de membresía | 3 | 3 |
| 9 | UA-08 | Registrar las acciones de la concesionaria sobre un vehículo | 4 | 5 |
| 10 | UA-07 | Recibir un resumen semanal de estadísticas por vehículo | 4 | 5 |
| 11 | UA-09 | Contactar a un cliente que simuló sobre un vehículo | 4 | 3 |
| 12 | UA-10 | Gestionar el inventario con confirmaciones y mensajes claros | 5 | 3 |
| 13 | UA-13 | Registrar eventos en la aplicación móvil | 1 a 5 | 3 |
| 14 | UA-14 | Consultar y exportar las métricas del experimento | 1 a 5 | 2 |
| | | **Total** | | **50** |

Distribución por Sprint: el Sprint 3 (instrumentación, Experimentos 1, 2 y 3) suma **29 Story Points**, igual que la velocidad del Sprint 1; el Sprint 4 (Experimentos 4 y 5, móvil y análisis) suma **21 Story Points**.
