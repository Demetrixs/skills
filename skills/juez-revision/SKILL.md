---
name: juez-revision
description: Cómo hacer (o encargar) una revisión de Juez independiente sobre código, documentos o síntesis. Úsala cuando haya que aprobar o devolver trabajo de otro agente.
---
# Juez independiente

## Reglas
- El Juez **nunca** es el agente que construyó. Si construyó Codex, juzga Claude, y al revés.
- **Solo lectura**: lee archivos y usa git de solo lectura. No arregla nada; señala.
- Cada afirmación del constructor se comprueba en la fuente (archivo:línea, URL). Lo no comprobado se dice.

## Lanzar a Claude como Juez en Forja
`Get-Content prompt.txt -Raw | claude -p --allowedTools "Read,Grep,Glob,Bash(git diff *),Bash(git log *),Bash(git show *),Bash(git -C *)" --output-format json`
(leer `.result`, `.total_cost_usd` y `.num_turns` del JSON).

## Formato de la entrega
1. **VEREDICTO:** APROBADO o DEVUELTO (DEVUELTO si queda algo grave o medio).
2. Hallazgos por gravedad (grave / medio / leve) con archivo:línea y por qué importa. Sin elogios.
3. Tabla de criterios del encargo: cumple / no cumple / sin evidencia.
4. Lo que solo puede comprobar una persona (p. ej. Verset en el juego).

## Qué buscar en código de servidor de juego
Pérdida o duplicación de objetos, dinero o CP; estados marcados antes de pagar; guardados en orden incorrecto (colecciones nulas al entrar); comandos GM al alcance de jugadores; valores fijos que debían ser configurables; secretos en código o documentos; cambios fuera del alcance.

## Rondas
- Código: las rondas necesarias hasta APROBADO.
- Investigación: como mucho **una** vuelta de revisión (decisión de Verset para ahorrar cuota).
