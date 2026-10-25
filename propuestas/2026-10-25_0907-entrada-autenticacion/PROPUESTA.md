# Propuesta: comprobar la entrada antes de atribuir fallos al hash

Tipo: nueva, `comprobar-entrada-autenticacion`.
Estado: borrador pendiente del Juez; no instalar ni repartir.

## Lección y evidencia

Registro y cambio aceptaban una cadena completa, mientras el login recortaba sus extremos. Un algoritmo de hash compatible no podía compensar esa diferencia. Cumple por un hallazgo del Juez evitable con una instrucción.

- `C:\Conquer\NUEVO-PROYECTO\REVISION-T55-CODEX.md:25`: «El login ejecuta `trim` antes de verificar» y «Es una diferencia en el tratamiento de la entrada».
- `C:\Conquer\NUEVO-PROYECTO\REVISION-T57-CODEX.md:25`: «El login conserva literalmente las claves antiguas, incluidos sus espacios». La fila documenta también el lector común y la validación de valores nuevos.
- `C:\Conquer\NUEVO-PROYECTO\INFORME-T57.md`, apartado «La clave se trata igual en las tres páginas»: «Antes, el login recortaba los espacios».

T57 registra la corrección; no se presenta como un defecto actual ni como un segundo incidente.

## Diferencia respecto a lo existente

Ninguna skill aprobada concreta el contrato de entrada entre alta, cambio y verificación. La propuesta `identidad-prueba` comprueba qué cuenta usa una herramienta; esta comprueba el tratamiento del valor recibido y la compatibilidad entre flujos. No se copian políticas particulares de longitud o coste del hash como reglas universales.

## Una prueba concreta en Forja

Una prueba A/B documental, por cálculo simbólico, sin valores de claves, cuentas, hashes reales ni servicios. El Juez puede leer este caso y cotejar el mecanismo con M3 de `REVISION-T55-CODEX.md` y la fila «Lectura uniforme de claves» de `REVISION-T57-CODEX.md`, sin activar el borrador.

Caso común: S es una cadena abstracta con un espacio inicial y otro final. R es el resultado de recortar S; R es distinto de S. El alta acepta S y guarda H(S). El login recibe exactamente S pero verifica R contra H(S). H representa un hash de autenticación correcto; no se calcula ni se guarda ningún valor.

- A, sin el control: comprobar solo que alta y login emplean algoritmos compatibles. Declara el contrato correcto y omite la transformación.
- B, con el control: seguir la cadena completa. Debe detectar que se verifica R cuando se guardó S. Una corrección válida rechaza S antes de guardarlo como valor nuevo o verifica S literalmente; un rechazo en el alta no se presenta como un registro exitoso. Para datos antiguos aceptados, recortar o aplicar restricciones nuevas sin estrategia de compatibilidad no cierra el caso.

Éxito: B detecta la incompatibilidad que A deja pasar y explica una corrección coherente sin inventar valores. Registrar resultados observados. Prueba diseñada, evaluación independiente pendiente; demuestra el contrato documental, no interoperabilidad ejecutada.
