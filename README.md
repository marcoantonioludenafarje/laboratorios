# Laboratorios

Índice maestro de todas las exploraciones tecnológicas bajo
`ideas_negocio/`. Cada exploración es su propio repo (nunca uno por
tecnología) y sigue la misma metodología: [PLAYBOOK.md](./PLAYBOOK.md).

Este repo no tiene código de producto — es documentación pura: el índice,
el playbook reutilizable, el catálogo de qué ya está resuelto, y los
conceptos de tooling que se repiten entre exploraciones.

## Exploraciones

| Exploración | Tecnologías | Repo | Sitio en vivo | Estado |
|---|---|---|---|---|
| WebAR Lab | MindAR, A-Frame | [webar](https://github.com/marcoantonioludenafarje/webar-lab) | [Pages](https://marcoantonioludenafarje.github.io/webar-lab/) | [ROADMAP](https://github.com/marcoantonioludenafarje/webar-lab/blob/master/ROADMAP.md): A1-A2 implementados, A3-A5 + 2 demos integrales planeados |
| Agent Remote Labs | tmux, Claude Code, ntfy, PWA, Tailscale | [agent-remote-labs](https://github.com/marcoantonioludenafarje/agent-remote-labs) | — (local-only por ahora) | Estructura creada, labs pendientes de ejecutar |
| NFC Labs | NFC | *(sin repo aún — solo roadmap)* | — | Roadmap escrito |
| Avatar Labs | *(por definir)* | *(sin repo aún)* | — | Placeholder |
| Computer Vision Labs | *(por definir)* | *(sin repo aún)* | — | Placeholder |
| Social Media Labs | *(por definir)* | *(sin repo aún)* | — | Placeholder |
| WhatsApp Labs | *(por definir)* | *(sin repo aún)* | — | Placeholder |

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

## Estructura de una exploración

Ver [PLAYBOOK.md](./PLAYBOOK.md) §15 para el detalle completo. Resumen:

```text
<exploracion>/
├── CLAUDE.md              delgado: solo lo específico de esta exploración
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
