# Revisión del PRD

**Equipo:** Justin Peñafiel · **Fecha:** 23 de noviembre de 2026
**Fuentes:** `docs/fuentes/descripcion-proyecto.md` y `docs/cliente/preguntas.md`
**Cómo se hizo:** con IA, como autorizó el profe. La IA (Claude) recorrió el PRD con la lista de 8 tipos de hueco y después lo atacó como socio escéptico. Justin revisa cada fila y decide si se acepta; lo que rechaza se tacha y se explica.

Tipos de hueco: 1 supuesto escrito como hecho · 2 regla vaga o sin cifra · 3 alcance inflado · 4 contradicción resuelta en silencio · 5 pregunta abierta desaparecida · 6 perfil o permiso incompleto · 7 detalle técnico · 8 regla sin trazabilidad.

## Huecos

| # | Sección | Frase exacta del PRD | Tipo | Gravedad | Origen | Qué dicen las fuentes | Corrección |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 6 · R22 | «Se ordena así: vencidas, próximas a vencer (la que vence antes, primero), en ejecución, sin asignar y completadas.» | 2 | alta | IA | El cliente dio el orden vencidas, por vencer, sin asignar, terminadas y añadió «en ejecución» al final. Nunca dijo dónde van las pendientes que aún no están por vencer. | Aceptado. Las pendientes van después de en ejecución, por hora límite, y una tarea con menos de 1 hora (pendiente o en ejecución) va en «próximas a vencer». Nuevo S-11. |
| 2 | 6 · R12 | «Una tarea en ejecución queda bloqueada: ningún administrador puede editarla ni borrarla.» | 4 | alta | IA | El cliente pidió el bloqueo, pero también dijo que si una tarea tenía más gente de la necesaria, «hay que comunicarse con un administrador para que edite la tarea». Se contradicen. | Aceptado. El bloqueo se mantiene y la contradicción pasa a puntos abiertos como pregunta al cliente. |
| 3 | 6 · R16 | «queda completada para todos y desaparece de las pendientes de los demás.» | 2 | alta | IA | El cliente dijo que uno la abre y la completa, y que no hace falta sincronizar. No dijo qué ve un segundo responsable mientras el primero la está ejecutando. | Aceptado. Mientras uno la ejecuta, los demás la ven «en ejecución por [nombre]» y no pueden marcar pasos. Igual para urgentes. Nuevo S-12. |
| 4 | 6 · R5 | «solo aparecen los estudiantes disponibles en esa fecha y hora.» | 2 | alta | IA | La tarea solo tiene hora límite (descripción del proyecto). La disponibilidad es por día y hora, pero no se dijo con qué hora se compara. | Aceptado. Se compara con la hora de vencimiento. Nuevo S-14. |
| 5 | 6 · R7 | «Una tarea tiene título, lugar, fecha y hora de vencimiento, checklist (pasos) y responsables.» | 1 | media | IA | La descripción no menciona un título. En la sesión el cliente solo habló de «título» de pasada, sin confirmarlo. | Aceptado. El título queda como supuesto. Nuevo S-13. |
| 6 | 6 · R9 | «**no asignado** (sin responsables)» | 5 | media | IA | No se habló de una tarea sin responsables que llega a su hora límite. | Aceptado. También pasa a vencida. Nuevo S-15. |
| 7 | 6 · R18 | «El estudiante puede hacer sus tareas asignadas en el orden que quiera.» | 5 | media | IA | La pregunta P-09 (orden de los pasos dentro de una tarea) no tiene respuesta y desapareció del PRD. | Aceptado. Los pasos se pueden marcar en cualquier orden. Nuevo S-16. |
| 8 | 6 · R14 | «Una tarea se completa cuando todos los pasos están marcados y el estudiante presiona finalizar.» | 5 | media | IA | P-08 (desmarcar o reabrir una tarea completada) quedó sin respuesta y sin mención. El cliente solo dijo que las completadas no se borran. | Aceptado. Una tarea completada no se reabre ni se desmarca. Mismo S-16, con pregunta para el cliente. |
| 9 | 6 · R3 | «Existe un administrador master inicial, entregado al cliente.» | 6 | media | IA | El cliente quiere un usuario por encima de los demás por si alguien pierde la clave. No dijo si se puede eliminar. | Aceptado. Nadie puede eliminar al master y un administrador no se elimina a sí mismo. Nuevo S-17. |
| 10 | 2 · Estudiante | «Cambiar su contraseña.» | 6 | baja | IA | El cliente dijo que el staff ve tareas, historial y cambia su contraseña. No dijo si puede editar su teléfono o correo. | Aceptado. Solo un administrador cambia nombre, correo y teléfono. Nuevo S-18. |
| 11 | 4 · Must | «Disponibilidad del staff por día y hora.» | 3 | media | IA | El cliente dijo «eso sí es importante». El avance funcional del 2 de diciembre es pequeño y ya hay recuperación de contraseña por correo en Must. | Rechazado: se queda en Must por lo que dijo el cliente. El recorte se decide al armar las specs del Avance 3, no en el PRD. |
| 12 | 3 · Objetivos | «Al cerrar el evento no quedan tareas pendientes ni vencidas sin atender.» | 2 | baja | IA | El cliente no dio cifras. | Rechazado: ya está declarado como supuesto S-10. |
| 13 | 6 · R14 | «Antes de completar pide una confirmación.» | 2 | baja | IA | El cliente propuso una ventana de confirmación o un deslizador. | Rechazado: cómo se confirma es decisión de diseño y va en el DESIGN.md, no en el PRD. |

## Para presentar

**1. El bloqueo contra la edición contradecía lo que pidió el cliente (fila 2).**
Qué decía el PRD: una tarea en ejecución no se puede editar. Por qué era un problema: el cliente también dijo que, si sobra gente, un administrador edita la tarea. Cómo quedó: el bloqueo sigue y la contradicción es la segunda pregunta para el cliente. Lo encontró la IA.

**2. El orden del tablero dejaba afuera a las pendientes (fila 1).**
Qué decía el PRD: vencidas, por vencer, en ejecución, sin asignar y completadas. Por qué era un problema: una tarea pendiente a más de una hora de vencer no tenía lugar en el tablero. Cómo quedó: va después de en ejecución, por hora límite (S-11). Lo encontró la IA.

**3. La disponibilidad se comparaba con una hora que la tarea no tiene (fila 4).**
Qué decía el PRD: al asignar, salen los disponibles «en esa fecha y hora». Por qué era un problema: la tarea solo tiene hora de vencimiento. Cómo quedó: se compara con la hora de vencimiento (S-14). Lo encontró la IA.

## Preguntas para el cliente

Ordenadas por prioridad, para el 2 de diciembre:

1. Una tarea vencida, ¿se puede completar tarde o solo después de que un administrador cambie la fecha? (S-02)
2. Si una tarea en ejecución tiene más gente de la necesaria, ¿cómo se reduce si está bloqueada? (fila 2)
3. Si una tarea vence mientras alguien la ejecuta, ¿conserva lo marcado y quién puede terminarla? (S-03)
4. Si cambia la disponibilidad de un estudiante, ¿qué pasa con las tareas que ya tenía asignadas? (R6)
5. Mientras un responsable ejecuta una tarea, ¿los demás la ven bloqueada con su nombre? (S-12)
6. ¿Una tarea completada se puede reabrir si se hizo mal? (S-16)
7. Si se elimina a un usuario, ¿su historial de tareas se conserva? (S-06)
8. ¿Cuántos estudiantes usarán la herramienta a la vez?
9. ¿Cada tarea lleva un título? ¿Qué otros datos debe tener? (S-13)
