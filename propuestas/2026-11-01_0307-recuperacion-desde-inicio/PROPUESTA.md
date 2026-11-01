# Propuesta: proteger la recuperación desde el inicio

Tipo: nueva, `proteger-recuperacion-desde-inicio`.
Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección y evidencia

La vuelta atrás puede existir y aun así quedar fuera del fallo que debe resolver. El mismo tropiezo aparece en operaciones distintas: despliegue, cambio de zona e interruptor web. Cumple tanto por repetición como por hallazgos del Juez evitables con una instrucción.

- `C:\Conquer\NUEVO-PROYECTO\REVISION-R158.md`, hallazgo sobre despliegue: «el `try/catch` solo rodea `EncenderJuego`» y «Las copias posteriores al apagado quedan fuera».
- `C:\Conquer\NUEVO-PROYECTO\REVISION-R175.md`, hallazgo 1: «ApagarTodo ocurre antes del try». El fallo de apagado parcial tampoco alcanza la recuperación.
- `C:\Conquer\NUEVO-PROYECTO\REVISION-R177.md`, Bloqueo: «salida 1, configuración queda en portada, no se restaura prereg». El Juez reprodujo PHP ausente sobre una copia temporal.
- `C:\Conquer\NUEVO-PROYECTO\REVISION-R127.md`, hallazgo 1: «Preparar el registro de recuperación antes de cambiar y actualizarlo por paso». La vuelta exigía un resultado escrito al final.
- `C:\Conquer\NUEVO-PROYECTO\REVISION-R179.md`, revisión del interruptor: «try desde antes de la primera escritura» y «finally restaura y compara bytes si no terminó la validación».

R179 documenta el cierre del caso del interruptor; no se presenta como un defecto vigente. Tampoco se convierte la promesa del constructor de recuperar cualquier interrupción en una garantía frente a caída del proceso o del equipo.

## Diferencia respecto a lo existente

`forja-powershell` trata codificación y ejecución; `montar-source-conquer-forja`, el montaje inicial; `juez-revision`, la revisión general. Ninguna concreta el tramo protegido de una operación y la recuperación de sus estados parciales. La propuesta de renombrado valida estructura y rutas. La de resultados de autenticación sigue transiciones de login, sin cubrir estos guiones. No se modifica ninguna de ellas.

## Una prueba concreta en Forja

Una prueba A/B documental por lectura, sin activar el borrador ni ejecutar el interruptor. El Juez lee Bloqueo de R177 y el apartado del interruptor en R179, ambos en las rutas anteriores, y evalúa esta traza sintética:

```text
Estado inicial: archivo de configuración con valor prereg; copia válida disponible.
Paso 1: escribir portada.
Paso 2: ejecutar el validador; lanza una excepción porque falta su herramienta.
Paso 3: si la lista de fallos contiene errores, restaurar la copia.
No hay manejador de excepciones alrededor de los pasos 1 y 2.
```

- A, sin el control: comprobar que hay copia y un paso de restauración ante errores. Ese criterio acepta el guion, pero la excepción del paso 2 impide llegar al 3; queda portada.
- B, con el control como objeto de evaluación: seguir la excepción desde la primera escritura. Debe detectar el salto, exigir protección hasta terminar la validación y describir la salida correcta: error original, valor prereg restaurado y bytes cotejados; si falla restaurar, recuperación no comprobada. No debe prometer recuperación automática ante una terminación forzada.

Éxito: B detecta el fallo que A omite y distingue recuperación comprobada de intento de recuperación. R177 y R179 permiten contrastar fallo y cierre históricos por lectura. El Juez registra el resultado observado de A y B; la prueba acredita el control documental, no ejecución real ni conducta de un agente. Evaluación independiente pendiente; no se declara superada.
