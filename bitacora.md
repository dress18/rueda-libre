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

### Esquema de las regiones de cada página

```text
index.html
┌ header
│  nombre del negocio (h1) + presentación + navegación principal (nav)
├ main
│  ├ section: ¿Quiénes somos?
│  ├ section: Nuestros servicios
│  │  ├ article: Alquiler de bicicletas urbanas
│  │  ├ article: Rutas turísticas
│  │  └ article: Alquiler por horas o días
│  ├ section: ¿Cómo alquilar?
│  └ section: Encuéntranos
└ footer: derechos reservados

paginas/tarifas.html
┌ header
│  nombre del negocio + título de la página (h1) + presentación
│  + navegación principal (nav)
├ main
│  ├ section: Tarifas de alquiler de bicicletas + tabla
│  ├ section: Recorridos guiados + tabla
│  └ section: Información importante
│     └ aside: lista de qué debes llevar
└ footer: derechos reservados + enlace a inicio

paginas/reservas.html
┌ header
│  nombre del negocio + título de la página (h1)
│  + navegación principal (nav)
├ main
│  ├ section: Reserva con nosotros
│  ├ section: Horario de atención
│  │  └ aside: horario y salida de recorridos
│  └ section: Consulta nuestras tarifas
└ footer: contacto + derechos reservados
```

No se conservan `div` ni `span`: los elementos actuales pueden expresarse
con regiones o elementos HTML semánticos, y no se necesita un contenedor
genérico para aplicar estructura o presentación.

### Decisiones de controles del formulario de reserva

- El número de documento usa un campo de texto, no uno numérico: porquecon este campo no se van a hacer operaciones.
- El correo electrónico usa `type="email"` para que el navegador compruebe
  que tenga un formato de correo antes de enviar el formulario.
- La fecha usa `type="date"` para ofrecer un selector de fecha y recibir un
  valor estructurado en lugar de texto libre.

### Pruebas de validación del formulario

| Campo | Dato de prueba | Resultado esperado | Resultado obtenido |
|---|---|---|---|
| Nombre completo | `Al` | Rechazado: menos de 3 caracteres | Please lengthen this text to 3 characters or more |
| Documento | `12345` | Escribe entre 6 y 10 dígitos, sin puntos ni espacios. | Escribe entre 6 y 10 dígitos, sin puntos ni espacios. |
| Documento | `12AB567` | Rechazado: contiene letras | Please match the request format: Escribe entre 6 y 10 dígitos, sin puntos ni espacios. |
| Correo electrónico | `persona@` | Por favor ingrese la parte siguiente después del @| please enter a part following '@'. 'persona@' is incomplete |
| Celular | `3001234567` | Aceptado: 10 dígitos e inicia por 3 | Sin mensaje |
| Celular | `1234567890` | Escribe 10 digitos y comienza por 3, por ejemplo 3001234567 | Escribe 10 digitos y comienza por 3, por ejemplo 3001234567 |
| Celular | `300123` | Escribe 10 digitos y comienza por 3, por ejemplo 3001234567 | Escribe 10 digitos y comienza por 3, por ejemplo 3001234567 |
| Fecha del alquiler | `2026-10-31` | Rechazado: anterior al 1 de noviembre | Value must be 11/01/2026 or later |
| Fecha del alquiler | `2027-01-01` | Rechazado: posterior al 31 de diciembre | Value must be 11/01/2026 or later |
| Cantidad de bicicletas | `7` | Rechazado: supera el máximo de 6 | valuw must be less than or equal to 6 |
| Comentarios | 301 caracteres | Rechazado: supera el máximo de 300 | No deja ingresar más caracteres después de el límite establecido |

### Recorrido de teclado

El formulario mantiene el orden de foco del documento: datos personales,
fecha y opciones de alquiler, confirmación y botón de envío. Las opciones
del plan comparten un grupo de radio para recorrerlas con las flechas; la
aceptación de políticas se activa con la barra espaciadora.
Resultado del recorrido completo por teclado: pendiente de ejecutar en navegador.
