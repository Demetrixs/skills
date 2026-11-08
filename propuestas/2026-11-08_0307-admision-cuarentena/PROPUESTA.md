# Propuesta: admisión obligatoria ante diarios ilegibles

Tipo: nueva, `comprobar-admision-cuarentena`.
Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección y evidencia

Una cuarentena puede existir y aun así ser evitable si depende de un paso que el cliente no necesita enviar, o si un fallo de lectura se transforma en ausencia de afectados. Cumple por hallazgos del Juez; las sucesivas devoluciones no son dos incidentes independientes.

- `C:\Conquer\NUEVO-PROYECTO\REVISION-CODEX-T292.md`, H03: «No equivale a una condición obligatoria de admisión del núcleo». Un gestor capturaba la excepción del módulo sin imponer desconexión.
- `C:\Conquer\NUEVO-PROYECTO\INFORME-T293.md`, H03: «dentro del mismo handler». El constructor usó la sincronía para justificar el cierre del hueco; la revisión posterior distingue esa propiedad de la obligación de ejecutar el handler.
- `C:\Conquer\NUEVO-PROYECTO\REVISION-CODEX-T293.md`, N04: «no obliga al cliente a enviarlo». El Juez trazó el filtro de paquetes hasta la venta y constató que se podía omitir CompleteLogin.
- Mismo N04: «no pone cuarentena ni expulsa». Una excepción al consultar pendientes podía salir antes del bloque de expulsión; otra captura podía devolver una lista parcial o vacía.
- `C:\Conquer\NUEVO-PROYECTO\INFORME-T294.md`, Estado: «No hay corrección implementada ni despliegue aprobado». El hallazgo sigue abierto según esa entrega.

## Diferencia respecto a lo existente

`juez-revision` contiene controles generales. `fecha-todas-opciones` comprueba apertura temporal de un NPC; `resultados-autenticacion` comprueba resultados de conservación y consumo de autorizaciones. Esta candidata cubre una puerta de admisión del servidor y la pérdida de verificabilidad durante sesiones activas. No modifica esas propuestas ni redefine roles.

## Una prueba concreta en Forja

Una prueba A/B documental de dos trazas del mismo control de admisión, cotejadas con N04 y H03 en las rutas anteriores. Sin paquetes, servicios, escrituras ni activación del borrador.

Caso sintético: sesión de prueba sin privilegios excepcionales. CargarMapa habilita la marca LoginFull; VerificarDiarios vive en el paquete separado FinalizarEntrada. El filtro permite Venta si LoginFull está activo. El barrido llama EnumerarPendientes antes de su try; el gestor exterior captura errores y solo los registra.

Traza 1: existe diario ilegible; CargarMapa, omitir FinalizarEntrada, solicitar Venta. Traza 2: sesión admitida previamente; el directorio pasa a ser ilegible, EnumerarPendientes lanza, el gestor registra y llega una Venta.

- A, sin el control: verificar únicamente que FinalizarEntrada es síncrono y que el caso normal de diario ilegible desconecta. Ese criterio deja pasar ambas trazas: la primera no ejecuta el control y la segunda solo registra el error.
- B, con el control como objeto de evaluación: exigir admisión verificada antes de Venta y tratar la imposibilidad de verificar como estado bloqueado según la política del caso. Rechazar ambas trazas como fallos del diseño; exigir que la primera venta espere la verificación y que la segunda no continúe al fallar la enumeración.

Éxito esperado: B identifica las dos rutas abiertas y no confunde handler síncrono con paso obligatorio ni error con cero afectados. El Juez registra lo observado. Es una prueba del criterio documental, no una implementación ni una orden de mantenimiento; la conducta real queda pendiente.
