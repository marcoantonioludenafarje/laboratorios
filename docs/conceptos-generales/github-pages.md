# GitHub Pages — hosting estático gratuito por repo

> Concepto general. Primera vez usado en `webar` (9 ago 2026): repo → build
> con GitHub Actions → sitio en `usuario.github.io/repo/`.

## Qué es

Hosting **estático** gratuito, servido desde un repo, con HTTPS automático,
bajo `usuario.github.io/nombre-repo/`. No ejecuta backend, no corre
consultas a una base de datos — sirve exactamente los archivos HTML/CSS/JS
que le entregues.

## El límite real: repos privados en el plan free

En el plan gratuito, Pages **rechaza por completo** los repos privados — no
es que el sitio quede visible igual, la API de habilitación devuelve error
directamente:

```json
{"message":"Your current plan does not support GitHub Pages for this repository."}
```

Esto obliga a elegir, por cada exploración que quiera un sitio en vivo:

| Opción | Privacidad del código | Costo |
|---|---|---|
| Repo público + Pages | Código visible por cualquiera | Gratis |
| Repo privado, sin Pages | Privado | Gratis — solo local/`ngrok` para probar |
| Repo privado + Vercel/Netlify (plan free) | Privado, URL no listada pero no protegida por contraseña | Gratis, cuenta aparte |

`webar` eligió repo público + Pages, de forma consciente.

## Dos formas de generar el sitio

**Sin build (Jekyll por defecto)** — sirve para repos que son solo
Markdown/HTML sin paso de compilación (como este mismo repo
`laboratorios`): se activa apuntando Pages a una rama y carpeta, sin
workflow.

**Con build (GitHub Actions)** — necesario cuando el sitio se genera con
una herramienta (Vite, en el caso de `webar`). Tres piezas:

```yaml
# .github/workflows/deploy-pages.yml
on:
  push:
    branches: [master]
  workflow_dispatch:

permissions:
  contents: read
  pages: write      # el runner solo puede publicar Pages, nada más
  id-token: write

jobs:
  build:
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci && npm run build
      - uses: actions/upload-pages-artifact@v3
        with: { path: dist }
  deploy:
    needs: build
    steps:
      - uses: actions/deploy-pages@v4
```

Habilitar Pages con este modo (una sola vez, vía API):

```bash
gh api -X POST repos/<owner>/<repo>/pages -f "build_type=workflow"
```

## Rutas relativas — el detalle que rompe todo si se ignora

Un sitio en la raíz de un dominio y uno servido en
`usuario.github.io/repo/` no son lo mismo. Cualquier link/asset con ruta
**absoluta** (`/index.html`, `/src/...`) se rompe bajo un subpath. Regla
aplicada en `webar`:

- `vite.config.ts` → `base: "./"` (rutas de build relativas).
- Todo `href`/`src` en el HTML y en el código → relativo, nunca con `/`
  inicial.

Con eso, el mismo build funciona igual en local, en un dominio raíz, o bajo
`usuario.github.io/repo/`.

## Verificar un deploy

```bash
gh run list --workflow=deploy-pages.yml --limit 1 --json status,conclusion
curl -s -o /dev/null -w "%{http_code}\n" https://usuario.github.io/repo/
```

Ver [github-cli.md](./github-cli.md) para el resto de comandos de `gh`
usados en este flujo.
