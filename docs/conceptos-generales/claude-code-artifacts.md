# Claude Code Artifacts — páginas privadas publicadas por el propio agente

> Concepto general. Usado por primera vez en `webar` (9 ago 2026) para
> publicar una guía de conceptos de GitHub sin necesidad de un repo.

## Qué es

Una página (HTML o Markdown) que Claude Code puede publicar directamente
como URL en `claude.ai/code/artifact/...`, **privada por defecto** — solo
el usuario la ve hasta que decide compartirla desde el menú de la propia
página. No requiere repo, no requiere hosting propio, no tiene costo
adicional.

## Cuándo usarlo en vez de un repo/Pages

| Necesitas... | Usa |
|---|---|
| Código real que se sigue desarrollando (app, demo con lógica) | Repo + GitHub Pages |
| Una nota/guía/reporte de una sola vez, sin necesidad de build | Artifact |
| Privacidad real por defecto (nadie lo ve sin que tú compartas) | Artifact |
| Un link estable que se re-despliega con cada cambio (`git push`) | Repo + Pages |

Un Artifact es la opción correcta para: documentación de referencia,
reportes, mockups, y en general cualquier "página única" que no necesita
vivir en control de versiones compartido con el resto del proyecto.

## Restricciones técnicas

- **Autocontenido**: un solo archivo `.html` o `.md`, CSS/JS inline, sin
  imports de módulos externos, sin CDNs (Content-Security-Policy estricta
  bloquea peticiones salientes). Esto lo hace **no apto** para una app real
  con build de Vite/dependencias — para eso, repo + Pages.
- **Ambos temas**: debe verse bien en modo claro y oscuro sin asumir cuál
  usará quien lo abra.
- **Tamaño**: 16 MB máximo por página, contando cualquier asset embebido.

## Cómo se actualiza

Publicar de nuevo con la **misma ruta de archivo** en la misma conversación
re-despliega a la misma URL. Desde otra conversación, hay que pasar la URL
existente explícitamente para actualizar en el mismo lugar — si no,
siempre nace una URL nueva.

## Relación con el resto de este índice

Este mismo repo (`laboratorios`) podría, en teoría, existir como un
Artifact en vez de un repo con GitHub Pages — pero se descartó esa opción a
propósito: el índice necesita **historial versionado y editable desde
cualquier chat/exploración**, algo que un Artifact (ligado a la
conversación donde se publicó) no ofrece igual de bien.
