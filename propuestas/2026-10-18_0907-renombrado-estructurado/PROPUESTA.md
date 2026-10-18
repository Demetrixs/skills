# Propuesta: comprobar estructura y rutas tras renombrar

Tipo: **nueva**, `validar-renombrado-estructurado`.
Estado: borrador del Bibliotecario, pendiente del Juez; no instalar ni repartir.

## Lección y umbral

El nombre nuevo puede estar presente y aun así quedar fuera de la clave que consume el programa, o dentro de una ruta rota. La búsqueda textual y la compilación no sustituyen la comprobación del consumidor. Cumple el umbral por hallazgos del Juez en T17 y T18.

## Evidencia local depurada

- `C:\Conquer\_pruebas\codex-tareas\T17\VEREDICTO-GEMINI.md:10`: «INI mal formateado en `Login.cfg` (L29-30)». El Juez describe una clave que conservó parte del nombre antiguo y el nombre nuevo en una línea sin clave. Se omite el ejemplo completo porque contiene campos ajenos a esta lección.
- `C:\Conquer\_pruebas\codex-tareas\T18\VEREDICTO-GEMINI.md:39`: «Falta la barra invertida entre `src` y `reparar`». La ruta del lanzador quedó concatenada y su destino no se encontraba.

No se presupone que estos defectos sigan presentes: se propone prevenir su repetición.

## Diferencia respecto a lo existente

`forja-powershell` cubre codificación, comillas y ejecución en Windows, pero no valida los consumidores de un renombrado. `montar-source-conquer-forja` cubre el montaje; `juez-revision` exige cotejar afirmaciones. Ninguna concreta este control de claves y destinos. La propuesta archivada de revisión de skills trata versiones y huellas, no renombrados. Por eso se propone una skill específica nueva y no copiar una skill general sin relación directa con el trabajo.

## Una prueba concreta para el Juez en Forja

**Una prueba A/B documental de un renombrado ficticio**, realizable por lectura, sin escribir archivos ni ejecutar lanzadores. No cargar el borrador como skill activa.

Caso común, íntegramente sintético:

```text
Formato del lector: sección [Juego] y una línea Nombre=valor.
No admite líneas de datos sin signo igual.

Configuración entregada:
[Juego]
Nombre=Anterior
Nuevo

Destino entregado por el lanzador: C:\CASO\Nuevo\srcreparar.ps1
Único destino del inventario ficticio: C:\CASO\Nuevo\src\reparar.ps1
Informe entregado: nombre Nuevo encontrado; compilación correcta.
```

El inventario es parte del caso; no se consulta ni crea esa ruta en disco.

- **A, sin el control propuesto:** comprobar solo que configuración y lanzador contienen `Nuevo` y que el informe declara compilación correcta. Los dos textos pasan ese criterio, aunque el lector conserva `Anterior` y el destino no coincide. Ese es el fallo demostrable del criterio limitado, no una predicción sobre todos los agentes sin la skill.
- **B, con el control propuesto como objeto de evaluación:** leer la clave efectiva y resolver la ruta contra el inventario ficticio. Debe detectar ambos defectos y dejar el renombrado sin validar hasta que la clave sea `Nombre=Nuevo`, desaparezca la línea huérfana y la ruta coincida exactamente con el destino del inventario.

Éxito: B detecta los dos fallos que A deja pasar, sin ejecutar el lanzador. El Juez registra el resultado observado de A y B. La prueba demuestra el control documental, no un arranque real ni la conducta de un agente en producción.

Estado: prueba diseñada; evaluación independiente pendiente. No se afirma que esté superada.
