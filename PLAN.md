# Plan: Privacy policies site for Android apps (GitHub Pages)

## Primary goal

Cada app Android del usuario tiene una URL pública y estable de política de privacidad que se puede pegar en Google Play Console, y un índice que lista todas las apps y enlaza a cada política.

## Phase 0: Documentation discovery

**How this serves the primary goal:** fija las reglas reales de GitHub Pages y de Google Play para que las URLs sean válidas y no cambien.

Facts to confirm before building (read these docs, do not assume):
- GitHub Pages: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
  - Project site URL is `https://<user>.github.io/<repo>/` → all internal links must be relative (no leading `/`).
  - `.nojekyll` at the root disables Jekyll so plain HTML is served as-is.
- Google Play Console privacy policy requirements (Play Console Help, "Provide information for Google Play's Data safety section" and "User Data" policy):
  - URL must be public, not geofenced, not a PDF, and should be a web page that names the app/developer.
  - Policy must cover data collected, use, sharing, retention/deletion and a contact.
- Inputs needed from the user (blocking for Phase 2): GitHub username, repo name (default `irondroid-legal`), developer name, contact email, and per app: name, package id, languages, data collected / SDKs (ads, analytics, crash reporting), permissions.

Anti-patterns: PDF policies, URLs containing dates or versions, absolute `/path` links, JS-only rendering of policy text.

## Phase 1: Site skeleton

**How this serves the primary goal:** crea la estructura que define las URLs estables.

- `index.html` (lists apps, links `./<app-slug>/`)
- `<app-slug>/index.html` per app → final URL `https://<user>.github.io/<repo>/<app-slug>/`
- `assets/style.css` shared, `.nojekyll`
- Plain HTML + CSS, no build step. Each page has `<title>`, `lang`, viewport meta.
- Copy one app page as a template for new apps (`_template/` is not published as a link; keep it out of the index).

Verification: open files locally; `grep -rn 'href="/' .` returns nothing.

## Phase 2: Policy content per app

**How this serves the primary goal:** el contenido es lo que Google Play revisa.

- Use the template sections: developer + contact, data collected, how it is used, third parties/SDKs, retention and deletion, children, changes, effective date.
- Content must match the app's Data safety form in Play Console.

Verification: each policy names the app, developer and contact email; checklist vs Data safety answers.

## Phase 3: Publish

**How this serves the primary goal:** hace las URLs públicas.

- `git init`, create GitHub repo (public), push `main`.
- Settings → Pages → Deploy from branch `main` / root.

Verification: `curl -sI https://<user>.github.io/<repo>/<app-slug>/` returns 200 for index and every app.

## Phase 4: Verify and register

**How this serves the primary goal:** confirma que lo publicado es lo que se pega en Play Console.

- Check all index links resolve (curl loop), pages load without login, no PDF.
- Paste each app URL in Play Console → App content → Privacy policy.

## Not now

Custom domain · multi-language policies (unless requested) · static site generator · analytics on the site
