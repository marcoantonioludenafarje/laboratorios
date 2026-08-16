# Laboratorios

Índice maestro de todas las exploraciones tecnológicas bajo
`ideas_negocio/`. Cada exploración es su propio repo (nunca uno por
tecnología) y sigue la misma metodología: [PLAYBOOK.md](./PLAYBOOK.md).
Reglas de nombres, visibilidad y cómo arrancar una exploración nueva:
[TAXONOMIA.md](./TAXONOMIA.md).

Este repo no tiene código de producto — es documentación pura: el índice,
el playbook reutilizable, el catálogo de qué ya está resuelto, y los
conceptos de tooling que se repiten entre exploraciones.

## Exploraciones con repo

| Categoría | Exploración | Tecnologías | Repo | Visibilidad | Sitio en vivo | Estado |
|---|---|---|---|---|---|---|
| `exploraciones/retail-tech/` | [webar](https://github.com/marcoantonioludenafarje/webar) | MindAR, A-Frame | ✓ | Público (necesita Pages) | [Pages](https://marcoantonioludenafarje.github.io/webar/) | [ROADMAP](https://github.com/marcoantonioludenafarje/webar/blob/master/ROADMAP.md): A1-A2 implementados, A3-A5 + 2 demos integrales planeados |
| `exploraciones/agent-tooling/` | [agent-remote-labs](https://github.com/marcoantonioludenafarje/agent-remote-labs) | tmux, Claude Code, ntfy, PWA, Tailscale | ✓ | Privado (sin demo web) | — | Estructura creada, labs pendientes de ejecutar |
| `exploraciones/customer-engagement/` | [whatsapp-integration](https://github.com/marcoantonioludenafarje/whatsapp-integration) | WhatsApp Cloud API, WPPConnect, Baileys, whatsapp-web.js, Evolution API | ✓ | Privado (sin demo web) | — | [ROADMAP](https://github.com/marcoantonioludenafarje/whatsapp-integration/blob/main/ROADMAP.md): 16 labs documentados; WA-CLOUD-01 implementado, pendiente de ejecución manual (config en Meta) |

## Exploraciones sin repo — `exploraciones-pendientes/`

Carpeta creada, propuesta escrita, todavía sin `gh repo create`. Ver
[TAXONOMIA.md §6](./TAXONOMIA.md#6-cómo-arrancar-una-exploración-nueva-en-un-chat)
para arrancar cualquiera de estas en un chat nuevo — al arrancar, se
mueven de aquí a su categoría correspondiente.

| Exploración | Categoría probable | Doc |
|---|---|---|
| nfc-labs | `retail-tech/` | `exploraciones-pendientes/nfc-labs/EXPLORATION.md` |
| instagram-platform | `social-platforms/` | `exploraciones-pendientes/instagram-platform/EXPLORATION.md` |
| tiktok-developer-platform | `social-platforms/` | `exploraciones-pendientes/tiktok-developer-platform/EXPLORATION.md` |
| tiktok-in-app-interactive | `social-platforms/` | `exploraciones-pendientes/tiktok-in-app-interactive/EXPLORATION.md` |
| tiktok-live-interactive | `social-platforms/` | `exploraciones-pendientes/tiktok-live-interactive/EXPLORATION.md` |
| avatar-lab | *(por definir)* | `exploraciones-pendientes/avatar-lab/EXPLORATION.md` |

"Sitio en vivo" solo aplica a exploraciones con demos web — un lab en bash
(ej. tmux) se documenta igual pero no tiene URL, solo su
`labs/<tech>/lab-NN/README.md` con la evidencia del experimento.

## Antes de crear un laboratorio nuevo

Revisar [CATALOGO.md](./CATALOGO.md) — puede que la capacidad que vas a
validar (o el tooling que vas a necesitar) ya esté resuelto en otra
exploración.

## Conceptos generales (no específicos de una exploración)

Tooling y conceptos que aparecen repetidamente entre exploraciones, para no
volver a explicarlos cada vez:

- [git-worktrees.md](./docs/conceptos-generales/git-worktrees.md) — trabajar varios chats en paralelo dentro del mismo repo.
- [github-cli.md](./docs/conceptos-generales/github-cli.md) — `gh`, autenticación por device flow, scopes.
- [github-pages.md](./docs/conceptos-generales/github-pages.md) — hosting estático, límite con repos privados, rutas relativas.
- [claude-code-artifacts.md](./docs/conceptos-generales/claude-code-artifacts.md) — páginas privadas publicadas por el agente, sin repo.

## Historial de decisiones sobre el propio flujo de trabajo

- [2026-08-09 — Flujo paralelo y worktrees](./docs/historial/2026-08-09-flujo-paralelo-worktrees.md) — cómo se llegó a la estructura actual.
- [TAXONOMIA.md](./TAXONOMIA.md) — reglas de nombres/visibilidad y por qué existen (nacieron de inconsistencias reales encontradas el mismo día).

## Estructura de una exploración

Ver [PLAYBOOK.md](./PLAYBOOK.md) §15 para el detalle completo. Resumen:

```text
<exploracion>/
├── CLAUDE.md              delgado: primera línea apunta a este PLAYBOOK.md
├── OBJECTIVE.md           problema, objetivo final, preguntas, diagrama
├── ROADMAP.md             matriz tecnología → lab → pregunta → resultado
├── README.md              cómo correr, cómo probar, estado
├── docs/
│   ├── concepts.md        teoría específica de esta exploración
│   ├── findings.md        qué resolvió cada tecnología, limitaciones, decisión
│   └── decisions.md       registro de decisiones arquitectónicas
├── labs/
│   └── <tecnologia>/
│       └── lab-NN-<nombre>/README.md
├── demos-integrales/
│   └── demo-NN-<nombre>/README.md
└── ARCHITECTURE-V1.md     al cierre de la fase exploratoria
```
