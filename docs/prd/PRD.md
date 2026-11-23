# PRD · Herramienta de organización del staff del Interact2Hack

**Versión:** borrador 1 · **Fecha:** 23 de noviembre de 2026 · **Equipo:** Justin Peñafiel
**Fuentes:** descripción del proyecto (`docs/fuentes/descripcion-proyecto.md`) y respuestas del cliente de la sesión del 11 de noviembre (`docs/cliente/preguntas.md`)

Este documento dice qué debe hacer la herramienta y qué no. Cómo se construye se decide después, en las specs.

---

// 1. Problema y contexto

En ediciones anteriores del Interact2Hack, las tareas del staff se repartían por grupos de WhatsApp. Con tantos mensajes, las instrucciones se perdían: a quien le encargaban algo, su mensaje quedaba 80 mensajes atrás.

La herramienta reemplaza eso. Los administradores crean tareas en forma de checklist, con lugar y hora límite, y las asignan a estudiantes del staff. Cada estudiante ve en su celular qué le toca, lo ejecuta paso a paso y confirma. Los administradores ven en una sola pantalla cómo va todo.

Se usa durante el hackathon, que dura tres días (viernes a domingo), en el campus. El staff no está todos los días ni a todas horas. La herramienta debe estar lista para empezar a probarse en enero.

---

// 2. Usuarios y perfiles

| Perfil | Puede | No puede |
| --- | --- | --- |
| **Administrador** | Ver, crear, editar y eliminar usuarios (administradores y staff). Cambiar la contraseña de cualquier usuario. Definir la disponibilidad del staff. Ver, crear, editar y eliminar tareas. Asignarlas a uno o varios estudiantes, o marcarlas como urgentes. Agregar lugares. Ver el tablero y todas las tareas, también las de otros administradores. Reasignar una tarea vencida y cambiarle la fecha. | Ser staff a la vez. Editar o borrar una tarea en ejecución. Editar una tarea que otro administrador está editando. Borrar una tarea completada. |
| **Estudiante de staff** | Ver sus tareas asignadas y las urgentes abiertas. Ejecutar una tarea: marcar el checklist, dejar observaciones y finalizar. Ver su historial de tareas realizadas. Ver los compañeros asignados a la misma tarea y llamarlos. Cambiar su contraseña. | Crear, editar o borrar tareas. Ver las tareas de otros. Ser administrador a la vez. Registrarse por su cuenta. |

Hay además un **administrador master**: una cuenta inicial que se entrega al cliente. Es un administrador más; su papel es crear a los demás la primera vez y servir de respaldo si alguien pierde el acceso.

Todos entran con correo y contraseña. No existe registro: los usuarios los crea un administrador.

---

// 3. Objetivos y éxito

| Objetivo | Cómo sabrá el cliente que se cumplió |
| --- | --- |
| Que ninguna instrucción se pierda | Cada estudiante abre la herramienta y ve sus tareas pendientes, con lugar, hora y pasos, sin buscar entre mensajes. |
| Saber cómo va todo sin abrir tarea por tarea | El administrador abre el tablero y, de un vistazo, sabe cuántas tareas están completadas, en ejecución, pendientes, sin asignar y vencidas. |
| Que lo urgente se atienda primero | Las tareas vencidas y las próximas a vencer aparecen arriba del tablero; el staff recibe un aviso cuando le queda menos de una hora. |
| Que las tareas se terminen | Al cerrar el evento no quedan tareas pendientes ni vencidas sin atender. |

El cliente no dio cifras de éxito. Las medidas de arriba son comprobables en la práctica, pero son nuestra propuesta [SUPUESTO S-10].

---

// 4. Alcance (MoSCoW)

| Prioridad | Funcionalidad |
| --- | --- |
| **Must** | Inicio de sesión para los dos perfiles. Gestión de usuarios por administradores (nombre, correo institucional, teléfono, perfil). Administrador master inicial. Cambio de contraseña, recuperación por correo y cambio por un administrador. Lugares precargados y gestión de lugares. Crear, editar y eliminar tareas con checklist. Asignación a uno o varios estudiantes. Los cinco estados y sus bloqueos. Ejecución de la tarea en el celular, con confirmación al finalizar. Tablero del administrador ordenado por prioridad. Aviso en la app cuando falta menos de una hora. Aviso de falta de conexión. Disponibilidad del staff por día y hora. |
| **Should** | Tareas urgentes abiertas a todo el staff. Historial de tareas del estudiante. Contador de tiempo restante al abrir una tarea. Ver compañeros de la tarea con enlace para llamar. Envío de credenciales por correo al crear un usuario. |
| **Could** | Evidencia opcional al completar (foto o PDF). Modo demo con tareas de prueba para que el staff aprenda antes del evento. Registro de auditoría de lo que se hizo. |
| **Won't (esta versión)** | Ver sección 5. |

---

// 5. No-alcance

- Correos de aviso o recordatorios de vencimiento: el aviso es solo dentro de la app.
- Trabajo sin conexión con sincronización posterior.
- Chat o grupos de conversación dentro de la herramienta.
- Líder de grupo o reparto del checklist entre varios estudiantes.
- Usuarios con dos perfiles a la vez.
- Categorías de tareas (videojuegos, apps, etc.).
- Registro de usuarios por su cuenta.
- Tareas repetidas o programadas por adelantado [SUPUESTO S-07].
- Tareas de redes sociales o fotos del evento.
- Aplicación móvil instalable: se usa desde el navegador del celular.

---

// 6. Reglas de negocio

**Usuarios y acceso**

| Id | Regla |
| --- | --- |
| R1 | Un usuario es administrador o staff, nunca los dos. |
| R2 | No hay registro público. Solo un administrador crea usuarios. Para crear uno se piden tres datos: nombre completo, correo institucional y teléfono celular, además de su perfil. |
| R3 | Existe un administrador master inicial, entregado al cliente. Crea a los primeros administradores y puede cambiar la contraseña de cualquiera. |
| R4 | El administrador pone la contraseña inicial. Cada usuario puede cambiarla desde su perfil. Si la olvida, puede recuperarla desde la pantalla de acceso con su correo, y también puede pedir a un administrador que se la cambie. |
| R5 | Al crear o editar a un estudiante de staff, el administrador define en qué días y horas está disponible. Al asignar una tarea, solo aparecen los estudiantes disponibles en esa fecha y hora. |
| R6 | Cuando un estudiante avisa fuera de la herramienta que no podrá asistir, el administrador cambia su disponibilidad para que no le asignen más tareas. |

**Tareas**

| Id | Regla |
| --- | --- |
| R7 | Una tarea tiene título, lugar, fecha y hora de vencimiento, checklist (pasos) y responsables. Los responsables pueden ser uno o varios, o ninguno: la tarea se puede guardar sin asignar. |
| R8 | El lugar se escoge de una lista, no se escribe. La lista parte con cinco lugares: Casa Blanca, Salón Azul, Patio del Da Vinci, Teatro Calderón de la Barca y Teatro Shakespeare. Un administrador puede agregar más (por ejemplo, un aula específica). |
| R9 | Una tarea está siempre en uno de cinco estados: **no asignado** (sin responsables), **pendiente** (con responsables, sin empezar), **en ejecución**, **completada** y **vencida**. |
| R10 | Una tarea pasa a **en ejecución** cuando un estudiante marca el primer paso de su checklist. Solo abrirla no la cambia de estado. |
| R11 | Un estudiante solo puede tener una tarea en ejecución a la vez. Para empezar otra, debe terminar la actual. Puede abrir otras tareas para verlas, pero no marcar pasos hasta terminar la actual. |
| R12 | Una tarea en ejecución queda bloqueada: ningún administrador puede editarla ni borrarla. |
| R13 | Dos administradores no pueden editar la misma tarea al mismo tiempo. Mientras uno la tiene abierta para editar, la tarea figura como en edición y el otro administrador solo puede verla. |
| R14 | Una tarea se completa cuando todos los pasos están marcados y el estudiante presiona finalizar. El sistema no deja finalizar con pasos sin marcar. Antes de completar pide una confirmación. |
| R15 | Las observaciones son opcionales. Es la forma en que el staff avisa de un problema o sugiere algo a los administradores; el staff no puede crear tareas. |
| R16 | Si una tarea tiene varios responsables, basta con que uno la complete: queda completada para todos y desaparece de las pendientes de los demás. Todos tienen la misma capacidad de ejecutarla. Se registra el nombre de quien la completó. |
| R17 | Una tarea marcada como urgente no necesita responsables: queda abierta a todo el staff disponible. El primero que la completa se la adjudica y la cierra. |
| R18 | El estudiante puede hacer sus tareas asignadas en el orden que quiera. Todas tienen la misma prioridad. |

**Tiempos**

| Id | Regla |
| --- | --- |
| R19 | Una tarea está **próxima a vencer** cuando falta menos de 1 hora para su hora límite. El staff ve un aviso destacado arriba de la pantalla, dentro de la app. |
| R20 | Si pasa la hora límite sin completarse, la tarea pasa a **vencida**. Un administrador puede entrar, cambiarle la fecha y hora y reasignarla. Mientras esté vencida, no se puede completar [SUPUESTO S-02]. |
| R21 | Al abrir una tarea, el estudiante ve cuánto tiempo falta para que venza. |

**Tablero, historial y conexión**

| Id | Regla |
| --- | --- |
| R22 | La pantalla principal del administrador es un tablero de tarjetas, una por tarea, con su estado y un código de color. Se ordena así: vencidas, próximas a vencer (la que vence antes, primero), en ejecución, sin asignar y completadas. |
| R23 | Las tareas completadas se agrupan en una sección plegable al final del tablero y no se pueden borrar: quedan como registro. Una tarea eliminada se oculta pero no se pierde [SUPUESTO S-06]. |
| R24 | El estudiante solo ve las tareas que le asignaron y las urgentes abiertas. Los administradores ven todas, incluidas las de otros administradores. |
| R25 | El estudiante ve su historial de tareas realizadas. |
| R26 | En la tarea se muestran los compañeros asignados con su teléfono, y tocar el número inicia una llamada. |
| R27 | Si el dispositivo pierde la conexión, la herramienta lo avisa y no permite guardar ni finalizar hasta que vuelva. No guarda nada para sincronizar después. |
| R28 | (Could) Al completar una tarea se puede adjuntar una evidencia, como una foto o un PDF. Nunca es obligatoria. |

---

// 7. Épicas

| Id | Épica | Descripción | Prioridad |
| --- | --- | --- | --- |
| E1 | Acceso y usuarios | Inicio de sesión con dos perfiles, administrador master y gestión de usuarios por los administradores. Incluye contraseña inicial, cambio de contraseña, recuperación por correo y cambio por un administrador. (R1–R4) | Must |
| E2 | Disponibilidad y lugares | El administrador define cuándo está disponible cada estudiante y mantiene la lista de lugares del evento. Así, las tareas solo se asignan a quien está y en lugares válidos. (R5, R6, R8) | Must |
| E3 | Tareas y asignación | El administrador crea, edita y elimina tareas con su checklist, las asigna a uno o varios estudiantes o las marca como urgentes, y las reasigna si vencen. Respeta los bloqueos mientras alguien las ejecuta o las edita. (R7, R9, R12, R13, R17, R20) | Must |
| E4 | Ejecución de tareas | El estudiante, desde su celular, ve sus tareas, abre una, marca los pasos, deja observaciones y la finaliza con confirmación. Incluye el contador, los compañeros y el historial. (R10, R11, R14–R16, R18, R21, R25, R26) | Must |
| E5 | Tablero de cumplimiento | Pantalla principal del administrador: tarjetas con estado y color, ordenadas por prioridad, con las completadas archivadas al final. (R22–R24) | Must |
| E6 | Avisos y conexión | Aviso dentro de la app cuando una tarea está por vencer y aviso de falta de conexión que impide guardar. (R19, R27) | Must |
| E7 | Evidencia y práctica | Adjuntar evidencia opcional al completar y un modo demo para que el staff practique antes del evento. (R28) | Could |

---

// 8. Supuestos y puntos abiertos

| Id | Supuesto | Por qué lo decidimos así | Estado |
| --- | --- | --- | --- |
| S-01 | Al crear un usuario, la herramienta le envía sus credenciales por correo. | El cliente dijo que le parecía mejor y más automático, pero también aceptó que el administrador se las dé. | `[SUPUESTO]` |
| S-02 | Una tarea vencida no se puede completar hasta que un administrador le cambie la fecha. | El cliente dijo "se bloquea" al preguntar qué pasa cuando vence, y que el administrador cambia la fecha y reasigna. No dijo nada de completarla tarde. | `[SUPUESTO]` · preguntar |
| S-03 | Si una tarea vence mientras está en ejecución, pasa a vencida y conserva los pasos ya marcados. | No se habló de este caso. Conservar el avance evita que el estudiante pierda su trabajo. | `[SUPUESTO]` · preguntar |
| S-04 | Al reasignar una tarea que ya tenía pasos marcados, los pasos se conservan. | Las tareas se tratan como una sola lista compartida (R16); el avance pertenece a la tarea. | `[SUPUESTO]` |
| S-05 | No se impide asignar a un estudiante dos tareas para la misma hora; solo puede ejecutar una a la vez (R11). | El cliente puso el límite en la ejecución, no en la asignación. | `[SUPUESTO]` |
| S-06 | Eliminar una tarea o un usuario lo oculta, pero conserva su registro. | El cliente pidió no perder el historial de lo completado y habló de borrado lógico. De usuarios no dijo nada. | `[SUPUESTO]` |
| S-07 | No hay tareas repetidas: cada una se crea por separado. | No se habló del tema; es lo más simple para esta versión. | `[SUPUESTO]` |
| S-08 | Cada paso se guarda al marcarlo, no solo al finalizar. | El cliente dijo que el primer check pasa la tarea a en ejecución, lo que requiere que se registre en ese momento. | `[SUPUESTO]` |
| S-09 | Seguimos la identidad visual del Interact2Hack que tenemos (brandboard "Señal neón"), a la espera de la carpeta de materiales que el cliente prometió. | El cliente pidió usar la identidad del evento; los colores bastan y el resto es libre. | `[SUPUESTO]` |
| S-10 | Las medidas de éxito de la sección 3 son propuestas nuestras. | El cliente no dio cifras. | `[SUPUESTO]` |

**Puntos abiertos (para el cliente el 2 de diciembre):**

- ¿Una tarea vencida se puede completar tarde, o solo después de que un administrador cambie la fecha? (S-02)
- ¿Qué pasa con una tarea que vence mientras alguien la está ejecutando? (S-03)
- ¿Qué pasa con las tareas ya completadas cuando se elimina a un usuario? (S-06)
- ¿Cuántos estudiantes usarán la herramienta a la vez? No se habló y afecta el diseño de las listas.
- Si se necesita un plan de pago de la base de datos, el cliente dijo que se pagaría un mes. No lo resolvemos aquí.

---

// 9. Trazabilidad

| Regla | Origen |
| --- | --- |
| R1 | P-20 |
| R2 | P-22 y descripción del proyecto (no hay registro) |
| R3 | Respuesta nueva del cliente (usuario master) |
| R4 | P-22, P-23 y S-01 |
| R5 | Respuesta nueva del cliente (disponibilidad) |
| R6 | Respuesta nueva del cliente (imprevistos) |
| R7 | Descripción del proyecto (cómo crear tareas) y P-18 |
| R8 | P-18 |
| R9 | P-05 |
| R10 | P-05 y P-07 |
| R11 | P-04 |
| R12 | P-16 |
| R13 | P-16 |
| R14 | P-06 y descripción del proyecto (cómo completar una tarea) |
| R15 | P-10 |
| R16 | P-01, P-02 y P-14 |
| R17 | Respuesta nueva del cliente (tareas urgentes) |
| R18 | P-09 |
| R19 | P-13 y P-28 |
| R20 | P-11, P-12, S-02 y S-03 |
| R21 | Respuesta nueva del cliente (contador) |
| R22 | P-15 y descripción del proyecto (tablero de cumplimiento) |
| R23 | P-17 y S-06 |
| R24 | P-21 |
| R25 | Respuesta nueva del cliente (historial) |
| R26 | Respuesta nueva del cliente (teléfono y llamada) |
| R27 | P-25 |
| R28 | Respuesta nueva del cliente (evidencia opcional) |
