# GitHub CLI (`gh`) — operar GitHub sin salir de la terminal

> Concepto general. Primera vez documentado durante la creación de `webar`
> (9 ago 2026) — instalación vía `winget`, login por device flow, creación
> de repo, habilitar Pages, disparar workflows, todo desde Claude Code.

## Qué es

`gh` es la herramienta oficial de GitHub para hacer desde la terminal casi
todo lo que harías en la web: crear repos, revisar pull requests, disparar
workflows, leer la API. En cada exploración nueva, es lo que usamos para
crear el repo, hacer push, habilitar Pages y revisar el estado del deploy
sin salir del flujo de Claude Code.

## Instalación (Windows)

```powershell
winget install --id GitHub.cli --source winget --accept-package-agreements --accept-source-agreements --silent
```

Una sesión de terminal ya abierta **no** ve el `gh` recién instalado hasta
que se refresca el PATH — o se abre una terminal nueva, o se antepone la
ruta manualmente en la sesión actual:

```bash
export PATH="$PATH:/c/Program Files/GitHub CLI"   # bash
```

## El login sin contraseña: device flow

```bash
gh auth login --hostname github.com --git-protocol https --web
```

Esto genera un **código de un solo uso** y una URL fija
(`github.com/login/device`). El código se pega ahí y se autoriza desde la
propia sesión de navegador del usuario — quien ejecuta el comando (incluido
un agente como Claude Code) nunca ve ni maneja la contraseña. Es el mismo
mecanismo que usan las apps de smart-TV para loguearte sin teclado.

Lo que queda al final no es la contraseña: es un **token OAuth**, con
permisos acotados (ver scopes abajo), revocable en cualquier momento desde
[github.com/settings/applications](https://github.com/settings/applications)
sin tocar la contraseña.

## Scopes — qué permiso le diste a qué

Un scope es un permiso específico sobre la cuenta — el token solo puede
hacer lo que sus scopes autorizan.

| Scope | Qué permite | Nota |
|---|---|---|
| `repo` | Control total de repos privados y públicos | Amplio a propósito — `gh` está pensado para uso interactivo personal |
| `workflow` | Crear/editar archivos en `.github/workflows/` | Necesario para subir un workflow de deploy |
| `user` | Leer/escribir info de perfil, incluidos emails | Se pide aparte, solo si hace falta (ej. leer el email noreply) |
| `read:org` | Ver a qué organizations perteneces (solo lectura) | Parte del paquete *default* de `gh`, se pide siempre exista o no una organization — no significa que se haya usado |
| `gist` | Crear/editar gists | Parte del paquete default, no siempre se usa |

Para automatizaciones futuras (un bot, un script de terceros) la mejor
práctica es un **Fine-grained Personal Access Token**
([github.com/settings/tokens?type=beta](https://github.com/settings/tokens?type=beta)):
se limita a un repo específico, a permisos específicos, y expira solo — a
diferencia del token amplio que genera `gh` para uso interactivo.

## Comandos usados hasta ahora

```bash
gh repo create <nombre> --private --source=. --remote=origin --push
gh repo edit <owner>/<repo> --visibility public --accept-visibility-change-consequences
gh api -X POST repos/<owner>/<repo>/pages -f "build_type=workflow"
gh workflow run deploy-pages.yml
gh run list --workflow=deploy-pages.yml --limit 1
gh auth refresh -h github.com -s <scope-adicional>
gh api user/emails
```

Ver [github-pages.md](./github-pages.md) para el flujo completo de deploy.
