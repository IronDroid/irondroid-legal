# irondroid-legal

Sitio estático (HTML + CSS planos, sin build) con las políticas de privacidad de las apps Android de IronDroid, publicado en GitHub Pages: https://irondroid.github.io/irondroid-legal/. El contenido está en español. El README solo lista páginas, URLs y correos de contacto; el resto de la documentación va aquí.

## Estructura

```
index.html                    # Portada con la lista de apps
assets/style.css              # Estilos compartidos (claro/oscuro, color por app)
assets/img/<slug>/            # Capturas originales de cada app (no se publican)
assets/img/<slug>/web/        # Capturas optimizadas (WebP 480 px) que usan las páginas
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

## Imágenes

Las capturas originales se guardan en `assets/img/<slug>/` y las páginas solo usan las versiones optimizadas de `assets/img/<slug>/web/` (`1.webp`, `2.webp`…; la 1 es la del hero y la tarjeta de la portada). Se referencian con ruta relativa (`../assets/img/...` desde la política, `./assets/img/...` desde la portada) y llevan `width`/`height` y `alt`.

No publicar capturas con datos personales: nombres, fotos, correos, listas de alumnos ni nombres de colegio. Por eso se excluyeron `00_inicio`, `02_estudiantes`, `05_exportar_asistencia`, `08_tomar_asistencia` y `09_centralizador` de ColeApp, el perfil y el ranking de Joven Adventista, y el menú principal y el rincón de unidad del Club de Conquistadores.

## Reglas

- Todos los enlaces internos son relativos (sin `/` inicial): el sitio vive bajo `/irondroid-legal/`.
- No usar PDF ni URLs con fechas o versiones: las URLs se registran en Play Console y deben ser estables.
- Sin scripts externos. Única dependencia externa permitida: Google Fonts (Outfit para titulares, Work Sans para texto), con `display=swap`.
- Remoto `origin` por SSH (`git@github.com:IronDroid/irondroid-legal.git`); por HTTPS el push falla por falta de credenciales.

## Diseño

Estilo landing de app, una sola marca IronDroid; cada app cambia solo color y capturas. Todo en `assets/style.css`.

- **Color por app**: clase en `<body>` (política) y en el `<li>` (portada): `app-hiad`, `app-joven`, `app-coleapp`, `app-club`, `app-pathfinder`. Fijan `--brand` y `--accent`, con variante oscura (`--on-brand` solo en oscuro). `--soft` se calcula en `body, [class*="app-"]` (depende de `--brand`; no moverlo a `:root`). Contraste mínimo 4.5:1 en texto.
- **Política**: barra superior → hero (icono, package ID, titular, frase, botones Google Play / política, 3 teléfonos) → carrusel "Así se ve" → política con índice lateral sticky (los `<h3>` llevan `id`) → pie con contacto.
- **Teléfonos**: componente `.phone` (marco CSS) que contiene la captura completa, sin recortar. Hero: izquierda, centro y derecha; el índice 0 de `web/` es la captura principal.
- **Icono**: el original va en `assets/img/<slug>/icon.png` (512×512, no se sube) y las páginas usan `assets/img/<slug>/web/icon.webp` (192 px). Se muestra sobre un cuadrado blanco (`.icon.has-img`) porque los iconos tienen formas y fondos distintos.
- Modo oscuro automático (`prefers-color-scheme`), diseño adaptable a móvil, `prefers-reduced-motion` respetado.

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
