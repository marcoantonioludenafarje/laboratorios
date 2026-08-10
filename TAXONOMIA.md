# Taxonomía y reglas operativas

Reglas fijas para toda carpeta bajo `ideas_negocio/`. Definidas y
corregidas dos veces el 9 ago 2026 tras encontrar inconsistencias reales:
primero nombres (`webar` vs `webar-lab`, `whatsapp_labs`, `social_medias`
con 4 exploraciones mezcladas), después estructura física (todo suelto en
la raíz, sin categoría, sin `CLAUDE.md` de workspace). Ver
[docs/historial/](./docs/historial/) para el detalle de cómo se llegó a
esto.

## 0. `ideas_negocio/` no es un repo

Es solo el contenedor local de repos independientes. Nunca `git init` a
ese nivel. Su `CLAUDE.md` (en la raíz del workspace, fuera de este repo)
es el punto de entrada — apunta aquí.

## 1. Nombres: kebab-case, carpeta = repo, siempre

- Sin guión bajo, nunca. `whatsapp_labs` → `whatsapp-integration`.
- El nombre de la carpeta (el último segmento de la ruta, no la ruta
  completa) y el nombre del repo en GitHub son **exactamente el mismo
  string**, sin excepción. (`webar` vivía como `webar-lab` en GitHub —
  corregido vía `gh repo rename`.)
- Sufijo `-labs` es opcional, úsalo si describe bien qué es
  (`agent-remote-labs`, `nfc-labs`) — no es obligatorio (`webar`,
  `laboratorios` no lo llevan).

## 2. Estructura física: categoría → exploración

```text
ideas_negocio/
├── CLAUDE.md
├── laboratorios/                 índice maestro — no es categoría, no es exploración
├── exploraciones-pendientes/     ver §3
│
├── retail-tech/
│   └── webar/
├── agent-tooling/
│   └── agent-remote-labs/
└── <categoria>/
    └── <exploracion>/            repo real
```

Una carpeta de categoría existe solo si ya contiene al menos un repo
real — no se crean categorías vacías por adelantado. Mover una carpeta
con `.git` adentro a otra categoría es seguro: un repo no depende de la
ruta de su carpeta padre, ni local ni en GitHub.

**Nota Windows**: si la carpeta está abierta en VS Code, un watcher activo
puede bloquear el `mv`/rename de esa carpeta (no bloquea copiar). Si pasa:
`Copy-Item -Recurse` a la ruta nueva, verificar `git status`/`git log` ahí,
luego borrar el original.

## 3. Antes de tener repo: centralizado en `exploraciones-pendientes/`

Una exploración que todavía no arrancó **no** vive dentro de una carpeta
de categoría — categorizar algo que ni siquiera empezó es prematuro. Vive
centralizada:

```text
exploraciones-pendientes/
└── <nombre-kebab-case>/
    └── EXPLORATION.md      ← el doc de propuesta (Contexto/Objetivo/Preguntas)
```

Un solo archivo, nombre fijo `EXPLORATION.md` (no `NOMBRE-EXPLORATION.md`
ni variantes) — así cualquier chat nuevo sabe exactamente qué abrir. Si
una carpeta tiene *varios* documentos de propuesta distintos mezclados
(pasó con `social_medias/`, 4 docs sueltos), es señal de que en realidad
son *varias* exploraciones — se separan, una carpeta cada una.

Repo real (`gh repo create`) nace recién cuando esa exploración
efectivamente arranca — no antes. En ese momento la carpeta **se mueve**
de `exploraciones-pendientes/<nombre>/` a `<categoria>/<nombre>/`.

## 4. Visibilidad: privado por defecto

Todo repo nuevo nace **privado**. Se pasa a público únicamente cuando esa
exploración específica necesita GitHub Pages (un link que se pueda abrir
directo desde un celular sin pedir acceso) — ver
[docs/conceptos-generales/github-pages.md](./docs/conceptos-generales/github-pages.md)
sobre por qué Pages no funciona con repos privados en el plan free.

Si no hay demo web (labs de terminal, de API, de investigación pura), no
hay razón para ser público. `agent-remote-labs` se corrigió a privado el
9 ago 2026 por esta regla — se había hecho público sin necesitarlo.

## 5. Cómo un chat nuevo se entera de todo esto

Dos capas, no una sola:

1. **`ideas_negocio/CLAUDE.md`** (raíz del workspace) — se carga si la
   sesión abre esa carpeta directamente. Si Claude Code también lo
   recoge al abrir una subcarpeta (buscando hacia arriba en el árbol) no
   está confirmado con certeza — de ahí la capa 2.
2. **El `CLAUDE.md` de cada exploración** repite el puntero como primera
   línea, explícito, por si la sesión arrancó ya dentro de esa carpeta y
   la capa 1 no aplicó por algún motivo:

   ```markdown
   > **Antes de cualquier otra cosa**: lee
   > `C:\repositorios\ideas_negocio\laboratorios\PLAYBOOK.md` y
   > `CATALOGO.md`. Esta exploración los sigue; no los repite aquí.
   ```

Ruta absoluta, no relativa. Ninguna de las dos capas es una garantía
dura — siguen siendo instrucciones que un agente debe decidir seguir —
pero juntas son el mecanismo más confiable disponible.

## 6. Cómo arrancar una exploración nueva en un chat

Con `exploraciones-pendientes/<nombre>/EXPLORATION.md` ya existente, el
primer mensaje al chat nuevo:

```text
Vamos a iniciar la exploración de exploraciones-pendientes/<nombre>/EXPLORATION.md.
Sigue laboratorios/PLAYBOOK.md. Primero: crea el repo (privado por
defecto) en <categoria>/<nombre>/, genera OBJECTIVE.md y ROADMAP.md a
partir de ese doc, y presenta el LAB 01 recomendado. No implementes nada
todavía.
```
