Petición del documento
- Url completa: http://127.0.0.1:5500/index.html
- Protocolo: http
- Host: 127.0.0.1:5500
- Puerto: 5500
- Ruta: 127.0.0.1:5500/index.html
- Método de la petición: GET
- Código de estado: 304 

El código que me aparece al buscar una página que no aparece es el código 404, que significa que la página no exite

Roles:
- HTML: La estructura de todas las páginas, Por ejemplos el titulo, la bienvenida y todo lo que lleva la página de inicio
- CSS: EL estilo de todas las páginas, por ejemplo los colores, el fondo y tamaños de la página de inicio
- JS: Es el que le va a dar funcionalidad a todas las páginas, alertas, verificación de las páginas

### Tabla de rutas relativas
| Archivo de origen | Destino | Ruta escrita |
| ---| --- | --- |
| index.html | Inicio | index.html |
| index.html | Tarifas y rutas | paginas/tarifas.html |
| index.html | Reservas | paginas/reservas.html |
| paginas/tarifas.html | Inicio | ../index.html |
| paginas/tarifas.html | Tarifas y rutas | tarifas.html |
| paginas/tarifas.html | Reservas | reservas.html |
| paginas/reservas.html | Inicio | ../index.html |
| paginas/reservas.html | Tarifas y rutas | tarifas.html |
| paginas/reservas.html | Reservas | reservas.html |

### Formulario de reservas
- `email` para el correo electrónico: el navegador puede validar el formato antes del envío.
- `radio` para el tipo de bicicleta: las opciones comparten `name="tipo_bicicleta"` y permiten seleccionar solo una.
- `date` para la fecha de recogida: ofrece un selector de fecha y evita entradas con formato arbitrario.

### Validación del formulario de reserva
| Campo | Dato de prueba | Resultado esperado | Resultado obtenido |
| --- | --- | --- | --- |
| Nombre completo | `Al` | Bloquear por menos de 3 caracteres | Bloqueado por `minlength` |
| Nombre completo | Vacío | Bloquear por ser obligatorio | `invalid` en `nombre`; no se disparó `submit` |
| Documento | `12ab5678` | Bloquear letras | Bloqueado por el patrón `[0-9]{6,10}` |
| Documento | Vacío | Bloquear por ser obligatorio | `invalid` en `documento`; no se disparó `submit` |
| Correo | `correo-invalido` | Bloquear formato no válido | Bloqueado por `type="email"` |
| Correo | Vacío | Bloquear por ser obligatorio | `invalid` en `correo`; no se disparó `submit` |
| Celular | `1234567890` | Rechazar porque no empieza por 3 | Bloqueado por el patrón `3[0-9]{9}` |
| Celular | `300123` | Rechazar por tener menos de 10 dígitos | Bloqueado por el patrón `3[0-9]{9}` |
| Celular | `3001234567` | Aceptar 10 dígitos que empiezan por 3 | Aceptado; no produjo error de patrón |
| Fecha del alquiler | `2026-10-31` | Bloquear antes del 1 de noviembre | Bloqueado por `min="2026-11-01"` |
| Fecha del alquiler | `2027-01-01` | Bloquear después del 31 de diciembre | Bloqueado por `max="2026-12-31"` |
| Tipo de bicicleta | Ninguna opción | Bloquear por ser obligatorio | `invalid` en el grupo de radios; no se disparó `submit` |
| Plan | Opción vacía | Bloquear por ser obligatorio | `invalid` en `plan`; no se disparó `submit` |
| Cantidad de bicicletas | `0` y `7` | Bloquear fuera del rango 1–6 | Ambos valores bloqueados por `min`/`max` |
| Cantidad de bicicletas | Vacía | Bloquear por ser obligatorio | `invalid` en `cantidad`; no se disparó `submit` |
| Comentarios | 301 caracteres | No permitir más de 300 caracteres | El navegador conservó solo 300 caracteres |
| Políticas de alquiler | Casilla desmarcada | Bloquear por ser obligatorio | `invalid` en `politicas`; no se disparó `submit` |

### Prueba de teclado
- `Tab` recorrió los controles en orden visual desde los datos personales hasta el botón de envío.
- Las flechas cambiaron la opción de bicicleta a “Montaña”; `Shift+Tab` regresó del botón a políticas y comentarios.
- La barra espaciadora desmarcó y volvió a marcar la aceptación de políticas.
- `Enter` en “Enviar reserva” disparó el evento `submit` con todos los datos válidos. La prueba interceptó el envío para evitar un POST sin un servidor de reservas configurado.

### Auditoría de accesibilidad
| Página | Criterio | Hallazgo y corrección | Resultado |
| --- | --- | --- | --- |
| Inicio | Texto alternativo | Las tres imágenes informativas tienen descripciones del contenido; se precisaron para describir la portada, el anuncio de bicicleta y la escena de ruta. | Cumple |
| Tarifas | Texto alternativo | El logotipo tiene `alt="Logo de Rueda Libre"`; no hay imágenes decorativas sin marcar. | Cumple |
| Reservas | Texto alternativo | No hay imágenes que requieran texto alternativo. | Cumple |
| Inicio | Encabezados | `h1` seguido por secciones `h2` y subsecciones `h3`, sin saltos. | Cumple |
| Tarifas | Encabezados | `h1`, encabezados `h2` de sección y `h3` subordinado dentro de la sección informativa. | Cumple |
| Reservas | Encabezados | `h1` seguido por encabezados `h2` para las secciones. | Cumple |
| Inicio | Enlaces | “Encuéntranos aquí” no describía el destino fuera de contexto; se cambió a “Ir a la sección Encuéntranos”. | Corregido |
| Tarifas y reservas | Enlaces | Los textos “Tarifas y rutas”, “Reservas”, “Ver tarifas y rutas” y “Volver a la página principal” describen sus destinos. | Cumple |
| Las tres páginas | Idioma | Cada documento declara `lang="es"`. | Cumple |
| Las tres páginas | Teclado | `Tab` recorre enlaces y contenido interactivo en orden de lectura; `Shift+Tab` vuelve en orden inverso. En reservas se probaron también flechas en radios, Espacio en políticas y Enter para enviar. | Cumple; no se detectaron trampas |

### Contraste de la paleta
Resultados consultados en WebAIM Contrast Checker. Se considera texto normal desde 4.5:1 y texto grande desde 3:1.

| Texto | Fondo | Ratio | Clasificación |
| --- | --- | ---: | --- |
| Blanco `#FFFFFF` | Verde Ruta `#1E7A4F` | 5.31:1 | Apta para texto normal |
| Blanco `#FFFFFF` | Naranja Pedal `#F39A2B` | 2.21:1 | No apta |
| Azul Noche `#14213D` | Naranja Pedal `#F39A2B` | 7.20:1 | Apta para texto normal |
| Azul Noche `#14213D` | Crema `#FAF6EF` | 14.8:1 | Apta para texto normal |
| Gris Asfalto `#5B6470` | Crema `#FAF6EF` | 5.56:1 | Apta para texto normal |
| Verde Ruta `#1E7A4F` | Crema `#FAF6EF` | 4.93:1 | Apta para texto normal |
| Naranja Pedal `#F39A2B` | Crema `#FAF6EF` | 2.05:1 | No apta |
| Blanco `#FFFFFF` | Azul Noche `#14213D` | 15.9:1 | Apta para texto normal |

### Mapa de uso de color
- Fondo general: Crema `#FAF6EF`.
- Texto principal y títulos: Azul Noche `#14213D`; texto secundario: Gris Asfalto `#5B6470`.
- Enlaces: Verde Ruta `#1E7A4F`, con subrayado visible y un indicador de foco contrastante.
- Botón primario: Verde Ruta con texto blanco.
- Botón secundario y destacados: Naranja Pedal con texto Azul Noche.
- Evitar texto blanco sobre Naranja Pedal y texto Naranja Pedal sobre Crema; ambos fallan incluso el contraste para texto grande.

### Estado de publicación
- El sitio público responde en `https://dress18.github.io/rueda-libre/` y sus páginas cargan.

### Hoja de estilos y herencia
- Las tres páginas cargan Google Fonts antes de la hoja externa `styles.css`; la página de inicio usa `css/styles.css` y las páginas de `paginas/` usan `../css/styles.css`.
- En el navegador, Montserrat 700 y Open Sans 400/600 aparecieron como fuentes cargadas. Los títulos computan Montserrat 700 y los párrafos Open Sans 400.
- En los estilos calculados, un párrafo mostró el mismo `font-family` Open Sans y el mismo `color` Azul Noche que `body`: ambas propiedades se heredan.
- `background-color` no se hereda: el cuerpo computa Crema y el párrafo transparente. También `margin-top` del párrafo conserva el margen del agente de usuario, distinto del margen cero de `body`.
- Se buscaron atributos `style`, etiquetas `<style>` y códigos hexadecimales en HTML/CSS: no hay estilos en línea ni etiquetas `<style>`; los códigos de color están declarados solamente en `:root`.

### Navegación, cascada y foco
- El selector `#menu a` tiene especificidad `(1,0,1)` (un ID y un elemento). `.activo` tiene `(0,1,0)` (una clase); por eso el color declarado en `.activo` pierde frente al color del menú y aparece tachado en Styles.
- Se conserva la clase `.activo` y se corrige el color con `#menu a.activo`, especificidad `(1,1,1)`, sin `!important` ni estilos en línea.
- Cada lista de navegación usa `id="menu"` y cada página marca su enlace actual con `.activo`.
- Los estados del menú y de “Reservar ahora” usan texto blanco sobre verde al pasar el mouse (5.31:1) y blanco sobre azul al enfocar (15.9:1). El menú normal usa gris sobre crema (5.56:1) y la página actual verde sobre crema (4.93:1).
- Los campos muestran borde verde al pasar el mouse y contorno azul al enfocar; el texto azul sobre crema tiene contraste 14.8:1.
- Se recorrieron las páginas con `Tab`; el foco permanece visible en el menú, enlaces de reserva, campos y botón. Se comprobaron los estados `:hover` y `:focus` en el navegador.

### Box model
- En DevTools Computed, para una tarjeta con `width: 100%`, `padding: 1rem` y `border: 1px`, a 876 px de ancho de ventana, `content-box` produjo un ancho calculado de 812.8 px y un ancho total de 846.4 px.
- Cambiando solo a `box-sizing: border-box`, el ancho total medido fue 812.8 px. El relleno y el borde quedan incluidos en el ancho asignado.
