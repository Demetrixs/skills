# Propuesta: conservar el plan de una recompensa parcial

Tipo: nueva, `conservar-plan-recompensa-parcial`.
Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección y evidencia

Los recibos de unidades entregadas no sustituyen el total comprometido. Cambiar identidades según la configuración puede duplicar; reconstruir el total desde recibos parciales puede perder lo restante. Cumple por hallazgos reproducidos del Juez. Las re-revisiones no se cuentan como incidentes independientes.

- `C:\Conquer\NUEVO-PROYECTO\REVISION-R178.md`, B1: «El mismo ID de concesión deja de tener la misma identidad de entrega». Tras entregar una unidad, perder el diario y configurar tres, el ensayo acabó con cuatro correos.
- Mismo archivo, B2: «Resolver de forma durable las concesiones empezadas». El cambio posterior de conexión cerraba una entrega de una de tres unidades.
- `C:\Conquer\NUEVO-PROYECTO\REVISION-R180.md`, B3: «reconstruye `Units = started`» y «considera completada esa cantidad reducida». El Juez reprodujo perder solo el plan después de entregar una de tres unidades; quedó una y la concesión cerrada.
- `C:\Conquer\NUEVO-PROYECTO\INFORME-T185.md`, La corrección: «Queda **pendiente** de que se restaure el plan o se revise»; Pruebas: «con la corrección pasan los 35».

R180 confirma el cierre de B1/B2 y descubre B3. T185 declara su corrección y prueba de sanidad contra la versión anterior; eso es evidencia del constructor, no aprobación independiente de T185. No se afirma aquí cuál es el estado actual del módulo ni se autoriza activarlo.

## Diferencia respecto a lo existente

`juez-revision` pide buscar pérdidas y duplicaciones, pero no define la relación entre plan, diario y recibos de una entrega reanudable. La propuesta de resultados de autenticación controla avances de login tras errores; no cubre identidad por unidad ni recuperación del total comprometido. Las demás propuestas tampoco cubren este contrato. Se propone una skill nueva de alcance específico.

## Una prueba concreta en Forja

Una prueba A/B documental de recuperación, sin instalar el módulo, borrar archivos ni activar el borrador. El Juez lee B3 de R180 y La corrección y Pruebas de T185, en las rutas anteriores, y recorre este caso sintético:

```text
Una concesión comprometió tres unidades del objeto ficticio OBJETO-A.
Se entregó una; su recibo permanente sigue intacto.
Se pierde el plan. El diario aún no marca la concesión completada.
Hay espacio para dos unidades más. La configuración actual dice tres.
Algoritmo presentado: contar recibos, reconstruir total=1 y marcar completada.
Después aparece una copia válida del plan original: total=3, mismo objeto.
```

- A, sin el control: comprobar solamente que el reintento no duplica objetos. El algoritmo pasa ese criterio y cierra con una de tres: pierde dos.
- B, con el control como objeto de evaluación: exigir el total comprometido además de no duplicar. Sin plan debe quedar pendiente, conservar un objeto y su recibo, y no crear un plan reducido ni usar la configuración como prueba del compromiso. Al recuperar el plan original, debe permitir entregar solo las dos unidades que faltan y cerrar con tres en total.

Éxito: B detecta la pérdida que A omite y conserva tanto el pendiente como la ausencia de duplicados. El Juez registra las dos fases y contrasta el mecanismo con R180/T185, distinguiendo revisión y afirmación del constructor. A representa un criterio insuficiente, no una predicción sobre cualquier agente sin la skill. Prueba documental diseñada; evaluación independiente pendiente. No demuestra ejecución del módulo ni durabilidad ante cortes eléctricos.
