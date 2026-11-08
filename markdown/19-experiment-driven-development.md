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
