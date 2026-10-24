Url del sitio: https://dress18.github.io/rueda-libre/
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

- El número de documento usa un campo de texto, no uno numérico, porque con los datos obtenidos en este campo no se van a hacer operaciones
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

Prueba realizada en Chrome con teclado: `Tab` recorre Inicio, Tarifas y rutas,
Reservas, el enlace a tarifas y después los controles del formulario en orden
de lectura. El control de fecha expone sus segmentos internos durante el
recorrido; al completar la fecha el foco continúa hacia tipo de bicicleta.
`Shift + Tab` desde el botón vuelve a la casilla de políticas. Las flechas
cambian la opción del plan, la barra espaciadora marca las políticas y `Enter`
envía el formulario válido por `POST` al punto de prueba local. No se añadieron
índices `tabindex` ni controles que alteren el orden natural.

### Auditoría de accesibilidad de las páginas

| Página | Hallazgo | Corrección o resultado |
|---|---|---|
| Inicio | El enlace interno decía «Encuéntranos aquí», texto poco claro fuera de contexto | Cambiado a «Ir a la sección de contacto»; conserva el destino `#encuentranos` |
| Inicio | Imágenes con alternativas descriptivas; jerarquía h1-h2-h3 coherente; `lang="es"` presente | Sin cambios necesarios |
| Tarifas | El logo tiene alternativa «Logo de Rueda Libre»; jerarquía h1-h2-h3 coherente; enlaces con texto descriptivo; `lang="es"` presente | Sin cambios necesarios |
| Reservas | Jerarquía h1-h2 coherente; navegación y enlace a tarifas descriptivos; `lang="es"` presente | Sin cambios necesarios |
| Las tres páginas | Recorrido con teclado y orden de foco | Orden nativo comprobado en Chrome; formulario recorre datos, alquiler, confirmación y envío |

### Contraste y mapa de uso de color

Se evaluaron en WebAIM Contrast Checker. Criterios WCAG AA: texto normal,
mínimo 4.5:1; texto grande, mínimo 3:1.

| Texto (primer plano) | Fondo | Contraste | Clasificación |
|---|---|---:|---|
| Blanco `#FFFFFF` | Verde Ruta `#1E7A4F` | 5.31:1 | Apta para texto normal |
| Blanco `#FFFFFF` | Naranja Pedal `#F39A2B` | 2.21:1 | No apta |
| Azul Noche `#14213D` | Naranja Pedal `#F39A2B` | 7.20:1 | Apta para texto normal |
| Azul Noche `#14213D` | Crema `#FAF6EF` | 14.82:1 | Apta para texto normal |
| Gris Asfalto `#5B6470` | Crema `#FAF6EF` | 5.56:1 | Apta para texto normal |
| Verde Ruta `#1E7A4F` | Crema `#FAF6EF` | 4.93:1 | Apta para texto normal |
| Naranja Pedal `#F39A2B` | Crema `#FAF6EF` | 2.05:1 | No apta |
| Blanco `#FFFFFF` | Azul Noche `#14213D` | 15.97:1 | Apta para texto normal |

No hubo combinaciones aptas solo para texto grande: las que pasan superan
4.5:1 y las otras dos no alcanzan 3:1.

#### Mapa de uso de color

- **Fondo general:** Crema `#FAF6EF`.
- **Texto principal y títulos:** Azul Noche `#14213D` sobre Crema; ambos
  alcanzan contraste para texto normal.
- **Texto secundario:** Gris Asfalto `#5B6470` sobre Crema.
- **Encabezado oscuro:** fondo Azul Noche con texto blanco.
- **Enlaces:** Verde Ruta sobre Crema.
- **Botón principal:** fondo Verde Ruta con texto blanco.
- **Botón secundario y destacados con texto:** fondo Naranja Pedal con texto
  Azul Noche. Evitar texto blanco sobre Naranja Pedal y texto Naranja Pedal
  sobre Crema; ambas combinaciones fallan incluso para texto grande.

### Comprobación de herencia en DevTools

En `index.html`, comprobé los estilos calculados de un párrafo dentro de
`main`. Para contrastarlo en DevTools, selecciona ese párrafo: **Styles** debe
mostrar `font-family` y `color` heredados de `body`, y **Computed** debe mostrar:

| Propiedad | Valor calculado | Comprobación |
|---|---|---|
| `font-family` | `"Open Sans", Arial, sans-serif` en el párrafo y en `body` | Se hereda |
| `margin` | `16px 0px` en el párrafo; `0px 99.5px` en `body` | No se hereda |

El color calculado del párrafo también coincide con el de `body`
(`rgb(20, 33, 61)`), confirmando la herencia de `color`.

### Cascada y especificidad de la navegación

La regla inicial del compañero para el menú es `#menu a`, con especificidad
`(1, 0, 1)` (un ID, cero clases/pseudoclases y un elemento). La regla
`.activo` tiene especificidad `(0, 1, 0)` (cero ID, una clase y cero elementos).
Por eso `#menu a` gana para `color`: en **Styles** el color de `.activo` queda
tachado, aunque `font-weight` sí se aplica porque el menú no lo declara.

Se conserva `.activo` y se añade `#menu a.activo`, cuya especificidad es
`(1, 1, 1)`, para que el verde de la página actual venza al gris de `#menu a`.
No se usa `!important` ni estilos en línea. El menú tiene fondo Crema, por lo
que Gris Asfalto y Verde Ruta conservan sus contrastes aprobados. Comprueba la
cascada seleccionando el enlace actual en **Styles**: la corrección específica
debe ganar para `color`; usa `:hov` para forzar `:hover` y `:focus`.

Los estados del menú usan `header nav #menu a:hover` y
`header nav #menu a:focus`, con especificidad `(1, 1, 3)`, para que el estado
interactivo también venza al selector del enlace actual.

### Prueba de interacción y teclado

Forcé `:hover` mediante el protocolo CSS del navegador y revisé el estado
visual: el elemento del menú y el CTA cambian a fondo Naranja Pedal con texto
Azul Noche. El botón usa el mismo par al pasar el puntero; los campos muestran
borde Verde Ruta. En reposo, los enlaces del menú usan Gris Asfalto y el enlace
actual Verde Ruta sobre Crema.

Recorrí con `Tab` las tres páginas: inicio y tarifas tienen 6 y 5 destinos de
foco distintos; reservas tiene 18, incluidos los controles del formulario.
Los destinos muestran contorno Azul Noche de 3 px y halo Crema. El selector de
fecha también tiene una regla de foco específica para reforzar el indicador
cuando el navegador enfoca sus segmentos nativos. En Chrome, al recorrer con
`Tab` los segmentos internos de la fecha, el segmento activo aparece
seleccionado; en ese subestado el contorno CSS puede calcularse como `none`,
pero el indicador nativo de selección permanece visible.

Se añadieron estados para menú, enlaces CTA, botón y campos. El foco usa un
contorno Azul Noche y un halo Crema para seguir visible tanto sobre el fondo
claro como dentro del encabezado oscuro. Los estados hover/focus del menú y CTA
usan Azul Noche sobre Naranja Pedal; el CTA en reposo usa Blanco sobre Verde
Ruta. Los campos muestran borde Verde Ruta al pasar el puntero.
