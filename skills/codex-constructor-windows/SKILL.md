---
name: codex-constructor-windows
description: Cómo encargar trabajo a Codex como constructor (o auditor) en Forja y recoger el resultado. Úsala cuando el orquestador lance codex exec en Windows.
---
# Codex como constructor en Forja

## Lanzar
- Solo lectura (auditar, investigar en disco): desde `C:\Conquer`  
  `Get-Content prompt.txt -Raw | codex exec --json --skip-git-repo-check --sandbox read-only - 2> run.err | Set-Content run8.jsonl -Encoding UTF8`
- Escribir código: desde la carpeta del repo, `--sandbox workspace-write` (solo puede escribir dentro de esa carpeta).
- Guarda prompt, salida y errores en `C:\Conquer\_pruebas\codex-tareas\T<n>-<nombre>\` (evidencia).
- Leer el resultado: script que recorra el JSONL y saque el último `agent_message` y `turn.completed.usage` (tokens).

## Limitaciones conocidas
- En Windows, el sandbox **no puede escribir en `.git`**: Codex no hace commit. Commitea el orquestador después, con autor «Puente Forja».
- Bajo una tarea programada **S4U**, el sandbox falla («timed out connecting runner pipe-in»): usa sesión interactiva.
- Un mismo hilo de Codex solo admite **un escritor**; no lances dos sobre el mismo hilo.
- Sin red dentro del sandbox: no podrá descargar nada (es lo deseado).

## Cómo escribir el encargo
1. Rol y jefe («Eres Codex, CONSTRUCTOR… tu jefe es Claude»).
2. **Prohibiciones explícitas:** fuera de la carpeta, commits, ejecutar servidor/cliente, MySQL, red, contraseñas, descargas.
3. Contexto breve y la tarea numerada, con archivo:línea si se conoce.
4. **Entrega:** compilar (0 errores o error exacto), documento de cambios en español sencillo con cómo probarlo, respuesta final corta (archivos, compilación, riesgos).
5. Si el mismo error se repite 3 veces: parar y explicar.

## Después
- El orquestador comprueba **en persona** el hallazgo o arreglo más importante (leer las líneas) y la compilación.
- Revisión SIEMPRE por otro agente (ver skill `juez-revision`). Quien construye no se juzga.
