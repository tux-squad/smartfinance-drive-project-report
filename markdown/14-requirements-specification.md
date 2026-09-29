# Capítulo III: Requirements Specification

## 3.1. To-Be Scenario Mapping

**Segmento 1: Compradores interesados**

![to-be-scenario-mapping-segmento-1](../assets/Chapter-3/to-be-scenario-mapping-segmento-1.png)

**Segmento 2: Concesionarias de vehículos nuevos**

![to-be-scenario-mapping-segmento-2](../assets/Chapter-3/to-be-scenario-mapping-segmento-2.png)

**Segmento 3: Concesionarias de vehículos usados**

![to-be-scenario-mapping-segmento-3](../assets/Chapter-3/to-be-scenario-mapping-segmento-3.png)

* **Enlace interactivo del tablero en Miro:** [https://miro.com/app/board/uXjVHpkhWe4=/?share_link_id=221895309503](https://miro.com/app/board/uXjVHpkhWe4=/?share_link_id=221895309503)

## 3.2. User Stories

En esta sección se definen los requisitos funcionales, no funcionales y técnicos de SmartFinance Drive mediante un conjunto estructurado de Epics y User Stories. La redacción contempla los tres segmentos objetivo (Compradores, Concesionarias de nuevos y Concesionarias de usados), así como las historias técnicas necesarias para la viabilidad de la plataforma.

| **US-01** | **Registro de cuenta y perfil personal** |
| :--- | :--- |
| **User** | Visitante |
| **Priority** | Alta |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Visitante, quiero crear una cuenta ingresando mi correo, contraseña y datos personales básicos desde la aplicación web, para acceder a la plataforma como Cliente y contar con un perfil inicial. |
| **Acceptance Criteria** | **Escenario 1 — Registro exitoso**<br>**Dado** que el visitante se encuentra en el formulario de registro,<br>**Cuando** ingresa un correo válido, una contraseña y los datos personales obligatorios y confirma el registro,<br>**Entonces** la plataforma crea su cuenta y muestra una confirmación.<br><br>**Escenario 2 — Registro con datos inválidos o duplicados**<br>**Dado** que el visitante intenta registrarse con datos obligatorios incompletos o un correo ya registrado,<br>**Cuando** envía el formulario,<br>**Entonces** la plataforma impide el registro e informa qué dato debe corregir. |

<br>

| **US-02** | **Inicio de sesión** |
| :--- | :--- |
| **User** | Usuario Registrado |
| **Priority** | Alta |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Usuario Registrado, quiero iniciar sesión con mis credenciales, para acceder a las funcionalidades correspondientes a mi rol. |
| **Acceptance Criteria** | **Escenario 1 — Inicio de sesión exitoso**<br>**Dado** que el usuario registrado tiene credenciales válidas,<br>**Cuando** ingresa su correo y contraseña y selecciona iniciar sesión,<br>**Entonces** accede a la plataforma con los permisos correspondientes a su rol.<br><br>**Escenario 2 — Inicio de sesión con credenciales inválidas**<br>**Dado** que el usuario ingresa credenciales incorrectas o incompletas,<br>**Cuando** intenta iniciar sesión,<br>**Entonces** el acceso es rechazado y se muestra un mensaje de error sin revelar información sensible. |

<br>

| **US-03** | **Cierre de sesión** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Alta |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Usuario Autenticado, quiero cerrar sesión desde cualquier pantalla, para proteger mi cuenta y finalizar mi acceso a la plataforma. |
| **Acceptance Criteria** | **Escenario 1 — Cierre de sesión exitoso**<br>**Dado** que el usuario tiene una sesión activa,<br>**Cuando** selecciona cerrar sesión desde cualquier pantalla web o móvil,<br>**Entonces** la sesión finaliza y se le redirige a la pantalla de acceso.<br><br>**Escenario 2 — Acceso después del cierre de sesión**<br>**Dado** que el usuario cerró sesión,<br>**Cuando** intenta acceder a una funcionalidad protegida usando la sesión anterior,<br>**Entonces** la plataforma solicita autenticarse nuevamente. |

<br>

| **US-04** | **Cambiar contraseña** |
| :--- | :--- |
| **User** | Usuario Registrado |
| **Priority** | Alta |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Usuario Registrado, quiero cambiar mi contraseña desde la configuración de mi cuenta, para mantener protegido mi acceso. |
| **Acceptance Criteria** | **Escenario 1 — Cambio de contraseña exitoso**<br>**Dado** que el usuario está autenticado y accede a la configuración de su cuenta,<br>**Cuando** ingresa su contraseña actual y una nueva contraseña válida y confirma el cambio,<br>**Entonces** la plataforma actualiza sus credenciales y confirma la operación.<br><br>**Escenario 2 — Cambio de contraseña rechazado**<br>**Dado** que la contraseña actual es incorrecta o la nueva contraseña no cumple las reglas establecidas,<br>**Cuando** intenta guardar el cambio,<br>**Entonces** la plataforma conserva la contraseña anterior e informa el error. |

<br>

| **US-05** | **Edición y completitud de perfil** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Cliente, quiero actualizar mis datos de contacto y completar información adicional como mis ingresos desde la aplicación web, para mantener mi perfil actualizado. |
| **Acceptance Criteria** | **Escenario 1 — Actualización de perfil exitosa**<br>**Dado** que el cliente inició sesión y abrió la edición de perfil,<br>**Cuando** actualiza sus datos de contacto o ingresos con información válida y guarda los cambios,<br>**Entonces** el perfil muestra la información actualizada.<br><br>**Escenario 2 — Actualización con información inválida**<br>**Dado** que el cliente ingresa información inválida en un campo editable,<br>**Cuando** intenta guardar el perfil,<br>**Entonces** la plataforma señala los campos que debe corregir y no guarda los datos inválidos. |

<br>

| **US-06** | **Solicitud de rol Concesionaria** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Cliente, quiero solicitar el rol de Concesionaria ingresando mi RUC desde la aplicación web, para que la plataforma valide mi información y habilite las funciones correspondientes. |
| **Acceptance Criteria** | **Escenario 1 — Solicitud de rol registrada**<br>**Dado** que el cliente accede a la solicitud de rol Concesionaria,<br>**Cuando** ingresa su RUC y envía la solicitud,<br>**Entonces** la plataforma registra la solicitud y presenta su estado de validación.<br><br>**Escenario 2 — Solicitud de rol con RUC inválido**<br>**Dado** que el RUC ingresado no cumple el formato requerido o no supera la validación,<br>**Cuando** se envía la solicitud,<br>**Entonces** la plataforma informa el problema y no habilita las funciones de Concesionaria. |

<br>

| **US-07** | **Solicitud de rol Entidad Financiera** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Cliente, quiero solicitar el rol de Entidad Financiera ingresando mi RUC desde la aplicación web, para que la plataforma valide mi información y habilite las funciones financieras. |
| **Acceptance Criteria** | **Escenario 1 — Solicitud de rol financiero registrada**<br>**Dado** que el cliente accede a la solicitud de rol Entidad Financiera,<br>**Cuando** ingresa su RUC y envía la solicitud,<br>**Entonces** la plataforma registra la solicitud y presenta su estado de validación.<br><br>**Escenario 2 — Solicitud de rol financiero con RUC inválido**<br>**Dado** que el RUC ingresado no cumple el formato requerido o no supera la validación,<br>**Cuando** se envía la solicitud,<br>**Entonces** la plataforma informa el problema y no habilita las funciones financieras. |

<br>

| **US-08** | **Modificar roles de usuario** |
| :--- | :--- |
| **User** | Administrador |
| **Priority** | Alta |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Administrador, quiero asignar o modificar los roles de las cuentas registradas desde el backoffice de la aplicación web, para gestionar los permisos de los usuarios. |
| **Acceptance Criteria** | **Escenario 1 — Modificación de rol exitosa**<br>**Dado** que el administrador accede al backoffice y selecciona una cuenta registrada,<br>**Cuando** asigna o modifica su rol y confirma la operación,<br>**Entonces** la plataforma guarda el cambio de permisos.<br><br>**Escenario 2 — Modificación de rol no autorizada**<br>**Dado** que un usuario sin privilegios de administrador intenta modificar roles,<br>**Cuando** solicita la operación,<br>**Entonces** la plataforma deniega el acceso y mantiene los roles existentes. |

<br>

| **US-09** | **Resumen financiero del cliente** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Cliente, quiero visualizar un resumen de mi score crediticio, simulaciones y proyecciones desde la aplicación web, para consultar mi información financiera desde un solo lugar. |
| **Acceptance Criteria** | **Escenario 1 — Visualización del resumen financiero**<br>**Dado** que el cliente inició sesión y cuenta con información financiera disponible,<br>**Cuando** abre su dashboard,<br>**Entonces** visualiza en un solo lugar su score crediticio, simulaciones y proyecciones disponibles.<br><br>**Escenario 2 — Información financiera no disponible**<br>**Dado** que alguno de los datos financieros aún no está disponible,<br>**Cuando** el cliente consulta el dashboard,<br>**Entonces** la plataforma indica que no hay información para ese apartado sin mostrar datos incorrectos. |

<br>

| **US-10** | **Selección obligatoria de membresía B2B** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Concesionaria recién validada, quiero seleccionar un plan de membresía desde la aplicación web antes de utilizar las funciones B2B, para habilitar la gestión de mi inventario. |
| **Acceptance Criteria** | **Escenario 1 — Selección de membresía obligatoria**<br>**Dado** que una concesionaria fue validada y aún no tiene membresía,<br>**Cuando** intenta utilizar las funciones B2B,<br>**Entonces** la plataforma solicita seleccionar un plan antes de habilitar la gestión de inventario.<br><br>**Escenario 2 — Activación de funciones B2B**<br>**Dado** que la concesionaria selecciona un plan disponible y completa la confirmación requerida,<br>**Cuando** se registra la membresía,<br>**Entonces** la plataforma habilita las funciones B2B correspondientes al plan. |

<br>

| **US-11** | **Registrar entidad financiera** |
| :--- | :--- |
| **User** | Entidad Financiera |
| **Priority** | Alta |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Entidad Financiera, quiero registrar mis tasas, comisiones y condiciones crediticias desde la aplicación web, para ofrecer opciones de financiamiento a los compradores. |
| **Acceptance Criteria** | **Escenario 1 — Registro de condiciones crediticias exitoso**<br>**Dado** que la entidad financiera inició sesión y abrió el registro de condiciones crediticias,<br>**Cuando** ingresa tasas, comisiones y condiciones válidas y guarda,<br>**Entonces** la plataforma registra la información para ofrecer opciones de financiamiento.<br><br>**Escenario 2 — Registro con información inválida**<br>**Dado** que la entidad financiera omite un dato obligatorio o ingresa valores no válidos,<br>**Cuando** intenta guardar las condiciones,<br>**Entonces** la plataforma señala los errores y no registra información incompleta. |

<br>

| **US-12** | **Consultar plan de membresía** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Concesionaria, quiero consultar la información de mi plan de membresía desde la aplicación web, para conocer sus características, beneficios y vigencia. |
| **Acceptance Criteria** | **Escenario 1 — Consulta de membresía activa**<br>**Dado** que la concesionaria tiene una membresía registrada,<br>**Cuando** accede a la sección de su plan,<br>**Entonces** visualiza sus características, beneficios y vigencia.<br><br>**Escenario 2 — Consulta sin membresía activa**<br>**Dado** que la concesionaria no tiene una membresía activa,<br>**Cuando** consulta la sección de plan,<br>**Entonces** la plataforma informa que no existe un plan activo y muestra las opciones disponibles si corresponde. |

<br>

| **US-13** | **Cambiar plan de membresía** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Concesionaria, quiero cambiar mi plan de membresía desde la aplicación web, para adaptar mi suscripción a las necesidades de mi negocio. |
| **Acceptance Criteria** | **Escenario 1 — Cambio de plan exitoso**<br>**Dado** que la concesionaria tiene una membresía vigente,<br>**Cuando** selecciona otro plan disponible y confirma el cambio,<br>**Entonces** la plataforma registra la solicitud o actualización y muestra el plan resultante.<br><br>**Escenario 2 — Cambio de plan no disponible**<br>**Dado** que la concesionaria intenta cambiar a un plan no disponible o la operación no puede completarse,<br>**Cuando** confirma el cambio,<br>**Entonces** la plataforma informa el motivo y conserva la membresía vigente. |

<br>

| **US-14** | **Renovar membresía** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Concesionaria, quiero renovar mi membresía desde la aplicación web, para mantener activas las funcionalidades de mi plan. |
| **Acceptance Criteria** | **Escenario 1 — Renovación de membresía exitosa**<br>**Dado** que la concesionaria tiene una membresía próxima a vencer o vencida,<br>**Cuando** selecciona renovar y completa la confirmación requerida,<br>**Entonces** la plataforma registra la renovación y muestra la nueva vigencia.<br><br>**Escenario 2 — Renovación no completada**<br>**Dado** que la renovación no puede completarse,<br>**Cuando** la concesionaria intenta confirmarla,<br>**Entonces** la plataforma informa el resultado y no presenta la membresía como renovada. |

<br>

| **US-15** | **Listar inventario de vehículos** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero visualizar todos mis vehículos publicados desde la aplicación web, para consultar y controlar mi inventario. |
| **Acceptance Criteria** | **Escenario 1 — Visualización del inventario**<br>**Dado** que la concesionaria inició sesión y tiene vehículos registrados,<br>**Cuando** abre su inventario,<br>**Entonces** visualiza el listado de sus vehículos con la información disponible de cada uno.<br><br>**Escenario 2 — Inventario vacío**<br>**Dado** que la concesionaria aún no registra vehículos,<br>**Cuando** accede al inventario,<br>**Entonces** la plataforma muestra un estado vacío y la opción de registrar o publicar un vehículo. |

<br>

| **US-16** | **Publicar vehículo** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero publicar un vehículo con sus características y precio desde la aplicación web, para ofrecerlo en el catálogo. |
| **Acceptance Criteria** | **Escenario 1 — Publicación de vehículo exitosa**<br>**Dado** que la concesionaria cuenta con permisos para gestionar inventario,<br>**Cuando** completa las características y el precio obligatorios de un vehículo y confirma la publicación,<br>**Entonces** el vehículo se registra y aparece en el catálogo.<br><br>**Escenario 2 — Publicación con datos inválidos**<br>**Dado** que faltan datos obligatorios o existen valores inválidos,<br>**Cuando** la concesionaria intenta publicar el vehículo,<br>**Entonces** la plataforma señala los errores y no publica el registro. |

<br>

| **US-17** | **Editar vehículo publicado** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero actualizar el precio, las características y el estado de stock de un vehículo publicado desde la aplicación web, para mantener actualizado mi inventario. |
| **Acceptance Criteria** | **Escenario 1 — Edición de vehículo exitosa**<br>**Dado** que la concesionaria selecciona un vehículo de su inventario,<br>**Cuando** modifica su precio, características o stock con datos válidos y guarda,<br>**Entonces** el sistema actualiza la información publicada.<br><br>**Escenario 2 — Edición inválida o no autorizada**<br>**Dado** que la concesionaria intenta guardar cambios inválidos o sobre un vehículo que no le pertenece,<br>**Cuando** confirma la edición,<br>**Entonces** la plataforma rechaza la operación y conserva los datos existentes. |

<br>

| **US-18** | **Cambiar estado transaccional del vehículo** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero cambiar el estado comercial de un vehículo entre Disponible, Reservado y Vendido desde la aplicación web, para mantener actualizado su estado comercial. |
| **Acceptance Criteria** | **Escenario 1 — Cambio de estado exitoso**<br>**Dado** que la concesionaria selecciona un vehículo de su inventario,<br>**Cuando** cambia su estado comercial a Disponible, Reservado o Vendido y confirma,<br>**Entonces** el nuevo estado queda reflejado en el inventario.<br><br>**Escenario 2 — Cambio de estado inválido o no autorizado**<br>**Dado** que la concesionaria intenta asignar un estado distinto de los permitidos o modificar un vehículo ajeno,<br>**Cuando** confirma la operación,<br>**Entonces** la plataforma rechaza el cambio. |

<br>

| **US-19** | **Eliminar vehículo** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero eliminar un vehículo de mi inventario desde la aplicación web, para retirarlo del catálogo. |
| **Acceptance Criteria** | **Escenario 1 — Eliminación de vehículo confirmada**<br>**Dado** que la concesionaria selecciona un vehículo de su inventario,<br>**Cuando** confirma su eliminación,<br>**Entonces** el vehículo deja de aparecer en su inventario y en el catálogo publicado.<br><br>**Escenario 2 — Cancelación de eliminación**<br>**Dado** que la concesionaria cancela la confirmación de eliminación,<br>**Cuando** vuelve al inventario,<br>**Entonces** el vehículo permanece registrado sin cambios. |

<br>

| **US-20** | **Proyectar depreciación del vehículo** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero consultar la proyección de depreciación de un vehículo a 2, 3 y 5 años desde la aplicación web, para evaluar su valor a futuro. |
| **Acceptance Criteria** | **Escenario 1 — Proyección de depreciación disponible**<br>**Dado** que la concesionaria consulta un vehículo con información suficiente,<br>**Cuando** solicita la proyección de depreciación,<br>**Entonces** la plataforma presenta los valores estimados para los horizontes de 2, 3 y 5 años.<br><br>**Escenario 2 — Información insuficiente para proyectar**<br>**Dado** que el vehículo no cuenta con información suficiente para calcular la proyección,<br>**Cuando** la concesionaria solicita el cálculo,<br>**Entonces** la plataforma informa qué información falta y no presenta estimaciones como definitivas. |

<br>

| **US-21** | **Panel de estadísticas del concesionario** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero consultar estadísticas de mis vehículos, como vistas y simulaciones, desde la aplicación web, para conocer el interés generado por mi inventario. |
| **Acceptance Criteria** | **Escenario 1 — Visualización de estadísticas**<br>**Dado** que la concesionaria tiene vehículos publicados con actividad registrada,<br>**Cuando** abre su panel de estadísticas,<br>**Entonces** visualiza las métricas disponibles de vistas y simulaciones de su inventario.<br><br>**Escenario 2 — Sin actividad registrada**<br>**Dado** que todavía no existe actividad registrada,<br>**Cuando** consulta las estadísticas,<br>**Entonces** la plataforma muestra valores vacíos o cero claramente identificados. |

<br>

| **US-22** | **Ver datos de contacto de prospectos** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero consultar los datos de contacto de los clientes que realizaron simulaciones con mis vehículos desde la aplicación web, para poder contactarlos. |
| **Acceptance Criteria** | **Escenario 1 — Consulta de prospectos autorizados**<br>**Dado** que un cliente realizó una simulación asociada a un vehículo de la concesionaria,<br>**Cuando** la concesionaria consulta los prospectos,<br>**Entonces** puede visualizar los datos de contacto permitidos para esos clientes.<br><br>**Escenario 2 — Consulta de prospectos no autorizada**<br>**Dado** que la concesionaria intenta consultar prospectos que no corresponden a su inventario o no tiene permisos,<br>**Cuando** solicita los datos,<br>**Entonces** la plataforma deniega el acceso. |

<br>

| **US-23** | **Búsqueda y filtrado de vehículos** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Exploración y comparación de vehículos |
| **Description** | Como Cliente, quiero buscar vehículos utilizando filtros como marca, precio, año y condición desde la aplicación web, para encontrar opciones que se ajusten a mis necesidades. |
| **Acceptance Criteria** | **Escenario 1 — Búsqueda con resultados**<br>**Dado** que el cliente abre el catálogo de vehículos,<br>**Cuando** introduce filtros de marca, precio, año o condición,<br>**Entonces** la plataforma muestra los vehículos que cumplen los criterios seleccionados.<br><br>**Escenario 2 — Búsqueda sin resultados**<br>**Dado** que ningún vehículo coincide con los filtros aplicados,<br>**Cuando** se ejecuta la búsqueda,<br>**Entonces** la plataforma informa que no hay resultados y permite modificar o limpiar los filtros. |

<br>

| **US-24** | **Filtrar catálogo por concesionaria** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Exploración y comparación de vehículos |
| **Description** | Como Cliente, quiero filtrar los vehículos por concesionaria desde la aplicación web, para consultar únicamente el inventario de un distribuidor específico. |
| **Acceptance Criteria** | **Escenario 1 — Filtrado por concesionaria exitoso**<br>**Dado** que el cliente consulta el catálogo,<br>**Cuando** selecciona una concesionaria como filtro,<br>**Entonces** la plataforma muestra únicamente los vehículos asociados a esa concesionaria.<br><br>**Escenario 2 — Concesionaria sin vehículos disponibles**<br>**Dado** que la concesionaria seleccionada no tiene vehículos publicados disponibles,<br>**Cuando** se aplica el filtro,<br>**Entonces** la plataforma muestra un resultado vacío informativo. |

<br>

| **US-25** | **Ver detalle de vehículo** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Exploración y comparación de vehículos |
| **Description** | Como Cliente, quiero consultar la información detallada de un vehículo desde la aplicación web, para conocer sus características antes de iniciar una simulación. |
| **Acceptance Criteria** | **Escenario 1 — Visualización del detalle del vehículo**<br>**Dado** que el cliente selecciona un vehículo del catálogo,<br>**Cuando** abre su ficha,<br>**Entonces** visualiza la información detallada disponible para evaluar el vehículo antes de simular un crédito.<br><br>**Escenario 2 — Vehículo no disponible**<br>**Dado** que el vehículo ya no está disponible o su ficha no puede cargarse,<br>**Cuando** el cliente intenta consultarla,<br>**Entonces** la plataforma informa la situación y evita mostrar información desactualizada como vigente. |

<br>

| **US-26** | **Ver datos de contacto de la concesionaria** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Exploración y comparación de vehículos |
| **Description** | Como Cliente, quiero consultar los datos de contacto de la concesionaria desde la ficha del vehículo en la aplicación web, para poder comunicarme con el vendedor. |
| **Acceptance Criteria** | **Escenario 1 — Visualización de datos de contacto**<br>**Dado** que el cliente se encuentra en la ficha de un vehículo publicado por una concesionaria,<br>**Cuando** consulta la sección de contacto,<br>**Entonces** visualiza los datos de contacto habilitados de dicha concesionaria.<br><br>**Escenario 2 — Datos de contacto no disponibles**<br>**Dado** que no existen datos de contacto disponibles para la concesionaria,<br>**Cuando** el cliente abre esa sección,<br>**Entonces** la plataforma informa que los datos no están disponibles. |

<br>

| **US-27** | **Comparar vehículos** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Exploración y comparación de vehículos |
| **Description** | Como Cliente, quiero comparar hasta dos vehículos desde la aplicación web, para consultar sus principales características y costos de forma conjunta. |
| **Acceptance Criteria** | **Escenario 1 — Comparación de dos vehículos**<br>**Dado** que el cliente selecciona dos vehículos para comparar,<br>**Cuando** abre la comparación,<br>**Entonces** la plataforma presenta conjuntamente sus principales características y costos.<br><br>**Escenario 2 — Límite de vehículos para comparación**<br>**Dado** que el cliente intenta agregar un tercer vehículo o seleccionar menos de dos vehículos,<br>**Cuando** solicita la comparación,<br>**Entonces** la plataforma mantiene el límite de dos y solicita completar la selección requerida. |

<br>

| **US-28** | **Pre-evaluación de riesgo crediticio** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Simulación y evaluación crediticia |
| **Description** | Como Cliente, quiero generar una pre-evaluación crediticia basada en mis ingresos y deudas desde la aplicación web, para conocer mi capacidad de endeudamiento antes de solicitar un crédito. |
| **Acceptance Criteria** | **Escenario 1 — Pre-evaluación crediticia exitosa**<br>**Dado** que el cliente ingresa sus ingresos y deudas requeridos,<br>**Cuando** solicita la pre-evaluación crediticia,<br>**Entonces** la plataforma calcula y presenta el resultado estimado de su capacidad de endeudamiento.<br><br>**Escenario 2 — Pre-evaluación con datos incompletos o inválidos**<br>**Dado** que el cliente omite datos requeridos o ingresa valores inválidos,<br>**Cuando** solicita la pre-evaluación,<br>**Entonces** la plataforma señala los campos que debe corregir y no genera un resultado basado en datos incompletos. |

<br>

| **US-29** | **Crear simulación de crédito vehicular** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Simulación y evaluación crediticia |
| **Description** | Como Cliente, quiero simular un crédito indicando el vehículo, entidad financiera, cuota inicial y plazo desde la aplicación web, para conocer las condiciones estimadas de pago. |
| **Acceptance Criteria** | **Escenario 1 — Simulación de crédito exitosa**<br>**Dado** que el cliente selecciona un vehículo y una entidad financiera e ingresa cuota inicial y plazo válidos,<br>**Cuando** ejecuta la simulación,<br>**Entonces** la plataforma presenta las condiciones estimadas de pago.<br><br>**Escenario 2 — Simulación con datos inválidos**<br>**Dado** que faltan datos requeridos o la cuota inicial o el plazo no son válidos,<br>**Cuando** el cliente intenta simular,<br>**Entonces** la plataforma informa los errores y no genera la simulación. |

<br>

| **US-30** | **Ver cronograma detallado de pagos** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Simulación y evaluación crediticia |
| **Description** | Como Cliente, quiero consultar el cronograma detallado de una simulación desde la aplicación web, para conocer la distribución de mis pagos durante el crédito. |
| **Acceptance Criteria** | **Escenario 1 — Visualización del cronograma**<br>**Dado** que el cliente tiene una simulación registrada,<br>**Cuando** consulta su cronograma,<br>**Entonces** visualiza el detalle de los pagos y su distribución durante el crédito.<br><br>**Escenario 2 — Cronograma no disponible**<br>**Dado** que la simulación no tiene un cronograma disponible,<br>**Cuando** el cliente intenta consultarlo,<br>**Entonces** la plataforma informa que no es posible mostrar el detalle. |

<br>

| **US-31** | **Descargar resumen de simulación en PDF** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Simulación y evaluación crediticia |
| **Description** | Como Cliente, quiero descargar mi simulación financiera en formato PDF desde la aplicación web, para conservarla como documento. |
| **Acceptance Criteria** | **Escenario 1 — Descarga de simulación en PDF exitosa**<br>**Dado** que el cliente cuenta con una simulación disponible,<br>**Cuando** selecciona descargar el resumen en PDF,<br>**Entonces** la plataforma genera y entrega un documento legible con la información de esa simulación.<br><br>**Escenario 2 — Error al generar el PDF**<br>**Dado** que ocurre un error al generar el PDF,<br>**Cuando** el cliente solicita la descarga,<br>**Entonces** la plataforma informa que no pudo completarse y permite volver a intentarlo. |

<br>

| **US-32** | **Ver y eliminar simulaciones guardadas** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Simulación y evaluación crediticia |
| **Description** | Como Cliente, quiero consultar y eliminar mis simulaciones guardadas desde la aplicación web, para mantener organizado mi historial. |
| **Acceptance Criteria** | **Escenario 1 — Consulta y eliminación de simulación**<br>**Dado** que el cliente tiene simulaciones guardadas,<br>**Cuando** abre su historial,<br>**Entonces** visualiza sus simulaciones y puede seleccionar una para eliminarla.<br><br>**Escenario 2 — Cancelación de eliminación**<br>**Dado** que el cliente confirma la eliminación de una simulación propia,<br>**Cuando** se completa la operación,<br>**Entonces** esta deja de aparecer en su historial; si cancela, permanece guardada. |

<br>

| **US-33** | **Filtrar simulaciones por estado** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Simulación y evaluación crediticia |
| **Description** | Como Cliente, quiero filtrar mis simulaciones por estado desde la aplicación web, para localizar rápidamente las que están pendientes, aprobadas o rechazadas. |
| **Acceptance Criteria** | **Escenario 1 — Filtrado de simulaciones por estado**<br>**Dado** que el cliente tiene simulaciones con distintos estados,<br>**Cuando** selecciona un estado como filtro,<br>**Entonces** la plataforma muestra únicamente las simulaciones que coinciden.<br><br>**Escenario 2 — Filtro sin resultados**<br>**Dado** que ninguna simulación coincide con el estado seleccionado,<br>**Cuando** se aplica el filtro,<br>**Entonces** la plataforma muestra un mensaje de ausencia de resultados. |

<br>

| **US-34** | **Cancelar simulación guardada** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Simulación y evaluación crediticia |
| **Description** | Como Cliente, quiero cancelar una simulación que esté pendiente de revisión desde la aplicación web, para detener el proceso de solicitud de crédito. |
| **Acceptance Criteria** | **Escenario 1 — Cancelación de simulación exitosa**<br>**Dado** que el cliente tiene una simulación pendiente de revisión,<br>**Cuando** selecciona cancelarla y confirma la acción,<br>**Entonces** la plataforma actualiza su estado a cancelada.<br><br>**Escenario 2 — Cancelación no permitida o cancelada por el usuario**<br>**Dado** que la simulación no está pendiente o el cliente cancela la confirmación,<br>**Cuando** intenta cancelar,<br>**Entonces** la plataforma no modifica su estado. |

<br>

| **US-35** | **Ver solicitudes de crédito entrantes** |
| :--- | :--- |
| **User** | Entidad Financiera |
| **Priority** | Alta |
| **Epic** | Evaluación y gestión de solicitudes de crédito |
| **Description** | Como Entidad Financiera, quiero consultar las solicitudes de crédito recibidas desde la aplicación web, para gestionar y priorizar su revisión. |
| **Acceptance Criteria** | **Escenario 1 — Visualización de solicitudes recibidas**<br>**Dado** que la entidad financiera inició sesión y tiene solicitudes recibidas,<br>**Cuando** abre la bandeja de solicitudes,<br>**Entonces** visualiza las solicitudes disponibles para su revisión.<br><br>**Escenario 2 — Bandeja de solicitudes vacía**<br>**Dado** que no existen solicitudes entrantes,<br>**Cuando** la entidad financiera consulta la bandeja,<br>**Entonces** la plataforma muestra un estado vacío informativo. |

<br>

| **US-36** | **Evaluación oficial de solicitud de crédito** |
| :--- | :--- |
| **User** | Entidad Financiera |
| **Priority** | Alta |
| **Epic** | Evaluación y gestión de solicitudes de crédito |
| **Description** | Como Entidad Financiera, quiero revisar una solicitud de crédito y registrar su resultado como Aprobada o Rechazada desde la aplicación web, para formalizar la evaluación. |
| **Acceptance Criteria** | **Escenario 1 — Evaluación oficial registrada**<br>**Dado** que la entidad financiera abre una solicitud que puede evaluar,<br>**Cuando** registra el resultado Aprobada o Rechazada y confirma,<br>**Entonces** la plataforma guarda la decisión y actualiza el estado de la solicitud.<br><br>**Escenario 2 — Evaluación no autorizada o inválida**<br>**Dado** que el usuario no pertenece a la entidad financiera autorizada o no selecciona un resultado válido,<br>**Cuando** intenta registrar la evaluación,<br>**Entonces** la plataforma rechaza la operación. |

<br>

| **US-37** | **Notificación del resultado de evaluación** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Evaluación y gestión de solicitudes de crédito |
| **Description** | Como Cliente, quiero recibir automáticamente por correo el resultado de la evaluación crediticia en formato PDF, para conservar un registro de la decisión de la entidad financiera. |
| **Acceptance Criteria** | **Escenario 1 — Notificación de evaluación enviada**<br>**Dado** que una entidad financiera registra el resultado de evaluación de una solicitud,<br>**Cuando** el proceso de notificación se ejecuta,<br>**Entonces** el cliente recibe un correo con el resultado y el PDF correspondiente.<br><br>**Escenario 2 — Fallo en la notificación**<br>**Dado** que el envío del correo o la generación del PDF falla,<br>**Cuando** se procesa la notificación,<br>**Entonces** el sistema registra o comunica el fallo para permitir su seguimiento y reintento. |

<br>

| **US-38** | **Ver estado de solicitudes desde la aplicación móvil** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Evaluación y gestión de solicitudes de crédito |
| **Description** | Como Cliente, quiero consultar el estado de mis solicitudes de crédito desde la aplicación móvil nativa, para conocer si están pendientes, aprobadas o rechazadas. |
| **Acceptance Criteria** | **Escenario 1 — Visualización del estado de solicitudes**<br>**Dado** que el cliente inició sesión en la aplicación móvil,<br>**Cuando** abre sus solicitudes de crédito,<br>**Entonces** visualiza el estado de cada solicitud como pendiente, aprobada o rechazada.<br><br>**Escenario 2 — Cliente sin solicitudes registradas**<br>**Dado** que el cliente no tiene solicitudes registradas,<br>**Cuando** accede a esa sección móvil,<br>**Entonces** la aplicación muestra un estado vacío informativo. |

<br>

| **US-39** | **Bandeja de Inbox y conversaciones activas** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Alta |
| **Epic** | Mensajería y comunicación |
| **Description** | Como Usuario Autenticado, quiero consultar un Inbox con mis conversaciones activas desde la aplicación móvil nativa, para acceder rápidamente a mis chats pendientes. |
| **Acceptance Criteria** | **Escenario 1 — Visualización de conversaciones activas**<br>**Dado** que el usuario autenticado abre el Inbox en la aplicación móvil,<br>**Cuando** existen conversaciones activas,<br>**Entonces** visualiza la lista de conversaciones para acceder a ellas.<br><br>**Escenario 2 — Inbox sin conversaciones activas**<br>**Dado** que el usuario no tiene conversaciones activas,<br>**Cuando** abre el Inbox,<br>**Entonces** la aplicación muestra un estado vacío y una indicación para iniciar una conversación si corresponde. |

<br>

| **US-40** | **Indicadores de mensajes no leídos** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Media |
| **Epic** | Mensajería y comunicación |
| **Description** | Como Usuario Autenticado, quiero visualizar indicadores de mensajes no leídos en mi Inbox desde la aplicación móvil nativa, para identificar rápidamente las conversaciones con nueva actividad. |
| **Acceptance Criteria** | **Escenario 1 — Visualización de mensajes no leídos**<br>**Dado** que una conversación contiene mensajes no leídos,<br>**Cuando** el usuario visualiza su Inbox,<br>**Entonces** la aplicación muestra un indicador asociado a esa conversación.<br><br>**Escenario 2 — Actualización del indicador al leer mensajes**<br>**Dado** que el usuario abre una conversación y sus mensajes quedan leídos,<br>**Cuando** vuelve al Inbox,<br>**Entonces** el indicador se actualiza para reflejar el estado leído. |

<br>

| **US-41** | **Iniciar chat directo con la concesionaria** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Mensajería y comunicación |
| **Description** | Como Cliente, quiero iniciar un chat con la concesionaria desde la ficha de un vehículo en la aplicación móvil nativa, para realizar consultas sobre su disponibilidad. |
| **Acceptance Criteria** | **Escenario 1 — Inicio de chat exitoso**<br>**Dado** que el cliente abre la ficha de un vehículo en la aplicación móvil,<br>**Cuando** selecciona iniciar chat con la concesionaria,<br>**Entonces** se crea o abre una conversación asociada al contacto.<br><br>**Escenario 2 — Inicio de chat no disponible**<br>**Dado** que el cliente no está autenticado o el vehículo no tiene una concesionaria contactable,<br>**Cuando** intenta iniciar el chat,<br>**Entonces** la aplicación solicita autenticación o informa que el contacto no está disponible. |

<br>

| **US-42** | **Cargar y ver historial de chat** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Alta |
| **Epic** | Mensajería y comunicación |
| **Description** | Como Usuario Autenticado, quiero visualizar el historial de una conversación al abrirla desde la aplicación móvil nativa, para conservar el contexto de la comunicación. |
| **Acceptance Criteria** | **Escenario 1 — Carga del historial de conversación**<br>**Dado** que el usuario autenticado selecciona una conversación existente,<br>**Cuando** la abre en la aplicación móvil,<br>**Entonces** se carga y muestra el historial de mensajes disponible en orden cronológico.<br><br>**Escenario 2 — Historial vacío o no disponible**<br>**Dado** que la conversación no tiene mensajes anteriores o no se puede cargar el historial,<br>**Cuando** el usuario la abre,<br>**Entonces** la aplicación muestra un estado vacío o un aviso de error con opción de reintento. |

<br>

| **US-43** | **Enviar y recibir mensajes de texto en tiempo real** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Alta |
| **Epic** | Mensajería y comunicación |
| **Description** | Como Usuario Autenticado, quiero enviar y recibir mensajes en tiempo real desde la aplicación móvil nativa, para comunicarme con otros usuarios sin salir de la plataforma. |
| **Acceptance Criteria** | **Escenario 1 — Envío de mensaje exitoso**<br>**Dado** que el usuario autenticado se encuentra en una conversación activa,<br>**Cuando** envía un mensaje de texto válido,<br>**Entonces** el mensaje se entrega a la conversación y aparece en el chat.<br><br>**Escenario 2 — Recepción de mensaje en tiempo real**<br>**Dado** que llega un mensaje nuevo a una conversación abierta,<br>**Cuando** la aplicación recibe la actualización,<br>**Entonces** lo muestra en el chat sin requerir que el usuario recargue manualmente. |

<br>

| **US-44** | **Atención rápida de prospectos por chat** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Mensajería y comunicación |
| **Description** | Como Concesionaria, quiero responder consultas de los prospectos mediante el chat desde la aplicación móvil nativa, para brindar atención comercial y facilitar el contacto. |
| **Acceptance Criteria** | **Escenario 1 — Respuesta a prospecto enviada**<br>**Dado** que la concesionaria abre una conversación con un prospecto en la aplicación móvil,<br>**Cuando** redacta y envía una respuesta,<br>**Entonces** el mensaje aparece en el historial de la conversación.<br><br>**Escenario 2 — Envío de mensaje inválido o fallido**<br>**Dado** que la concesionaria intenta enviar un mensaje vacío o se produce un error de envío,<br>**Cuando** confirma el envío,<br>**Entonces** la aplicación impide el mensaje vacío o informa el fallo para que pueda reintentarlo. |

<br>

| **US-45** | **Recibir notificaciones push** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Alta |
| **Epic** | Mensajería y comunicación |
| **Description** | Como Usuario Autenticado, quiero recibir notificaciones push en la aplicación móvil nativa, para enterarme de nuevos mensajes, cambios en mis solicitudes y otras actividades importantes. |
| **Acceptance Criteria** | **Escenario 1 — Recepción de notificación push**<br>**Dado** que el usuario autenticado habilitó las notificaciones y ocurre un nuevo mensaje o cambio relevante en una solicitud,<br>**Cuando** el dispositivo recibe el evento,<br>**Entonces** muestra una notificación push con información pertinente.<br><br>**Escenario 2 — Notificaciones deshabilitadas**<br>**Dado** que el usuario deshabilitó las notificaciones o el dispositivo no puede recibirlas,<br>**Cuando** ocurre un evento,<br>**Entonces** la aplicación respeta la configuración y mantiene disponible la información al consultar la plataforma. |

## 3.3. Product Backlog

En esta sección se presenta el Product Backlog priorizado del proyecto. Siguiendo las directrices del curso, el orden de los elementos se ha determinado estrictamente por el valor que aportan al negocio, colocando en las primeras posiciones las historias relacionadas con el sitio web estático (Landing Page) para asegurar su inclusión desde el primer sprint. Asimismo, se ha evitado el anti-patrón de colocar las historias de seguridad o autenticación al inicio, priorizando antes la visualización del catálogo y la propuesta de valor.

A continuación, se detalla la tabla de estimación utilizando la escala de Story Points (1, 2, 3, 5, 8).

| # Orden | User Story Id | Título | Descripción | Story Points |
| :---: | :---: | :--- | :--- | :---: |
| 1 | US-01 | Visualizar módulos funcionales de la plataforma | Como visitante, deseo visualizar las funcionalidades principales del producto para entender cómo me ayudará a buscar o vender un vehículo. | 2 |
| 2 | US-02 | Consultar planes de membresía B2B | Como visitante gerente comercial, deseo consultar los planes de suscripción para evaluar los beneficios de afiliar mi concesionaria a la plataforma. | 2 |
| 3 | US-04 | Navegación fluida mediante menú interactivo | Como visitante, deseo utilizar un menú de navegación para saltar directamente a la sección de mi interés sin perder el contexto de la página. | 1 |
| 4 | US-08 | Explorar catálogo unificado de vehículos | Como comprador interesado, deseo visualizar un catálogo general de vehículos nuevos y usados para conocer la oferta disponible en el mercado. | 5 |
| 5 | US-10 | Visualizar ficha detallada del vehículo | Como comprador interesado, deseo revisar las especificaciones completas de un vehículo para analizar sus características técnicas antes de solicitar una pre-evaluación crediticia. | 3 |
| 6 | US-09 | Visualizar Dashboard de métricas comerciales | Como gerente comercial, deseo visualizar un panel resumen (Dashboard) al ingresar a mi cuenta para monitorear el rendimiento de mis publicaciones y prospectos. | 5 |
| 7 | US-05 | Registro de nueva cuenta para comprador | Como comprador interesado, deseo registrarme en la plataforma creando una cuenta segura para poder guardar mis preferencias y solicitar pre-evaluaciones. | 3 |
| 8 | US-06 | Inicio de sesión para compradores | Como comprador registrado, deseo iniciar sesión en mi cuenta para continuar con la búsqueda de mi vehículo y visualizar mis opciones guardadas. | 2 |
| 9 | US-07 | Inicio de sesión para concesionarias | Como gerente comercial de una concesionaria, deseo iniciar sesión en mi portal B2B para gestionar mi inventario y atender a los prospectos. | 2 |
| 10 | TS-01 | Implementar lógica de internacionalización (i18n) | Como desarrollador, deseo implementar un script para el cambio de idioma estático que actualice los textos utilizando atributos de datos sin necesidad de recargar la página web. | 3 |
| 11 | US-03 | Cambiar el idioma de la interfaz estática | Como visitante internacional, deseo cambiar el idioma de la página para leer el contenido corporativo en mi idioma de preferencia. | 1 |

**Evidencia de Product Backlog gestionado en Trello:**

![ProductBacklog-Trello](../assets/Chapter-3/productbacklog-trello.png)

**Enlace público del Product Backlog:**  
[Tablero de Product Backlog en Trello](https://trello.com/invite/b/68cef3b9540a3e849e12d1e2/ATTI55e37783ca94033bfa115ee21378ce0d092EEDDF/smartfinance-drive)

## 3.4. Impact Mapping

En esta sección el equipo explica y presenta el Impact Mapping para el modelo de negocio digital de SmartFinance Drive, elaborado en la herramienta UXPressia. Para su desarrollo, tomamos como base las fichas de los User Personas elaboradas previamente.

El proceso inició con la definición de un objetivo de negocio principal (Business Goal) estructurado bajo criterios SMART para asegurar su medición. A partir de esta meta general, el mapa se ramifica respondiendo a las siguientes interrogantes estratégicas:

* **Actors/Personas:** ¿Quiénes nos ayudarán a lograr la meta? (Alineados directamente con nuestros tres segmentos objetivo).

* **Impacts:** ¿Qué tendrían que hacer o cómo esperamos que cambien su comportamiento para ayudar a lograr la meta?

* **Deliverables:** ¿Qué podemos hacer o construir como negocio digital para provocar esos impactos?

* **User Stories:** ¿Cuáles son las historias de usuario específicas ("Como... deseo... para...") que permitirán al equipo técnico construir los entregables identificados?

A continuación, se presenta la captura del mapa estructurado con todos sus componentes consolidados.

![Impact-Mapping](../assets/Chapter-3/impact-map.png)
