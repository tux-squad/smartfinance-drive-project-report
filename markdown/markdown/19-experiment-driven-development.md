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
  
