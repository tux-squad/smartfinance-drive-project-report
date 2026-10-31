## 2.4. Ubiquitous Language

En este glosario solo se incluyen términos del dominio y se excluyen los términos técnicos del área de ingeniería de software. Tal como señala Eric Evans sobre Ubiquitous Language en su libro *Domain-Driven Design: Tackling Complexity in the Heart of Software*, establecer este lenguaje común aborda la complejidad en el núcleo del sistema. 

* **Balloon Payment (Cuota balón):** Pago final de mayor monto que se difiere al término del plazo del crédito para reducir las cuotas mensuales; se contrasta con el valor proyectado del vehículo por depreciación.
* **Budget (Presupuesto mensual):** Monto máximo de dinero que un comprador está dispuesto y es capaz de destinar mes a mes para pagar la cuota de un crédito automotriz.
* **CAC (Customer Acquisition Cost / Costo de Adquisición de Clientes):** Métrica comercial que representa el gasto total en publicidad y marketing dividido por la cantidad de clientes (o prospectos) generados en los canales digitales.
* **Days-on-lot (Días en patio):** Métrica que cuantifica la cantidad de días que un vehículo permanece inmovilizado en el inventario o salón de la concesionaria antes de concretarse su venta.
* **Dealership (Concesionaria):** Establecimiento comercial, formalmente constituido, que se dedica a la exhibición y venta de vehículos nuevos (distribuidor oficial) o seminuevos/usados.
* **Depreciation (Devaluación / Depreciación):** Concepto contable y comercial que refleja la pérdida del valor de un vehículo a lo largo del tiempo, estimado en hasta un 20% al segundo año de antigüedad.
* **Down Payment (Cuota inicial):** Monto de dinero que el comprador paga por adelantado al contado al momento de adquirir el vehículo, determinando así el saldo restante a financiar.
* **DTI (Debt-to-Income / Relación deuda-ingreso):** Indicador que expresa la proporción de los ingresos mensuales del cliente que se destina al pago de deudas, incluida la cuota del crédito simulado.
* **Financial Institution (Entidad financiera):** Banco o institución registrada en la plataforma, previa validación de su RUC, que publica sus condiciones de financiamiento (TEA/TNA, cuota inicial, seguros) y realiza la evaluación oficial de las simulaciones que recibe.
* **French Method / Payment Schedule (Cronograma de pagos, método francés):** Calendario de cuotas constantes de un crédito en el que cada pago combina interés y amortización de capital, mostrando el saldo de la deuda periodo a periodo.
* **Inventory Turnover (Rotación de inventario):** Métrica de negocio que indica la velocidad con la que los vehículos de una concesionaria son vendidos y reemplazados por nuevo stock, impactando directamente en el flujo de caja.
* **Lead (Prospecto comercial):** Contacto de un cliente que simuló un crédito sobre un vehículo de la concesionaria y cuyos datos de contacto quedan disponibles para ella.
* **Membership (Membresía):** Plan de suscripción obligatorio, pagado mediante Stripe, que habilita a una concesionaria a publicar sus vehículos y acceder al panel de estadísticas.
* **Official Evaluation (Evaluación oficial):** Resolución (aprobado o rechazado, con notas) que emite la entidad financiera sobre una simulación de crédito. La decisión crediticia corresponde exclusivamente al banco, no a la plataforma.
* **Risk Pre-assessment (Pre-evaluación de riesgo):** Análisis que realiza la plataforma a partir del perfil socioeconómico del cliente y que arroja un puntaje (score), el indicador DTI y un Risk Tier (A, B o C). Es una estimación referencial de viabilidad; no constituye una aprobación de crédito.
* **Risk Tier (Nivel de riesgo):** Clasificación A, B o C del cliente resultante de la pre-evaluación de riesgo, en función de su score y de su DTI.
* **Simulation (Simulación):** Cálculo de un crédito vehicular (cuota, TCEA, TIR, VAN y cronograma) para un vehículo y una entidad financiera, que el cliente puede guardar, comparar y consultar posteriormente.
* **TCEA (Tasa de Costo Efectivo Anual):** Tasa que refleja el costo total anual del crédito, incluyendo intereses, comisiones y seguros.
* **TIR (Tasa Interna de Retorno):** Tasa de descuento que iguala el valor presente de los flujos del crédito con el monto financiado; se utiliza en la simulación para expresar el costo efectivo del financiamiento.
* **VAN (Valor Actual Neto):** Valor presente de los flujos de pago del crédito descontados a una tasa de referencia.
