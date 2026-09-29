# Capítulo III: Requirements Specification

## 3.1. To-Be Scenario Mapping

**Segmento 1: Compradores interesados**

![to-be-scenario-mapping-segmento-1](assets/Chapter-3/to-be-scenario-mapping-segmento-1.png)

**Segmento 2: Concesionarias de vehículos nuevos**

![to-be-scenario-mapping-segmento-2](assets/Chapter-3/to-be-scenario-mapping-segmento-2.png)

**Segmento 3: Concesionarias de vehículos usados**

![to-be-scenario-mapping-segmento-3](assets/Chapter-3/to-be-scenario-mapping-segmento-3.png)

* **Enlace interactivo del tablero en Miro:** [https://miro.com/app/board/uXjVHpkhWe4=/?share_link_id=221895309503](https://miro.com/app/board/uXjVHpkhWe4=/?share_link_id=221895309503)

## 3.2. User Stories

En esta sección se definen los requisitos funcionales, no funcionales y técnicos de SmartFinance Drive mediante un conjunto estructurado de Epics y User Stories. La redacción contempla los tres segmentos objetivo (Compradores, Concesionarias de nuevos y Concesionarias de usados), así como las historias técnicas necesarias para la viabilidad de la plataforma.

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-01         | Visitante                         | Alta              | Gestión de acceso |
|               |                                   |                   | y cuenta          |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Registro de cuenta y perfil personal                                      |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Visitante, quiero crear una cuenta ingresando mi correo, contraseña y datos          |
| personales básicos desde la aplicación web, para acceder a la plataforma como Cliente     |
| y contar con un perfil inicial.                                                           |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Registro exitoso**\                                                       |
| **Dado** que el visitante se encuentra en el formulario de registro,\                    |
| **Cuando** ingresa un correo válido, una contraseña y los datos personales obligatorios   |
| y confirma el registro,\                                                                  |
| **Entonces** la plataforma crea su cuenta y muestra una confirmación.\                    |
| \                                                                                         |
| **Escenario 2 — Registro con datos inválidos o duplicados**\                              |
| **Dado** que el visitante intenta registrarse con datos obligatorios incompletos o un     |
| correo ya registrado,\                                                                    |
| **Cuando** envía el formulario,\                                                          |
| **Entonces** la plataforma impide el registro e informa qué dato debe corregir.           |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-02         | Usuario Registrado                | Alta              | Gestión de acceso |
|               |                                   |                   | y cuenta          |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Inicio de sesión                                                          |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Usuario Registrado, quiero iniciar sesión con mis credenciales, para acceder a      |
| las funcionalidades correspondientes a mi rol.                                            |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Inicio de sesión exitoso**\                                               |
| **Dado** que el usuario registrado tiene credenciales válidas,\                           |
| **Cuando** ingresa su correo y contraseña y selecciona iniciar sesión,\                   |
| **Entonces** accede a la plataforma con los permisos correspondientes a su rol.\          |
| \                                                                                         |
| **Escenario 2 — Inicio de sesión con credenciales inválidas**\                            |
| **Dado** que el usuario ingresa credenciales incorrectas o incompletas,\                  |
| **Cuando** intenta iniciar sesión,\                                                       |
| **Entonces** el acceso es rechazado y se muestra un mensaje de error sin revelar          |
| información sensible.                                                                     |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-03         | Usuario Autenticado               | Alta              | Gestión de acceso |
|               |                                   |                   | y cuenta          |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Cierre de sesión                                                          |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Usuario Autenticado, quiero cerrar sesión desde cualquier pantalla, para proteger   |
| mi cuenta y finalizar mi acceso a la plataforma.                                          |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Cierre de sesión exitoso**\                                               |
| **Dado** que el usuario tiene una sesión activa,\                                         |
| **Cuando** selecciona cerrar sesión desde cualquier pantalla web o móvil,\                |
| **Entonces** la sesión finaliza y se le redirige a la pantalla de acceso.\                |
| \                                                                                         |
| **Escenario 2 — Acceso después del cierre de sesión**\                                    |
| **Dado** que el usuario cerró sesión,\                                                    |
| **Cuando** intenta acceder a una funcionalidad protegida usando la sesión anterior,\      |
| **Entonces** la plataforma solicita autenticarse nuevamente.                              |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-04         | Usuario Registrado                | Alta              | Gestión de acceso |
|               |                                   |                   | y cuenta          |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Cambiar contraseña                                                        |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Usuario Registrado, quiero cambiar mi contraseña desde la configuración de mi        |
| cuenta, para mantener protegido mi acceso.                                                |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Cambio de contraseña exitoso**\                                           |
| **Dado** que el usuario está autenticado y accede a la configuración de su cuenta,\       |
| **Cuando** ingresa su contraseña actual y una nueva contraseña válida y confirma el        |
| cambio,\                                                                                  |
| **Entonces** la plataforma actualiza sus credenciales y confirma la operación.\           |
| \                                                                                         |
| **Escenario 2 — Cambio de contraseña rechazado**\                                         |
| **Dado** que la contraseña actual es incorrecta o la nueva contraseña no cumple las       |
| reglas establecidas,\                                                                     |
| **Cuando** intenta guardar el cambio,\                                                    |
| **Entonces** la plataforma conserva la contraseña anterior e informa el error.            |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-05         | Cliente                           | Alta              | Gestión de perfil |
|               |                                   |                   | y roles           |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Edición y completitud de perfil                                           |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero actualizar mis datos de contacto y completar información adicional   |
| como mis ingresos desde la aplicación web, para mantener mi perfil actualizado.           |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Actualización de perfil exitosa**\                                        |
| **Dado** que el cliente inició sesión y abrió la edición de perfil,\                      |
| **Cuando** actualiza sus datos de contacto o ingresos con información válida y guarda los |
| cambios,\                                                                                 |
| **Entonces** el perfil muestra la información actualizada.\                               |
| \                                                                                         |
| **Escenario 2 — Actualización con información inválida**\                                 |
| **Dado** que el cliente ingresa información inválida en un campo editable,\               |
| **Cuando** intenta guardar el perfil,\                                                    |
| **Entonces** la plataforma señala los campos que debe corregir y no guarda los datos      |
| inválidos.                                                                                |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-06         | Cliente                           | Alta              | Gestión de perfil |
|               |                                   |                   | y roles           |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Solicitud de rol Concesionaria                                            |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero solicitar el rol de Concesionaria ingresando mi RUC desde la         |
| aplicación web, para que la plataforma valide mi información y habilite las funciones     |
| correspondientes.                                                                         |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Solicitud de rol registrada**\                                            |
| **Dado** que el cliente accede a la solicitud de rol Concesionaria,\                     |
| **Cuando** ingresa su RUC y envía la solicitud,\                                          |
| **Entonces** la plataforma registra la solicitud y presenta su estado de validación.\     |
| \                                                                                         |
| **Escenario 2 — Solicitud de rol con RUC inválido**\                                      |
| **Dado** que el RUC ingresado no cumple el formato requerido o no supera la               |
| validación,\                                                                              |
| **Cuando** se envía la solicitud,\                                                        |
| **Entonces** la plataforma informa el problema y no habilita las funciones de              |
| Concesionaria.                                                                            |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-07         | Cliente                           | Alta              | Gestión de perfil |
|               |                                   |                   | y roles           |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Solicitud de rol Entidad Financiera                                       |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero solicitar el rol de Entidad Financiera ingresando mi RUC desde la    |
| aplicación web, para que la plataforma valide mi información y habilite las funciones     |
| financieras.                                                                              |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Solicitud de rol financiero registrada**\                                 |
| **Dado** que el cliente accede a la solicitud de rol Entidad Financiera,\                 |
| **Cuando** ingresa su RUC y envía la solicitud,\                                          |
| **Entonces** la plataforma registra la solicitud y presenta su estado de validación.\     |
| \                                                                                         |
| **Escenario 2 — Solicitud de rol financiero con RUC inválido**\                           |
| **Dado** que el RUC ingresado no cumple el formato requerido o no supera la               |
| validación,\                                                                              |
| **Cuando** se envía la solicitud,\                                                        |
| **Entonces** la plataforma informa el problema y no habilita las funciones financieras.   |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-08         | Administrador                     | Alta              | Gestión de perfil |
|               |                                   |                   | y roles           |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Modificar roles de usuario                                                |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Administrador, quiero asignar o modificar los roles de las cuentas registradas desde |
| el backoffice de la aplicación web, para gestionar los permisos de los usuarios.          |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Modificación de rol exitosa**\                                            |
| **Dado** que el administrador accede al backoffice y selecciona una cuenta                |
| registrada,\                                                                              |
| **Cuando** asigna o modifica su rol y confirma la operación,\                             |
| **Entonces** la plataforma guarda el cambio de permisos.\                                 |
| \                                                                                         |
| **Escenario 2 — Modificación de rol no autorizada**\                                      |
| **Dado** que un usuario sin privilegios de administrador intenta modificar roles,\        |
| **Cuando** solicita la operación,\                                                        |
| **Entonces** la plataforma deniega el acceso y mantiene los roles existentes.             |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-09         | Cliente                           | Alta              | Dashboard y       |
|               |                                   |                   | configuración B2B |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Resumen financiero del cliente                                            |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero visualizar un resumen de mi score crediticio, simulaciones y         |
| proyecciones desde la aplicación web, para consultar mi información financiera desde un   |
| solo lugar.                                                                               |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización del resumen financiero**\                                   |
| **Dado** que el cliente inició sesión y cuenta con información financiera disponible,\    |
| **Cuando** abre su dashboard,\                                                            |
| **Entonces** visualiza en un solo lugar su score crediticio, simulaciones y proyecciones   |
| disponibles.\                                                                             |
| \                                                                                         |
| **Escenario 2 — Información financiera no disponible**\                                   |
| **Dado** que alguno de los datos financieros aún no está disponible,\                     |
| **Cuando** el cliente consulta el dashboard,\                                             |
| **Entonces** la plataforma indica que no hay información para ese apartado sin mostrar    |
| datos incorrectos.                                                                        |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-10         | Concesionaria                     | Alta              | Dashboard y       |
|               |                                   |                   | configuración B2B |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Selección obligatoria de membresía B2B                                    |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria recién validada, quiero seleccionar un plan de membresía desde la      |
| aplicación web antes de utilizar las funciones B2B, para habilitar la gestión de mi       |
| inventario.                                                                               |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Selección de membresía obligatoria**\                                     |
| **Dado** que una concesionaria fue validada y aún no tiene membresía,\                    |
| **Cuando** intenta utilizar las funciones B2B,\                                           |
| **Entonces** la plataforma solicita seleccionar un plan antes de habilitar la gestión     |
| de inventario.\                                                                           |
| \                                                                                         |
| **Escenario 2 — Activación de funciones B2B**\                                            |
| **Dado** que la concesionaria selecciona un plan disponible y completa la confirmación    |
| requerida,\                                                                               |
| **Cuando** se registra la membresía,\                                                     |
| **Entonces** la plataforma habilita las funciones B2B correspondientes al plan.           |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-11         | Entidad Financiera                | Alta              | Dashboard y       |
|               |                                   |                   | configuración B2B |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Registrar entidad financiera                                              |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Entidad Financiera, quiero registrar mis tasas, comisiones y condiciones crediticias |
| desde la aplicación web, para ofrecer opciones de financiamiento a los compradores.       |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Registro de condiciones crediticias exitoso**\                            |
| **Dado** que la entidad financiera inició sesión y abrió el registro de condiciones       |
| crediticias,\                                                                             |
| **Cuando** ingresa tasas, comisiones y condiciones válidas y guarda,\                     |
| **Entonces** la plataforma registra la información para ofrecer opciones de                |
| financiamiento.\                                                                          |
| \                                                                                         |
| **Escenario 2 — Registro con información inválida**\                                      |
| **Dado** que la entidad financiera omite un dato obligatorio o ingresa valores no         |
| válidos,\                                                                                 |
| **Cuando** intenta guardar las condiciones,\                                              |
| **Entonces** la plataforma señala los errores y no registra información incompleta.       |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-12         | Concesionaria                     | Media             | Dashboard y       |
|               |                                   |                   | configuración B2B |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Consultar plan de membresía                                               |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero consultar la información de mi plan de membresía desde la      |
| aplicación web, para conocer sus características, beneficios y vigencia.                  |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Consulta de membresía activa**\                                           |
| **Dado** que la concesionaria tiene una membresía registrada,\                            |
| **Cuando** accede a la sección de su plan,\                                               |
| **Entonces** visualiza sus características, beneficios y vigencia.\                       |
| \                                                                                         |
| **Escenario 2 — Consulta sin membresía activa**\                                          |
| **Dado** que la concesionaria no tiene una membresía activa,\                             |
| **Cuando** consulta la sección de plan,\                                                  |
| **Entonces** la plataforma informa que no existe un plan activo y muestra las opciones    |
| disponibles si corresponde.                                                               |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-13         | Concesionaria                     | Media             | Dashboard y       |
|               |                                   |                   | configuración B2B |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Cambiar plan de membresía                                                 |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero cambiar mi plan de membresía desde la aplicación web, para     |
| adaptar mi suscripción a las necesidades de mi negocio.                                   |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Cambio de plan exitoso**\                                                 |
| **Dado** que la concesionaria tiene una membresía vigente,\                               |
| **Cuando** selecciona otro plan disponible y confirma el cambio,\                         |
| **Entonces** la plataforma registra la solicitud o actualización y muestra el plan        |
| resultante.\                                                                              |
| \                                                                                         |
| **Escenario 2 — Cambio de plan no disponible**\                                           |
| **Dado** que la concesionaria intenta cambiar a un plan no disponible o la operación no   |
| puede completarse,\                                                                       |
| **Cuando** confirma el cambio,\                                                           |
| **Entonces** la plataforma informa el motivo y conserva la membresía vigente.             |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-14         | Concesionaria                     | Alta              | Dashboard y       |
|               |                                   |                   | configuración B2B |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Renovar membresía                                                         |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero renovar mi membresía desde la aplicación web, para mantener    |
| activas las funcionalidades de mi plan.                                                   |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Renovación de membresía exitosa**\                                        |
| **Dado** que la concesionaria tiene una membresía próxima a vencer o vencida,\            |
| **Cuando** selecciona renovar y completa la confirmación requerida,\                      |
| **Entonces** la plataforma registra la renovación y muestra la nueva vigencia.\           |
| \                                                                                         |
| **Escenario 2 — Renovación no completada**\                                               |
| **Dado** que la renovación no puede completarse,\                                         |
| **Cuando** la concesionaria intenta confirmarla,\                                         |
| **Entonces** la plataforma informa el resultado y no presenta la membresía como           |
| renovada.                                                                                 |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-15         | Concesionaria                     | Alta              | Gestión de        |
|               |                                   |                   | inventario de     |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Listar inventario de vehículos                                            |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero visualizar todos mis vehículos publicados desde la aplicación  |
| web, para consultar y controlar mi inventario.                                            |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización del inventario**\                                           |
| **Dado** que la concesionaria inició sesión y tiene vehículos registrados,\               |
| **Cuando** abre su inventario,\                                                           |
| **Entonces** visualiza el listado de sus vehículos con la información disponible de cada  |
| uno.\                                                                                     |
| \                                                                                         |
| **Escenario 2 — Inventario vacío**\                                                       |
| **Dado** que la concesionaria aún no registra vehículos,\                                 |
| **Cuando** accede al inventario,\                                                         |
| **Entonces** la plataforma muestra un estado vacío y la opción de registrar o publicar    |
| un vehículo.                                                                              |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-16         | Concesionaria                     | Alta              | Gestión de        |
|               |                                   |                   | inventario de     |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Publicar vehículo                                                         |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero publicar un vehículo con sus características y precio desde la |
| aplicación web, para ofrecerlo en el catálogo.                                            |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Publicación de vehículo exitosa**\                                        |
| **Dado** que la concesionaria cuenta con permisos para gestionar inventario,\             |
| **Cuando** completa las características y el precio obligatorios de un vehículo y         |
| confirma la publicación,\                                                                 |
| **Entonces** el vehículo se registra y aparece en el catálogo.\                           |
| \                                                                                         |
| **Escenario 2 — Publicación con datos inválidos**\                                        |
| **Dado** que faltan datos obligatorios o existen valores inválidos,\                      |
| **Cuando** la concesionaria intenta publicar el vehículo,\                                |
| **Entonces** la plataforma señala los errores y no publica el registro.                   |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-17         | Concesionaria                     | Alta              | Gestión de        |
|               |                                   |                   | inventario de     |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Editar vehículo publicado                                                 |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero actualizar el precio, las características y el estado de       |
| stock de un vehículo publicado desde la aplicación web, para mantener actualizado mi     |
| inventario.                                                                               |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Edición de vehículo exitosa**\                                            |
| **Dado** que la concesionaria selecciona un vehículo de su inventario,\                   |
| **Cuando** modifica su precio, características o stock con datos válidos y guarda,\       |
| **Entonces** el sistema actualiza la información publicada.\                              |
| \                                                                                         |
| **Escenario 2 — Edición inválida o no autorizada**\                                       |
| **Dado** que la concesionaria intenta guardar cambios inválidos o sobre un vehículo que   |
| no le pertenece,\                                                                         |
| **Cuando** confirma la edición,\                                                          |
| **Entonces** la plataforma rechaza la operación y conserva los datos existentes.          |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-18         | Concesionaria                     | Alta              | Gestión de        |
|               |                                   |                   | inventario de     |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Cambiar estado transaccional del vehículo                                 |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero cambiar el estado comercial de un vehículo entre Disponible,  |
| Reservado y Vendido desde la aplicación web, para mantener actualizado su estado          |
| comercial.                                                                                |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Cambio de estado exitoso**\                                               |
| **Dado** que la concesionaria selecciona un vehículo de su inventario,\                   |
| **Cuando** cambia su estado comercial a Disponible, Reservado o Vendido y confirma,\     |
| **Entonces** el nuevo estado queda reflejado en el inventario.\                           |
| \                                                                                         |
| **Escenario 2 — Cambio de estado inválido o no autorizado**\                              |
| **Dado** que la concesionaria intenta asignar un estado distinto de los permitidos o     |
| modificar un vehículo ajeno,\                                                             |
| **Cuando** confirma la operación,\                                                        |
| **Entonces** la plataforma rechaza el cambio.                                             |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-19         | Concesionaria                     | Media             | Gestión de        |
|               |                                   |                   | inventario de     |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Eliminar vehículo                                                         |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero eliminar un vehículo de mi inventario desde la aplicación web, |
| para retirarlo del catálogo.                                                              |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Eliminación de vehículo confirmada**\                                     |
| **Dado** que la concesionaria selecciona un vehículo de su inventario,\                   |
| **Cuando** confirma su eliminación,\                                                      |
| **Entonces** el vehículo deja de aparecer en su inventario y en el catálogo publicado.\   |
| \                                                                                         |
| **Escenario 2 — Cancelación de eliminación**\                                             |
| **Dado** que la concesionaria cancela la confirmación de eliminación,\                    |
| **Cuando** vuelve al inventario,\                                                         |
| **Entonces** el vehículo permanece registrado sin cambios.                                |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-20         | Concesionaria                     | Media             | Gestión de        |
|               |                                   |                   | inventario de     |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Proyectar depreciación del vehículo                                       |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero consultar la proyección de depreciación de un vehículo a 2, 3  |
| y 5 años desde la aplicación web, para evaluar su valor a futuro.                         |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Proyección de depreciación disponible**\                                  |
| **Dado** que la concesionaria consulta un vehículo con información suficiente,\           |
| **Cuando** solicita la proyección de depreciación,\                                       |
| **Entonces** la plataforma presenta los valores estimados para los horizontes de 2, 3 y   |
| 5 años.\                                                                                  |
| \                                                                                         |
| **Escenario 2 — Información insuficiente para proyectar**\                                |
| **Dado** que el vehículo no cuenta con información suficiente para calcular la            |
| proyección,\                                                                              |
| **Cuando** la concesionaria solicita el cálculo,\                                         |
| **Entonces** la plataforma informa qué información falta y no presenta estimaciones como  |
| definitivas.                                                                              |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-21         | Concesionaria                     | Media             | Gestión de        |
|               |                                   |                   | inventario de     |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Panel de estadísticas del concesionario                                   |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero consultar estadísticas de mis vehículos, como vistas y         |
| simulaciones, desde la aplicación web, para conocer el interés generado por mi            |
| inventario.                                                                               |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización de estadísticas**\                                          |
| **Dado** que la concesionaria tiene vehículos publicados con actividad registrada,\       |
| **Cuando** abre su panel de estadísticas,\                                                |
| **Entonces** visualiza las métricas disponibles de vistas y simulaciones de su            |
| inventario.\                                                                              |
| \                                                                                         |
| **Escenario 2 — Sin actividad registrada**\                                               |
| **Dado** que todavía no existe actividad registrada,\                                     |
| **Cuando** consulta las estadísticas,\                                                    |
| **Entonces** la plataforma muestra valores vacíos o cero claramente identificados.        |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-22         | Concesionaria                     | Alta              | Gestión de        |
|               |                                   |                   | inventario de     |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Ver datos de contacto de prospectos                                       |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero consultar los datos de contacto de los clientes que realizaron |
| simulaciones con mis vehículos desde la aplicación web, para poder contactarlos.          |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Consulta de prospectos autorizados**\                                     |
| **Dado** que un cliente realizó una simulación asociada a un vehículo de la               |
| concesionaria,\                                                                           |
| **Cuando** la concesionaria consulta los prospectos,\                                     |
| **Entonces** puede visualizar los datos de contacto permitidos para esos clientes.\       |
| \                                                                                         |
| **Escenario 2 — Consulta de prospectos no autorizada**\                                   |
| **Dado** que la concesionaria intenta consultar prospectos que no corresponden a su       |
| inventario o no tiene permisos,\                                                          |
| **Cuando** solicita los datos,\                                                           |
| **Entonces** la plataforma deniega el acceso.                                             |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-23         | Cliente                           | Alta              | Exploración y     |
|               |                                   |                   | comparación de    |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Búsqueda y filtrado de vehículos                                          |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero buscar vehículos utilizando filtros como marca, precio, año y        |
| condición desde la aplicación web, para encontrar opciones que se ajusten a mis           |
| necesidades.                                                                              |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Búsqueda con resultados**\                                                |
| **Dado** que el cliente abre el catálogo de vehículos,\                                   |
| **Cuando** introduce filtros de marca, precio, año o condición,\                          |
| **Entonces** la plataforma muestra los vehículos que cumplen los criterios seleccionados.\ |
| \                                                                                         |
| **Escenario 2 — Búsqueda sin resultados**\                                                |
| **Dado** que ningún vehículo coincide con los filtros aplicados,\                         |
| **Cuando** se ejecuta la búsqueda,\                                                       |
| **Entonces** la plataforma informa que no hay resultados y permite modificar o limpiar    |
| los filtros.                                                                              |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-24         | Cliente                           | Media             | Exploración y     |
|               |                                   |                   | comparación de    |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Filtrar catálogo por concesionaria                                        |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero filtrar los vehículos por concesionaria desde la aplicación web,     |
| para consultar únicamente el inventario de un distribuidor específico.                    |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Filtrado por concesionaria exitoso**\                                     |
| **Dado** que el cliente consulta el catálogo,\                                            |
| **Cuando** selecciona una concesionaria como filtro,\                                     |
| **Entonces** la plataforma muestra únicamente los vehículos asociados a esa               |
| concesionaria.\                                                                           |
| \                                                                                         |
| **Escenario 2 — Concesionaria sin vehículos disponibles**\                                |
| **Dado** que la concesionaria seleccionada no tiene vehículos publicados disponibles,\    |
| **Cuando** se aplica el filtro,\                                                          |
| **Entonces** la plataforma muestra un resultado vacío informativo.                        |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-25         | Cliente                           | Alta              | Exploración y     |
|               |                                   |                   | comparación de    |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Ver detalle de vehículo                                                   |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero consultar la información detallada de un vehículo desde la           |
| aplicación web, para conocer sus características antes de iniciar una simulación.         |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización del detalle del vehículo**\                                 |
| **Dado** que el cliente selecciona un vehículo del catálogo,\                             |
| **Cuando** abre su ficha,\                                                                |
| **Entonces** visualiza la información detallada disponible para evaluar el vehículo antes |
| de simular un crédito.\                                                                   |
| \                                                                                         |
| **Escenario 2 — Vehículo no disponible**\                                                 |
| **Dado** que el vehículo ya no está disponible o su ficha no puede cargarse,\             |
| **Cuando** el cliente intenta consultarla,\                                               |
| **Entonces** la plataforma informa la situación y evita mostrar información               |
| desactualizada como vigente.                                                              |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-26         | Cliente                           | Media             | Exploración y     |
|               |                                   |                   | comparación de    |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Ver datos de contacto de la concesionaria                                 |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero consultar los datos de contacto de la concesionaria desde la ficha   |
| del vehículo en la aplicación web, para poder comunicarme con el vendedor.                |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización de datos de contacto**\                                     |
| **Dado** que el cliente se encuentra en la ficha de un vehículo publicado por una         |
| concesionaria,\                                                                           |
| **Cuando** consulta la sección de contacto,\                                              |
| **Entonces** visualiza los datos de contacto habilitados de dicha concesionaria.\         |
| \                                                                                         |
| **Escenario 2 — Datos de contacto no disponibles**\                                       |
| **Dado** que no existen datos de contacto disponibles para la concesionaria,\             |
| **Cuando** el cliente abre esa sección,\                                                  |
| **Entonces** la plataforma informa que los datos no están disponibles.                    |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-27         | Cliente                           | Media             | Exploración y     |
|               |                                   |                   | comparación de    |
|               |                                   |                   | vehículos         |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Comparar vehículos                                                        |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero comparar hasta dos vehículos desde la aplicación web, para consultar |
| sus principales características y costos de forma conjunta.                               |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Comparación de dos vehículos**\                                           |
| **Dado** que el cliente selecciona dos vehículos para comparar,\                          |
| **Cuando** abre la comparación,\                                                          |
| **Entonces** la plataforma presenta conjuntamente sus principales características y       |
| costos.\                                                                                  |
| \                                                                                         |
| **Escenario 2 — Límite de vehículos para comparación**\                                   |
| **Dado** que el cliente intenta agregar un tercer vehículo o seleccionar menos de dos     |
| vehículos,\                                                                               |
| **Cuando** solicita la comparación,\                                                      |
| **Entonces** la plataforma mantiene el límite de dos y solicita completar la selección    |
| requerida.                                                                                |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-28         | Cliente                           | Alta              | Simulación y      |
|               |                                   |                   | evaluación        |
|               |                                   |                   | crediticia        |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Pre-evaluación de riesgo crediticio                                       |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero generar una pre-evaluación crediticia basada en mis ingresos y       |
| deudas desde la aplicación web, para conocer mi capacidad de endeudamiento antes de       |
| solicitar un crédito.                                                                     |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Pre-evaluación crediticia exitosa**\                                      |
| **Dado** que el cliente ingresa sus ingresos y deudas requeridos,\                        |
| **Cuando** solicita la pre-evaluación crediticia,\                                        |
| **Entonces** la plataforma calcula y presenta el resultado estimado de su capacidad de   |
| endeudamiento.\                                                                           |
| \                                                                                         |
| **Escenario 2 — Pre-evaluación con datos incompletos o inválidos**\                       |
| **Dado** que el cliente omite datos requeridos o ingresa valores inválidos,\              |
| **Cuando** solicita la pre-evaluación,\                                                   |
| **Entonces** la plataforma señala los campos que debe corregir y no genera un resultado   |
| basado en datos incompletos.                                                              |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-29         | Cliente                           | Alta              | Simulación y      |
|               |                                   |                   | evaluación        |
|               |                                   |                   | crediticia        |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Crear simulación de crédito vehicular                                     |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero simular un crédito indicando el vehículo, entidad financiera, cuota   |
| inicial y plazo desde la aplicación web, para conocer las condiciones estimadas de pago.  |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Simulación de crédito exitosa**\                                          |
| **Dado** que el cliente selecciona un vehículo y una entidad financiera e ingresa cuota   |
| inicial y plazo válidos,\                                                                 |
| **Cuando** ejecuta la simulación,\                                                        |
| **Entonces** la plataforma presenta las condiciones estimadas de pago.\                   |
| \                                                                                         |
| **Escenario 2 — Simulación con datos inválidos**\                                         |
| **Dado** que faltan datos requeridos o la cuota inicial o el plazo no son válidos,\       |
| **Cuando** el cliente intenta simular,\                                                   |
| **Entonces** la plataforma informa los errores y no genera la simulación.                 |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-30         | Cliente                           | Alta              | Simulación y      |
|               |                                   |                   | evaluación        |
|               |                                   |                   | crediticia        |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Ver cronograma detallado de pagos                                         |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero consultar el cronograma detallado de una simulación desde la         |
| aplicación web, para conocer la distribución de mis pagos durante el crédito.             |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización del cronograma**\                                           |
| **Dado** que el cliente tiene una simulación registrada,\                                 |
| **Cuando** consulta su cronograma,\                                                       |
| **Entonces** visualiza el detalle de los pagos y su distribución durante el crédito.\      |
| \                                                                                         |
| **Escenario 2 — Cronograma no disponible**\                                               |
| **Dado** que la simulación no tiene un cronograma disponible,\                            |
| **Cuando** el cliente intenta consultarlo,\                                               |
| **Entonces** la plataforma informa que no es posible mostrar el detalle.                  |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-31         | Cliente                           | Media             | Simulación y      |
|               |                                   |                   | evaluación        |
|               |                                   |                   | crediticia        |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Descargar resumen de simulación en PDF                                    |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero descargar mi simulación financiera en formato PDF desde la           |
| aplicación web, para conservarla como documento.                                          |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Descarga de simulación en PDF exitosa**\                                  |
| **Dado** que el cliente cuenta con una simulación disponible,\                            |
| **Cuando** selecciona descargar el resumen en PDF,\                                       |
| **Entonces** la plataforma genera y entrega un documento legible con la información de    |
| esa simulación.\                                                                          |
| \                                                                                         |
| **Escenario 2 — Error al generar el PDF**\                                                |
| **Dado** que ocurre un error al generar el PDF,\                                          |
| **Cuando** el cliente solicita la descarga,\                                              |
| **Entonces** la plataforma informa que no pudo completarse y permite volver a             |
| intentarlo.                                                                               |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-32         | Cliente                           | Alta              | Simulación y      |
|               |                                   |                   | evaluación        |
|               |                                   |                   | crediticia        |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Ver y eliminar simulaciones guardadas                                     |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero consultar y eliminar mis simulaciones guardadas desde la aplicación  |
| web, para mantener organizado mi historial.                                               |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Consulta y eliminación de simulación**\                                   |
| **Dado** que el cliente tiene simulaciones guardadas,\                                    |
| **Cuando** abre su historial,\                                                            |
| **Entonces** visualiza sus simulaciones y puede seleccionar una para eliminarla.\         |
| \                                                                                         |
| **Escenario 2 — Cancelación de eliminación**\                                             |
| **Dado** que el cliente confirma la eliminación de una simulación propia,\                |
| **Cuando** se completa la operación,\                                                     |
| **Entonces** esta deja de aparecer en su historial; si cancela, permanece guardada.       |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-33         | Cliente                           | Media             | Simulación y      |
|               |                                   |                   | evaluación        |
|               |                                   |                   | crediticia        |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Filtrar simulaciones por estado                                           |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero filtrar mis simulaciones por estado desde la aplicación web, para    |
| localizar rápidamente las que están pendientes, aprobadas o rechazadas.                   |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Filtrado de simulaciones por estado**\                                    |
| **Dado** que el cliente tiene simulaciones con distintos estados,\                        |
| **Cuando** selecciona un estado como filtro,\                                             |
| **Entonces** la plataforma muestra únicamente las simulaciones que coinciden.\            |
| \                                                                                         |
| **Escenario 2 — Filtro sin resultados**\                                                  |
| **Dado** que ninguna simulación coincide con el estado seleccionado,\                     |
| **Cuando** se aplica el filtro,\                                                          |
| **Entonces** la plataforma muestra un mensaje de ausencia de resultados.                  |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-34         | Cliente                           | Media             | Simulación y      |
|               |                                   |                   | evaluación        |
|               |                                   |                   | crediticia        |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Cancelar simulación guardada                                              |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero cancelar una simulación que esté pendiente de revisión desde la      |
| aplicación web, para detener el proceso de solicitud de crédito.                          |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Cancelación de simulación exitosa**\                                      |
| **Dado** que el cliente tiene una simulación pendiente de revisión,\                      |
| **Cuando** selecciona cancelarla y confirma la acción,\                                   |
| **Entonces** la plataforma actualiza su estado a cancelada.\                               |
| \                                                                                         |
| **Escenario 2 — Cancelación no permitida o cancelada por el usuario**\                     |
| **Dado** que la simulación no está pendiente o el cliente cancela la confirmación,\       |
| **Cuando** intenta cancelar,\                                                             |
| **Entonces** la plataforma no modifica su estado.                                         |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-35         | Entidad Financiera                | Alta              | Evaluación y      |
|               |                                   |                   | gestión de        |
|               |                                   |                   | solicitudes de    |
|               |                                   |                   | crédito           |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Ver solicitudes de crédito entrantes                                      |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Entidad Financiera, quiero consultar las solicitudes de crédito recibidas desde la   |
| aplicación web, para gestionar y priorizar su revisión.                                   |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización de solicitudes recibidas**\                                 |
| **Dado** que la entidad financiera inició sesión y tiene solicitudes recibidas,\          |
| **Cuando** abre la bandeja de solicitudes,\                                               |
| **Entonces** visualiza las solicitudes disponibles para su revisión.\                     |
| \                                                                                         |
| **Escenario 2 — Bandeja de solicitudes vacía**\                                           |
| **Dado** que no existen solicitudes entrantes,\                                           |
| **Cuando** la entidad financiera consulta la bandeja,\                                     |
| **Entonces** la plataforma muestra un estado vacío informativo.                           |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-36         | Entidad Financiera                | Alta              | Evaluación y      |
|               |                                   |                   | gestión de        |
|               |                                   |                   | solicitudes de    |
|               |                                   |                   | crédito           |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Evaluación oficial de solicitud de crédito                                |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Entidad Financiera, quiero revisar una solicitud de crédito y registrar su resultado |
| como Aprobada o Rechazada desde la aplicación web, para formalizar la evaluación.         |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Evaluación oficial registrada**\                                          |
| **Dado** que la entidad financiera abre una solicitud que puede evaluar,\                 |
| **Cuando** registra el resultado Aprobada o Rechazada y confirma,\                        |
| **Entonces** la plataforma guarda la decisión y actualiza el estado de la solicitud.\     |
| \                                                                                         |
| **Escenario 2 — Evaluación no autorizada o inválida**\                                    |
| **Dado** que el usuario no pertenece a la entidad financiera autorizada o no selecciona   |
| un resultado válido,\                                                                     |
| **Cuando** intenta registrar la evaluación,\                                              |
| **Entonces** la plataforma rechaza la operación.                                          |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-37         | Cliente                           | Alta              | Evaluación y      |
|               |                                   |                   | gestión de        |
|               |                                   |                   | solicitudes de    |
|               |                                   |                   | crédito           |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Notificación del resultado de evaluación                                  |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero recibir automáticamente por correo el resultado de la evaluación     |
| crediticia en formato PDF, para conservar un registro de la decisión de la entidad        |
| financiera.                                                                               |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Notificación de evaluación enviada**\                                     |
| **Dado** que una entidad financiera registra el resultado de evaluación de una            |
| solicitud,\                                                                               |
| **Cuando** el proceso de notificación se ejecuta,\                                        |
| **Entonces** el cliente recibe un correo con el resultado y el PDF correspondiente.\      |
| \                                                                                         |
| **Escenario 2 — Fallo en la notificación**\                                               |
| **Dado** que el envío del correo o la generación del PDF falla,\                          |
| **Cuando** se procesa la notificación,\                                                   |
| **Entonces** el sistema registra o comunica el fallo para permitir su seguimiento y      |
| reintento.                                                                                |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-38         | Cliente                           | Alta              | Evaluación y      |
|               |                                   |                   | gestión de        |
|               |                                   |                   | solicitudes de    |
|               |                                   |                   | crédito           |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Ver estado de solicitudes desde la aplicación móvil                       |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero consultar el estado de mis solicitudes de crédito desde la           |
| aplicación móvil nativa, para conocer si están pendientes, aprobadas o rechazadas.        |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización del estado de solicitudes**\                                |
| **Dado** que el cliente inició sesión en la aplicación móvil,\                            |
| **Cuando** abre sus solicitudes de crédito,\                                              |
| **Entonces** visualiza el estado de cada solicitud como pendiente, aprobada o            |
| rechazada.\                                                                               |
| \                                                                                         |
| **Escenario 2 — Cliente sin solicitudes registradas**\                                    |
| **Dado** que el cliente no tiene solicitudes registradas,\                                |
| **Cuando** accede a esa sección móvil,\                                                   |
| **Entonces** la aplicación muestra un estado vacío informativo.                           |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-39         | Usuario Autenticado               | Alta              | Mensajería y      |
|               |                                   |                   | comunicación      |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Bandeja de Inbox y conversaciones activas                                 |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Usuario Autenticado, quiero consultar un Inbox con mis conversaciones activas desde  |
| la aplicación móvil nativa, para acceder rápidamente a mis chats pendientes.              |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización de conversaciones activas**\                                |
| **Dado** que el usuario autenticado abre el Inbox en la aplicación móvil,\                |
| **Cuando** existen conversaciones activas,\                                               |
| **Entonces** visualiza la lista de conversaciones para acceder a ellas.\                  |
| \                                                                                         |
| **Escenario 2 — Inbox sin conversaciones activas**\                                       |
| **Dado** que el usuario no tiene conversaciones activas,\                                 |
| **Cuando** abre el Inbox,\                                                                |
| **Entonces** la aplicación muestra un estado vacío y una indicación para iniciar una      |
| conversación si corresponde.                                                              |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-40         | Usuario Autenticado               | Media             | Mensajería y      |
|               |                                   |                   | comunicación      |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Indicadores de mensajes no leídos                                         |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Usuario Autenticado, quiero visualizar indicadores de mensajes no leídos en mi       |
| Inbox desde la aplicación móvil nativa, para identificar rápidamente las conversaciones   |
| con nueva actividad.                                                                      |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Visualización de mensajes no leídos**\                                    |
| **Dado** que una conversación contiene mensajes no leídos,\                               |
| **Cuando** el usuario visualiza su Inbox,\                                                |
| **Entonces** la aplicación muestra un indicador asociado a esa conversación.\             |
| \                                                                                         |
| **Escenario 2 — Actualización del indicador al leer mensajes**\                           |
| **Dado** que el usuario abre una conversación y sus mensajes quedan leídos,\             |
| **Cuando** vuelve al Inbox,\                                                              |
| **Entonces** el indicador se actualiza para reflejar el estado leído.                     |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-41         | Cliente                           | Alta              | Mensajería y      |
|               |                                   |                   | comunicación      |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Iniciar chat directo con la concesionaria                                 |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Cliente, quiero iniciar un chat con la concesionaria desde la ficha de un vehículo   |
| en la aplicación móvil nativa, para realizar consultas sobre su disponibilidad.           |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Inicio de chat exitoso**\                                                 |
| **Dado** que el cliente abre la ficha de un vehículo en la aplicación móvil,\             |
| **Cuando** selecciona iniciar chat con la concesionaria,\                                 |
| **Entonces** se crea o abre una conversación asociada al contacto.\                       |
| \                                                                                         |
| **Escenario 2 — Inicio de chat no disponible**\                                           |
| **Dado** que el cliente no está autenticado o el vehículo no tiene una concesionaria      |
| contactable,\                                                                             |
| **Cuando** intenta iniciar el chat,\                                                      |
| **Entonces** la aplicación solicita autenticación o informa que el contacto no está       |
| disponible.                                                                               |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-42         | Usuario Autenticado               | Alta              | Mensajería y      |
|               |                                   |                   | comunicación      |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Cargar y ver historial de chat                                            |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Usuario Autenticado, quiero visualizar el historial de una conversación al abrirla   |
| desde la aplicación móvil nativa, para conservar el contexto de la comunicación.          |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Carga del historial de conversación**\                                    |
| **Dado** que el usuario autenticado selecciona una conversación existente,\               |
| **Cuando** la abre en la aplicación móvil,\                                               |
| **Entonces** se carga y muestra el historial de mensajes disponible en orden              |
| cronológico.\                                                                             |
| \                                                                                         |
| **Escenario 2 — Historial vacío o no disponible**\                                        |
| **Dado** que la conversación no tiene mensajes anteriores o no se puede cargar el         |
| historial,\                                                                               |
| **Cuando** el usuario la abre,\                                                           |
| **Entonces** la aplicación muestra un estado vacío o un aviso de error con opción de      |
| reintento.                                                                                |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-43         | Usuario Autenticado               | Alta              | Mensajería y      |
|               |                                   |                   | comunicación      |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Enviar y recibir mensajes de texto en tiempo real                         |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Usuario Autenticado, quiero enviar y recibir mensajes en tiempo real desde la        |
| aplicación móvil nativa, para comunicarme con otros usuarios sin salir de la plataforma.  |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Envío de mensaje exitoso**\                                               |
| **Dado** que el usuario autenticado se encuentra en una conversación activa,\             |
| **Cuando** envía un mensaje de texto válido,\                                             |
| **Entonces** el mensaje se entrega a la conversación y aparece en el chat.\               |
| \                                                                                         |
| **Escenario 2 — Recepción de mensaje en tiempo real**\                                    |
| **Dado** que llega un mensaje nuevo a una conversación abierta,\                          |
| **Cuando** la aplicación recibe la actualización,\                                        |
| **Entonces** lo muestra en el chat sin requerir que el usuario recargue manualmente.      |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-44         | Concesionaria                     | Alta              | Mensajería y      |
|               |                                   |                   | comunicación      |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Atención rápida de prospectos por chat                                    |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Concesionaria, quiero responder consultas de los prospectos mediante el chat desde   |
| la aplicación móvil nativa, para brindar atención comercial y facilitar el contacto.      |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Respuesta a prospecto enviada**\                                          |
| **Dado** que la concesionaria abre una conversación con un prospecto en la aplicación     |
| móvil,\                                                                                   |
| **Cuando** redacta y envía una respuesta,\                                                |
| **Entonces** el mensaje aparece en el historial de la conversación.\                      |
| \                                                                                         |
| **Escenario 2 — Envío de mensaje inválido o fallido**\                                    |
| **Dado** que la concesionaria intenta enviar un mensaje vacío o se produce un error de     |
| envío,\                                                                                   |
| **Cuando** confirma el envío,\                                                            |
| **Entonces** la aplicación impide el mensaje vacío o informa el fallo para que pueda      |
| reintentarlo.                                                                             |
+-------------------------------------------------------------------------------------------+

<br>

+---------------+-----------------------------------+-------------------+-------------------+
| **Story ID**  | **User**                          | **Priority**      | **Epic**          |
+---------------+-----------------------------------+-------------------+-------------------+
| US-45         | Usuario Autenticado               | Alta              | Mensajería y      |
|               |                                   |                   | comunicación      |
+---------------+-----------------------------------+-------------------+-------------------+
| **Title**     | Recibir notificaciones push                                               |
+---------------+---------------------------------------------------------------------------+
| **Description**                                                                           |
+-------------------------------------------------------------------------------------------+
| Como Usuario Autenticado, quiero recibir notificaciones push en la aplicación móvil       |
| nativa, para enterarme de nuevos mensajes, cambios en mis solicitudes y otras actividades |
| importantes.                                                                              |
+-------------------------------------------------------------------------------------------+
| **Acceptance Criteria**                                                                   |
+-------------------------------------------------------------------------------------------+
| **Escenario 1 — Recepción de notificación push**\                                         |
| **Dado** que el usuario autenticado habilitó las notificaciones y ocurre un nuevo mensaje |
| o cambio relevante en una solicitud,\                                                     |
| **Cuando** el dispositivo recibe el evento,\                                              |
| **Entonces** muestra una notificación push con información pertinente.\                   |
| \                                                                                         |
| **Escenario 2 — Notificaciones deshabilitadas**\                                          |
| **Dado** que el usuario deshabilitó las notificaciones o el dispositivo no puede          |
| recibirlas,\                                                                              |
| **Cuando** ocurre un evento,\                                                             |
| **Entonces** la plataforma respeta la configuración y mantiene disponible la información |
| al consultar la plataforma.                                                               |
+-------------------------------------------------------------------------------------------+

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

![ProductBacklog-Trello](assets/Chapter-3/productbacklog-trello.png)

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

![Impact-Mapping](assets/Chapter-3/impact-map.png)
