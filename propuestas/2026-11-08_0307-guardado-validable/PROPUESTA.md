# Propuesta: confirmar guardados aceptados por el cargador

Tipo: nueva, `comprobar-guardado-inventario`.
Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección y evidencia

Volver del guardado sin excepción y encontrar un UID al releer son controles insuficientes si el guardado puede fallar en silencio o el lector acepta archivos que el juego rechaza. Cumple por hallazgos del Juez evitables con instrucciones; no se cuentan las revisiones sucesivas como incidentes independientes.

- `C:\Conquer\NUEVO-PROYECTO\REVISION-CODEX-T292.md`, H01: «Esas rutas vuelven normalmente al llamador». La cadena de guardado podía conservar el archivo previo sin lanzar y permitir limpiar la cola.
- `C:\Conquer\NUEVO-PROYECTO\INFORME-T293.md`, apartado 1: «mismo parser que `ValidateItemsFile`». Es una afirmación del constructor, contradicha por la revisión siguiente.
- `C:\Conquer\NUEVO-PROYECTO\REVISION-CODEX-T293.md`, N03: «DurableUids devuelve los UIDs aunque ese resto esté truncado o sea basura». El Juez reconstruyó en memoria un objeto de 152 bytes con un byte residual; el lector parcial lo aceptaba y el validador completo lo rechazaba.
- Mismo N03: «Evitar validar una lectura y confirmar otra distinta».
- `C:\Conquer\NUEVO-PROYECTO\INFORME-T294.md`, Estado: «Los cuatro hallazgos de T293 siguen abiertos». La tarea se detuvo para proponer simplificación; no se presenta esta propuesta como una corrección aplicada.

## Diferencia respecto a lo existente

`juez-revision` pide buscar pérdidas y guardados incorrectos, sin concretar la equivalencia entre lector de confirmación y cargador. La propuesta `resultados-autenticacion` sigue resultados de login; `campos-paquetes` trata posiciones y capacidad de campos de red; `plan-recompensa-parcial` conserva el compromiso de una concesión. Aquí se verifica el contrato completo del archivo usado como prueba de un guardado. No se modifica ninguna skill ni otro borrador.

## Una prueba concreta en Forja

Una prueba A/B documental por lectura de H01 y N03 en las rutas anteriores y cálculo de tamaños. No ejecutar el juego ni activar el borrador.

Caso sintético único: formato de prueba con contador inicial de 4 bytes, un registro de objeto de 152 bytes y contador final obligatorio de 4 bytes que vale cero. No hay depósitos ni otras entradas. La confirmación exige archivo íntegro y presencia del objeto esperado.

Se ofrecen dos instantáneas del mismo caso: V tiene 160 bytes y todos sus contadores correctos; T tiene el mismo contador inicial y objeto, pero solo un byte tras el registro, total 157. El respaldo anterior es válido y no contiene el objeto. No son archivos de personajes reales ni una especificación universal del juego.

- A, sin el control: aceptar la presencia del UID tras leer contador y objeto, ignorando el resto. A confirma V y T; con T puede cerrar la obligación pese a que el cargador rechazaría el archivo y el respaldo no tiene el objeto.
- B, con el control propuesto como objeto de evaluación: exigir la validación completa de esa misma instantánea antes de consultar el UID. B confirma V y rechaza T por faltar tres bytes del contador final. Para T conserva el pendiente y no emite confirmación definitiva.

Éxito esperado: B detecta la confirmación falsa que A permite y conserva la aceptación de V. El Juez debe registrar su resultado observado. Esta prueba acredita el criterio documental; no ejecuta el parser real ni demuestra resistencia a cortes. Pendiente de evaluación independiente.
