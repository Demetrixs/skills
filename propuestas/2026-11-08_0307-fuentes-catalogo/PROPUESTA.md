# Propuesta: coherencia de fuentes al valorar un catálogo

Tipo: nueva, `comprobar-fuentes-catalogo`.
Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección y evidencia

Una fórmula correcta produce precios incorrectos si mezcla versiones, convierte definiciones ausentes en ceros o interpreta mal secciones e identidades de recursos. Cumple por hallazgos del Juez evitables con instrucciones; no se cuenta la revisión de un arreglo como un incidente nuevo.

- `C:\Conquer\NUEVO-PROYECTO\REVISION-CODEX-T289.md`, B01: «Las 47 sí existen en el itemtype preparado». La generación usaba el desplegado, asignando cero a piezas ausentes allí.
- Mismo archivo, B02: «El parser de precios no distingue secciones». Mezclaba una recomendación con las ventas.
- `C:\Conquer\NUEVO-PROYECTO\REVISION-CODEX-T292.md`, H04: «PEND usa IDs de origen». Dos IDs remapeados cobraban prima porque el algoritmo no cotejaba su origen pendiente.
- `C:\Conquer\NUEVO-PROYECTO\INFORME-T293.md`, apartado 3: «ahora mira objetivo y origen». Es la corrección declarada por el constructor.
- `C:\Conquer\NUEVO-PROYECTO\REVISION-CODEX-T293.md`, resultado H04: «0 discrepancias de score/estado/precio». El Juez confirmó el recálculo de las 272 filas; no se presenta el fallo histórico como vigente ni esa comprobación como aprobación de balance o despliegue.

## Diferencia respecto a lo existente

Las skills aprobadas no detallan el cruce entre catálogo objetivo, definiciones y recursos remapeados. `renombrado-estructurado` conserva sintaxis y rutas; `recursos-servibles` busca marcas en recursos web. Aquí se verifica qué datos permiten valorar cada pieza y cómo la identidad de origen afecta a la clasificación. No cambia ninguna skill aprobada ni otro borrador.

## Una prueba concreta en Forja

Una prueba A/B documental de un catálogo sintético, por lectura y cálculo manual en Forja; cotejar B01/B02 y H04 en las rutas anteriores. No ejecutar generadores, escribir CSV, usar clientes ni activar el borrador.

Caso común:

```text
Catálogo objetivo autorizado: piezas A y B.
INI: sección Normal contiene A y B; sección recommend contiene C.
Definiciones desplegadas: A=100 puntos; B ausente.
Definiciones preparadas del objetivo: A=100 puntos; B=900 puntos.
Recurso de B: ID final B procede de origen O; O está pendiente.
Regla sintética de prueba: precio = 10 + puntuación/100;
prima visual = 5 solo si confirmado. Sin redondeo necesario.
```

- A, sin el control: extraer todos los IDs, usar definiciones desplegadas con cero por ausencia y considerar confirmado B porque su ID final no está en pendientes. A incluye C, valora B como cero y le cobra prima; su precio de B es 15. La generación puede parecer completa aunque usa datos incompatibles.
- B, con el control como objeto de evaluación: usar solo Normal y el catálogo objetivo A/B; exigir las definiciones preparadas y resolver B a O. Resultado: dos piezas, A=11, B=19, B pendiente y sin prima, C fuera de ventas. Si se insiste en usar las definiciones desplegadas, B debe bloquear la generación completa por definición ausente, sin asignarle cero.

Éxito esperado: B obtiene dos ventas y distingue ausencia, cero real y recurso pendiente; A falla esos controles. El Juez registra su resultado observado. La prueba evalúa el criterio documental, no la fórmula real, el balance comercial ni el renderizado. Pendiente de evaluación independiente.
