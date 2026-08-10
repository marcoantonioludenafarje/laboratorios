# Taxonomía y reglas operativas

Reglas fijas para toda carpeta bajo `ideas_negocio/`, definidas el 9 ago
2026 tras encontrar inconsistencias reales (`webar` vs `webar-lab`,
`whatsapp_labs`, `social_medias` con 4 exploraciones mezcladas). Ver
[docs/historial/](./docs/historial/) para el detalle de cómo se llegó a
esto.

## 1. Nombres: kebab-case, carpeta = repo, siempre

- Sin guión bajo, nunca. `whatsapp_labs` → `whatsapp-integration`.
- El nombre de la carpeta local y el nombre del repo en GitHub son
  **exactamente el mismo string**, sin excepción. (`webar` vivía como
  `webar-lab` en GitHub — corregido vía `gh repo rename`.)
- Sufijo `-labs` es opcional, úsalo si describe bien qué es
  (`agent-remote-labs`, `nfc-labs`) — no es obligatorio (`webar`,
  `laboratorios` no lo llevan).

## 2. Antes de tener repo: carpeta + `EXPLORATION.md`

Una exploración que todavía no arrancó vive como:

```text
<nombre-kebab-case>/
└── EXPLORATION.md      ← el doc de propuesta (Contexto/Objetivo/Preguntas)
```

Un solo archivo, nombre fijo `EXPLORATION.md` (no `NOMBRE-EXPLORATION.md`
ni variantes) — así cualquier chat nuevo sabe exactamente qué abrir. Si
una carpeta tiene *varios* documentos de propuesta distintos mezclados
(pasó con `social_medias/`, 4 docs sueltos), es señal de que en realidad
son *varias* exploraciones — se separan en su propia carpeta cada una,
antes de que cualquiera tenga repo.

Repo real (`gh repo create`) nace recién cuando esa exploración
efectivamente arranca — no antes. Una carpeta vacía o con solo un doc de
propuesta no es todavía una exploración activa.

## 3. Visibilidad: privado por defecto

Todo repo nuevo nace **privado**. Se pasa a público únicamente cuando esa
exploración específica necesita GitHub Pages (un link que se pueda abrir
directo desde un celular sin pedir acceso) — ver
[docs/conceptos-generales/github-pages.md](./docs/conceptos-generales/github-pages.md)
sobre por qué Pages no funciona con repos privados en el plan free.

Si no hay demo web (labs de terminal, de API, de investigación pura), no
hay razón para ser público. `agent-remote-labs` se corrigió a privado el
9 ago 2026 por esta regla — se había hecho público sin necesitarlo.

## 4. `CLAUDE.md` de cada exploración: la primera línea importa

Un chat nuevo en una exploración **no** carga automáticamente el
`CLAUDE.md` de otro repo — solo el de la carpeta donde arrancó. Para que
de verdad lea este Playbook y el catálogo, el `CLAUDE.md` de cada
exploración debe empezar, literal, con:

```markdown
> **Antes de cualquier otra cosa**: lee
> `C:\repositorios\ideas_negocio\laboratorios\PLAYBOOK.md` y
> `CATALOGO.md`. Esta exploración los sigue; no los repite aquí.
```

Ruta absoluta, no relativa — no depende de desde dónde se abrió la
sesión. Esto no es una garantía dura (sigue siendo una instrucción que un
agente debe decidir seguir), es simplemente el mecanismo más confiable
disponible.

## 5. Cómo arrancar una exploración nueva en un chat

Con la carpeta + `EXPLORATION.md` ya existentes, el primer mensaje al
chat nuevo:

```text
Vamos a iniciar la exploración de <carpeta>/EXPLORATION.md.
Sigue laboratorios/PLAYBOOK.md. Primero: crea el repo (privado por
defecto), genera OBJECTIVE.md y ROADMAP.md a partir de este doc, y
presenta el LAB 01 recomendado. No implementes nada todavía.
```
