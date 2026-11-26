# Elección y crítica · Dirección B «Claro y directo»

Fecha: 23 de noviembre de 2026 · Equipo: Justin Peñafiel

// Por qué la B
Justin eligió la B entre las tres direcciones (`direcciones.html`). Razones que se propusieron y que el equipo aceptó:

- El brief pide «sencillo de usar» y toma como referentes Uber, Airbnb y Spotify. La B es la más cercana a Uber y Airbnb: tarjetas claras con una acción obvia.
- El staff usa el celular de pie, con prisa y a veces al aire libre. Un fondo claro se lee mejor con luz fuerte.
- Es la que mejor contraste calculado tiene en los estados (texto y fondo de 6,5:1 a 13,3:1).
- Conserva la identidad del Interact2Hack con el morado como acción, el lima para lo que está en curso y una franja negra con el logo.

Costo que se acepta: pierde parte del ambiente nocturno del evento.

**Razón de Justin:** elegí este estilo porque quería un poco más de diseño en la app, o sea, un dinamismo entre blanco y negro y arriesgar a ver cómo se ve un tono claro con los mismos colores del Interact2Hack. Solo negro es muy básico. Por eso también va el modo oscuro, para gusto de cada usuario, porque con la luz o con una pantalla de celular no tan buena las notificaciones pueden no verse bien. Como se va a usar sobre todo en el celular, tiene que funcionar así.

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
| C-10 | Volver a fondo negro para conservar el ambiente. | Rechazado el 23 de noviembre; retomado de otra forma el 25 (ver abajo) | Como fondo único contradice la razón de elegir la B (legibilidad al sol). Como tema opcional y con bloques negros en el claro, sí. |

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

// Cambio del 25 de noviembre: B reforzada y modo oscuro

Justin vio el brand board y sintió que la B, tal cual, no se parecía lo suficiente al Interact2Hack: era como cambiarle el negro por blanco a una identidad que es negra. Pidió algo en medio: un claro que predomine, pero con los colores fuertes del evento bien presentes, y un modo oscuro para quien lo prefiera. Se aceptó, y es la dirección que sigue el DESIGN.md versión 1.1.

| Id | Hallazgo | Decisión | Razón |
| --- | --- | --- | --- |
| C-11 | El tema claro pierde la identidad del evento. | Aceptado | Se agregan bloques negros con lima y blanco: franja con el logo (ya estaba), barra inferior del celular, panel de indicadores del tablero y menú lateral. |
| C-12 | El staff también trabaja de noche. | Aceptado | Tema oscuro con los mismos tokens. Sigue la preferencia del sistema y se puede cambiar en Perfil. |
| C-13 | Dos temas duplican el trabajo de contraste. | Aceptado | Se calculó cada par en los dos temas (tablas de §8 del DESIGN.md) y todos pasan. |
| C-14 | Las tareas vencidas sin responsables no se distinguían. | Aceptado | Marca «Sin responsables» sobre la insignia Vencida; no es un sexto estado (PRD S-15). |
| C-15 | El administrador no sabe si cruza dos tareas del mismo estudiante. | Aceptado | Aviso de atención al asignar, que no bloquea (PRD R29). |
| C-16 | Usar el morado neón del brandboard en el tema oscuro. | Rechazado | Da 3,4:1 con blanco como fondo de botón. Se usa un morado claro `#B794FF` con texto negro (8,29:1). |
| C-17 | Usar el rojo `#B3261E` y el verde `#1E6B3A` también en oscuro. | Rechazado | Sobre fondo oscuro casi no se separan del fondo. En oscuro van coral `#FF6B61` y verde claro `#52D982` con texto negro. |
| A-10 | Sobre los bloques negros del tema claro el anillo de foco morado se ve poco. | Aceptado | Ahí el anillo va en lima (`--color-acento-franja`). |
| A-11 | El texto de los avisos ámbar cambiaba de color con el tema. | Aceptado | Token propio `--color-sobre-aviso` (`#0B0612` en los dos temas). |
| A-12 | El borde de campos en oscuro. | Aceptado | `#8F86A0`: 5,67:1 sobre el fondo, 5,36:1 sobre la superficie y 4,82:1 sobre la superficie alta. |
| C-18 | Los iconos eran emojis y símbolos de texto (⏳, ⚡, 🔒, ▲). | Aceptado (Justin) | Se cambian por círculos en SVG, todos de la misma familia: vacío, medio lleno, con punto que parpadea, con visto, con equis, con raya, relleno, punteado, con manecillas y con exclamación. Nada de emojis en ninguna parte. |
| C-19 | Todos los iconos parpadeando o ninguno. | Rechazado | Si todo parpadea no se nota nada. Solo parpadea el punto de «En ejecución» y, con movimiento reducido, se queda fijo. |
