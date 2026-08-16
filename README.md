# Barbate C.F. — web del club

Web estática de una sola página (`index.html`) para el Barbate Club de Fútbol.
Sin build, sin framework: HTML + CSS puro, con un único script de unas
pocas líneas para el menú móvil.

## Estructura

```
index.html           toda la web (HTML + CSS en <style>, un <script> mínimo)
images/               logos de patrocinadores y fotos del club
.claude/launch.json   arranca un servidor local para previsualizar (npx http-server)
```

No hay `package.json` ni dependencias: todo lo que hace falta para ver la
web es un navegador.

## Ver la web en local

Dos formas:

- Abrir `index.html` directamente con doble clic (funciona para casi todo).
- Levantar un servidor local (recomendado, evita restricciones del navegador
  con `file://`):

  ```bash
  npx --yes http-server -p 4173
  ```

  y abrir `http://localhost:4173`.

## Secciones de la página

| Sección | Ancla | Contenido |
|---|---|---|
| Inicio | `#inicio` | Hero con el escudo y la frase "Sangre roja, mar azul" |
| Historia | `#historia` | Texto del club + datos clave |
| Hazte socio | — | Precios de abonado |
| Partidos | `#partidos` | Próximos partidos + calendario completo de liga (escrito a mano en el HTML) |
| Categorías | `#categorias` | Todas las categorías, de prebenjamín a senior |
| Primer equipo | `#plantel` | Jugadores y cuerpo técnico (foto, nombre, posición) |
| Galería | `#galeria` | Foto del primer equipo + foto familiar del club |
| Contacto | `#contacto` | Campo, redes sociales, mapa de Google |
| Patrocinadores | — | Logos de los colaboradores del club |

## Cómo editar cada cosa

### Patrocinadores

Cada logo es una imagen en `images/` referenciada directamente en el HTML
(buscar `class="sponsor-row"`). Para añadir uno nuevo: sube el archivo a
`images/` y añade una línea `<img src="images/archivo.jpeg" alt="Nombre">`.

### Primer equipo (jugadores y cuerpo técnico)

Cada tarjeta usa un sistema de "foto pendiente" automático (clase
`.foto-slot`, buscar `class="jugador"` en el HTML): mientras el archivo de
imagen no exista, se ve un patrón rayado de aviso; en cuanto subes el
archivo con el nombre exacto, la foto aparece sola, sin tocar el CSS.

Para añadir un jugador: duplica un bloque `<div class="jugador">...</div>`,
cambia el nombre y la posición, y sube su foto a `images/plantel/` con el
nombre que pusiste en `--foto:url('images/plantel/....jpg')`.

### Fotos de la galería (equipo y foto familiar)

Mismo sistema de foto pendiente. Rutas esperadas:

- `images/primer-equipo.jpg` — foto del primer equipo
- `images/foto-familiar.jpg` — foto familiar del club

### Calendario de partidos

No hay base de datos ni CMS: cada jornada es una fila escrita a mano en el
HTML (buscar `jornada-row`). Para actualizar un resultado o fecha, se edita
directamente ahí.

### Menú móvil

El menú hamburguesa es CSS puro (un `<input type="checkbox">` oculto +
`:checked` para mostrar/ocultar), sin dependencias. El único JavaScript de
toda la página son 3 líneas al final del `<body>` que cierran el menú al
tocar un enlace.

## Pendiente

- Subir las fotos reales: `images/primer-equipo.jpg`, `images/foto-familiar.jpg`
  y las de cada jugador/entrenador en `images/plantel/`.
- No hay remoto de git configurado todavía (`git remote -v` vacío) — el
  repositorio solo existe en local.
- El feed automático de Instagram se descartó a propósito; la Galería usa
  fotos propias en su lugar.
