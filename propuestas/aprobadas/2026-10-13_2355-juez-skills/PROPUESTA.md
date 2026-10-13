# Propuesta: revisión de una versión exacta de skill

- Tipo: mejora de `skills/juez-revision/SKILL.md`; se copia la skill aprobada y se añade el caso de propuestas de skills.
- Autor: Bibliotecario (Codex), 13/10/2026.
- Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección
Una revisión general no basta para aprobar una skill: hay que revisar todos sus archivos, demostrar la lección con una prueba controlada y vincular el veredicto al contenido exacto. De otro modo, una modificación posterior o un auxiliar sin revisar podría viajar con una aprobación antigua.

La skill vigente exige comprobar afirmaciones y revisar en solo lectura, pero no concreta estos controles para skills. Se conservan esas reglas y se añade el procedimiento específico. Se corrige también la línea de rondas de código sin límite para respetar el máximo de tres vueltas de la constitución; después decide el fundador.

## Evidencia local
Candidata por hallazgo del Juez evitable con instrucciones, sin exigir dos incidentes. Fragmentos del último `agent_message` de cada archivo JSONL:

1. `C:\Conquer\_pruebas\codex-tareas\T9-juez-constitucion-skills\run8.jsonl`, veredicto DEVUELTO: «Tampoco vincula la aprobación a una versión concreta.»
2. Mismo archivo, arreglo 5: «Exigir una prueba local comprobable de la lección aprendida antes de activarla».
3. Mismo archivo, arreglo 3: «Exigir que otro agente revise instrucciones, programas, archivos y posibles órdenes maliciosas.»
4. `C:\Conquer\_pruebas\codex-tareas\T9-juez-constitucion-skills\run2.jsonl`, veredicto APROBADO, punto 4: «Solo reparte la versión exacta aprobada; cualquier cambio exige revisión nueva».
5. Mismo archivo, mejora opcional: «Aclarar que la prueba del borrador se realiza de forma controlada, sin cargarlo como skill utilizable.»

La v2 documental fue aprobada; eso no aprueba este borrador. Las huellas por archivo son la forma propuesta de concretar el control de versión, no una herramienta exigida por la evidencia.

## Una prueba concreta para el Juez en Forja
Prueba A/B de revisión de un auxiliar cambiado después de aprobar, sin red, servidores ni instalación. El Juez prepara un caso ficticio en memoria; no necesita escribir archivos ni cargar el borrador como skill activa.

Caso común: una propuesta ficticia trae SKILL.md y un auxiliar `comprobar.ps1`. SKILL.md conserva su contenido y la etiqueta v1. El auxiliar aprobado contenía `Write-Output 'OK'`; el auxiliar presentado para reparto contiene `Write-Output 'CAMBIADO'`. La revisión anterior solo dejó «APROBADO v1» y no registró huellas. La prueba funcional previa solo cubría el auxiliar anterior.

A: revisar este caso con la skill vigente como criterio. Registrar si sus instrucciones permiten demostrar qué contenido del auxiliar quedó aprobado: la etiqueta v1 y el veredicto no bastan, y la skill no exige guardar esa identidad. Este es el fallo del control que se quiere evitar; no se presume que un agente concreto vaya a aprobarlo.

B: revisar el mismo caso contra las instrucciones propuestas, tratándolas como objeto de evaluación. Debe exigir la identidad de ambos archivos, marcar que falta evidencia para el auxiliar cambiado y devolverlo para nueva revisión; no debe instalarlo ni ejecutarlo.

Comprobación auxiliar reproducible en PowerShell, solo en memoria:

```powershell
$sha = [Security.Cryptography.SHA256]::Create()
try {
    $anterior = [BitConverter]::ToString($sha.ComputeHash([Text.Encoding]::UTF8.GetBytes("Write-Output 'OK'")))
    $actual = [BitConverter]::ToString($sha.ComputeHash([Text.Encoding]::UTF8.GetBytes("Write-Output 'CAMBIADO'")))
    if ($anterior -eq $actual) { throw 'La prueba no distingue los contenidos' }
    'Contenido cambiado: requiere nueva revision'
} finally { $sha.Dispose() }
```

Criterio de éxito: B detecta que la aprobación anterior no cubre el auxiliar actual y exige nueva revisión de todos los archivos y de la prueba afectada. A deja documentada la ausencia del control explícito. Si el Juez no observa una mejora en la evaluación A/B, devuelve la propuesta. El cálculo de huellas por sí solo no demuestra mejora de conducta.

Estado de esta prueba: diseñada, pendiente de ejecución y evaluación independiente por el Juez. El Bibliotecario no aprueba su propio trabajo.

## Vuelta 2

Arreglos del veredicto DEVUELTO de la vuelta 1, aplicados punto por punto:

1. **Comando, huellas y prueba:** se conserva el lanzamiento del Juez en solo lectura. El Bibliotecario u otro operador con autorización previa calcula las huellas y entrega comando, salida y archivos exactos; el Juez coteja la evidencia por lectura y no aprueba si no puede vincularla al contenido revisado. La prueba A/B documental se evalúa leyendo, sin escribir ni ejecutar. Cualquier ejecución necesaria corresponde a un operador previamente autorizado y se documenta para el Juez; la skill no concede esa autorización. Se distingue el control documental de una prueba de conducta real.
2. **BLOQUEADO:** añadido al formato, con el impedimento que lo justifica y la decisión de Verset; no equivale a aprobación ni concede permisos.
3. **Rondas:** el máximo de tres vueltas cubre código, documentos, síntesis y propuestas de skills. Se conserva la excepción de una vuelta para investigación, incluidos sus documentos y síntesis.
4. **Descripción:** recuperadas las expresiones «hacer o encargar» y «aprobar o devolver», conservando el alcance de revisión independiente.
5. **Nueva presentación:** borrador corregido para revisión independiente, vuelta 2. No se instala, reparte ni aprueba por el Bibliotecario.

Comprobación auxiliar ejecutada por el Bibliotecario en Forja, solo en memoria, con el bloque PowerShell de esta propuesta. Resultado observado: `Contenido cambiado: requiere nueva revision`. Esta comprobación solo distingue los contenidos; la evaluación A/B independiente por el Juez sigue pendiente.

Huella nueva del archivo que se propone repartir, calculada después de los arreglos con `Get-FileHash -LiteralPath 'propuestas\2026-10-13_2355-juez-skills\SKILL.md' -Algorithm SHA256`:

- `SKILL.md`: `707762e98524e0f7e066f4de625e8cfbb8608dc5ca7aee61238ba2b0ea496356`

Esta huella es aportada por el Bibliotecario para su cotejo por el Juez; no constituye aprobación.