# Resumen: laboratorios en paralelo → fusión en un solo proyecto

> Escrito para llevar al chat de webar y decidir juntos el flujo de trabajo.
> Contexto: sesión sobre `agent-remote-labs`, 9 ago 2026.

## 0. La metodología ya existía: el Playbook

`Technology Exploration & Progressive Demo Playbook (1).md` (raíz de
`ideas_negocio/`) es la plantilla reutilizable detrás de esto: `ENTENDER →
EXPERIMENTAR → VALIDAR → INTEGRAR → CONSTRUIR`, máximo 3 labs por
tecnología, 3-4 demos integrales, terminando en `ARCHITECTURE-V1.md`. Tanto
`webar/CLAUDE.md` como `agent-remote-labs/CLAUDE.md` ya siguen esta
estructura casi al pie de la letra — lo de hoy fue resolver **cómo
ejecutarla con varios chats trabajando a la vez**, no cambiar la
metodología.

Pendiente de decidir con el chat de webar: dónde debería vivir este
playbook de forma permanente (¿su propio repo "plantilla", ya que se
reutiliza en cada idea nueva?).

## 1. El problema

`ideas_negocio/` contiene varias ideas independientes, cada una su propio
repo:

```text
webar/               ya existe — master, GitHub Pages: webar-lab
agent-remote-labs/   creado hoy — github.com/marcoantonioludenafarje/agent-remote-labs
nfc-labs/            próximo chat
```

Quieres trabajar varios experimentos en paralelo (uno por chat) sin (a)
terminar manejando un repo por cada tecnología, ni (b) que dos chats se
pisen editando la misma carpeta de trabajo a la vez.

## 2. Decisión: repo único por idea + git worktrees adentro

Cada idea sigue siendo **un solo repo git** — nunca uno por tecnología. El
paralelismo entre chats se resuelve *dentro* de cada repo con **git
worktrees**: carpetas físicas hermanas, cada una un checkout independiente
en su propio branch, todas compartiendo el mismo `.git` / historial /
remoto. Nada que sincronizar entre "repos" porque es uno solo.

```text
agent-remote-labs/                     worktree principal, branch: master
../agent-remote-labs-a-tmux/           worktree extra, branch: lab/a-tmux
../agent-remote-labs-b-claude-code/    worktree extra, branch: lab/b-claude-code
```

Detalle completo del mecanismo (comandos, ciclo de vida) en
[`agent-remote-labs/docs/conceptos/worktrees.md`](./agent-remote-labs/docs/conceptos/worktrees.md).

### Convención de branches dentro de cada repo

| Tipo | Branch | Depende de |
|---|---|---|
| Laboratorio conceptual (tecnología aislada) | `lab/<id>-<nombre>` | nada |
| Demo integral (combina 2+ labs) | `demo/<n>-<nombre>` | sus labs base, ya mergeados a `master` |

Regla: un demo integral solo abre su worktree **desde un `master`
actualizado**, después de que los labs de los que depende ya fueron
mergeados — igual que integrar código que ya aterrizó, no una foto vieja.

### Ciclo de vida de un worktree

```text
git worktree add ../<repo>-<lab> -b lab/<id>-<nombre>   (desde el worktree principal)
   ↓
trabajar el lab (branch propio, carpeta propia)
   ↓
merge a master (desde el worktree principal) + push
   ↓
git worktree remove ../<repo>-<lab>
```

## 3. Ya ejecutado hoy en `agent-remote-labs`

- Repo creado y pusheado: <https://github.com/marcoantonioludenafarje/agent-remote-labs>
- Estructura: `labs/{a-tmux,b-claude-code,c-ntfy,d-pwa,e-tailscale}`,
  `demos-integrales/{1-notify-me..4-multi-agent-control-center}`,
  `docs/conceptos/worktrees.md`
- Worktree activo: `agent-remote-labs-a-tmux`, branch `lab/a-tmux` — LAB A1
  (persistencia de sesiones tmux) pendiente de correr, falta confirmar
  tmux/WSL disponible en esta máquina.

## 4. Nivel superior: catálogo cruzado entre ideas

Cuando haya 2-3 labs publicados con demo online, tiene sentido un repo
`laboratorios` (índice) que enlace a los sitios de cada producto (webar,
agent-remote-labs, nfc-labs...), tageado por **tecnologías base** vs
**demos-integrales**, con link directo si hay demo online o descriptivo si
es local-only. Se acordó crearlo ahora, pero **todavía no se ejecutó** — se
priorizó terminar la estructura de `agent-remote-labs` primero. Sigue
pendiente.

## 5. Documentación de conceptos teóricos

Cada repo mantiene su propio `docs/conceptos/*.md` (no centralizado) — el
mismo espíritu que el artifact **"GitHub para WebAR Lab — Conceptos y
Buenas Prácticas"** que ya existe para la sesión de webar, pero ese todavía
**solo vive como Claude Artifact**, no está volcado a archivo. Pendiente:
¿lo guardamos como `webar/docs/conceptos/github-fundamentals.md` para que
quede versionado igual que `worktrees.md` en agent-remote-labs?

## 6. Preguntas abiertas para el chat de webar

1. ¿Adoptamos worktrees también en webar para las demos 03-07? Hoy webar
   corre en un solo branch (`master`) secuencial — funcionó porque hasta
   ahora un solo chat trabajaba ahí a la vez.
2. ¿Creamos ya el repo `laboratorios` (índice) o esperamos a tener más
   contenido publicado?
3. ¿Volcamos el artifact de conceptos de GitHub a
   `webar/docs/conceptos/github-fundamentals.md`?
4. ¿`nfc-labs` sigue exactamente el mismo patrón (repo propio + worktrees)
   cuando abras ese chat?
5. ¿Dónde vive el Playbook general de forma permanente?

## 7. Pendiente inmediato (chat de agent-remote-labs)

Confirmar tmux/WSL disponible y ejecutar LAB A1 en el worktree
`agent-remote-labs-a-tmux` (branch `lab/a-tmux`).
