# Propuesta: revisar los recursos servibles al retirar marcas

Tipo: nueva, `comprobar-marcas-recursos-web`.
Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección y evidencia

La búsqueda textual y la revisión de enlaces dejaron pasar marcas incrustadas en imágenes. También quedó un logo sin referencias dentro de la raíz servida. Cumple por hallazgo del Juez; T55 y T57 son revisiones del mismo defecto, no dos incidentes independientes.

- `C:\Conquer\NUEVO-PROYECTO\REVISION-T55-CODEX.md:13`: «La búsqueda de nombres en PHP no detecta texto incrustado en imágenes».
- `C:\Conquer\NUEVO-PROYECTO\REVISION-T57-CODEX.md:15`: «Permanece como recurso de la raíz servida, accesible por su ruta». La misma línea distingue el favicon corregido del logo pendiente.
- `C:\Conquer\NUEVO-PROYECTO\REVISION-T58-CODEX.md:13`: «Se inspeccionaron los seis». El cierre incluye los PNG y los tamaños internos del icono.

Es un defecto histórico corregido según T58; no se afirma que continúe.

## Diferencia respecto a lo existente

Las skills aprobadas no detallan la inspección visual del inventario servible. La propuesta `2026-10-18_0907-renombrado-estructurado` comprueba claves de configuración y rutas de lanzadores; no cubre marcas dibujadas ni recursos web sin enlaces. No se modifica esa propuesta ni ninguna skill aprobada.

## Una prueba concreta en Forja

Prueba A/B documental por lectura de `REVISION-T55-CODEX.md:11-13`, `REVISION-T57-CODEX.md:9-17` y `REVISION-T58-CODEX.md:11-15`. El Juez trata este borrador como objeto de revisión, sin activarlo. No hace peticiones ni arranca la web.

Caso común: la entrega T57 tiene el favicon corregido; game-logo.png conserva la marca previa, no tiene referencias en las páginas y sigue dentro de la raíz servida.

- A, sin el control: evaluar solo el favicon y las referencias activas. Ese criterio da por terminada la retirada y omite el logo.
- B, con el control: incluir recursos sin referencias y la inspección visual registrada por el Juez. Debe señalar el logo como pendiente y distinguirlo del favicon corregido. Contrastar con T58 para identificar su cierre posterior.

Éxito: B detecta el recurso accesible que A omite y no confunde T57 con T58. Registrar resultado observado y rutas leídas. Demuestra cobertura documental, no comportamiento de un agente ni una prueba HTTP. Evaluación independiente pendiente; no se declara superada.
