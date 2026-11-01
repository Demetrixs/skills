# Propuesta: cubrir todas las opciones con la fecha de apertura

Tipo: nueva, `comprobar-fecha-todas-opciones-npc`.
Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección y evidencia

Cambiar bien la fecha no basta si la condición solo se ejecuta al mostrar el saludo. Cumple por un hallazgo del Juez evitable con una instrucción; la revisión del arreglo no es un segundo incidente.

- `C:\Conquer\NUEVO-PROYECTO\REVISION-R150.md`, hallazgo 6: «la condición está dentro de `case 0`» y «Las opciones de preguntas/respuestas y cobro no vuelven a comprobarla».
- Mismo apartado: el control global tiene «modo **1, solo registro**». No había evidencia de un bloqueo efectivo que compensase la omisión.
- `C:\Conquer\NUEVO-PROYECTO\INFORME-T158.md`, fila 6: «está antes del `switch`, así que vale para **todas** las opciones del NPC».
- `C:\Conquer\NUEVO-PROYECTO\REVISION-R158.md`, Extras de R150: «ScholarWise **APROBADO por lectura**» y «aplicada a todas las opciones».
- `C:\Conquer\NUEVO-PROYECTO\REVISION-R159.md`, fila ScholarWise: «no se reintrodujo el acceso previo por otras opciones».

El defecto está documentado como corregido por lectura en R158/R159. Se propone prevenir su repetición, sin afirmar que siga presente ni cambiar la decisión sobre otros eventos.

## Diferencia respecto a lo existente

La skill aprobada `juez-revision` contiene controles generales de servidor, pero no el análisis de entradas directas a opciones de un diálogo con apertura temporal. Las propuestas de paquetes y autenticación cubren otros contratos. La de identidad de prueba comprueba quién inicia una sesión, no qué opciones quedan protegidas por una fecha. No se modifica ninguna de ellas.

## Una prueba concreta en Forja

Una prueba A/B documental por lectura de R150, hallazgo 6, y R158, Extras de R150, en las rutas anteriores. El Juez no carga el borrador ni envía paquetes. Evalúa esta tabla sintética:

```text
Evento aún cerrado según su reloj autorizado; jugador normal.
Opción 0: si está cerrado, mostrar aviso y terminar; si no, abrir preguntas.
Opción 2: conceder progreso.
Opción 3: entregar premio.
Filtro global de opciones: solo registra, no rechaza.
Entrada recibida: opción 3 directamente, sin pedir antes la opción 0.
Excepción de prueba ya autorizada: GM puede recorrer el evento antes de abrir.
```

- A, sin el control: evaluar solo la opción 0. Devuelve el aviso correcto y da por validada la fecha; omite que la entrada directa a 3 entrega el premio.
- B, con el control como objeto de evaluación: recorrer la entrada directa y el modo del filtro. Debe señalar el premio indebido y exigir una condición común o equivalente que cubra también 2 y 3. Con esa cobertura, el jugador normal no progresa ni cobra antes de abrir; al abrir puede recorrer el flujo normal; la excepción GM autorizada sigue disponible.

Éxito: B detecta la vía omitida por A, cubre progreso y premio y conserva la excepción sin ampliar permisos. El Juez registra los resultados y distingue la comprobación documental de una prueba en juego. Prueba diseñada; evaluación independiente pendiente, sin declaración de éxito ejecutado ni activación del evento.
