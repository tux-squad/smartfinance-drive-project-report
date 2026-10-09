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

| **US-01** | **Visualizar información de la plataforma** |
| :--- | :--- |
| **User** | Visitante |
| **Priority** | Alta |
| **Epic** | Landing Page y captación |
| **Description** | Como Visitante, quiero visualizar información general de la plataforma, para conocer su propósito, funcionamiento y propuesta de valor antes de registrarme. |
| **Acceptance Criteria** | **Escenario 1 — Visualización de información**<br>**Dado** que el visitante accede a la plataforma,<br>**Cuando** consulta la información general del servicio,<br>**Entonces** puede visualizar información general sobre la plataforma y sus principales funcionalidades.<br><br>**Escenario 2 — Navegación de información**<br>**Dado** que el visitante consulta la información de la plataforma,<br>**Cuando** explora sus diferentes contenidos y servicios,<br>**Entonces** puede acceder a la información presentada de manera clara y organizada. |

<br>

| **US-02** | **Conocer beneficios de la plataforma** |
| :--- | :--- |
| **User** | Visitante |
| **Priority** | Alta |
| **Epic** | Landing Page y captación |
| **Description** | Como Visitante, quiero conocer los beneficios de utilizar la plataforma, para comprender cómo puede facilitar la búsqueda y gestión de opciones de financiamiento vehicular. |
| **Acceptance Criteria** | **Escenario 1 — Visualización de beneficios**<br>**Dado** que el visitante accede a la plataforma,<br>**Cuando** consulta los beneficios de la solución,<br>**Entonces** puede visualizar los principales beneficios ofrecidos por la plataforma.<br><br>**Escenario 2 — Información comprensible**<br>**Dado** que el visitante revisa los beneficios,<br>**Cuando** analiza cada propuesta de valor,<br>**Entonces** la información se presenta de forma clara y comprensible. |

<br>

| **US-03** | **Conocer beneficios de los planes** |
| :--- | :--- |
| **User** | Visitante |
| **Priority** | Alta |
| **Epic** | Landing Page y captación |
| **Description** | Como Visitante, quiero conocer los beneficios de los planes disponibles, para identificar qué opción se adapta a las necesidades de una concesionaria. |
| **Acceptance Criteria** | **Escenario 1 — Visualización de planes**<br>**Dado** que el visitante requiere evaluar las opciones de suscripción,<br>**Cuando** consulta los planes comerciales disponibles,<br>**Entonces** puede visualizar los planes ofrecidos y sus principales características.<br><br>**Escenario 2 — Comparación de beneficios**<br>**Dado** que existen diferentes planes de membresía,<br>**Cuando** el visitante compara sus características y coberturas,<br>**Entonces** puede identificar las diferencias entre sus beneficios. |

<br>

| **US-04** | **Acceder al registro desde la Landing Page** |
| :--- | :--- |
| **User** | Visitante |
| **Priority** | Alta |
| **Epic** | Landing Page y captación |
| **Description** | Como Visitante, quiero acceder al registro desde la plataforma, para crear una cuenta y utilizar sus funcionalidades. |
| **Acceptance Criteria** | **Escenario 1 — Acceso al registro**<br>**Dado** que el visitante no cuenta con una cuenta registrada,<br>**Cuando** solicita registrarse en la plataforma,<br>**Entonces** la plataforma inicia el proceso de registro de cuenta.<br><br>**Escenario 2 — Inicio del registro**<br>**Dado** que el visitante inicia el proceso de registro,<br>**Cuando** proporciona los datos requeridos para la creación de cuenta,<br>**Entonces** puede ingresar la información necesaria para registrarse. |

<br>

| **US-05** | **Registro de cuenta y perfil personal** |
| :--- | :--- |
| **User** | Visitante |
| **Priority** | Alta |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Visitante, quiero registrar una cuenta y completar mi perfil personal, para acceder a las funcionalidades disponibles para usuarios registrados. |
| **Acceptance Criteria** | **Escenario 1 — Registro exitoso**<br>**Dado** que el visitante inicia su registro en la plataforma,<br>**Cuando** completa correctamente los campos obligatorios y confirma su solicitud,<br>**Entonces** la plataforma crea su cuenta y solicita la verificación del correo electrónico.<br><br>**Escenario 2 — Datos incompletos**<br>**Dado** que el visitante intenta registrarse,<br>**Cuando** omite información obligatoria o proporciona datos inválidos,<br>**Entonces** la plataforma informa los campos que deben corregirse y no procesa el registro. |

<br>

| **US-06** | **Verificar correo electrónico** |
| :--- | :--- |
| **User** | Usuario Registrado |
| **Priority** | Alta |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Usuario Registrado, quiero verificar mi correo electrónico, para confirmar la propiedad de mi cuenta y habilitar su uso. |
| **Acceptance Criteria** | **Escenario 1 — Verificación exitosa**<br>**Dado** que el usuario se registró y recibió un código o enlace de verificación,<br>**Cuando** utiliza un mecanismo de verificación válido,<br>**Entonces** la plataforma verifica su correo electrónico y actualiza el estado de la cuenta a activa.<br><br>**Escenario 2 — Enlace inválido o vencido**<br>**Dado** que el usuario intenta verificar su correo,<br>**Cuando** utiliza un código o enlace inválido o vencido,<br>**Entonces** la plataforma informa que debe solicitar una nueva verificación. |

<br>

| **US-07** | **Inicio de sesión** |
| :--- | :--- |
| **User** | Usuario Registrado |
| **Priority** | Alta |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Usuario Registrado, quiero iniciar sesión, para acceder de forma segura a las funcionalidades correspondientes a mi cuenta. |
| **Acceptance Criteria** | **Escenario 1 — Inicio de sesión exitoso**<br>**Dado** que el usuario posee una cuenta activa y verificada,<br>**Cuando** proporciona credenciales válidas para autenticarse,<br>**Entonces** la plataforma inicia su sesión y habilita los permisos correspondientes a su rol.<br><br>**Escenario 2 — Credenciales incorrectas**<br>**Dado** que el usuario intenta autenticarse,<br>**Cuando** proporciona credenciales incorrectas,<br>**Entonces** la plataforma rechaza el acceso e informa que las credenciales no son válidas. |

<br>

| **US-08** | **Recuperar contraseña** |
| :--- | :--- |
| **User** | Usuario Registrado |
| **Priority** | Alta |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Usuario Registrado, quiero recuperar mi contraseña, para volver a acceder a mi cuenta cuando no recuerde mis credenciales. |
| **Acceptance Criteria** | **Escenario 1 — Solicitud de recuperación**<br>**Dado** que el usuario no recuerda su contraseña,<br>**Cuando** solicita recuperar el acceso mediante su correo registrado,<br>**Entonces** la plataforma envía las instrucciones para restablecer la contraseña.<br><br>**Escenario 2 — Nueva contraseña**<br>**Dado** que el usuario cuenta con una solicitud de recuperación válida,<br>**Cuando** establece una nueva contraseña que cumple las reglas de seguridad,<br>**Entonces** la plataforma actualiza su contraseña y permite su uso para futuras autenticaciones. |

<br>

| **US-09** | **Cierre de sesión** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Alta |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Usuario Autenticado, quiero cerrar mi sesión, para finalizar de forma segura mi acceso a la plataforma. |
| **Acceptance Criteria** | **Escenario 1 — Cierre exitoso**<br>**Dado** que el usuario tiene una sesión activa,<br>**Cuando** solicita cerrar su sesión activa,<br>**Entonces** la plataforma finaliza la sesión activa y revoca el acceso a recursos protegidos.<br><br>**Escenario 2 — Acceso posterior**<br>**Dado** que el usuario cerró su sesión activa,<br>**Cuando** intenta acceder a una funcionalidad protegida,<br>**Entonces** la plataforma solicita autenticarse nuevamente. |

<br>

| **US-10** | **Cambiar contraseña** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Media |
| **Epic** | Gestión de acceso y cuenta |
| **Description** | Como Usuario Autenticado, quiero cambiar mi contraseña, para mantener segura mi cuenta y actualizar mis credenciales cuando lo considere necesario. |
| **Acceptance Criteria** | **Escenario 1 — Cambio exitoso**<br>**Dado** que el usuario está autenticado en la plataforma,<br>**Cuando** ingresa su contraseña actual y una nueva contraseña válida,<br>**Entonces** la plataforma actualiza la contraseña de la cuenta.<br><br>**Escenario 2 — Contraseña actual incorrecta**<br>**Dado** que el usuario intenta cambiar su contraseña,<br>**Cuando** proporciona una contraseña actual que no coincide con la registrada,<br>**Entonces** la plataforma rechaza el cambio e informa el error. |

<br>

| **US-11** | **Visualizar perfil** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Media |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Usuario Autenticado, quiero visualizar mi perfil, para consultar la información asociada a mi cuenta. |
| **Acceptance Criteria** | **Escenario 1 — Visualización del perfil**<br>**Dado** que el usuario está autenticado,<br>**Cuando** consulta la información de su perfil,<br>**Entonces** la plataforma presenta sus datos registrados y roles asociados.<br><br>**Escenario 2 — Información actualizada**<br>**Dado** que el usuario posee información personal registrada,<br>**Cuando** consulta los datos de su perfil,<br>**Entonces** visualiza la información almacenada actualmente. |

<br>

| **US-12** | **Editar perfil** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Media |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Usuario Autenticado, quiero editar mis datos personales, para mantener mi perfil actualizado. |
| **Acceptance Criteria** | **Escenario 1 — Edición exitosa**<br>**Dado** que el usuario tiene una sesión activa y puede modificar sus datos personales,<br>**Cuando** modifica datos permitidos y confirma los cambios,<br>**Entonces** la plataforma actualiza la información de su perfil.<br><br>**Escenario 2 — Información inválida**<br>**Dado** que el usuario modifica su información personal,<br>**Cuando** proporciona datos que no cumplen las validaciones requeridas,<br>**Entonces** la plataforma informa los errores y no guarda los datos inválidos. |

<br>

| **US-13** | **Actualizar foto de perfil** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Baja |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Usuario Autenticado, quiero actualizar mi foto de perfil, para personalizar la identificación visual de mi cuenta. |
| **Acceptance Criteria** | **Escenario 1 — Foto actualizada**<br>**Dado** que el usuario está autenticado en la plataforma,<br>**Cuando** proporciona un archivo de imagen válido y confirma la actualización,<br>**Entonces** la plataforma actualiza su foto de perfil.<br><br>**Escenario 2 — Archivo no válido**<br>**Dado** que el usuario intenta actualizar su foto de perfil,<br>**Cuando** proporciona un archivo que no cumple con el formato o tamaño requerido,<br>**Entonces** la plataforma rechaza el archivo e informa el motivo. |

<br>

| **US-14** | **Eliminar cuenta** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Media |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Usuario Autenticado, quiero eliminar mi cuenta, para dejar de utilizar la plataforma cuando ya no necesite sus servicios. |
| **Acceptance Criteria** | **Escenario 1 — Eliminación confirmada**<br>**Dado** que el usuario solicita eliminar su cuenta,<br>**Cuando** confirma la operación de baja,<br>**Entonces** la plataforma procesa la eliminación de acuerdo con las reglas del negocio y finaliza su acceso.<br><br>**Escenario 2 — Eliminación cancelada**<br>**Dado** que el usuario inició la solicitud de eliminación de cuenta,<br>**Cuando** desiste de la operación antes de confirmarla,<br>**Entonces** la cuenta permanece activa sin modificaciones. |

<br>

| **US-15** | **Solicitar rol de Concesionaria** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Cliente, quiero solicitar el rol de Concesionaria, para poder acceder a las funcionalidades destinadas a gestionar un negocio de venta de vehículos. |
| **Acceptance Criteria** | **Escenario 1 — Solicitud de rol**<br>**Dado** que el cliente está autenticado y no posee el rol de Concesionaria,<br>**Cuando** solicita el rol de Concesionaria y proporciona los datos empresariales requeridos,<br>**Entonces** la plataforma registra la solicitud para su respectiva evaluación.<br><br>**Escenario 2 — Solicitud existente**<br>**Dado** que el cliente ya cuenta con una solicitud de rol en estado pendiente,<br>**Cuando** intenta registrar una nueva solicitud,<br>**Entonces** la plataforma informa que ya existe una solicitud en proceso. |

<br>

| **US-16** | **Solicitar rol de Entidad Financiera** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Cliente, quiero solicitar el rol de Entidad Financiera, para acceder a las funcionalidades destinadas a gestionar solicitudes de crédito. |
| **Acceptance Criteria** | **Escenario 1 — Solicitud de rol**<br>**Dado** que el cliente está autenticado y no posee el rol de Entidad Financiera,<br>**Cuando** solicita el rol de Entidad Financiera y proporciona la información requerida,<br>**Entonces** la plataforma registra la solicitud para su evaluación.<br><br>**Escenario 2 — Solicitud pendiente**<br>**Dado** que el cliente ya tiene una solicitud pendiente de aprobación,<br>**Cuando** intenta enviar otra solicitud para el mismo rol,<br>**Entonces** la plataforma informa que existe una solicitud en proceso. |

<br>

| **US-17** | **Consultar resumen financiero del cliente** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Cliente, quiero consultar mi resumen financiero, para conocer la información relevante utilizada en la evaluación de mis solicitudes de crédito. |
| **Acceptance Criteria** | **Escenario 1 — Consulta del resumen**<br>**Dado** que el cliente está autenticado en la plataforma,<br>**Cuando** solicita consultar su resumen financiero,<br>**Entonces** la plataforma presenta la información crediticia y financiera registrada para su cuenta.<br><br>**Escenario 2 — Sin información disponible**<br>**Dado** que el cliente no posee información financiera registrada,<br>**Cuando** consulta su resumen,<br>**Entonces** la plataforma informa que no existe información disponible para mostrar. |

<br>

| **US-18** | **Seleccionar plan de membresía** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Concesionaria, quiero seleccionar un plan de membresía, para acceder a las funcionalidades y beneficios correspondientes. |
| **Acceptance Criteria** | **Escenario 1 — Selección de plan**<br>**Dado** que la concesionaria está habilitada para contratar una membresía,<br>**Cuando** elige un plan disponible y confirma la suscripción,<br>**Entonces** la plataforma registra el plan seleccionado y actualiza el estado de la membresía.<br><br>**Escenario 2 — Plan no disponible**<br>**Dado** que un plan no se encuentra habilitado para contratación,<br>**Cuando** la concesionaria intenta contratarlo,<br>**Entonces** la plataforma impide la contratación e informa su indisponibilidad. |

<br>

| **US-19** | **Registrar condiciones crediticias de la Entidad Financiera** |
| :--- | :--- |
| **User** | Entidad Financiera |
| **Priority** | Alta |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Entidad Financiera, quiero registrar mis condiciones crediticias, para definir los parámetros utilizados en las opciones de financiamiento ofrecidas. |
| **Acceptance Criteria** | **Escenario 1 — Registro exitoso**<br>**Dado** que la entidad financiera está autenticada y habilitada,<br>**Cuando** registra parámetros crediticios válidos,<br>**Entonces** la plataforma guarda las condiciones financieras asociadas a la entidad.<br><br>**Escenario 2 — Datos inválidos**<br>**Dado** que la entidad financiera intenta registrar condiciones crediticias,<br>**Cuando** proporciona valores incompletos o fuera de los rangos permitidos,<br>**Entonces** la plataforma informa los campos que deben corregirse y no guarda los cambios. |

<br>

| **US-20** | **Consultar plan de membresía** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Concesionaria, quiero consultar mi plan de membresía actual, para conocer sus características, beneficios y estado. |
| **Acceptance Criteria** | **Escenario 1 — Consulta del plan**<br>**Dado** que la concesionaria cuenta con un plan contratado,<br>**Cuando** solicita información sobre su membresía,<br>**Entonces** la plataforma presenta las condiciones, beneficios y vigencia del plan activo.<br><br>**Escenario 2 — Sin plan activo**<br>**Dado** que la concesionaria no tiene un plan activo,<br>**Cuando** consulta el estado de su membresía,<br>**Entonces** la plataforma informa que no posee una membresía activa. |

<br>

| **US-21** | **Cambiar plan de membresía** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Concesionaria, quiero cambiar mi plan de membresía, para adaptar los beneficios de la plataforma a mis necesidades. |
| **Acceptance Criteria** | **Escenario 1 — Cambio de plan**<br>**Dado** que la concesionaria tiene un plan activo,<br>**Cuando** solicita cambiar a otro plan disponible y confirma la operación,<br>**Entonces** la plataforma registra el nuevo plan conforme a las condiciones acordadas.<br><br>**Escenario 2 — Cambio cancelado**<br>**Dado** que la concesionaria inició el proceso de cambio de plan,<br>**Cuando** cancela la operación antes de confirmarla,<br>**Entonces** la plataforma mantiene el plan actual sin modificaciones. |

<br>

| **US-22** | **Renovar membresía** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Concesionaria, quiero renovar mi membresía, para mantener activos los beneficios y funcionalidades de mi plan. |
| **Acceptance Criteria** | **Escenario 1 — Renovación exitosa**<br>**Dado** que la membresía de la concesionaria se encuentra próxima a vencer o vencida,<br>**Cuando** confirma la renovación y completa el proceso correspondiente,<br>**Entonces** la plataforma actualiza la vigencia de la membresía.<br><br>**Escenario 2 — Renovación no completada**<br>**Dado** que la concesionaria inicia la renovación de su membresía,<br>**Cuando** no culmina el proceso requerido,<br>**Entonces** la membresía conserva su estado anterior. |

<br>

| **US-23** | **Consultar historial de pagos** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Dashboard y configuración B2B |
| **Description** | Como Concesionaria, quiero consultar mi historial de pagos, para revisar las transacciones realizadas relacionadas con mi membresía. |
| **Acceptance Criteria** | **Escenario 1 — Historial disponible**<br>**Dado** que la concesionaria registra pagos de membresía previos,<br>**Cuando** solicita consultar su historial de pagos,<br>**Entonces** la plataforma presenta el registro detallado de las transacciones efectuadas.<br><br>**Escenario 2 — Sin pagos**<br>**Dado** que no existen transacciones de pago registradas,<br>**Cuando** la concesionaria consulta su historial,<br>**Entonces** la plataforma informa que no existen pagos registrados. |

<br>

| **US-24** | **Listar inventario de vehículos** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero visualizar mi inventario de vehículos, para administrar las unidades disponibles en la plataforma. |
| **Acceptance Criteria** | **Escenario 1 — Inventario disponible**<br>**Dado** que la concesionaria posee vehículos registrados,<br>**Cuando** consulta su inventario de unidades,<br>**Entonces** la plataforma presenta la relación de vehículos asociados a su cuenta.<br><br>**Escenario 2 — Inventario vacío**<br>**Dado** que la concesionaria no tiene vehículos registrados en su inventario,<br>**Cuando** realiza la consulta,<br>**Entonces** la plataforma informa que no cuenta con vehículos en inventario. |

<br>

| **US-25** | **Registrar vehículo** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero registrar un vehículo, para incorporarlo a mi inventario y posteriormente publicarlo en la plataforma. |
| **Acceptance Criteria** | **Escenario 1 — Registro exitoso**<br>**Dado** que la concesionaria cuenta con la información técnica y comercial de un vehículo,<br>**Cuando** ingresa todos los datos obligatorios válidos y confirma el registro,<br>**Entonces** la plataforma almacena el vehículo en su inventario.<br><br>**Escenario 2 — Datos incompletos**<br>**Dado** que la concesionaria intenta registrar un vehículo,<br>**Cuando** omite datos obligatorios o proporciona información inválida,<br>**Entonces** la plataforma impide el registro e indica la información faltante. |

<br>

| **US-26** | **Publicar vehículo** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Alta |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero publicar un vehículo registrado, para permitir que los clientes puedan visualizarlo y considerarlo para una compra. |
| **Acceptance Criteria** | **Escenario 1 — Publicación exitosa**<br>**Dado** que la concesionaria tiene un vehículo en inventario con información completa,<br>**Cuando** solicita publicar el vehículo,<br>**Entonces** el vehículo cambia a estado publicado y queda disponible para los compradores.<br><br>**Escenario 2 — Información incompleta**<br>**Dado** que un vehículo no cumple con los requisitos mínimos de publicación,<br>**Cuando** la concesionaria intenta publicarlo,<br>**Entonces** la plataforma impide la publicación e indica los requisitos pendientes. |

<br>

| **US-27** | **Editar vehículo publicado** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero editar la información de un vehículo publicado, para mantener actualizados sus datos. |
| **Acceptance Criteria** | **Escenario 1 — Edición exitosa**<br>**Dado** que existe un vehículo publicado perteneciente a la concesionaria,<br>**Cuando** modifica campos permitidos con información válida y guarda los cambios,<br>**Entonces** la plataforma actualiza los datos del vehículo.<br><br>**Escenario 2 — Datos inválidos**<br>**Dado** que la concesionaria modifica la información de un vehículo,<br>**Cuando** ingresa valores fuera de rango o datos no permitidos,<br>**Entonces** la plataforma rechaza los cambios e informa los errores correspondientes. |

<br>

| **US-28** | **Cambiar estado del vehículo** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero cambiar el estado de un vehículo, para indicar si se encuentra disponible, reservado, vendido u otro estado permitido. |
| **Acceptance Criteria** | **Escenario 1 — Cambio de estado**<br>**Dado** que la concesionaria tiene un vehículo registrado,<br>**Cuando** asigna un estado válido (disponible, reservado, vendido) y confirma la acción,<br>**Entonces** la plataforma actualiza el estado operativo del vehículo.<br><br>**Escenario 2 — Estado no permitido**<br>**Dado** que la concesionaria intenta asignar una transición de estado no permitida,<br>**Cuando** confirma la operación,<br>**Entonces** la plataforma rechaza la actualización y mantiene el estado anterior. |

<br>

| **US-29** | **Eliminar vehículo** |
| :--- | :--- |
| **User** | Concesionaria |
| **Priority** | Media |
| **Epic** | Gestión de inventario de vehículos |
| **Description** | Como Concesionaria, quiero eliminar un vehículo de mi inventario, para retirar unidades que ya no debo gestionar. |
| **Acceptance Criteria** | **Escenario 1 — Eliminación exitosa**<br>**Dado** que existe un vehículo en el inventario que no tiene procesos activos,<br>**Cuando** la concesionaria confirma su eliminación,<br>**Entonces** la plataforma retira el vehículo del inventario y confirma la baja.<br><br>**Escenario 2 — Eliminación cancelada**<br>**Dado** que la concesionaria inició la eliminación de un vehículo,<br>**Cuando** cancela la operación antes de confirmarla,<br>**Entonces** el vehículo permanece en el inventario sin modificaciones. |

<br>

| **US-30** | **Buscar y filtrar vehículos** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Exploración y búsqueda de vehículos |
| **Description** | Como Cliente, quiero buscar y filtrar vehículos, para encontrar opciones que se ajusten a mis necesidades y preferencias. |
| **Acceptance Criteria** | **Escenario 1 — Búsqueda de vehículos**<br>**Dado** que existen vehículos publicados en la plataforma,<br>**Cuando** el cliente busca utilizando términos o palabras clave válidas,<br>**Entonces** la plataforma presenta los vehículos que coinciden con los criterios de búsqueda.<br><br>**Escenario 2 — Aplicación de filtros**<br>**Dado** que existen vehículos disponibles en la oferta general,<br>**Cuando** el cliente aplica uno o más filtros específicos (precio, marca, año, condición),<br>**Entonces** la plataforma actualiza los resultados mostrando únicamente las unidades que cumplen los filtros. |

<br>

| **US-31** | **Ordenar resultados de búsqueda** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Baja |
| **Epic** | Exploración y búsqueda de vehículos |
| **Description** | Como Cliente, quiero ordenar los resultados de búsqueda, para visualizar primero los vehículos según el criterio que me resulte más conveniente. |
| **Acceptance Criteria** | **Escenario 1 — Ordenamiento exitoso**<br>**Dado** que existen resultados de vehículos para una consulta,<br>**Cuando** el cliente define un criterio de ordenamiento (precio, año o kilometraje),<br>**Entonces** la plataforma reorganiza los vehículos según el criterio solicitado.<br><br>**Escenario 2 — Cambio de orden**<br>**Dado** que los resultados se encuentran ordenados por un criterio previo,<br>**Cuando** el cliente indica un criterio diferente,<br>**Entonces** la plataforma actualiza la secuencia de los resultados conforme a la nueva regla. |

<br>

| **US-32** | **Filtrar catálogo por concesionaria** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Exploración y búsqueda de vehículos |
| **Description** | Como Cliente, quiero filtrar el catálogo por concesionaria, para consultar vehículos ofrecidos por una empresa específica. |
| **Acceptance Criteria** | **Escenario 1 — Filtro por concesionaria**<br>**Dado** que existen vehículos publicados por distintas concesionarias,<br>**Cuando** el cliente filtra por una concesionaria determinada,<br>**Entonces** la plataforma muestra exclusivamente los vehículos comercializados por dicha empresa.<br><br>**Escenario 2 — Sin coincidencias**<br>**Dado** que una concesionaria no dispone de vehículos activos publicados,<br>**Cuando** el cliente consulta la oferta de dicha empresa,<br>**Entonces** la plataforma informa que no existen vehículos disponibles para esa concesionaria. |

<br>

| **US-33** | **Ver detalle de vehículo** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Exploración y búsqueda de vehículos |
| **Description** | Como Cliente, quiero visualizar el detalle de un vehículo, para conocer sus características antes de decidir si deseo solicitar financiamiento o contactar a la concesionaria. |
| **Acceptance Criteria** | **Escenario 1 — Visualización del detalle**<br>**Dado** que existe un vehículo publicado en la plataforma,<br>**Cuando** el cliente consulta la información detallada de la unidad,<br>**Entonces** la plataforma presenta sus especificaciones técnicas, precio, imágenes y condiciones comerciales.<br><br>**Escenario 2 — Vehículo no disponible**<br>**Dado** que un vehículo ha dejado de estar publicado o fue dado de baja,<br>**Cuando** el cliente intenta consultar su información,<br>**Entonces** la plataforma informa que el vehículo ya no se encuentra disponible. |

<br>

| **US-34** | **Ver datos de contacto de la concesionaria** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Exploración y búsqueda de vehículos |
| **Description** | Como Cliente, quiero visualizar los datos de contacto de la concesionaria, para poder comunicarme directamente con ella respecto al vehículo de mi interés. |
| **Acceptance Criteria** | **Escenario 1 — Datos de contacto disponibles**<br>**Dado** que el cliente consulta información sobre un vehículo publicado,<br>**Cuando** requiere los datos comerciales de la concesionaria vendedora,<br>**Entonces** la plataforma presenta los canales de atención y contacto habilitados.<br><br>**Escenario 2 — Contacto no disponible**<br>**Dado** que una concesionaria no tiene canales de atención activos,<br>**Cuando** el cliente solicita sus datos de contacto,<br>**Entonces** la plataforma informa que no existen canales de contacto disponibles temporalmente. |

<br>

| **US-35** | **Crear simulación de crédito vehicular** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Cliente, quiero crear una simulación de crédito vehicular, para conocer las condiciones aproximadas de financiamiento de un vehículo. |
| **Acceptance Criteria** | **Escenario 1 — Simulación exitosa**<br>**Dado** que el cliente vincula un vehículo y define monto inicial, plazo y tasa de interés,<br>**Cuando** solicita el cálculo de la simulación,<br>**Entonces** la plataforma calcula y presenta la cuota estimada, intereses proyectados y costo total del crédito.<br><br>**Escenario 2 — Datos insuficientes**<br>**Dado** que el cliente intenta realizar una simulación,<br>**Cuando** omite parámetros financieros obligatorios o introduce valores inconsistentes,<br>**Entonces** la plataforma solicita completar y corregir la información antes de procesar el cálculo. |

<br>

| **US-36** | **Consultar cronograma detallado de pagos** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Cliente, quiero consultar el cronograma detallado de pagos de una simulación, para conocer cómo se distribuirían las cuotas durante el periodo de financiamiento. |
| **Acceptance Criteria** | **Escenario 1 — Cronograma disponible**<br>**Dado** que el cliente cuenta con una simulación calculada,<br>**Cuando** solicita el cronograma de pagos,<br>**Entonces** la plataforma presenta el desglose periódico de amortización, intereses y saldos deudores.<br><br>**Escenario 2 — Simulación inexistente**<br>**Dado** que no se dispone de una simulación previa válida,<br>**Cuando** el cliente intenta consultar un cronograma,<br>**Entonces** la plataforma informa que no existe información disponible para generar el cronograma. |

<br>

| **US-37** | **Consultar simulaciones guardadas** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Cliente, quiero consultar mis simulaciones guardadas, para revisar nuevamente las opciones de financiamiento que evalué anteriormente. |
| **Acceptance Criteria** | **Escenario 1 — Simulaciones disponibles**<br>**Dado** que el cliente posee simulaciones previamente almacenadas en su cuenta,<br>**Cuando** consulta su registro de simulaciones,<br>**Entonces** la plataforma presenta el listado de simulaciones guardadas con sus condiciones estimadas.<br><br>**Escenario 2 — Sin simulaciones**<br>**Dado** que el cliente no cuenta con simulaciones guardadas,<br>**Cuando** solicita la consulta de su historial,<br>**Entonces** la plataforma informa que no existen simulaciones registradas. |

<br>

| **US-38** | **Eliminar simulación guardada** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Baja |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Cliente, quiero eliminar una simulación guardada, para mantener organizada mi lista y retirar simulaciones que ya no necesito consultar. |
| **Acceptance Criteria** | **Escenario 1 — Eliminación exitosa**<br>**Dado** que el cliente tiene una simulación almacenada en su cuenta,<br>**Cuando** confirma la eliminación de dicha simulación,<br>**Entonces** la plataforma retira el registro de su cuenta y confirma la operación.<br><br>**Escenario 2 — Eliminación cancelada**<br>**Dado** que el cliente inició la eliminación de una simulación guardada,<br>**Cuando** cancela la operación antes de confirmarla,<br>**Entonces** la simulación permanece almacenada sin alteraciones. |

<br>

| **US-39** | **Cancelar solicitud de crédito** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Cliente, quiero cancelar una solicitud de crédito que aún se encuentre en un estado que permita su cancelación, para detener su evaluación cuando ya no deseo continuar con el trámite. |
| **Acceptance Criteria** | **Escenario 1 — Cancelación permitida**<br>**Dado** que el cliente posee una solicitud de crédito en estado cancelable,<br>**Cuando** confirma la cancelación del trámite,<br>**Entonces** la plataforma actualiza el estado de la solicitud a cancelada y notifica a las partes involucradas.<br><br>**Escenario 2 — Cancelación no permitida**<br>**Dado** que la solicitud alcanzó un estado definitivo (aprobada o rechazada),<br>**Cuando** el cliente intenta cancelarla,<br>**Entonces** la plataforma impide la operación e informa que el trámite no puede cancelarse en su estado actual. |

<br>

| **US-40** | **Consultar estado de solicitudes desde la aplicación móvil** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Cliente, quiero consultar el estado de mis solicitudes de crédito desde la aplicación móvil, para realizar seguimiento al proceso sin necesidad de ingresar desde otro dispositivo. |
| **Acceptance Criteria** | **Escenario 1 — Consulta de solicitudes**<br>**Dado** que el cliente tiene solicitudes de crédito registradas,<br>**Cuando** consulta el estado de sus trámites mediante el canal móvil,<br>**Entonces** la plataforma presenta la relación de solicitudes y el estado de avance de cada una.<br><br>**Escenario 2 — Sin solicitudes**<br>**Dado** que el cliente no cuenta con solicitudes crediticias registradas,<br>**Cuando** solicita la consulta de trámites,<br>**Entonces** la plataforma informa que no existen solicitudes activas o históricas. |

<br>

| **US-41** | **Gestionar notificaciones** |
| :--- | :--- |
| **User** | Usuario Autenticado |
| **Priority** | Media |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Usuario Autenticado, quiero gestionar mis preferencias de notificaciones, para controlar qué tipos de avisos deseo recibir de la plataforma. |
| **Acceptance Criteria** | **Escenario 1 — Configuración de preferencias**<br>**Dado** que el usuario está autenticado en la plataforma,<br>**Cuando** consulta sus ajustes de notificación,<br>**Entonces** la plataforma presenta los canales y tipos de avisos configurables.<br><br>**Escenario 2 — Guardado de preferencias**<br>**Dado** que el usuario actualiza sus preferencias de comunicación,<br>**Cuando** confirma las nuevas configuraciones,<br>**Entonces** la plataforma guarda las preferencias y las aplica a futuros eventos del sistema. |

<br>

| **US-42** | **Recibir notificaciones push** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Media |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Cliente, quiero recibir notificaciones push relacionadas con mis solicitudes, para conocer cambios importantes en su estado. |
| **Acceptance Criteria** | **Escenario 1 — Notificación enviada**<br>**Dado** que el cliente tiene activas las notificaciones para su cuenta,<br>**Cuando** se produce un cambio de estado en una de sus solicitudes,<br>**Entonces** la plataforma emite una notificación push informando el evento.<br><br>**Escenario 2 — Notificaciones deshabilitadas**<br>**Dado** que el cliente desactivó las notificaciones automáticas,<br>**Cuando** se genera un evento en una solicitud,<br>**Entonces** la plataforma no emite notificaciones push y conserva el registro en el historial interno. |

<br>

| **US-43** | **Ver lista de solicitudes asignadas** |
| :--- | :--- |
| **User** | Entidad Financiera |
| **Priority** | Alta |
| **Epic** | Evaluación y gestión de solicitudes de crédito |
| **Description** | Como Entidad Financiera, quiero visualizar la lista de solicitudes de crédito asignadas, para identificar los expedientes que debo evaluar. |
| **Acceptance Criteria** | **Escenario 1 — Solicitudes disponibles**<br>**Dado** que existen solicitudes de crédito asignadas a la entidad financiera,<br>**Cuando** consulta la bandeja de expedientes asignados,<br>**Entonces** la plataforma presenta las solicitudes pendientes de atención con sus datos principales.<br><br>**Escenario 2 — Sin solicitudes asignadas**<br>**Dado** que no existen solicitudes asignadas a la entidad financiera,<br>**Cuando** consulta su bandeja de trabajo,<br>**Entonces** la plataforma informa que no cuenta con expedientes pendientes de evaluación. |

<br>

| **US-44** | **Ver detalle del expediente del cliente** |
| :--- | :--- |
| **User** | Entidad Financiera |
| **Priority** | Alta |
| **Epic** | Evaluación y gestión de solicitudes de crédito |
| **Description** | Como Entidad Financiera, quiero consultar el expediente de un cliente, para revisar la información necesaria antes de evaluar su solicitud de crédito. |
| **Acceptance Criteria** | **Escenario 1 — Consulta del expediente**<br>**Dado** que la entidad financiera tiene asignada una solicitud de crédito,<br>**Cuando** solicita el expediente del cliente,<br>**Entonces** la plataforma presenta los antecedentes personales, financieros y del vehículo requeridos para la evaluación.<br><br>**Escenario 2 — Acceso no autorizado**<br>**Dado** que una solicitud de crédito corresponde a otra entidad financiera,<br>**Cuando** se intenta acceder a dicho expediente,<br>**Entonces** la plataforma restringe el acceso por políticas de confidencialidad y permisos. |

<br>

| **US-45** | **Evaluar solicitud de crédito** |
| :--- | :--- |
| **User** | Entidad Financiera |
| **Priority** | Alta |
| **Epic** | Evaluación y gestión de solicitudes de crédito |
| **Description** | Como Entidad Financiera, quiero evaluar una solicitud de crédito, para determinar su resultado de acuerdo con las condiciones y criterios definidos. |
| **Acceptance Criteria** | **Escenario 1 — Evaluación aprobada**<br>**Dado** que la entidad financiera cuenta con un expediente asignado y la documentación conforme,<br>**Cuando** registra el dictamen favorable de la solicitud,<br>**Entonces** la plataforma actualiza el estado del crédito a aprobado y asocia las condiciones acordadas.<br><br>**Escenario 2 — Evaluación rechazada**<br>**Dado** que un expediente no cumple con los requisitos crediticios de la entidad,<br>**Cuando** se registra el dictamen desfavorable justificando el motivo,<br>**Entonces** la plataforma actualiza el estado a rechazado y registra las causales correspondientes. |

<br>

| **US-46** | **Notificar resultado de evaluación** |
| :--- | :--- |
| **User** | Cliente |
| **Priority** | Alta |
| **Epic** | Evaluación y gestión de solicitudes de crédito |
| **Description** | Como Cliente, quiero recibir el resultado de la evaluación de mi solicitud de crédito, para conocer si mi solicitud fue aprobada o rechazada y continuar con el proceso correspondiente. |
| **Acceptance Criteria** | **Escenario 1 — Resultado disponible**<br>**Dado** que la entidad financiera finalizó la evaluación de una solicitud,<br>**Cuando** se emite el dictamen formal,<br>**Entonces** la plataforma comunica el resultado al cliente a través de los canales de contacto configurados.<br><br>**Escenario 2 — Resultado no disponible**<br>**Dado** que una solicitud de crédito continúa en proceso de evaluación,<br>**Cuando** el cliente consulta el dictamen,<br>**Entonces** la plataforma informa que la solicitud aún se encuentra en revisión. |

<br>

| **US-47** | **Consultar usuarios registrados** |
| :--- | :--- |
| **User** | Administrador |
| **Priority** | Alta |
| **Epic** | Administración de usuarios y roles |
| **Description** | Como Administrador, quiero consultar la lista de usuarios registrados, para administrar y supervisar las cuentas existentes en la plataforma. |
| **Acceptance Criteria** | **Escenario 1 — Lista de usuarios**<br>**Dado** que existen cuentas de usuarios creadas en la plataforma,<br>**Cuando** el administrador solicita la consulta de usuarios registrados,<br>**Entonces** la plataforma presenta el listado de cuentas con su información administrativa y estado.<br><br>**Escenario 2 — Sin usuarios**<br>**Dado** que no existen cuentas que coincidan con un criterio de búsqueda,<br>**Cuando** el administrador realiza la consulta,<br>**Entonces** la plataforma informa que no se encontraron usuarios disponibles. |

<br>

| **US-48** | **Modificar roles de usuario** |
| :--- | :--- |
| **User** | Administrador |
| **Priority** | Alta |
| **Epic** | Administración de usuarios y roles |
| **Description** | Como Administrador, quiero modificar los roles de un usuario, para controlar los permisos y funcionalidades a los que puede acceder dentro de la plataforma. |
| **Acceptance Criteria** | **Escenario 1 — Modificación de rol**<br>**Dado** que el administrador cuenta con permisos de gestión de usuarios,<br>**Cuando** asigna un rol permitido a una cuenta y confirma la operación,<br>**Entonces** la plataforma actualiza el rol del usuario y aplica los privilegios correspondientes.<br><br>**Escenario 2 — Rol no permitido**<br>**Dado** que el administrador intenta asignar un rol no compatible o restringido,<br>**Cuando** solicita la confirmación del cambio,<br>**Entonces** la plataforma rechaza la asignación e informa que el rol no puede ser asignado. |

<br>

| **SP-01** | **Investigar el cálculo de simulaciones de crédito vehicular** |
| :--- | :--- |
| **User** | Developer |
| **Priority** | Alta |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Developer, quiero investigar las variables y fórmulas financieras para el cálculo de cuotas de crédito vehicular, **con el objetivo de** determinar la viabilidad técnica y definir el algoritmo que produzca resultados exactos según las tasas del mercado. |
| **Acceptance Criteria** | **Escenario 1 — Análisis y documentación de reglas de cálculo**<br>**Dado** que se requiere exactitud financiera en la simulación de créditos vehiculares,<br>**Cuando** se investigan y validan las variables, fórmulas y tasas de interés aplicables,<br>**Entonces** se presenta un documento técnico que detalla el algoritmo de cálculo, los datos de entrada requeridos y los casos de uso esperados.<br><br>**Escenario 2 — Prototipo funcional de prueba**<br>**Dado** que se cuenta con el algoritmo de cálculo documentado,<br>**Cuando** se ejecuta una prueba de concepto aislada con datos reales de simulación,<br>**Entonces** se entrega un prototipo funcional mínimo (script o test) que valide los resultados obtenidos frente a los valores esperados, adjuntando las conclusiones técnicas. |

<br>

| **SP-02** | **Investigar servicios de notificaciones por correo y push** |
| :--- | :--- |
| **User** | Developer |
| **Priority** | Media |
| **Epic** | Simulación y seguimiento crediticio |
| **Description** | Como Developer, quiero investigar pasarelas y servicios de mensajería (email y push), **con el objetivo de** seleccionar la herramienta más eficiente y compatible con nuestro backend para automatizar las notificaciones de cambio de estado en los créditos. |
| **Acceptance Criteria** | **Escenario 1 — Matriz comparativa de servicios de notificación**<br>**Dado** que el sistema necesita comunicar eventos en tiempo real a los clientes,<br>**Cuando** se investigan proveedores de notificaciones (ej. SendGrid, Firebase, etc.),<br>**Entonces** se documenta una matriz de evaluación que incluya compatibilidad, cuotas gratuitas, latencia y facilidad de integración con Spring Boot.<br><br>**Escenario 2 — Prueba funcional de envío**<br>**Dado** que se ha elegido un proveedor de notificaciones,<br>**Cuando** se configura la credencial de prueba y se simula un evento de solicitud aprobada,<br>**Entonces** se entrega un prototipo funcional mínimo que envía exitosamente un correo o notificación push de prueba, registrando las conclusiones técnicas. |

<br>

| **TS-01** | **Integrar validación de RUC con SUNAT** |
| :--- | :--- |
| **User** | Developer |
| **Priority** | Alta |
| **Epic** | Gestión de perfil y roles |
| **Description** | Como Developer, quiero integrar el servicio de consulta de RUC de SUNAT, para validar la información de las empresas ingresadas durante el registro o solicitud del rol de Concesionaria. |
| **Acceptance Criteria** | **Escenario 1 — RUC válido**<br>**Dado** que el sistema recibe un número de RUC válido,<br>**Cuando** consulta el servicio de SUNAT,<br>**Entonces** obtiene la información asociada al RUC y confirma que se encuentra registrado.<br><br>**Escenario 2 — RUC no encontrado**<br>**Dado** que el sistema recibe un número de RUC que no se encuentra registrado en SUNAT,<br>**Cuando** realiza la consulta,<br>**Entonces** informa que el RUC no pudo ser validado.<br><br>**Escenario 3 — Error en el servicio de SUNAT**<br>**Dado** que el servicio de SUNAT no se encuentra disponible,<br>**Cuando** el sistema intenta validar el RUC,<br>**Entonces** registra el error de la consulta e informa que no fue posible realizar la validación,<br>**Y** no considera el RUC como validado. |

<br>

## 3.3. Product Backlog

En esta sección se presenta el Product Backlog priorizado del proyecto. Siguiendo las directrices del curso, el orden de los elementos se ha determinado estrictamente por el valor que aportan al negocio, colocando en las primeras posiciones las historias relacionadas con el sitio web estático (Landing Page) para asegurar su inclusión desde el primer sprint. Asimismo, se ha evitado el anti-patrón de colocar las historias de seguridad o autenticación al inicio, priorizando antes la visualización del catálogo y la propuesta de valor.

A continuación, se detalla la tabla de estimación utilizando la escala de Story Points (1, 2, 3, 5, 8).

| # Orden | User Story Id | Título | Descripción | Story Points |
| :---: | :---: | :--- | :--- | :--- | :---: |
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
