# irondroid-legal

Sitio estático (HTML + CSS planos, sin build) con las políticas de privacidad de las apps Android de IronDroid, publicado en GitHub Pages: https://irondroid.github.io/irondroid-legal/. El contenido está en español. El README solo lista páginas, URLs y correos de contacto; el resto de la documentación va aquí.

## Estructura

```
index.html                    # Portada con la lista de apps
assets/style.css              # Estilos compartidos (claro/oscuro, color por app)
<slug>/index.html             # Una política por app
.nojekyll                     # Desactiva Jekyll en GitHub Pages
PLAN.md                       # Plan original del proyecto
```

## Apps

| Slug | Package ID | Clase de `<body>` | Google Play | Contacto |
|---|---|---|---|---|
| tu-himnario-adventista | `org.ajcm.hiad` | `app-hiad` | https://play.google.com/store/apps/details?id=org.ajcm.hiad | jhonlimaster@gmail.com |
| joven-adventista | `org.ajcm.jovenadventista` | `app-joven` | https://play.google.com/store/apps/details?id=org.ajcm.jovenadventista | jhonlimaster@gmail.com |
| coleapp | `com.coleappedu.coleapp` | `app-coleapp` | https://play.google.com/store/apps/details?id=com.coleappedu.coleapp | coleapp710@gmail.com |
| club-de-conquistadores | `org.ajcm.conquistadores` | `app-club` | https://play.google.com/store/apps/details?id=org.ajcm.conquistadores | jhonlimaster@gmail.com |
| conquistadores-y-guias-mayores | `org.ajcm.pathfinderdia` | `app-pathfinder` | https://play.google.com/store/apps/details?id=org.ajcm.pathfinderdia | jhonlimaster@gmail.com |

## Reglas

- Todos los enlaces internos son relativos (sin `/` inicial): el sitio vive bajo `/irondroid-legal/`.
- No usar PDF ni URLs con fechas o versiones: las URLs se registran en Play Console y deben ser estables.
- Sin fuentes ni scripts externos.
- Remoto `origin` por SSH (`git@github.com:IronDroid/irondroid-legal.git`); por HTTPS el push falla por falta de credenciales.

## Diseño

- Cada app tiene un color propio: la clase del `<body>` fija `--accent` en `assets/style.css`, con variante para modo oscuro.
- Cada política tiene cabecera (nombre, botón a Google Play, fecha, package ID) e índice lateral generado a partir de los `<h2>`, que llevan `id`.
- Modo oscuro automático (`prefers-color-scheme`) y diseño adaptable a móvil.

## Publicación

Settings → Pages → Deploy from a branch, `main`, `/ (root)`. Cada push a `main` actualiza el sitio en unos minutos. Las URLs son `https://irondroid.github.io/irondroid-legal/<slug>/`.

Si esa URL redirige a otro dominio, es el dominio personalizado heredado del repo `IronDroid/IronDroid.github.io` (se quita en su Settings → Pages y borrando su `CNAME`).

## Añadir o editar una app

1. Copiar una carpeta existente (por ejemplo `coleapp/`) con el nuevo slug.
2. Editar su `index.html`: título, nombre, package ID, URL de Google Play, correo y secciones.
3. Cambiar la clase del `<body>`; si hace falta un color nuevo, añadir `.app-xxx { --accent:#...; }` y su variante oscura en `assets/style.css`.
4. Añadir la tarjeta en `index.html` con la misma clase de color.
5. Actualizar la tabla del README y la de este archivo.

## Pendiente

- Las secciones marcadas `[EJEMPLO]` (datos recopilados, uso, terceros, permisos, conservación, menores) son texto genérico: reemplazarlas con los datos reales de cada app antes de usar las URLs en Play Console.
- Quitar el aviso "Contenido de ejemplo" de cada política al terminar.
