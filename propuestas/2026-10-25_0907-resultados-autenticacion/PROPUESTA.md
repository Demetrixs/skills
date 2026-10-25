# Propuesta: seguir los resultados de autenticación hasta la transición

Tipo: nueva, `comprobar-resultados-autenticacion`.
Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección y evidencia

El arreglo añadió resultados de error, pero los llamadores seguían descartándolos y avanzaban. Cumple por un hallazgo del Juez. La revisión inicial y su re-revisión son antecedentes del mismo arreglo, no incidentes independientes.

- `C:\Conquer\NUEVO-PROYECTO\REVISION-HOY-CODEX.md:128`: «El llamador sigue ignorando los resultados (R2)».
- Mismo archivo, línea 146: «el llamador lo ignora: activa `CreateCharacter` y envía NEW_ROLE igualmente».
- Mismo archivo, línea 148: «su resultado también se descarta y se continúa con `AcceptLogin` y `LoadMap`».
- `C:\Conquer\NUEVO-PROYECTO\INFORME-T50.md`, apartado R2: «el personaje queda guardado» y «Los casos de concurrencia no se han reproducido». El constructor documenta la corrección y su límite de pruebas; no se certifica aquí su ejecución.

## Diferencia respecto a lo existente

`juez-revision` menciona estados marcados antes de pagar y guardados incorrectos, pero no concreta el seguimiento de resultados desde una operación de autenticación hasta todos sus llamadores. Esta instrucción se aplica al constructor que cambia ese contrato. Las propuestas previas sobre campos binarios, identidad de prueba y renombrados no cubren este flujo. No sustituye la revisión independiente.

## Una prueba concreta en Forja

Prueba A/B documental de una tabla de transiciones, por lectura y sin activar el borrador. No requiere servicios, escrituras, cuentas ni valores de autorizaciones. El Juez coteja R2 de `REVISION-HOY-CODEX.md:142-150` y el apartado R2 de `INFORME-T50.md` con este caso sintético:

```text
AbrirCreacion:
  resultado = ConservarAutorizacion()
  ActivarCreacion()

FinalizarCreacion:
  GuardarPersonaje()
  resultado = ConsumirAutorizacion()
  EntrarAlMundo()

Fila 1: ConservarAutorizacion devuelve false.
Fila 2: GuardarPersonaje termina; ConsumirAutorizacion devuelve DbError.
```

- A, sin el control: comprobar que las operaciones devuelven resultados y registran errores. Acepta el cambio aunque ambos resultados se descarten.
- B, con el control: recorrer las dos filas hasta la acción siguiente. Debe rechazar ActivarCreacion en la fila 1 y la entrada incondicional en la fila 2. En la segunda debe mantener el personaje guardado y proponer una recuperación acotada sin crearlo otra vez ni declarar consumida la autorización.

Éxito: B identifica ambos avances indebidos y conserva el estado ya persistido que A omite. El Juez registra lo observado. Evaluación independiente pendiente; el caso demuestra el control documental del flujo, no una inyección de fallos ni concurrencia real.
