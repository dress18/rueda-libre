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
