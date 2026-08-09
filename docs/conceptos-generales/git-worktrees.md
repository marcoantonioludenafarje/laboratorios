# Git worktrees — trabajar varios chats en paralelo dentro del mismo repo

> Concepto general, no ligado a una exploración específica. Primera vez
> documentado a partir de `agent-remote-labs` (9 ago 2026).

## El problema que resuelven

Cada exploración es **un solo repo** (nunca uno por tecnología — ver
[PLAYBOOK.md](../../PLAYBOOK.md) y el índice en
[README.md](../../README.md)). Pero un repo git normal tiene **una** carpeta
de trabajo ligada a **un** branch a la vez. Si dos chats de Claude Code
trabajan en la misma carpeta al mismo tiempo:

- Cambiar de branch en uno mueve el suelo bajo los pies del otro — archivos
  sin commitear de un branch desaparecen (o entran en conflicto) al hacer
  `checkout` a otro.
- No se pueden correr dos servidores de desarrollo (`npm run dev`, etc.) al
  mismo tiempo desde la misma carpeta sin pisarse puertos y procesos.

La alternativa ingenua — un repo por laboratorio — evita el choque pero
multiplica remotos, historiales y configuración a mantener sincronizada.
Rompería además la regla de "un repo por exploración".

## Qué es un worktree

Un **worktree** es una carpeta de trabajo adicional, vinculada al mismo
`.git` de un repo ya existente, pero con su propio branch activo:

```text
<exploracion>/                       worktree principal — branch: master
../<exploracion>-<lab>/              worktree extra — branch: lab/<id>-<nombre>
../<exploracion>-<otro-lab>/         worktree extra — branch: lab/<id>-<nombre>
```

Todas comparten: el mismo historial de commits, los mismos branches
(visibles y creables desde cualquier worktree), el mismo remoto en GitHub.

Ninguna comparte: el estado del working directory (archivos editados sin
commitear), el branch actualmente activo, procesos corriendo en esa carpeta
(dev servers, tmux, etc.).

Es decir: **un repo, N carpetas físicas**, no N repos.

## Comandos base

```bash
# crear un worktree nuevo + su branch, desde el worktree principal
git worktree add ../<exploracion>-<lab> -b lab/<id>-<nombre>

# listar worktrees activos
git worktree list

# terminar un lab: mergear su branch en el principal
cd ../<exploracion>            # worktree principal, en master
git merge lab/<id>-<nombre>
git push

# borrar la carpeta extra una vez mergeado (el branch queda en el historial)
git worktree remove ../<exploracion>-<lab>
```

## Convención de branches dentro de cada exploración

| Tipo | Branch | Depende de |
|---|---|---|
| Laboratorio (tecnología aislada) | `lab/<id>-<nombre>` | nada |
| Demo integral (combina 2+ labs) | `demo/<n>-<nombre>` | sus labs base, ya mergeados a `master` |

Regla: un demo integral solo abre su worktree **desde un `master`
actualizado**, después de que los labs de los que depende ya fueron
mergeados — integrar código que ya aterrizó, no una foto vieja.

## Cuándo usarlo

Solo cuando **de verdad** hay dos chats trabajando la misma exploración al
mismo tiempo. Una exploración secuencial (un chat a la vez, como `webar`
hasta ahora) no necesita worktrees — el mecanismo está documentado aquí
para adoptarlo el día que sí haga falta, sin tener que re-decidirlo desde
cero en cada exploración nueva.

## Reflexión

Un worktree no reemplaza a un branch — es una forma de tener varios
branches **abiertos en el filesystem al mismo tiempo**. Resuelve
específicamente la colisión entre chats concurrentes *dentro de un mismo
repo*; no resuelve cómo catalogar o enlazar laboratorios que viven en
**repos distintos** (webar, agent-remote-labs, nfc-labs...) — eso es el
trabajo del [índice maestro](../../README.md) y el
[catálogo de reutilización](../../CATALOGO.md).
