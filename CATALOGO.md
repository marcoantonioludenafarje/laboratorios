# Catálogo de reutilización

Qué ya está validado y dónde — para no repetir un laboratorio o una
explicación que otra exploración ya resolvió. Antes de escribir un LAB
nuevo, revisar esta tabla.

Actualizar esta tabla al cerrar cualquier laboratorio o experimento que
produzca algo reutilizable (un patrón, un snippet, una decisión).

## Infraestructura / tooling

| Capacidad validada | Exploración | Dónde | Reutilizable como |
|---|---|---|---|
| Deploy estático a GitHub Pages vía GitHub Actions (build con Vite) | webar | `labs/mindar-aframe/lab-01-camera` | Copiar `.github/workflows/deploy-pages.yml` + `base: "./"` en `vite.config.ts` tal cual |
| Auth de `gh` CLI por device flow, sin exponer contraseña | webar (sesión) | [docs/conceptos-generales/github-cli.md](./docs/conceptos-generales/github-cli.md) | Aplica a cualquier repo nuevo — no repetir la explicación, solo enlazar |
| Reescritura de historial + identidad de commit con email noreply | webar (sesión) | [docs/conceptos-generales/github-cli.md](./docs/conceptos-generales/github-cli.md) | `git filter-branch --env-filter` + `git push --force`, solo viable si nadie más clonó el repo aún |
| Overlay de debug en pantalla + log de eventos (sin DevTools) | webar | `labs/mindar-aframe/lab-01-camera`, `lab-02-image-tracking` | `MetricsService` + `DebugOverlay` + `EventLog`, genéricos, sin dependencias de AR — copiables a cualquier exploración con UI web |
| Git worktrees para trabajar 2+ chats en paralelo dentro de un repo | agent-remote-labs | [docs/conceptos-generales/git-worktrees.md](./docs/conceptos-generales/git-worktrees.md) | Aplica cuando una exploración necesita paralelismo real, no antes |
| Arnés de evidencia para pruebas físicas: mide solo lo medible, pregunta solo lo que no, y emite JSON + Markdown descargables | webar | `src/core/evidence/` | Copiable a cualquier exploración con UI web y validación manual. Sin dependencias, sin backend. **Implementado, pendiente de validación física** — ver PLAYBOOK §23.4 |
| Publicar una página privada sin repo (Claude Artifact) | webar (sesión) | [docs/conceptos-generales/claude-code-artifacts.md](./docs/conceptos-generales/claude-code-artifacts.md) | Solo para contenido de una sola página, autocontenido, sin build |

## Capacidades de producto (por tecnología)

| Tecnología | Capacidad validada | Exploración | Estado |
|---|---|---|---|
| MindAR + A-Frame | Acceso a cámara trasera desde el navegador móvil | webar | Implementado, pendiente de prueba física |
| MindAR + A-Frame | Detección/tracking de imagen impresa | webar | Implementado, pendiente de prueba física |
| tmux | Persistencia de sesión tras cerrar terminal | agent-remote-labs | Pendiente de ejecutar |

## Cómo usar esta tabla

1. Antes de crear un LAB nuevo, buscar aquí si la capacidad (o algo muy
   cercano) ya fue validada.
2. Si ya existe: enlazar desde el `ROADMAP.md` de la nueva exploración en
   vez de repetir el experimento, salvo que la nueva exploración necesite
   validarlo bajo condiciones distintas.
3. Si no existe: crear el LAB, y al cerrarlo (decisión ADOPTAR/DESCARTAR/...)
   agregar la fila correspondiente aquí.
