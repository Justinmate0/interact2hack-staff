# Elección y crítica · Dirección B «Claro y directo»

Fecha: 23 de noviembre de 2026 · Equipo: Justin Peñafiel

// Por qué la B
Justin eligió la B entre las tres direcciones (`direcciones.html`). Razones que se propusieron y que el equipo aceptó:

- El brief pide «sencillo de usar» y toma como referentes Uber, Airbnb y Spotify. La B es la más cercana a Uber y Airbnb: tarjetas claras con una acción obvia.
- El staff usa el celular de pie, con prisa y a veces al aire libre. Un fondo claro se lee mejor con luz fuerte.
- Es la que mejor contraste calculado tiene en los estados (texto y fondo de 6,5:1 a 13,3:1).
- Conserva la identidad del Interact2Hack con el morado como acción, el lima para lo que está en curso y una franja negra con el logo.

Costo que se acepta: pierde parte del ambiente nocturno del evento.

Nota para Justin: agrega aquí, con tus palabras, la razón que a ti te convenció.

// Cómo se hizo la crítica
No se pudo correr `/impeccable` en este entorno. La crítica (usabilidad) y la auditoría (accesibilidad) se hicieron a mano sobre la tarjeta de la B: se midió cada par de colores con la fórmula de contraste de WCAG 2.1 y se revisaron el tamaño de los controles, el foco y los estados. Cada hallazgo se clasificó como aceptado o rechazado, con su razón.

## Crítica (usabilidad)

| Id | Hallazgo | Decisión | Razón |
| --- | --- | --- | --- |
| C-1 | «En ejecución» (lima) y «Pendiente» (morado) se distinguen casi solo por el color. | Aceptado | Cada estado lleva icono y texto (PRD R9). El color no informa solo. |
| C-2 | El aviso de «vence en 42 min» es igual a cualquier otro aviso. | Aceptado | Ámbar con icono de reloj de arena, arriba de todo y con `role="status"` (R19). |
| C-3 | Las tareas vencidas no destacan en el tablero del administrador. | Aceptado | Borde izquierdo rojo de 4 px, encabezado de grupo propio y orden fijo (R22). |
| C-4 | La tarjeta del administrador no dice quién tiene la tarea. | Aceptado | Se agrega la línea «Responsables» y, si ya la ejecuta alguien, su nombre (R16). |
| C-5 | «Finalizar tarea» está activo con pasos sin marcar. | Aceptado | Deshabilitado hasta marcar todos, con el texto «Faltan N pasos» (R14). |
| C-6 | La barra de progreso en lima casi no se ve sobre el riel claro (1,06:1). | Aceptado | La barra va en morado (5,99:1) y se acompaña del texto «2 de 5 pasos». |
| C-7 | La B no tiene el logo ni se siente del evento. | Aceptado | Franja superior negra con el logo, como pide el brandboard para fondos claros. |
| C-8 | Agregar sombras suaves y degradados para dar profundidad, como Airbnb. | Rechazado | El brandboard dice «sin sombras». La jerarquía sale de bordes, tamaño y espacio. |
| C-9 | Confirmar al finalizar con un deslizador, como en los bancos. | Rechazado | Un gesto de deslizar no se puede hacer con teclado ni lector de pantalla. Se usa una ventana de confirmación (R14). |
| C-10 | Volver a fondo negro para conservar el ambiente. | Rechazado | Contradice la razón de elegir la B: legibilidad al sol. |

## Auditoría (accesibilidad)

| Id | Hallazgo | Decisión | Razón |
| --- | --- | --- | --- |
| A-1 | El lima sobre blanco da 1,51:1. | Aceptado | El lima nunca es texto ni borde sobre claro: solo fondo con texto tinta (13,27:1). |
| A-2 | El borde de los campos (`#DCD5E8`) da 1,43:1 sobre blanco, y se pide 3:1. | Aceptado | Borde de control `#7A7285`: 4,59:1 sobre blanco y 4,18:1 sobre el fondo. |
| A-3 | La B no tiene foco visible. | Aceptado | Anillo de 3 px en el color de acento, separado 2 px. |
| A-4 | La barra de navegación del celular tiene textos de 11 px y sin altura mínima. | Aceptado | Destinos de 56 px de alto con texto de 12 px. |
| A-5 | Los textos de apoyo de la tarjeta son de 12 y 13 px. | Aceptado | Mínimo 14 px para todo texto informativo. |
| A-6 | El brandboard permite 10 px en la barra de pestañas. | Rechazado | En el celular de un staff con prisa, 10 px no se lee. Se usa 12 px. |
| A-7 | Big Shoulders Display bajo 24 px pierde legibilidad. | Aceptado | Solo se usa de 28 px en adelante y en mayúsculas: títulos de pantalla y cifras del tablero. |
| A-8 | No hay regla de movimiento reducido. | Aceptado | Con `prefers-reduced-motion`, todas las duraciones pasan a 0. |
| A-9 | El enlace para llamar a un compañero puede quedar chico. | Aceptado | Área táctil de 44 × 44 px como mínimo (R26). |
