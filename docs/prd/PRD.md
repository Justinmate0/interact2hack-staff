# PRD · Herramienta de organización del staff del Interact2Hack

**Versión:** 3 (revisado con las decisiones del 25 de noviembre, ver `docs/prd/revision.md`) · **Fecha:** 25 de noviembre de 2026 · **Equipo:** Justin Peñafiel
**Fuentes:** descripción del proyecto (`docs/fuentes/descripcion-proyecto.md`) y respuestas del cliente de la sesión del 11 de noviembre (`docs/cliente/preguntas.md`)

Este documento dice qué debe hacer la herramienta y qué no, o sea, el qué. El cómo se construye se decide después, en las specs.

---

// 1. Problema y contexto

En ediciones anteriores del Interact2Hack, las tareas del staff se repartían por grupos de WhatsApp. Con tantos mensajes, las instrucciones se perdían (a quien le encargaban algo, su mensaje quedaba 80 mensajes atrás).

La herramienta reemplaza eso. Los administradores crean tareas en forma de checklist, con lugar y hora límite, y las asignan a estudiantes del staff. Cada estudiante ve en su celular qué le toca, lo hace paso a paso y confirma. Los administradores ven en una sola pantalla cómo va todo.

Se usa durante el hackathon, que dura tres días (viernes a domingo), en el campus. El staff no está todos los días ni a todas horas, y la conexión puede fallar. La herramienta debe estar lista para empezar a probarse en enero.

---

// 2. Usuarios y perfiles

| Perfil | Puede | No puede |
| --- | --- | --- |
| **Administrador** | Ver, crear, editar y eliminar usuarios (administradores y staff). Cambiar la contraseña de cualquier usuario, incluso de otro administrador. Definir la disponibilidad del staff. Ver, crear, editar y eliminar tareas. Asignarlas a uno o varios estudiantes, o marcarlas como urgentes. Agregar lugares. Ver el tablero y todas las tareas, también las de otros administradores. Reasignar una tarea vencida y cambiarle la fecha. | Ser staff a la vez. Eliminarse a sí mismo ni eliminar al master. Editar o borrar una tarea en ejecución. Editar una tarea que otro administrador está editando. Borrar una tarea completada. |
| **Estudiante de staff** | Ver sus tareas asignadas y las urgentes abiertas. Ejecutar una tarea: marcar el checklist, dejar observaciones y finalizar. Ver su historial de tareas realizadas. Ver los compañeros asignados a la misma tarea y llamarlos. Cambiar su contraseña. | Crear, editar o borrar tareas. Ver las tareas de otros. Ser administrador a la vez. Registrarse por su cuenta. |

Hay además un **administrador master**: una cuenta inicial que se entrega al cliente. Es un administrador más, con los mismos poderes que los demás. Solo se diferencia en que nadie lo puede eliminar, así el cliente nunca se queda sin acceso.

Todos entran con correo y contraseña. No existe registro: los usuarios los crea un administrador.

---

// 3. Objetivos y éxito

| Objetivo | Cómo sabrá el cliente que se cumplió |
| --- | --- |
| Que ninguna instrucción se pierda | Cada estudiante abre la herramienta y ve sus tareas pendientes, con lugar, hora y pasos, sin buscar entre mensajes. |
| Saber cómo va todo sin abrir tarea por tarea | El administrador abre el tablero y, de un vistazo, sabe cuántas tareas están completadas, en ejecución, pendientes, sin asignar y vencidas. |
| Que lo urgente se atienda primero | Las tareas vencidas y las próximas a vencer aparecen arriba del tablero; el staff recibe un aviso cuando le queda menos de una hora. |
| Que las tareas se terminen | Al cerrar el evento, el administrador ve en el tablero que todas las tareas están completadas, o cuáles quedaron sin hacer. |

El cliente no dio cifras de éxito. Las medidas de arriba se pueden comprobar en la práctica, pero son propuesta nuestra [SUPUESTO S-10].

---

// 4. Alcance (MoSCoW)

| Prioridad | Funcionalidad |
| --- | --- |
| **Must** | Inicio de sesión para los dos perfiles. Gestión de usuarios por administradores (nombre, correo institucional, teléfono, perfil). Administrador master inicial. Cambio de contraseña, recuperación por correo y cambio por un administrador. Entrega de credenciales por correo o en persona, a elección del administrador. Lugares precargados y gestión de lugares. Crear, editar y eliminar tareas con checklist. Asignación a uno o varios estudiantes. Los cinco estados y sus bloqueos. Ejecución de la tarea en el celular, con confirmación al finalizar. Tablero del administrador ordenado por prioridad. Aviso en la app cuando falta menos de una hora. Aviso de falta de conexión. Disponibilidad del staff por día y hora. |
| **Should** | Tareas urgentes abiertas a todo el staff. Historial de tareas del estudiante. Contador de tiempo restante al abrir una tarea. Ver compañeros de la tarea con enlace para llamar. Aviso al administrador cuando asigna a un estudiante dos tareas que vencen a la misma hora. |
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
| R2 | No hay registro público. Solo un administrador crea usuarios. Para crear uno se piden tres datos: nombre completo, correo institucional y teléfono celular, además de su perfil. Solo un administrador cambia esos datos; cada usuario cambia solo su contraseña [SUPUESTO S-18]. |
| R3 | Existe un administrador master inicial, entregado al cliente. Crea a los primeros administradores y tiene los mismos poderes que cualquier otro administrador: todos los administradores tienen los mismos privilegios, y cualquiera puede cambiar la contraseña de cualquier usuario, incluso la de otro administrador. Nadie puede eliminar al master, y un administrador no puede eliminarse a sí mismo [SUPUESTO S-17]. |
| R4 | El administrador pone la contraseña inicial y, al crear el usuario, elige cómo se la entrega: la herramienta se la manda por correo, o se la da él en persona [SUPUESTO S-01]. Cada usuario puede cambiarla desde su perfil. Si la olvida, puede recuperarla desde la pantalla de acceso con su correo, y también puede pedir a un administrador que se la cambie. |
| R5 | Al crear o editar a un estudiante de staff, el administrador define en qué días y horas está disponible, con un solo rango de horas por día [SUPUESTO S-25]. Al asignar una tarea, solo aparecen los estudiantes disponibles en la fecha y hora de vencimiento de la tarea [SUPUESTO S-14]. |
| R6 | Cuando un estudiante avisa fuera de la herramienta que no podrá asistir, el administrador cambia su disponibilidad para que no le asignen más tareas. |

**Tareas**

| Id | Regla |
| --- | --- |
| R7 | Una tarea tiene título (obligatorio) [SUPUESTO S-13], lugar, fecha y hora de vencimiento, checklist (pasos) y responsables. Los responsables pueden ser uno o varios, o ninguno: la tarea se puede guardar sin asignar. |
| R8 | El lugar se escoge de una lista, no se escribe. La lista parte con cinco lugares: Casa Blanca, Salón Azul, Patio del Da Vinci, Teatro Calderón de la Barca y Teatro Shakespeare. Un administrador puede agregar más (por ejemplo, un aula específica). |
| R9 | Una tarea está siempre en uno de cinco estados: **no asignado** (sin responsables; si llega a su hora límite, pasa a vencida y la tarjeta lleva la marca «Sin responsables» [SUPUESTO S-15]), **pendiente** (con responsables, sin empezar), **en ejecución**, **completada** y **vencida**. |
| R10 | Una tarea pasa a **en ejecución** cuando un estudiante marca el primer paso de su checklist. Solo abrirla no la cambia de estado. |
| R11 | Un estudiante solo puede tener una tarea en ejecución a la vez. Para empezar otra, debe terminar la actual. Puede abrir otras tareas para verlas, pero no marcar pasos hasta terminar la actual. Si deja una tarea a medias, esta sigue en ejecución hasta que venza; al vencer pasa a vencida y el estudiante queda libre [SUPUESTO S-19]. |
| R12 | Una tarea en ejecución queda bloqueada: ningún administrador puede editarla ni borrarla. |
| R13 | Dos administradores no pueden editar la misma tarea al mismo tiempo. Mientras uno la tiene abierta para editar, la tarea figura como en edición y el otro administrador solo puede verla. |
| R14 | Una tarea se completa cuando todos los pasos están marcados y el estudiante presiona finalizar. El sistema no deja finalizar con pasos sin marcar. Antes de completar pide una confirmación. Los pasos se pueden marcar en cualquier orden, y una tarea completada no se reabre ni se desmarca [SUPUESTO S-16]. |
| R15 | Las observaciones son opcionales. Es la forma en que el staff avisa de un problema o sugiere algo a los administradores; el staff no puede crear tareas. |
| R16 | Si una tarea tiene varios responsables, basta con que uno la complete: queda completada para todos y desaparece de las pendientes de los demás. Todos tienen la misma capacidad de ejecutarla. Se registra el nombre de quien la completó. Mientras uno la está ejecutando, los demás responsables la ven «en ejecución» con su nombre y no pueden marcar pasos [SUPUESTO S-12]. |
| R17 | Una tarea marcada como urgente no necesita responsables: queda abierta a todo el staff disponible. El primero que marca un paso se la adjudica, y al completarla la cierra [SUPUESTO S-12]. Mientras nadie la toma, se ve como pendiente, no como no asignada [SUPUESTO S-20]. |
| R18 | El estudiante puede hacer sus tareas asignadas en el orden que quiera. Todas tienen la misma prioridad. |

**Tiempos**

| Id | Regla |
| --- | --- |
| R19 | Una tarea está **próxima a vencer** cuando falta menos de 1 hora para su hora límite. El staff ve un aviso destacado arriba de la pantalla, dentro de la app. |
| R20 | Si pasa la hora límite sin completarse, la tarea pasa a **vencida**. Un administrador puede entrar, cambiarle la fecha y hora y reasignarla. Mientras esté vencida, no se puede completar [SUPUESTO S-02]. Al reasignarla vuelve a pendiente si queda con responsables, o a no asignada si no, y conserva los pasos ya marcados [SUPUESTO S-22]. |
| R21 | Al abrir una tarea, el estudiante ve cuánto tiempo falta para que venza. |

**Tablero, historial y conexión**

| Id | Regla |
| --- | --- |
| R22 | La pantalla principal del administrador es un tablero de tarjetas, una por tarea, con su estado y un código de color. Se ordena así: vencidas, próximas a vencer (la que vence antes, primero), en ejecución, pendientes (por hora límite), sin asignar y completadas. Una vencida sin responsables sube igual arriba, con su marca «Sin responsables». Una tarea pendiente, en ejecución o sin asignar a la que le falta menos de 1 hora va en «próximas a vencer» [SUPUESTO S-11]. |
| R23 | Las tareas completadas se agrupan en una sección plegable al final del tablero y no se pueden borrar: quedan como registro. Una tarea eliminada se oculta pero no se pierde [SUPUESTO S-06]. Si se elimina a un usuario, sus tareas completadas se conservan; en las pendientes pierde su lugar de responsable, y si era el único la tarea pasa a no asignada [SUPUESTO S-24]. |
| R24 | El estudiante solo ve las tareas que le asignaron y las urgentes abiertas, incluidas sus tareas vencidas (que no puede completar). Los administradores ven todas, incluidas las de otros administradores [SUPUESTO S-23]. |
| R25 | El estudiante ve su historial de tareas realizadas. Ahí solo salen las que él completó, no las que completó otro responsable [SUPUESTO S-23]. |
| R26 | En la tarea se muestran los compañeros asignados con su teléfono, y tocar el número inicia una llamada. |
| R27 | Si el dispositivo pierde la conexión, la herramienta lo avisa y no permite marcar pasos, guardar ni finalizar hasta que vuelva, para que nadie crea que algo quedó guardado cuando no. No guarda nada para sincronizar después [SUPUESTO S-21]. |
| R28 | (Could) Al completar una tarea se puede adjuntar una evidencia, como una foto o un PDF. Nunca es obligatoria. |
| R29 | Al asignar una tarea, si el estudiante ya tiene otra que vence a la misma hora, la pantalla avisa al administrador. El aviso no impide asignarla: el administrador decide [SUPUESTO S-05]. |

---

// 7. Épicas

| Id | Épica | Descripción | Prioridad |
| --- | --- | --- | --- |
| E1 | Acceso y usuarios | Inicio de sesión con dos perfiles, administrador master y gestión de usuarios por los administradores. Incluye contraseña inicial, cambio de contraseña, recuperación por correo y cambio por un administrador. (R1–R4) | Must |
| E2 | Disponibilidad y lugares | El administrador define cuándo está disponible cada estudiante y mantiene la lista de lugares del evento. Así, las tareas solo se asignan a quien está y en lugares válidos. (R5, R6, R8) | Must |
| E3 | Tareas y asignación | El administrador crea, edita y elimina tareas con su checklist, las asigna a uno o varios estudiantes o las marca como urgentes, y las reasigna si vencen. Respeta los bloqueos mientras alguien las ejecuta o las edita. (R7, R9, R12, R13, R17, R20, R29) | Must |
| E4 | Ejecución de tareas | El estudiante, desde su celular, ve sus tareas, abre una, marca los pasos, deja observaciones y la finaliza con confirmación. Incluye el contador, los compañeros y el historial. (R10, R11, R14–R16, R18, R21, R25, R26) | Must |
| E5 | Tablero de cumplimiento | Pantalla principal del administrador: tarjetas con estado y color, ordenadas por prioridad, con las completadas archivadas al final. (R22–R24) | Must |
| E6 | Avisos y conexión | Aviso dentro de la app cuando una tarea está por vencer y aviso de falta de conexión que impide guardar. (R19, R27) | Must |
| E7 | Evidencia y práctica | Adjuntar evidencia opcional al completar y un modo demo para que el staff practique antes del evento. (R28) | Could |

---

// 8. Supuestos y puntos abiertos

| Id | Supuesto | Por qué lo decidimos así | Estado |
| --- | --- | --- | --- |
| S-01 | Al crear un usuario, el administrador elige si la herramienta le manda sus credenciales por correo o si se las da él en persona. | El cliente dijo que por correo le parecía mejor y más automático, pero también aceptó que el administrador se las dé. Dejamos las dos opciones. | `[SUPUESTO]` |
| S-02 | Una tarea vencida no se puede completar hasta que un administrador le cambie la fecha. | El cliente dijo "se bloquea" al preguntar qué pasa cuando vence, y que el administrador cambia la fecha y reasigna. No dijo nada de completarla tarde. | `[SUPUESTO]` · preguntar |
| S-03 | Si una tarea vence mientras está en ejecución, pasa a vencida y conserva los pasos ya marcados. | No se habló de este caso. Conservar el avance evita que el estudiante pierda su trabajo. | `[SUPUESTO]` · preguntar |
| S-04 | Al reasignar una tarea que ya tenía pasos marcados, los pasos se conservan. | Las tareas se tratan como una sola lista compartida (R16); el avance pertenece a la tarea. | `[SUPUESTO]` |
| S-05 | Se puede asignar a un estudiante dos tareas para la misma hora, pero la pantalla avisa al administrador. Solo se ejecuta una a la vez (R11). | El cliente puso el límite en la ejecución. Bloquear el cruce no se puede hacer bien porque la tarea solo tiene hora límite, sin hora de inicio ni duración; el aviso deja que el administrador decida. | `[SUPUESTO]` |
| S-06 | Eliminar una tarea o un usuario lo oculta, pero conserva su registro. | El cliente pidió no perder el historial de lo completado y habló de borrado lógico. De usuarios no dijo nada. | `[SUPUESTO]` |
| S-07 | No hay tareas repetidas: cada una se crea por separado. | No se habló del tema; es lo más simple para esta versión. | `[SUPUESTO]` |
| S-08 | Cada paso se guarda al marcarlo, no solo al finalizar. | El cliente dijo que el primer check pasa la tarea a en ejecución, lo que requiere que se registre en ese momento. | `[SUPUESTO]` |
| S-09 | Seguimos la identidad visual del Interact2Hack que tenemos (brandboard "Señal neón"), a la espera de la carpeta de materiales que el cliente prometió. | El cliente pidió usar la identidad del evento; los colores bastan y el resto es libre. | `[SUPUESTO]` |
| S-10 | Las medidas de éxito de la sección 3 son propuesta nuestra. | El cliente no dio cifras. Las armamos para que se puedan comprobar mirando la herramienta. | `[SUPUESTO]` |
| S-11 | Una tarea pendiente a más de 1 hora de vencer va después de las en ejecución, ordenada por hora límite, y antes de las sin asignar. Una sin asignar a la que le falta menos de 1 hora va en «próximas a vencer». | El cliente nombró los otros grupos pero no dónde van las pendientes. Una tarea con dueño que aún no empieza va antes que una sin dueño; y una que nadie tiene y está por vencer es la más peligrosa. | `[SUPUESTO]` |
| S-12 | Mientras un responsable ejecuta una tarea, los demás la ven en ejecución con su nombre y no marcan pasos. En una urgente, la reserva quien marca el primer paso. | El cliente quiso evitar que varios la completen a la vez y que haya que sincronizar. | `[SUPUESTO]` · preguntar |
| S-13 | Toda tarea tiene un título obligatorio. | Sin título no se puede distinguir una tarea en la lista. La descripción no lo menciona. | `[SUPUESTO]` |
| S-14 | La disponibilidad del staff se compara con la hora de vencimiento de la tarea. | La tarea solo tiene hora límite, no hora de inicio. | `[SUPUESTO]` |
| S-15 | Una tarea sin responsables que llega a su hora límite pasa a vencida y lleva la marca «Sin responsables». | Así no creamos un sexto estado (el cliente definió cinco) y el administrador la ve arriba del tablero, como pidió. | `[SUPUESTO]` |
| S-16 | Los pasos se marcan en cualquier orden, y una tarea completada es definitiva. | No se habló de orden de pasos ni de reabrir; el cliente solo dijo que las completadas no se borran. | `[SUPUESTO]` · preguntar |
| S-17 | Nadie elimina al administrador master y un administrador no se elimina a sí mismo. | El cliente quiere un administrador de respaldo por si se pierde una clave. | `[SUPUESTO]` |
| S-18 | Solo un administrador cambia nombre, correo y teléfono de un usuario. | El cliente dijo que el estudiante cambia su contraseña; no habló de otros datos. | `[SUPUESTO]` |
| S-19 | Si un estudiante deja una tarea a medias, esta sigue en ejecución hasta que venza; al vencer pasa a vencida y lo libera. | El cliente pidió el límite de una tarea a la vez y el bloqueo de la tarea en ejecución. Juntas, dejarían al estudiante atrapado. | `[SUPUESTO]` · preguntar |
| S-20 | Una tarea urgente que nadie ha tomado se ve como pendiente, no como no asignada. | Si no, una tarea que todo el staff puede tomar se mezclaría con las que nadie ve. | `[SUPUESTO]` |
| S-21 | Sin conexión tampoco se pueden marcar pasos. | Como cada paso se guarda al marcarlo (S-08), sin internet el estudiante creería que quedó guardado. | `[SUPUESTO]` |
| S-22 | Al reasignar una tarea vencida, vuelve a pendiente si queda con responsables o a no asignada si no, y conserva los pasos marcados. | El cliente dijo que el administrador cambia la fecha y reasigna, pero no a qué estado vuelve. | `[SUPUESTO]` |
| S-23 | El estudiante ve sus tareas vencidas (sin poder marcar pasos), y su historial solo incluye las que él completó. | El cliente habló de tareas pendientes e historial, sin decir qué pasa con estos casos. | `[SUPUESTO]` |
| S-24 | Al eliminar un usuario, sus tareas completadas se conservan; en las pendientes pierde su lugar de responsable, y si era el único la tarea pasa a no asignada. | El cliente no habló de eliminar usuarios. Es lo que menos daña el registro. | `[SUPUESTO]` · preguntar |
| S-25 | La disponibilidad es un solo rango de horas por día. | El cliente habló de «de qué hora a qué hora». Es lo más simple; dos bloques se pueden ampliar después. | `[SUPUESTO]` |

**Puntos abiertos (para el cliente el 2 de diciembre):**

- ¿Una tarea vencida se puede completar tarde, o solo después de que un administrador cambie la fecha? (S-02)
- ¿Qué pasa con una tarea que vence mientras alguien la está ejecutando? (S-03)
- ¿Qué pasa con las tareas ya completadas y las pendientes cuando se elimina a un usuario? (S-06, S-24)
- Si un estudiante empieza una tarea y la deja a medias, ¿cómo se libera antes de que venza? (S-19)
- Si una tarea en ejecución tiene más gente de la necesaria y está bloqueada, ¿cómo se reduce? El cliente pidió el bloqueo (R12) y también que un administrador la edite.
- Si cambia la disponibilidad de un estudiante, ¿qué pasa con las tareas que ya tenía asignadas? (R6)
- ¿Una tarea completada puede reabrirse si se hizo mal? (S-16)
- ¿Cuántos estudiantes usarán la herramienta a la vez? No se habló y afecta el diseño de las listas.
- Si hace falta pagar algún servicio de la herramienta, el cliente dijo que sería solo por un mes. No lo resolvemos aquí.

---

// 9. Trazabilidad

| Regla | Origen |
| --- | --- |
| R1 | P-20 |
| R2 | P-22, descripción del proyecto (no hay registro) y S-18 |
| R3 | Respuesta nueva del cliente (usuario master), P-21 (mismos privilegios para todos los administradores) y S-17 |
| R4 | P-22, P-23 y S-01 |
| R5 | Respuesta nueva del cliente (disponibilidad), S-14 y S-25 |
| R6 | Respuesta nueva del cliente (imprevistos) |
| R7 | Descripción del proyecto (cómo crear tareas), P-18 y S-13 |
| R8 | P-18 |
| R9 | P-05 y S-15 |
| R10 | P-05 y P-07 |
| R11 | P-04 y S-19 |
| R12 | P-16 |
| R13 | P-16 |
| R14 | P-06, descripción del proyecto (cómo completar una tarea) y S-16 |
| R15 | P-10 |
| R16 | P-01, P-02, P-14 y S-12 |
| R17 | Respuesta nueva del cliente (tareas urgentes), S-12 y S-20 |
| R18 | P-09 |
| R19 | P-13 y P-28 |
| R20 | P-11, P-12, S-02, S-03 y S-22 |
| R21 | Respuesta nueva del cliente (contador) |
| R22 | P-15, descripción del proyecto (tablero de cumplimiento), S-11 y S-15 |
| R23 | P-17, S-06 y S-24 |
| R24 | P-21 y S-23 |
| R25 | Respuesta nueva del cliente (historial) y S-23 |
| R26 | Respuesta nueva del cliente (teléfono y llamada) |
| R27 | P-25, S-08 y S-21 |
| R28 | Respuesta nueva del cliente (evidencia opcional) |
| R29 | P-04 y S-05 |
