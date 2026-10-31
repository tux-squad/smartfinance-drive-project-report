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

**Claims (Afirmaciones):**

* Una pre-evaluación previa reducirá el abandono y permitirá que al menos 50% de los clientes que la inician guarden una simulación.
* Las concesionarias pagarán la membresía solo si las estadísticas y los contactos les permiten reducir el tiempo de rotación de su inventario.
* Responder en menos de una hora por chat aumenta el envío de simulaciones a evaluación.

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
| **Hypothesis** | Se espera que al menos el 70% de las concesionarias participantes actúen sobre al menos un vehículo cada semana y que el número de simulaciones por vehículo publicado aumente en 20% frente a la semana previa al piloto. |

| Question | ¿Se responderán más consultas en menos de una hora si el cliente puede conversar por chat móvil con la concesionaria y con la entidad financiera? (Mobile) |
| --- | --- |
| **Why** | Los 9 entrevistados usan el smartphone como dispositivo principal y los compradores desean resolver dudas sobre disponibilidad y requisitos antes de decidir. La mensajería móvil (US42 a US49) es hoy la única función de la app, y de su uso depende que el móvil justifique su existencia. |
| **What** | Realizar un piloto de 2 semanas con 10 clientes, 3 concesionarias y 1 o 2 entidades financieras, que usan el chat móvil para consultas reales o de prueba sobre un vehículo y una simulación. Se miden las conversaciones iniciadas, el tiempo de primera respuesta y el porcentaje de consultas respondidas. |
| **Hypothesis** | Se espera que al menos el 60% de las consultas reciban respuesta en menos de una hora y que el 50% de los clientes con una evaluación en curso inicien un chat con la entidad financiera. |

---
