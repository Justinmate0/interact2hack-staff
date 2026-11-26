# Revisión del PRD

**Equipo:** Justin Peñafiel · **Fecha:** 23 de noviembre de 2026, actualizada el 25 de noviembre
**Fuentes:** `docs/fuentes/descripcion-proyecto.md` y `docs/cliente/preguntas.md`
**Cómo se hizo:** con IA, como autorizó el profe. La IA (Claude) recorrió el PRD con la lista de 8 tipos de hueco y después lo atacó como socio escéptico. Justin revisó y aprobó las filas 1 a 13 el 23 de noviembre y las filas 14 a 21 el 25 de noviembre. **Marca del curso para la columna «Origen»:** «Sin IA» quiere decir que Justin ya revisó y aprobó la fila; «Con IA» quiere decir que la IA la produjo y Justin aún no la revisa. Ahora todas están en «Sin IA». Transparencia: los 21 huecos y las correcciones los encontró y redactó la IA (Claude); lo que hizo Justin fue revisarlos y decidir.

Tipos de hueco: 1 supuesto escrito como hecho · 2 regla vaga o sin cifra · 3 alcance inflado · 4 contradicción resuelta en silencio · 5 pregunta abierta desaparecida · 6 perfil o permiso incompleto · 7 detalle técnico · 8 regla sin trazabilidad.

## Huecos

| # | Sección | Frase exacta del PRD | Tipo | Gravedad | Origen | Qué dicen las fuentes | Corrección |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 6 · R22 | «Se ordena así: vencidas, próximas a vencer (la que vence antes, primero), en ejecución, sin asignar y completadas.» | 2 | alta | Sin IA | El cliente dio el orden vencidas, por vencer, sin asignar, terminadas y añadió «en ejecución» al final. Nunca dijo dónde van las pendientes que aún no están por vencer. | Aceptado. Las pendientes van después de en ejecución, por hora límite, y una tarea con menos de 1 hora (pendiente o en ejecución) va en «próximas a vencer». Nuevo S-11. |
| 2 | 6 · R12 | «Una tarea en ejecución queda bloqueada: ningún administrador puede editarla ni borrarla.» | 4 | alta | Sin IA | El cliente pidió el bloqueo, pero también dijo que si una tarea tenía más gente de la necesaria, «hay que comunicarse con un administrador para que edite la tarea». Se contradicen. | Aceptado. El bloqueo se mantiene y la contradicción pasa a puntos abiertos como pregunta al cliente. |
| 3 | 6 · R16 | «queda completada para todos y desaparece de las pendientes de los demás.» | 2 | alta | Sin IA | El cliente dijo que uno la abre y la completa, y que no hace falta sincronizar. No dijo qué ve un segundo responsable mientras el primero la está ejecutando. | Aceptado. Mientras uno la ejecuta, los demás la ven «en ejecución por [nombre]» y no pueden marcar pasos. Igual para urgentes. Nuevo S-12. |
| 4 | 6 · R5 | «solo aparecen los estudiantes disponibles en esa fecha y hora.» | 2 | alta | Sin IA | La tarea solo tiene hora límite (descripción del proyecto). La disponibilidad es por día y hora, pero no se dijo con qué hora se compara. | Aceptado. Se compara con la hora de vencimiento. Nuevo S-14. |
| 5 | 6 · R7 | «Una tarea tiene título, lugar, fecha y hora de vencimiento, checklist (pasos) y responsables.» | 1 | media | Sin IA | La descripción no menciona un título. En la sesión el cliente solo habló de «título» de pasada, sin confirmarlo. | Aceptado. El título queda como supuesto. Nuevo S-13. |
| 6 | 6 · R9 | «**no asignado** (sin responsables)» | 5 | media | Sin IA | No se habló de una tarea sin responsables que llega a su hora límite. | Aceptado. También pasa a vencida. Nuevo S-15. |
| 7 | 6 · R18 | «El estudiante puede hacer sus tareas asignadas en el orden que quiera.» | 5 | media | Sin IA | La pregunta P-09 (orden de los pasos dentro de una tarea) no tiene respuesta y desapareció del PRD. | Aceptado. Los pasos se pueden marcar en cualquier orden. Nuevo S-16. |
| 8 | 6 · R14 | «Una tarea se completa cuando todos los pasos están marcados y el estudiante presiona finalizar.» | 5 | media | Sin IA | P-08 (desmarcar o reabrir una tarea completada) quedó sin respuesta y sin mención. El cliente solo dijo que las completadas no se borran. | Aceptado. Una tarea completada no se reabre ni se desmarca. Mismo S-16, con pregunta para el cliente. |
| 9 | 6 · R3 | «Existe un administrador master inicial, entregado al cliente.» | 6 | media | Sin IA | El cliente quiere un usuario por encima de los demás por si alguien pierde la clave. No dijo si se puede eliminar. | Aceptado. Nadie puede eliminar al master y un administrador no se elimina a sí mismo. Nuevo S-17. |
| 10 | 2 · Estudiante | «Cambiar su contraseña.» | 6 | baja | Sin IA | El cliente dijo que el staff ve tareas, historial y cambia su contraseña. No dijo si puede editar su teléfono o correo. | Aceptado. Solo un administrador cambia nombre, correo y teléfono. Nuevo S-18. |
| 11 | 4 · Must | «Disponibilidad del staff por día y hora.» | 3 | media | Sin IA | El cliente dijo «eso sí es importante». El avance funcional del 2 de diciembre es pequeño y ya hay recuperación de contraseña por correo en Must. | Rechazado: se queda en Must por lo que dijo el cliente. El recorte se decide al armar las specs del Avance 3, no en el PRD. |
| 12 | 3 · Objetivos | «Al cerrar el evento no quedan tareas pendientes ni vencidas sin atender.» | 2 | baja | Sin IA | El cliente no dio cifras. | Rechazado: ya está declarado como supuesto S-10. |
| 13 | 6 · R14 | «Antes de completar pide una confirmación.» | 2 | baja | Sin IA | El cliente propuso una ventana de confirmación o un deslizador. | Rechazado: cómo se confirma es decisión de diseño y va en el DESIGN.md, no en el PRD. |
| 14 | 6 · R11 | «Un estudiante solo puede tener una tarea en ejecución a la vez.» | 5 | alta | Sin IA | El cliente pidió ese límite y, al preguntarle si el estudiante puede salirse de una tarea, dijo que «mejor que no». No dijo cómo se libera una tarea que alguien empezó y dejó a medias. Con R11 y R12 juntas, el estudiante no podría tomar otra tarea y ningún administrador podría tocar la suya. | Aceptado el 25 de noviembre. Pregunta nueva para el cliente. Mientras tanto, la tarea sigue en ejecución hasta que venza; al vencer pasa a vencida y libera al estudiante (S-03). Nuevo S-19. |
| 15 | 6 · R17 | «Una tarea marcada como urgente no necesita responsables: queda abierta a todo el staff disponible.» | 4 | media | Sin IA | R9 dice que una tarea sin responsables es «no asignado». Entonces una urgente que todos pueden tomar aparecería en el tablero como «sin asignar», mezclada con tareas que nadie ve. El cliente solo dijo que queda abierta a todos. | Aceptado el 25 de noviembre. Una urgente abierta se muestra como pendiente, no como no asignada, hasta que alguien marque un paso. Nuevo S-20. |
| 16 | 6 · R27 | «la herramienta lo avisa y no permite guardar ni finalizar hasta que vuelva.» | 4 | media | Sin IA | El cliente dijo que el botón de guardar se deshabilita sin conexión. Pero S-08 dice que cada paso se guarda al marcarlo: sin conexión, marcar un paso tampoco se podría guardar y el estudiante creería que quedó registrado. | Aceptado el 25 de noviembre. Sin conexión tampoco se pueden marcar pasos, y R27 lo dice. Nuevo S-21. |
| 17 | 2 · Perfiles | «Es un administrador más; su papel es crear a los demás la primera vez y servir de respaldo si alguien pierde el acceso.» | 4 | media | Sin IA | El cliente quiere un usuario «un nivel más arriba» por si un administrador pierde la clave. Pero la tabla de perfiles ya deja que cualquier administrador cambie la contraseña de cualquier usuario, así que el master no sirve de respaldo. | Rechazado el 25 de noviembre. El cliente dijo que todos los administradores tienen los mismos privilegios (P-21). Queda como regla firme: cualquier administrador cambia la contraseña de cualquier usuario, incluso de otro administrador; lo único que no se puede es eliminar al master o eliminarse a sí mismo (S-17). No se agrega como pregunta al cliente. |
| 18 | 6 · R20 | «Un administrador puede entrar, cambiarle la fecha y hora y reasignarla.» | 5 | media | Sin IA | El cliente dijo que el administrador cambia la fecha y reasigna. No dijo a qué estado vuelve la tarea ni qué pasa con los pasos marcados. | Aceptado el 25 de noviembre. Vuelve a pendiente si queda con responsables, o a no asignado si no, y conserva los pasos marcados (S-04). Nuevo S-22. |
| 19 | 6 · R24 | «El estudiante solo ve las tareas que le asignaron y las urgentes abiertas.» | 6 | media | Sin IA | No dice si el estudiante sigue viendo sus tareas vencidas ni si su historial incluye las que completó otro responsable. El cliente solo habló de tareas pendientes e historial. | Aceptado el 25 de noviembre. Ve sus tareas vencidas (sin poder marcar pasos) y su historial solo incluye las que él completó. Nuevo S-23. |
| 20 | 8 · S-06 | «Eliminar una tarea o un usuario lo oculta, pero conserva su registro.» | 5 | media | Sin IA | El cliente no habló de eliminar usuarios. S-06 solo cubre el historial de lo completado, no las tareas pendientes asignadas a un usuario eliminado. | Aceptado el 25 de noviembre. La tarea pierde a ese responsable; si era el único, pasa a no asignado. Nuevo S-24. |
| 21 | 6 · R5 | «define en qué días y horas está disponible.» | 2 | baja | Sin IA | El cliente habló de «de qué hora a qué hora» y de gente que viene solo en la mañana o solo en la tarde. No dijo si un día admite dos bloques, por ejemplo mañana y tarde con una pausa. | Aceptado el 25 de noviembre. Un solo rango de horas por día. Nuevo S-25. |

**Segunda pasada (ataque, solo con IA):** las filas 14 a 21 son problemas nuevos que la IA buscó después de la primera pasada. Justin las revisó el 25 de noviembre: aceptó siete y rechazó la 17. Las aceptadas ya están en el PRD (versión 3) como S-19 a S-25.

## Decisiones del 25 de noviembre

Al revisar los supuestos con Justin cambiaron cinco, además de las filas de arriba:

| Supuesto | Cambio | Razón |
| --- | --- | --- |
| S-01 | El administrador elige al crear el usuario si las credenciales van por correo o en persona. | El usuario no se registra, así que no puede escoger; las dos opciones del cliente quedan cubiertas. |
| S-05 | Se puede asignar igual, pero la pantalla avisa al administrador (nueva R29). | No se puede bloquear un cruce de horas porque la tarea solo tiene hora límite. |
| S-10 | La cuarta medida de éxito ahora se comprueba mirando el tablero. | Es más fácil de verificar que «no queda nada pendiente». |
| S-11 | Pendientes antes que sin asignar, y una sin asignar con menos de 1 hora va en próximas a vencer. | Caso que no habíamos visto: la tarea que nadie tiene y está por vencer. |
| S-15 | Una tarea sin responsables que llega a su hora pasa a vencida con la marca «Sin responsables». | No se crea un sexto estado y el administrador la ve arriba. |

## Para presentar

**1. El bloqueo contra la edición contradecía lo que pidió el cliente (fila 2).**
Qué decía el PRD: una tarea en ejecución no se puede editar. Por qué era un problema: el cliente también dijo que, si sobra gente, un administrador edita la tarea. Cómo quedó: el bloqueo sigue y la contradicción es la segunda pregunta para el cliente. Lo encontró la IA, y Justin lo revisó.

**2. El orden del tablero dejaba afuera a las pendientes (fila 1).**
Qué decía el PRD: vencidas, por vencer, en ejecución, sin asignar y completadas. Por qué era un problema: una tarea pendiente a más de una hora de vencer no tenía lugar en el tablero. Cómo quedó: va después de en ejecución, por hora límite (S-11). Lo encontró la IA, y Justin lo revisó.

**3. La disponibilidad se comparaba con una hora que la tarea no tiene (fila 4).**
Qué decía el PRD: al asignar, salen los disponibles «en esa fecha y hora». Por qué era un problema: la tarea solo tiene hora de vencimiento. Cómo quedó: se compara con la hora de vencimiento (S-14). Lo encontró la IA, y Justin lo revisó.

## Preguntas para el cliente

Ordenadas por prioridad, para el 2 de diciembre. Cada una va en palabras simples, para que el cliente conteste sí o no, o con un ejemplo:

1. Si una tarea ya venció y nadie la completó, ¿el estudiante todavía la puede completar tarde, o primero un administrador tiene que cambiarle la fecha? (S-02)
2. Cuando una tarea está en ejecución se bloquea y nadie la edita. Pero si en esa tarea hay más estudiantes de los necesarios, ¿el administrador puede quitar gente aunque esté bloqueada? (fila 2)
3. Si llega la hora de vencimiento mientras un estudiante está marcando los pasos, ¿se guarda lo que ya marcó y quién la puede terminar? (S-03)
4. Si un estudiante cambia su disponibilidad después de que le asignaron una tarea, ¿la tarea se le queda o se le quita? (R6)
5. Cuando un estudiante está ejecutando una tarea, ¿los otros responsables la ven bloqueada, con el nombre de quien la está haciendo? (S-12)
6. Si una tarea completada quedó mal hecha, ¿se puede reabrir? (S-16)
7. Si un administrador borra a un usuario, ¿sus tareas anteriores se quedan guardadas o se borran con él? (S-06)
8. ¿Cuántos estudiantes van a usar la herramienta al mismo tiempo durante el evento?
9. ¿Cada tarea lleva un título? ¿Qué otros datos necesita, además de fecha, hora y lugar? (S-13)
10. Si un estudiante empieza una tarea y la deja a medias, ¿cómo se libera antes de que venza? (S-19)
