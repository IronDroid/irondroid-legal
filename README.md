# irondroid-legal

Sitio estático con las **políticas de privacidad** de las apps Android de IronDroid. Está pensado para publicarse en GitHub Pages y para pegar la URL de cada política en Google Play Console.

Sitio publicado: https://irondroid.github.io/irondroid-legal/

## Apps incluidas

| App | Package ID | Política | Google Play |
|---|---|---|---|
| Tu Himnario Adventista | `org.ajcm.hiad` | [/tu-himnario-adventista/](https://irondroid.github.io/irondroid-legal/tu-himnario-adventista/) | [Ver](https://play.google.com/store/apps/details?id=org.ajcm.hiad) |
| Joven Adventista | `org.ajcm.jovenadventista` | [/joven-adventista/](https://irondroid.github.io/irondroid-legal/joven-adventista/) | [Ver](https://play.google.com/store/apps/details?id=org.ajcm.jovenadventista) |
| ColeApp | `com.coleappedu.coleapp` | [/coleapp/](https://irondroid.github.io/irondroid-legal/coleapp/) | [Ver](https://play.google.com/store/apps/details?id=com.coleappedu.coleapp) |
| Club de Conquistadores | `org.ajcm.conquistadores` | [/club-de-conquistadores/](https://irondroid.github.io/irondroid-legal/club-de-conquistadores/) | [Ver](https://play.google.com/store/apps/details?id=org.ajcm.conquistadores) |
| Conquistadores y Guías Mayores | `org.ajcm.pathfinderdia` | [/conquistadores-y-guias-mayores/](https://irondroid.github.io/irondroid-legal/conquistadores-y-guias-mayores/) | [Ver](https://play.google.com/store/apps/details?id=org.ajcm.pathfinderdia) |

Contacto: ColeApp usa `coleapp710@gmail.com`; las demás apps usan `jhonlimaster@gmail.com`.

## Estructura

```
.
├── index.html                      # Portada con la lista de apps
├── assets/style.css                # Estilos compartidos (claro/oscuro, color por app)
├── <slug-de-la-app>/index.html     # Una política por app (5 carpetas)
├── .nojekyll                       # Desactiva Jekyll en GitHub Pages
├── PLAN.md                         # Plan original del proyecto
└── README.md
```

HTML y CSS planos, sin build ni dependencias. Todos los enlaces internos son relativos para funcionar bajo `/irondroid-legal/`.

## Diseño

- Cada app tiene un color propio, definido con una clase en `<body>` (`app-hiad`, `app-joven`, `app-coleapp`, `app-club`, `app-pathfinder`) que fija `--accent` en `assets/style.css`.
- Cada política tiene cabecera con nombre, botón a Google Play, fecha y package ID, además de un índice lateral generado a partir de los `<h2>`.
- Modo oscuro automático (`prefers-color-scheme`) y diseño adaptable a móvil.
- Sin fuentes ni scripts externos.

## Publicación (GitHub Pages)

1. En el repositorio: Settings → Pages.
2. Source: Deploy from a branch, rama `main`, carpeta `/ (root)`.
3. Cada push a `main` actualiza el sitio en unos minutos.

Las URLs tienen la forma `https://irondroid.github.io/irondroid-legal/<slug>/`. Estas son las que se registran en Play Console (App content → Privacy policy).

## Cómo añadir o editar una app

1. Copia una carpeta existente, por ejemplo `coleapp/`, con el nuevo slug.
2. Edita en su `index.html`: título, nombre, package ID, URL de Google Play, correo de contacto y las secciones de la política.
3. Cambia la clase del `<body>` y, si hace falta un color nuevo, añade `.app-xxx { --accent:#...; }` (y su variante oscura) en `assets/style.css`.
4. Añade la tarjeta en `index.html`, con la misma clase de color.
5. Mantén los enlaces relativos y no uses PDF ni URLs con fechas.

## Pendiente

- Las secciones marcadas `[EJEMPLO]` (datos recopilados, uso, servicios de terceros, permisos, conservación y menores) son texto genérico. Hay que reemplazarlas con los datos reales de cada app antes de usar las URLs en Play Console.
- Quitar el aviso "Contenido de ejemplo" de cada política al terminar.

## Notas

- Si `irondroid.github.io/irondroid-legal/` redirige a otro dominio, es el dominio personalizado heredado del repositorio `IronDroid/IronDroid.github.io`. Se quita en Settings → Pages de ese repositorio.
- El idioma del contenido es español.
