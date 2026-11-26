# DESIGN.md · Staff Interact2Hack

Sistema de diseño **«Claro y directo»**, versión 1.1 (25 de noviembre de 2026). Es el de la herramienta de organización del staff del Interact2Hack, con la identidad visual del evento (morado, lima y negro). Viene en dos temas: **claro** (el de siempre, con bloques negros y lima para que se sienta del evento) y **oscuro** (negro de fondo, morado y lima neón).

Este archivo es la fuente de verdad de cómo se **ve** y se **siente** la herramienta. No define funcionalidad (eso lo dice el PRD, `docs/prd/PRD.md`). Cuando una tarea toque la interfaz, el agente lee este archivo antes de escribir código.

## 1. Cómo se usa este archivo

| Pregunta | Respuesta |
| --- | --- |
| ¿Quién lo lee? | El equipo y el agente. |
| ¿Qué decide? | Tokens (color, tipografía, espaciado), componentes, layout, accesibilidad y reglas de estilo. |
| ¿Qué no decide? | Reglas de negocio, textos ni comportamiento. Viven en el PRD y en las specs. |
| ¿Cómo se relaciona con una spec? | La spec cita tokens y componentes **por su nombre** (`--color-vencida`, «Tarjeta de tarea»). No copia valores. |
| ¿Cómo se cambia? | Se edita este archivo y se vuelve a generar `docs/diseno/brand-board.html`. Si algo no coincide, manda este archivo. |
| ¿Qué pasa si choca con una spec? | Gana la spec en lo que hace la herramienta; gana este archivo en cómo se ve. Si la duda sigue, se pregunta antes de implementar. |

## 2. Brief

- **Personalidad:** sencilla de usar, confiable, interactiva.
- **Referente:** Uber, Airbnb y Spotify.
- **Quién la usa:** staff del Interact2Hack y sus administradores, en la USFQ, donde será el evento. El staff la usa sobre todo en el celular; los administradores, en computadora (PRD §1 y R24).
- **Restricción del cliente:** respetar la identidad visual del Interact2Hack. Con los colores basta; lo demás es libre (`docs/cliente/preguntas.md`, P-27).

El proceso que llevó a estas decisiones está en `docs/diseno/brief.md` y `docs/diseno/criticas/`.

## 3. Principios

1. **Qué hacer y hasta cuándo, primero.** En cada tarea lo primero que se lee es su estado, su título, su lugar y su hora límite.
2. **Nunca solo color.** Todo estado lleva icono y texto. El color refuerza; no informa por sí solo.
3. **Una acción por pantalla.** Un solo botón primario visible. En el celular, la acción principal queda al alcance del pulgar.
4. **El morado es la acción; el lima es lo que está en curso.** El lima marca el estado «En ejecución» y, sobre negro, sirve de acento (cifras, opción activa). Nunca es texto ni borde sobre fondo claro.
5. **Plano y claro.** Sin sombras ni degradados decorativos. La jerarquía sale del tamaño, el peso, el borde y el espacio.
6. **El celular manda.** Se diseña primero para 390 px; el escritorio reutiliza los mismos componentes con más densidad.
7. **Dos temas, los mismos componentes.** Cada token tiene un valor claro y uno oscuro. Los componentes solo usan tokens, así que cambian de tema sin tocarlos.

## 4. Decisiones de diseño

| Decisión | Por qué |
| --- | --- |
| Tema claro por defecto, con fondo lila muy suave | El staff usa el celular de pie y a veces al aire libre, y el claro se lee mejor con luz fuerte. Fue la razón para elegir la dirección B (`criticas/critica-direccion-b.md`). |
| Bloques negros dentro del tema claro | Un claro "a secas" no se sentía del Interact2Hack. La franja del logo, la barra inferior del celular y el panel de indicadores del tablero van en negro, con lima y blanco encima. |
| Modo oscuro que sigue al sistema, con interruptor | El staff también trabaja de noche en el evento. El tema se toma de la preferencia del celular o la computadora, y el usuario lo puede cambiar en su perfil. |
| Franja superior negra con el logo | El logo del Interact2Hack solo funciona sobre fondos oscuros (brandboard). Mantiene la identidad del evento en un tema claro. |
| Morado profundo como acción en claro, morado claro en oscuro | Blanco sobre morado profundo da 8,54:1 (el morado neón del brandboard da solo 3,4:1 con blanco). En oscuro, el morado claro `#B794FF` con texto negro da 8,29:1. |
| Sora para el texto y Big Shoulders Display solo para títulos de pantalla y cifras | Es el par del brandboard. Big Shoulders pierde legibilidad por debajo de 24 px, por eso solo de 28 px en adelante y en mayúsculas. |
| Cada estado con icono y texto | La crítica C-1 mostró que «Pendiente» y «En ejecución» se distinguían casi solo por el color. |
| «Sin responsables» como marca y no como sexto estado | El cliente definió cinco estados. Una tarea sin dueño que ya venció es «Vencida» (PRD R9) y lleva esta marca para que el administrador la vea. |
| Aviso al administrador si asigna dos tareas a la misma hora | PRD R29: avisa, no bloquea, porque la tarea solo tiene hora límite. |
| «Finalizar tarea» deshabilitado hasta marcar todo | Es la regla R14 hecha visible: el botón dice cuántos pasos faltan. |
| Confirmación con ventana, no con deslizador | El deslizador no se puede usar con teclado ni lector de pantalla (crítica C-9). |
| Tarjetas en el celular y en el tablero | La tarjeta es el componente central en ambos perfiles (PRD R22); cambia la cantidad por fila. |
| Esquinas redondeadas | Se aleja de las esquinas rectas del brandboard a propósito, para parecerse a Uber y Airbnb y dar sensación de «toque». Los círculos y píldoras del brandboard se mantienen. |
| Sin librería de estilos | El sistema es pequeño. Las variables CSS bastan. |

## 5. Tokens

Todos los tokens vivirán en `src/styles/tokens.css`, dentro de `:root`. Ningún otro archivo escribe un color, una fuente o un tamaño literal.

### 5.1 Color

Los valores de esta sección son del **tema claro**. Los del tema oscuro están en §5.2; los nombres de token son los mismos.

**Base**

| Token | Valor | Uso |
| --- | --- | --- |
| `--color-fondo` | `#F6F3FB` | Fondo de la página |
| `--color-superficie` | `#FFFFFF` | Tarjetas, paneles, campos |
| `--color-superficie-alta` | `#EDE8F7` | Fondo de insignias neutras, filas al pasar el cursor |
| `--color-borde` | `#DCD5E8` | Bordes decorativos de tarjetas y separadores |
| `--color-borde-control` | `#7A7285` | Borde de campos, casillas y controles |
| `--color-texto` | `#0B0612` | Texto principal |
| `--color-texto-suave` | `#5D5568` | Texto secundario y etiquetas de campo |
| `--color-acento` | `#5B2BB5` | Botón primario, enlaces, anillo de foco, barra de progreso |
| `--color-sobre-acento` | `#FFFFFF` | Texto sobre el acento |
| `--color-franja` | `#050307` | Franja superior con el logo, barra inferior del celular y panel de indicadores |
| `--color-sobre-franja` | `#FFFFFF` | Texto sobre la franja y los bloques negros |
| `--color-sobre-franja-suave` | `#B8AFC8` | Texto secundario sobre negro |
| `--color-acento-franja` | `#5CF000` | Lima de acento sobre negro (cifras, opción activa) |
| `--color-riel-franja` | `#2A2236` | Riel de barras de progreso sobre negro |

**Estados de una tarea (PRD R9)**

| Estado | Fondo | Texto e icono | Icono |
| --- | --- | --- | --- |
| No asignado | `--color-no-asignado-fondo` `#ECEAF0` | `--color-no-asignado` `#4A4358` | círculo vacío |
| Pendiente | `--color-pendiente` `#5B2BB5` | `--color-sobre-pendiente` `#FFFFFF` | reloj |
| En ejecución | `--color-en-ejecucion` `#5CF000` | `--color-sobre-en-ejecucion` `#0B0612` | círculo con punto |
| Completada | `--color-completada` `#1E6B3A` | `--color-sobre-completada` `#FFFFFF` | marca de verificación |
| Vencida | `--color-vencida` `#B3261E` | `--color-sobre-vencida` `#FFFFFF` | triángulo de alerta |

**Avisos y marcas**

| Token | Valor | Uso |
| --- | --- | --- |
| `--color-por-vencer` | `#FFC857` | Fondo del aviso «vence en menos de 1 hora» (PRD R19). Texto `--color-sobre-aviso` (`#0B0612` en los dos temas). Es un aviso, no un sexto estado. |
| `--color-en-edicion` | `#EDE8F7` | Insignia «En edición» (R13), con icono de candado y texto `--color-texto`. |
| `--color-urgente` | `#0B0612` | Fondo de la marca «Urgente» (R17), con texto `--color-sobre-urgente` (`#FFFFFF`) y icono de rayo. |
| `--color-sin-responsables` | `#EDE8F7` | Fondo de la marca «Sin responsables» (S-15), con texto `--color-texto`, borde `--color-borde-control` e icono de persona con signo de interrogación. |
| `--color-atencion` | `#FFC857` | Fondo del aviso al administrador cuando asigna dos tareas a la misma hora (R29). Texto `--color-sobre-aviso`. |

### 5.2 Tema oscuro

Se activa con el atributo `data-tema="oscuro"` en la raíz, o por la preferencia del sistema (`prefers-color-scheme: dark`) cuando el usuario no escogió un tema. El atributo `data-tema="claro"` fuerza el claro. Solo cambian los valores; ninguno de los demás tokens (tipografía, espaciado, radios, movimiento) cambia.

| Token | Valor oscuro |
| --- | --- |
| `--color-fondo` | `#0E0A16` |
| `--color-superficie` | `#17111F` |
| `--color-superficie-alta` | `#231A30` |
| `--color-borde` | `#3A2F4A` |
| `--color-borde-control` | `#8F86A0` |
| `--color-texto` | `#F5F2FA` |
| `--color-texto-suave` | `#B8AFC8` |
| `--color-acento` | `#B794FF` |
| `--color-sobre-acento` | `#0B0612` |
| `--color-franja` | `#050307` (igual; en oscuro lleva un borde inferior de 1 px `--color-borde`) |
| `--color-no-asignado-fondo` / `--color-no-asignado` | `#2A2236` / `#CFC6DD` |
| `--color-pendiente` / `--color-sobre-pendiente` | `#B794FF` / `#0B0612` |
| `--color-en-ejecucion` / `--color-sobre-en-ejecucion` | `#5CF000` / `#0B0612` |
| `--color-completada` / `--color-sobre-completada` | `#52D982` / `#0B0612` |
| `--color-vencida` / `--color-sobre-vencida` | `#FF6B61` / `#0B0612` |
| `--color-por-vencer` y `--color-atencion` | `#FFC857` (igual; el texto `--color-sobre-aviso` también es `#0B0612`) |
| `--color-en-edicion` | `#231A30` |
| `--color-urgente` / `--color-sobre-urgente` | `#F5F2FA` / `#0B0612` |
| `--color-sin-responsables` | `#231A30` |

El interruptor de tema vive en Perfil (celular) y en el menú lateral (escritorio): tres opciones, «Automático», «Claro» y «Oscuro». La elección se guarda en el dispositivo.

### 5.3 Tipografía

| Token | Valor |
| --- | --- |
| `--fuente-texto` | `"Sora", "Segoe UI", system-ui, sans-serif` |
| `--fuente-titulo` | `"Big Shoulders Display", "Arial Narrow", sans-serif` |

| Nivel | Tamaño / alto de línea | Peso | Uso |
| --- | --- | --- | --- |
| `--texto-titulo` | 32 / 32 px, mayúsculas, `--fuente-titulo` | 900 | Título de pantalla. Solo de 28 px en adelante. |
| `--texto-cifra` | 48 / 48 px, `--fuente-titulo` | 900 | Cifras del tablero |
| `--texto-seccion` | 18 / 24 px, `--fuente-texto` | 600 | Título de tarjeta y de sección |
| `--texto-base` | 16 / 24 px | 400 | Texto general (nunca menos de 16 px en campos, para evitar el zoom del celular) |
| `--texto-pequeno` | 14 / 20 px | 400 | Lugar, hora, ayudas. Es el mínimo para texto informativo |
| `--texto-etiqueta` | 14 / 16 px | 600 | Insignias, botones, etiquetas de campo |
| `--texto-navegacion` | 12 / 16 px | 600 | Barra inferior del celular |

### 5.4 Espaciado, radios y bordes

| Token | Valor |
| --- | --- |
| `--espacio-1` … `--espacio-8` | 4, 8, 12, 16, 24, 32, 48, 64 px |
| `--radio-control` | 14 px (botones, campos, tarjetas) |
| `--radio-ventana` | 20 px (ventana de confirmación) |
| `--radio-casilla` | 8 px |
| `--radio-pildora` | 999 px (insignias) |
| `--borde` | 1 px sólido |
| `--borde-estado` | 4 px (borde izquierdo de la tarjeta vencida) |
| `--alto-tactil` | 44 px |
| `--alto-boton` | 48 px |

### 5.5 Movimiento

| Token | Valor | Uso |
| --- | --- | --- |
| `--curva` | `cubic-bezier(0.16, 1, 0.3, 1)` | La del brandboard |
| `--duracion-rapida` | 120 ms | Cambios de color al tocar o enfocar |
| `--duracion-media` | 200 ms | Aparición de avisos y de la ventana de confirmación |

Con `prefers-reduced-motion: reduce`, todas las duraciones pasan a 0.

## 6. Layout

| Ancho | Comportamiento |
| --- | --- |
| Hasta 640 px (celular, staff) | Una columna. Franja negra con el logo arriba. Barra inferior negra (`--color-franja`) con tres destinos de 56 px de alto: Mis tareas, Historial, Perfil. El destino activo va en `--color-acento-franja`. El aviso de vencimiento y el de falta de conexión van entre la franja y el contenido. |
| 641 a 1023 px | Dos columnas de tarjetas. |
| 1024 px o más (administrador) | Contenedor de 1200 px máximo. Menú lateral negro. El tablero muestra tarjetas de 3 o 4 por fila, con el panel de Indicadores del tablero arriba. |

Márgenes laterales: `--espacio-4` en celular y `--espacio-6` en escritorio. Sin desplazamiento horizontal a 390 px.

**Tablero del administrador (PRD R22).** Grupos en este orden, cada uno con un encabezado que lleva su nombre y la cantidad: Vencidas, Próximas a vencer, En ejecución, Pendientes, Sin asignar y Completadas. Completadas va al final, plegado, y se abre al tocarlo. Una tarea sin asignar a la que le falta menos de 1 hora va en Próximas a vencer, y una vencida sin responsables va en Vencidas con su marca (PRD R22, S-11, S-15).

## 7. Componentes

### 7.1 Botón

| Variante | Fondo | Texto | Borde |
| --- | --- | --- | --- |
| Primario | `--color-acento` | `--color-sobre-acento` | — |
| Secundario | `--color-superficie` | `--color-acento` | `--color-borde-control` |
| Peligro | `--color-superficie` | `--color-vencida` | `--color-vencida` |

Alto `--alto-boton` en el celular y mínimo `--alto-tactil` en cualquier lugar. Estados: normal, presionado (fondo un tono más oscuro), foco (anillo de 3 px en `--color-acento` con 2 px de separación), deshabilitado (opacidad 0.5, `not-allowed`, y el motivo escrito junto al botón). Un solo botón primario por pantalla.

### 7.2 Formulario

Etiqueta arriba en `--texto-etiqueta` y `--color-texto-suave`. Campo con borde `--color-borde-control`, `--radio-control` y alto `--alto-tactil`. Incluye:

- **Campo de texto** (nombre, correo, teléfono, título, observaciones).
- **Selector de lugar:** lista, no texto libre (R8).
- **Selector de responsables:** muestra solo a los disponibles (R5); si no hay ninguno, dice «Nadie está disponible a esa hora». Si el estudiante elegido ya tiene otra tarea que vence a la misma hora, aparece debajo el Aviso de atención (§7.6) y el botón sigue activo (R29).
- **Disponibilidad:** días y un solo rango de horas por día (S-25).
- **Entrega de credenciales:** al crear un usuario, el administrador elige «Enviar por correo» o «Se las doy yo» (R4).
- **Casilla «Urgente».**

Estados: normal, foco (anillo), con error (borde y mensaje en `--color-vencida`, con el mensaje debajo y enlazado con `aria-describedby`), deshabilitado, bloqueado (cuando la tarea está en ejecución o en edición: campos de solo lectura con el motivo).

### 7.3 Insignia de estado

Píldora (`--radio-pildora`) con icono y texto, en los colores de §5.1. Una por tarea. Estados: No asignado, Pendiente, En ejecución, Completada, Vencida. Marcas adicionales: «En edición» (candado), «Urgente» (rayo) y «Sin responsables» (persona con interrogación, con borde `--color-borde-control`). El texto siempre está visible; el icono es decorativo (`aria-hidden`).

### 7.4 Tarjeta de tarea

Superficie blanca, borde `--color-borde`, `--radio-control`.

- **Staff (celular):** arriba la Insignia de estado. Después el título en `--texto-seccion`, el lugar y la hora límite en `--texto-pequeno`, el contador de tiempo restante (R21) y, al abrirla, los compañeros con su enlace para llamar. Toda la tarjeta es tocable.
- **Administrador (tablero):** igual, más la línea «Responsables» con sus nombres, o «Sin responsables». Si la ejecuta alguien, dice «Ejecuta: [nombre]».

Estados: pendiente, en ejecución, completada, vencida (borde izquierdo `--borde-estado` en `--color-vencida`; si no tiene responsables, además la marca «Sin responsables»), por vencer (el aviso ámbar aparece arriba de la lista del staff y la hora límite va en negrita), bloqueada (en ejecución o en edición: candado y sin acciones de edición).

### 7.5 Ítem de checklist

Fila de al menos 48 px de alto; toda la fila es el área táctil. Casilla de 24 px con `--radio-casilla` y borde `--color-borde-control`; marcada, se rellena con `--color-acento` y una marca blanca. Estados: sin marcar, marcado, foco (anillo), deshabilitado (otro responsable la ejecuta o la tarea está vencida: texto en `--color-texto-suave` y el motivo escrito arriba de la lista).

Debajo de la lista: texto «2 de 5 pasos» y barra de progreso en `--color-acento` sobre `--color-borde`.

### 7.6 Aviso

Bloque con icono y texto, en la parte superior de la pantalla y con `role="status"` (`role="alert"` para los de error).

| Tipo | Fondo | Texto | Icono |
| --- | --- | --- | --- |
| Por vencer (R19) | `--color-por-vencer` | `--color-sobre-aviso` | reloj de arena |
| Sin conexión (R27) | `--color-vencida` | `--color-sobre-vencida` | wifi tachado |
| Atención al asignar (R29) | `--color-atencion` | `--color-sobre-aviso` | signo de exclamación |
| Éxito | `--color-completada` | `--color-sobre-completada` | marca de verificación |
| Error | `--color-vencida` | `--color-sobre-vencida` | triángulo de alerta |

El aviso «Sin conexión a internet» se queda mientras no haya red y desaparece solo al volver. El aviso de atención dice, por ejemplo, «Ana Torres ya tiene otra tarea que vence a las 08:30». Es informativo: no impide asignar.

### 7.7 Ventana de confirmación

Aparece al presionar «Finalizar tarea» (R14). Fondo `--color-superficie`, `--radio-ventana`, título «¿Finalizar la tarea?» y dos botones: «Sí, finalizar» (primario) y «Cancelar» (secundario). Atrapa el foco, se cierra con Esc y el foco vuelve al botón que la abrió.

### 7.8 Indicador del tablero

Para el tablero del administrador (R22). Es un panel negro (`--color-franja`, con `--radio-control`) con una fila de indicadores, uno por estado: la cifra en `--texto-cifra` y `--color-sobre-franja`, y debajo el nombre del estado con su icono en `--color-sobre-franja-suave`. Ejemplo: «5» y «Completadas». Un indicador con 0 se muestra igual, con la cifra en `--color-sobre-franja-suave`. Si hay tareas vencidas, el indicador de Vencidas lleva el fondo `--color-vencida` con texto `--color-sobre-vencida`. Abajo va el resumen «5 de 10 completadas» con una barra en `--color-acento-franja` sobre `--color-riel-franja`.

### 7.9 Estados de pantalla

| Estado | Qué se muestra |
| --- | --- |
| Cargando | Esqueletos del tamaño de las tarjetas, sin animación si hay movimiento reducido. |
| Vacío | Texto que explica qué falta: «No tienes tareas asignadas por ahora.» |
| Error | Aviso de error con la acción «Reintentar». |
| Sin conexión | Aviso de §7.6; los botones de guardar y finalizar quedan deshabilitados con el motivo escrito. |

## 8. Accesibilidad

Todos los valores se calcularon con la fórmula de contraste de WCAG 2.1, para los dos temas.

**Tema claro**

| Par | Contraste | Mínimo |
| --- | --- | --- |
| `--color-texto` sobre `--color-fondo` | 18,24:1 | 4,5:1 |
| `--color-texto` sobre `--color-superficie` | 20,02:1 | 4,5:1 |
| `--color-texto` sobre `--color-superficie-alta` | 16,67:1 | 4,5:1 |
| `--color-texto-suave` sobre `--color-superficie` | 7,08:1 | 4,5:1 |
| `--color-texto-suave` sobre `--color-fondo` | 6,45:1 | 4,5:1 |
| `--color-texto-suave` sobre `--color-superficie-alta` | 5,90:1 | 4,5:1 |
| `--color-acento` sobre `--color-superficie` | 8,54:1 | 4,5:1 |
| `--color-acento` sobre `--color-fondo` | 7,78:1 | 4,5:1 |
| `--color-sobre-acento` sobre `--color-acento` | 8,54:1 | 4,5:1 |
| `--color-borde-control` sobre `--color-superficie` | 4,59:1 | 3:1 |
| `--color-borde-control` sobre `--color-fondo` | 4,18:1 | 3:1 |
| `--color-borde-control` sobre `--color-superficie-alta` | 3,82:1 | 3:1 |
| `--color-acento` sobre `--color-borde` (barra de progreso) | 5,99:1 | 3:1 |
| No asignado (texto sobre su fondo) | 7,87:1 | 4,5:1 |
| Pendiente (blanco sobre morado) | 8,54:1 | 4,5:1 |
| En ejecución (tinta sobre lima) | 13,27:1 | 4,5:1 |
| Completada (blanco sobre verde) | 6,52:1 | 4,5:1 |
| Vencida (blanco sobre rojo) | 6,54:1 | 4,5:1 |
| Por vencer (tinta sobre ámbar) | 13,01:1 | 4,5:1 |
| `--color-vencida` sobre `--color-superficie` (borde de tarjeta) | 6,54:1 | 3:1 |
| Blanco sobre `--color-franja` | 20,54:1 | 4,5:1 |
| `--color-sobre-franja-suave` sobre `--color-franja` | 9,78:1 | 4,5:1 |
| `--color-acento-franja` (lima) sobre `--color-franja` | 13,61:1 | 4,5:1 |
| `--color-acento-franja` sobre `--color-riel-franja` (barra de progreso) | 10,08:1 | 3:1 |

**Tema oscuro**

| Par | Contraste | Mínimo |
| --- | --- | --- |
| `--color-texto` sobre `--color-fondo` | 17,66:1 | 4,5:1 |
| `--color-texto` sobre `--color-superficie` | 16,69:1 | 4,5:1 |
| `--color-texto` sobre `--color-superficie-alta` | 15,03:1 | 4,5:1 |
| `--color-texto-suave` sobre `--color-fondo` | 9,32:1 | 4,5:1 |
| `--color-texto-suave` sobre `--color-superficie` | 8,80:1 | 4,5:1 |
| `--color-texto-suave` sobre `--color-superficie-alta` | 7,93:1 | 4,5:1 |
| `--color-acento` sobre `--color-fondo` | 8,10:1 | 4,5:1 |
| `--color-acento` sobre `--color-superficie` | 7,65:1 | 4,5:1 |
| `--color-sobre-acento` sobre `--color-acento` | 8,29:1 | 4,5:1 |
| `--color-borde-control` sobre `--color-fondo` | 5,67:1 | 3:1 |
| `--color-borde-control` sobre `--color-superficie` | 5,36:1 | 3:1 |
| `--color-borde-control` sobre `--color-superficie-alta` | 4,82:1 | 3:1 |
| `--color-acento` sobre `--color-borde` (barra de progreso) | 5,16:1 | 3:1 |
| No asignado (texto sobre su fondo) | 9,25:1 | 4,5:1 |
| Pendiente (tinta sobre morado claro) | 8,29:1 | 4,5:1 |
| En ejecución (tinta sobre lima) | 13,27:1 | 4,5:1 |
| Completada (tinta sobre verde claro) | 11,06:1 | 4,5:1 |
| Vencida (tinta sobre rojo claro) | 7,18:1 | 4,5:1 |
| Por vencer (tinta sobre ámbar) | 13,01:1 | 4,5:1 |
| `--color-vencida` sobre `--color-superficie` (borde de tarjeta) | 6,62:1 | 3:1 |

No se usan, porque no cumplen: el lima sobre blanco (1,51:1) y el ámbar sobre blanco (1,54:1) como texto o borde; el borde `--color-borde` (1,43:1) nunca se usa como borde de un control. El lima sí se usa sobre negro, donde da 13,61:1.

Además:

- **Foco visible** en todo elemento interactivo, en los dos temas: anillo de 3 px en `--color-acento` con 2 px de separación. Sobre los bloques negros del tema claro, el anillo va en `--color-acento-franja`.
- **Áreas táctiles** de al menos 44 × 44 px; botones principales y filas de checklist de 48 px.
- **Ningún estado depende solo del color:** todos llevan icono y texto.
- **Formularios:** todo campo tiene etiqueta visible; los errores se asocian con `aria-describedby`.
- **Avisos** con `role="status"` o `role="alert"`.
- **Movimiento reducido:** con `prefers-reduced-motion`, sin transiciones.
- **Texto mínimo:** 14 px para texto informativo, 12 px solo en la barra inferior.

## 9. Identidad del Interact2Hack

- El logo va solo sobre la franja negra `--color-franja`, nunca sobre un fondo claro, a un ancho mínimo de 96 px y con un margen de protección igual a la altura del «2».
- No se deforma, no se rota ni se le cambian los colores.
- Los colores de marca se usan con los roles de §5.1: morado profundo para la acción, lima para «En ejecución» y, sobre negro, como acento.
- El logo va en blanco sobre la franja negra en los dos temas.

## 10. Reglas para el agente

**DEBE:**

- Leer este archivo antes de cualquier tarea que toque la interfaz.
- Usar solo los tokens de §5, por su nombre, y probar cada pantalla en los dos temas.
- Mostrar cada estado de una tarea con la Insignia de estado (icono y texto).
- Deshabilitar «Finalizar tarea» hasta que todos los pasos estén marcados, y escribir cuántos faltan.
- Pedir confirmación con la Ventana de §7.7 antes de completar una tarea.
- Mostrar el aviso de §7.6 cuando falte menos de 1 hora, cuando no haya conexión y cuando el administrador asigne dos tareas a la misma hora.
- Deshabilitar el marcado de pasos, guardar y finalizar cuando no haya conexión, con el motivo escrito (R27).
- Diseñar y probar primero a 390 px.
- Mantener el orden y los grupos del tablero de §6.

**NO DEBE:**

- Escribir colores, fuentes o tamaños literales fuera del archivo de tokens.
- Usar lima o ámbar como color de texto o de borde sobre fondo claro (sobre negro, el lima sí).
- Bloquear la asignación cuando hay dos tareas a la misma hora: solo se avisa (R29).
- Crear un sexto estado para «Sin responsables»: es una marca.
- Usar Big Shoulders Display por debajo de 28 px.
- Añadir sombras, degradados o animaciones que no estén en §5.5.
- Usar un deslizador para confirmar.
- Instalar librerías de estilos o de componentes.
- Cambiar textos de la herramienta: vienen del PRD y de las specs.

## 11. Criterios verificables de diseño

| Id | Criterio | Cómo se verifica |
| --- | --- | --- |
| D-01 | No hay colores hexadecimales fuera del archivo de tokens. | `grep -rnE "#[0-9a-fA-F]{3,8}\b" src --include=*.css --include=*.tsx \| grep -v tokens.css` no devuelve nada. |
| D-02 | No hay `font-family` fuera del archivo de tokens. | `grep -rn "font-family" src \| grep -v tokens.css` no devuelve nada. |
| D-03 | Toda tarea muestra su estado con icono y texto. | En el navegador, cada Tarjeta de tarea tiene una Insignia con texto visible. |
| D-04 | Los cinco estados usan los colores de §5.1. | Con una tarea de cada estado, el color de fondo calculado de su Insignia coincide con el token. |
| D-05 | «Finalizar tarea» está deshabilitado con pasos sin marcar y dice cuántos faltan. | Con 2 de 5 pasos marcados, el botón está deshabilitado y muestra «Faltan 3 pasos». |
| D-06 | Finalizar abre la Ventana de confirmación. | Al presionar «Finalizar tarea» con todo marcado aparece la ventana; Esc la cierra y el foco vuelve al botón. |
| D-07 | Todo elemento interactivo tiene foco visible. | Recorrer la pantalla con Tab: cada elemento muestra el anillo de foco. |
| D-08 | Las áreas táctiles miden al menos 44 px; los botones principales y las filas de checklist, 48 px. | En las herramientas del navegador, esos elementos miden lo indicado de alto. |
| D-09 | No hay desplazamiento horizontal a 390 px. | `document.documentElement.scrollWidth` es 390 en una ventana de 390 px. |
| D-10 | El tablero muestra los grupos en el orden de §6, con las completadas plegadas. | Con tareas de todos los estados, el orden en pantalla es el de §6 y Completadas aparece cerrado. Una sin asignar a 30 minutos de vencer sale en Próximas a vencer. |
| D-11 | A una tarea con menos de 1 hora se le muestra el aviso arriba, con `role="status"`. | Con una tarea que vence en 30 minutos, el aviso ámbar aparece en la parte superior y tiene ese atributo. |
| D-12 | Sin conexión: aviso arriba, y marcar pasos, guardar y finalizar deshabilitados con el motivo escrito. | En las herramientas del navegador, poner la red en «Sin conexión»: aparece el aviso y los controles se deshabilitan. |
| D-13 | Cada par de §8 cumple su contraste mínimo, en el tema claro y en el oscuro. | Con las herramientas de contraste del navegador, en cada tema, cada par tiene al menos el valor de la tabla. |
| D-14 | Big Shoulders Display solo se usa en 28 px o más y en mayúsculas. | En las herramientas del navegador, todo texto con esa fuente calculada mide 28 px o más. |
| D-15 | Con movimiento reducido no hay transiciones. | Activar «reducir movimiento» en el sistema: las duraciones calculadas son 0. |
| D-16 | El logo está sobre la franja negra y mide al menos 96 px de ancho. | En el navegador, el logo está dentro de un contenedor con `--color-franja` y su ancho es 96 px o más. |
| D-17 | No hay sombras ni degradados decorativos. | `grep -rnE "box-shadow\|gradient" src \| grep -v tokens.css` no devuelve nada (el anillo de foco no usa sombra). |
| D-18 | El teléfono de un compañero es un enlace `tel:` de al menos 44 × 44 px. | En el navegador, el enlace tiene `href` que empieza con `tel:` y esa área táctil. |
| D-19 | La tarea muestra el tiempo restante hasta su hora límite al abrirla. | Al abrir una tarea que vence en 30 minutos, se ve el contador. |
| D-20 | Existen los dos temas, y todos los tokens de color tienen valor en ambos. | `tokens.css` tiene un bloque `:root` y un bloque `[data-tema="oscuro"]` con los mismos nombres de token. |
| D-21 | El tema sigue la preferencia del sistema y el usuario lo puede cambiar. | Con el sistema en oscuro, la herramienta abre en oscuro; en Perfil, elegir «Claro» la cambia y la elección sigue al recargar. |
| D-22 | Una tarea vencida sin responsables muestra la marca «Sin responsables» y está en el grupo Vencidas. | Con una tarea sin asignar cuya hora ya pasó, aparece en Vencidas con insignia «Vencida» y la marca. |
| D-23 | Al asignar a un estudiante que ya tiene una tarea a la misma hora, aparece el aviso de atención y el botón de guardar sigue activo. | Asignar dos tareas que vencen a la misma hora al mismo estudiante. |
| D-24 | En el tema claro, la barra inferior del celular y el panel de indicadores son negros. | En el navegador, su fondo calculado es el de `--color-franja`. |
| D-25 | Al crear un usuario, el administrador puede elegir cómo se entregan las credenciales. | En el formulario aparecen las opciones «Enviar por correo» y «Se las doy yo». |
