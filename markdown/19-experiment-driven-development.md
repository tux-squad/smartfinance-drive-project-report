# Capítulo VIII: Experiment-Driven Development

## 8.1. Experiment Planning

En esta sección se define **qué se investigará, por qué importa y qué experimentos se ejecutarán** sobre SmartFinance Drive. El punto de partida es el estado actual del producto (web y móvil) y el conocimiento acumulado en los capítulos I a VII: las 9 entrevistas (2.2), los User Personas (2.3), las hipótesis de Lean UX (1.2.2) y las User Stories vigentes (3.2).

### 8.1.1. As-Is Summary

SmartFinance Drive es un marketplace B2B2C de vehículos nuevos y usados con financiamiento, que conecta a clientes, concesionarias y entidades financieras. La aplicación web ya cubre el flujo principal para los cuatro roles de la plataforma: registro y solicitud de rol validando el RUC, catálogo con búsqueda, filtros y comparador de vehículos, comparador de entidades financieras, pre-evaluación de riesgo crediticio (score, DTI y Risk Tier), simulación de crédito con método francés (cuota, TCEA, TIR y VAN), comparación de cotizaciones multi-banco, proyección de depreciación, evaluación oficial de las simulaciones por la entidad financiera, membresías B2B y panel de estadísticas para la concesionaria. La aplicación móvil Android cubre el inicio y cierre de sesión y la mensajería entre clientes, concesionarias y entidades financieras.

No obstante, la plataforma aún no ha medido el comportamiento real de sus usuarios ni ha validado con ellos las funciones que la diferencian de NeoAuto y Autocosmos, por lo que la decisión de qué mejorar o ampliar descansa en suposiciones.

**Problemas identificados:**

* **Sin línea base de uso del cliente (Web):** Solo existen estadísticas para la concesionaria (vistas y simulaciones por vehículo); no se mide el recorrido del cliente entre búsqueda, detalle, pre-evaluación, simulación y envío a evaluación, ni dónde abandona.
* **Pre-evaluación que exige datos sensibles (Web):** El cliente debe ingresar ingresos y deudas antes de simular su crédito, y se desconoce cuántos clientes lo completan o abandonan por desconfianza.
* **Comparación de entidades sin validar (Web):** El cuadro comparativo multi-banco existe, pero no se sabe si cambia la decisión del cliente ni si aumenta los envíos a evaluación.
* **Valor de la membresía sin validar (Web):** Las concesionarias deben seleccionar un plan antes de operar, pero no existe evidencia de que estén dispuestas a pagar ni de que usen las estadísticas y los datos de contacto de los clientes que simularon.
* **Mensajería móvil sin medir (Mobile):** La app móvil se limita a inicio de sesión y chat, y se desconoce si clientes, concesionarias y bancos la usan y cuánto tardan en responder; las cuentas de concesionaria y entidad financiera se crean solo desde la web.

**Objetivos de mejora:**

* **Reducir la fricción de la evaluación crediticia:** Lograr que al menos 50% de los clientes que inician la pre-evaluación completen y guarden una simulación.
* **Aumentar los envíos a evaluación:** Alcanzar que 30% de las simulaciones guardadas se envíen a la entidad financiera y reciban una evaluación oficial.
* **Validar la monetización B2B:** Confirmar que las concesionarias pagan y renuevan la membresía (retención ≥ 80% y churn mensual < 5%).
* **Demostrar valor a la concesionaria:** Medir si las estadísticas por vehículo y los datos de contacto de los clientes se traducen en acciones (ajuste de precio y contacto).
* **Consolidar la comunicación móvil:** Lograr que las consultas por chat reciban respuesta de la concesionaria o del banco en menos de una hora.
  
### 8.1.2. Raw Material: Assumptions, Knowledge Gaps, Ideas, Claims

**Assumptions (Suposiciones):**

* **Disposición a compartir datos financieros:** Se asume que los clientes ingresarán sus ingresos y deudas en la plataforma para conocer su capacidad de endeudamiento antes de simular.
* **Valor de la comparación multi-banco:** Se asume que ver la cuota, la TCEA y el VAN de varias entidades en un solo cuadro ayuda al cliente a decidir y a enviar su simulación.
* **Pago de la membresía:** Se asume que las concesionarias de vehículos nuevos y usados pagarán una membresía mensual si la plataforma les genera visibilidad y clientes interesados.
* **Uso de las estadísticas:** Se asume que las concesionarias ajustarán precios y contactarán a los clientes a partir de las vistas y simulaciones por vehículo.
* **Preferencia por el chat móvil:** Se asume que los clientes preferirán consultar a la concesionaria y al banco desde el celular, el dispositivo principal de los 9 entrevistados.

**Knowledge Gaps (Brechas de conocimiento):**

* Se desconoce cuánto tiempo tarda hoy un cliente en encontrar una alternativa viable y cuántos abandonan antes de simular, por lo que no existe línea base para demostrar la reducción de 35%.
* Carecemos de evidencia sobre la disposición de pago y el precio aceptable de la membresía, ya que las entrevistas no exploraron este punto.
* No sabemos si el Risk Tier calculado por la plataforma anticipa la evaluación oficial de la entidad financiera.
* Se desconoce el tiempo de respuesta que las concesionarias y las entidades financieras pueden sostener por chat.

**Ideas:**

* **Pre-evaluación previa a la simulación:** Mostrar la capacidad máxima de endeudamiento antes de simular y precargar la cuota máxima en el simulador.
* **Envío desde el comparador multi-banco:** Permitir guardar y enviar a evaluación la oferta elegida directamente desde el cuadro comparativo.
* **Piloto de membresía:** Ofrecer un periodo de prueba de 30 días y un botón "Solicitar demo" en la sección de planes de la Landing Page.
* **Resumen de estadísticas:** Enviar a la concesionaria un resumen semanal de vistas, simulaciones y clientes interesados por vehículo.
* **Chat con contexto:** Abrir el chat móvil con un mensaje inicial que incluya el vehículo y la simulación en curso.

### 8.1.3. Experiment-Ready Questions

| Question | Confidence | Risk | Impact | Interest | Total Score |
| --- | --- | --- | --- | --- | --- |
| ¿Aumentará la cantidad de clientes que guardan una simulación si ven su **capacidad máxima de endeudamiento (pre-evaluación)** antes de simular? | 7 | 8 | 9 | 8 | **32** |
| ¿Aumentarán los envíos a evaluación de la entidad financiera si el cliente puede **comparar cotizaciones multi-banco** y enviar la oferta elegida desde el mismo cuadro? | 7 | 7 | 9 | 8 | **31** |
| ¿Están las concesionarias dispuestas a **pagar una membresía mensual** y a iniciar un piloto con la propuesta actual? | 5 | 9 | 9 | 7 | **30** |
| ¿Actuarán las concesionarias sobre las **estadísticas por vehículo y los datos de contacto** de los clientes que simularon, ajustando precios y contactándolos? | 6 | 7 | 8 | 7 | **28** |
| ¿Se responderán más consultas en menos de una hora si el cliente puede **conversar por chat móvil** con la concesionaria y con la entidad financiera? | 5 | 6 | 7 | 8 | **26** |

### 8.1.4. Question Backlog

| Prioridad (1,2,3,5,8) | Pregunta |
| --- | --- |
| 8 | ¿Aumentará la cantidad de clientes que guardan una simulación si ven su capacidad máxima de endeudamiento (pre-evaluación) antes de simular? |
| 5 | ¿Aumentarán los envíos a evaluación de la entidad financiera si el cliente puede comparar cotizaciones multi-banco y enviar la oferta elegida desde el mismo cuadro? |
| 5 | ¿Están las concesionarias dispuestas a pagar una membresía mensual y a iniciar un piloto con la propuesta actual? |
| 3 | ¿Actuarán las concesionarias sobre las estadísticas por vehículo y los datos de contacto de los clientes que simularon, ajustando precios y contactándolos? |
| 3 | ¿Se responderán más consultas en menos de una hora si el cliente puede conversar por chat móvil con la concesionaria y con la entidad financiera? |

**Claims (Afirmaciones):**

* Una pre-evaluación previa reducirá el abandono y permitirá que al menos 50% de los clientes que la inician guarden una simulación.
* Las concesionarias pagarán la membresía solo si las estadísticas y los contactos les permiten reducir el tiempo de rotación de su inventario.
* Responder en menos de una hora por chat aumenta el envío de simulaciones a evaluación.

### 8.1.5. Experiment Cards

| Question | ¿Aumentará la cantidad de clientes que guardan una simulación si ven su capacidad máxima de endeudamiento (pre-evaluación) antes de simular? (Web) |
| --- | --- |
| **Why** | Los 3 compradores entrevistados valoran conocer sus opciones de crédito antes de decidir, pero la pre-evaluación exige ingresar ingresos y deudas. Si el cliente no completa ese paso, no llega a simular ni a enviar su solicitud, y la plataforma pierde el recorrido que justifica su propuesta de valor. |
| **What** | Comparar con 10 a 15 clientes, en sesión moderada y con orden alternado, dos recorridos en la web: simular directamente un crédito y generar primero la pre-evaluación (US15), que muestra el score, el Risk Tier y la capacidad máxima de endeudamiento y precarga la cuota máxima en el simulador (US17). Se registra quién completa cada paso, cuánto tarda y qué datos se resisten a ingresar. |
| **Hypothesis** | Se espera que al menos el 50% de los clientes que inician la pre-evaluación completen y guarden una simulación y que el tiempo para llegar a una simulación viable se reduzca en 35% frente al recorrido sin pre-evaluación. |

| Question | ¿Aumentarán los envíos a evaluación de la entidad financiera si el cliente puede comparar cotizaciones multi-banco y enviar la oferta elegida desde el mismo cuadro? (Web) |
| --- | --- |
| **Why** | Los compradores entrevistados dedican tiempo a comparar opciones de financiamiento y piden información crediticia. El cuadro multi-banco (US19) existe, pero el cliente debe volver a simular para enviar la oferta, lo que puede cortar el recorrido antes de la evaluación oficial. |
| **What** | Comparar con 15 a 20 clientes, en sesión moderada, la versión actual del cuadro multi-banco con una versión que permite guardar y enviar a evaluación la oferta elegida desde el mismo cuadro, y medir la proporción de participantes que envía su simulación y el tiempo hasta hacerlo. |
| **Hypothesis** | Se espera que al menos el 30% de las simulaciones guardadas se envíen a evaluación de una entidad financiera con la versión nueva y que la proporción de clientes que envían su simulación aumente en 25% frente a la versión actual. |

| Question | ¿Están las concesionarias dispuestas a pagar una membresía mensual y a iniciar un piloto con la propuesta actual? (Web) |
| --- | --- |
| **Why** | La sostenibilidad del negocio (retención ≥ 80% y churn < 5%) depende de que las concesionarias paguen. Las entrevistas validaron el problema de rotación y exposición del inventario, pero no la disposición de pago, y Stripe, los planes y la selección obligatoria de membresía (US28) ya existen en el producto. |
| **What** | Agregar un botón "Solicitar demo" con formulario breve en la sección de planes de la Landing Page (*fake door*) con dos o tres niveles de precio, y realizar entrevistas de 20 minutos con 6 concesionarias (3 de nuevos y 3 de usados) para probar los precios y ofrecer un piloto de 30 días. |
| **Hypothesis** | Se espera que al menos el 50% de las concesionarias entrevistadas acepten un piloto de 30 días y que una de cada tres deje una solicitud de demo o contratación tras ver el precio. |

| Question | ¿Actuarán las concesionarias sobre las estadísticas por vehículo y los datos de contacto de los clientes que simularon, ajustando precios y contactándolos? (Web) |
| --- | --- |
| **Why** | Las concesionarias de usados buscan rotar su inventario y las de nuevos reducir su costo de prospección. El panel de estadísticas (US29) y los datos de contacto del cliente (US39) son el principal beneficio de la membresía, pero no sabemos si generan acciones. |
| **What** | Entregar durante 3 semanas a 4 a 6 concesionarias, con un resumen semanal por correo armado por el equipo, las vistas y simulaciones por vehículo y los clientes que simularon sobre sus unidades. Al final se registra cuántas ajustaron un precio, contactaron a un cliente o marcaron un vehículo como vendido. |
| **Hypothesis** | Se espera que al menos el 70% de las concesionarias participantes actúen sobre al menos un vehiculo cada semana y que el número de simulaciones por vehículo publicado aumente en 20% frente a la semana previa al piloto. |

| Question | ¿Se responderán más consultas en menos de una hora si el cliente puede conversar por chat móvil con la concesionaria y con la entidad financiera? (Mobile) |
| --- | --- |
| **Why** | Los 9 entrevistados usan el smartphone como dispositivo principal y los compradores desean resolver dudas sobre disponibilidad y requisitos antes de decidir. La mensajería móvil (US42 a US49) es hoy la única función de la app, y de su uso depende que el móvil justifique su existencia. |
| **What** | Realizar un piloto de 2 semanas con 10 clientes, 3 concesionarias y 1 o 2 entidades financieras, que usan el chat móvil para consultas reales o de prueba sobre un vehículo y una simulación. Se miden las conversaciones iniciadas, el tiempo de primera respuesta y el porcentaje de consultas respondidas. |
| **Hypothesis** | Se espera que al menos el 60% de las consultas reciban respuesta en menos de una hora y que el 50% de los clientes con una evaluación en curso inicien un chat con la entidad financiera. |

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

| Atributo | Detalle de la Hipótesis: Experimento 5 (Chat móvil con tiempo de respuesta) |
| --- | --- |
| **Question** | ¿Se responderán más consultas en menos de una hora si el cliente puede conversar por chat móvil con la concesionaria y con la entidad financiera? |
| **Belief** | Creemos que, al ser el smartphone el dispositivo principal de los 9 entrevistados, un canal de mensajería móvil directo con la concesionaria y el banco permitirá resolver dudas sobre disponibilidad y requisitos con rapidez, antes de que el cliente decida. |
| **Hypothesis** | Al menos el 60% de las consultas iniciadas por chat móvil recibirán respuesta en menos de una hora, y el 50% de los clientes con una evaluación en curso iniciarán un chat con la entidad financiera. |
| **Null Hypothesis** | Menos del 60% de las consultas iniciadas por chat móvil recibirán respuesta en menos de una hora, o menos del 50% de los clientes con una evaluación en curso iniciarán un chat con la entidad financiera. |

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
| **4 (S)** | **Variación de Simulaciones por Vehículo Publicado** | Mide si las acciones de la concesionaria se traducen en mayor interés del cliente en sus unidades. | `((Simulaciones por vehículo en semana de piloto − Simulaciones por vehículo en semana previa) / Simulaciones por vehículo en semana previa) * 100` | Conteo de simulaciones por vehículo desde el panel de estadísticas (US29), comparando la semana previa con cada semana del piloto. | **≥ +20.0%** |
| **5 (P)** | **Tasa de Respuesta en Menos de 1 Hora** | Evalúa la capacidad real de concesionarias y bancos de responder por chat móvil, condición para que el canal sea útil. | `(Consultas con primera respuesta en menos de 60 minutos / Consultas iniciadas) * 100` | Marcas de tiempo del primer mensaje del cliente y de la primera respuesta, registradas en la mensajería móvil durante las 2 semanas del piloto. | **≥ 60.0%** |
| **5 (S)** | **Tasa de Inicio de Chat con la Entidad Financiera** | Mide si el cliente usa el chat como apoyo durante una evaluación en curso. | `(Clientes con evaluación en curso que inician un chat con la entidad / Clientes con evaluación en curso) * 100` | Cruce de conversaciones iniciadas con evaluaciones en curso en la base de datos del piloto. | **≥ 50.0%** |

### 8.2.3. Measures

Las variables cuantitativas empleadas para contrastar las hipótesis corresponden a los datos crudos recolectados en las sesiones moderadas, los pilotos y las entrevistas:

* **Clientes que inician la pre-evaluación, clientes que guardan una simulación y tiempo hasta la simulación guardada (con y sin pre-evaluación):** Datos base para la Tasa de Guardado de Simulación y la reducción del tiempo hasta una simulación viable.
* **Simulaciones guardadas, simulaciones enviadas a evaluación y participantes que envían, por versión del cuadro multi-banco:** Datos utilizados para calcular la Tasa de Envío a Evaluación y su variación frente a la versión actual.
* **Concesionarias entrevistadas, que aceptan el piloto y que dejan solicitud de demo tras ver el precio:** Datos para la Tasa de Aceptación del Piloto y la Tasa de Solicitud de Demo o Contratación.
* **Acciones semanales por concesionaria (ajuste de precio, contacto, vehículo vendido) y simulaciones por vehículo publicado:** Datos para la Tasa de Acción Semanal y la variación de simulaciones por vehículo.
* **Consultas iniciadas por chat, marcas de tiempo de primera respuesta y clientes con evaluación en curso que inician chat con la entidad:** Datos para la Tasa de Respuesta en Menos de 1 Hora y la Tasa de Inicio de Chat con la Entidad Financiera.

### 8.2.4. Conditions

* **Condición Experimental (Grupo Expuesto):** Segmento de clientes y concesionarias que usa las funcionalidades nuevas de SmartFinance Drive: la pre-evaluación previa a la simulación con cuota máxima precargada, el envío a evaluación desde el cuadro multi-banco, el piloto de membresía con el botón "Solicitar demo", el resumen semanal de estadísticas por vehículo y el chat móvil con contexto de vehículo y simulación.
* **Condición de Control (Grupo Base):** Segmento que usa la versión actual de la plataforma, en la que el cliente simula directamente sin pre-evaluación, debe volver a simular para enviar su oferta desde el cuadro multi-banco, la concesionaria opera sin resumen de estadísticas (línea base de la semana previa) y no existe un piloto de membresía ni chat móvil piloto. En los experimentos 3 y 5, que son pruebas de validación sin control paralelo, el resultado se compara contra el umbral definido en la hipótesis.

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
| **Experimento 5: Chat móvil con tiempo de respuesta** | Creemos que el chat móvil permitirá resolver consultas con rapidez. Sabremos que esto es cierto cuando el 60% de las consultas reciba respuesta en menos de una hora. | Menos del 40%. | Entre 40% y 59%. | **60%.** | Más del 75%. (X) |

### 8.2.6. Methods Selection

| Herramienta | Precio | Capacidad de Análisis | Sencillez | Ventajas para SmartFinance Drive |
| --- | --- | --- | --- | --- |
| **Google Lighthouse** | Acceso gratuito. | Auditorías automatizadas de rendimiento, accesibilidad y buenas prácticas de la versión web. | Ejecución sencilla desde Chrome DevTools. | Verifica que la pre-evaluación, el simulador y el cuadro multi-banco carguen con rapidez en el celular, para que la lentitud técnica no se confunda con abandono por desconfianza. |
| **Google Analytics 4** | Acceso gratuito. | Rastreo de eventos personalizados y de embudos de conversión en la web. | Nivel de aprendizaje moderado. | Permite medir el recorrido del cliente (pre-evaluación, simulación guardada y envío a evaluación) y calcular la Tasa de Guardado y la Tasa de Envío a Evaluación. |
| **Registros del backend (base de datos propia)** | Incluido en la infraestructura existente. | Conteo exacto de simulaciones, envíos a evaluación, acciones de concesionarias y marcas de tiempo de mensajes. | Consultas directas sin configuración adicional. | Es la fuente más confiable para las métricas de los experimentos 2, 4 y 5, incluido el tiempo de primera respuesta en el chat móvil, donde GA4 no aplica. |

### 8.2.7. Data Analytics: Goals, KPIs and Metrics Selection

Dado que SmartFinance Drive se usa principalmente desde el celular, la calidad técnica de la web es una condición necesaria para que el abandono medido en los experimentos se deba a la propuesta y no a fallas técnicas. Se ejecutó una auditoría con Google Lighthouse en perfil móvil emulado (4G lento) sobre la pantalla pública de inicio de sesión:

* **Ruta bajo evaluación:** `https://smartfinance-drive-webapp.vercel.app/` (Perfil Móvil)
* **Performance (Rendimiento):** 97/100. FCP y LCP de 1.5 s, TBT de 110 ms y CLS de 0.001, dentro del rango óptimo.
* **Accessibility (Accesibilidad):** 88/100. Se detectaron contraste insuficiente y ausencia de un *main landmark*, puntos que se corregirán.
* **Best Practices (Buenas Prácticas):** 100/100. Cumple las verificaciones de seguridad y compatibilidad evaluadas.
* **SEO:** 91/100. Solo se identificó la falta de meta descripción.
