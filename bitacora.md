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
