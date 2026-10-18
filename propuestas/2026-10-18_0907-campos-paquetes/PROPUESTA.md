# Propuesta: comprobar posiciones y capacidad real de paquetes

Tipo: **nueva**, `validar-campos-paquetes`.
Estado: borrador del Bibliotecario, pendiente del Juez; no instalar ni repartir.

## Lección y umbral

Una llamada con longitud y posición intercambiadas puede compilar y romper el paquete. Corregir el orden tampoco garantiza que el método respete la capacidad: hay que mirar su copia real. Cumple el umbral por un hallazgo del Juez en T14; no se cuentan sus dos revisiones como dos incidentes.

## Evidencia local depurada

- `C:\Conquer\_pruebas\codex-tareas\T14\VEREDICTO-CODEX.md:5`: «ReadString/WriteString reciben longitud y después posición». El Juez confirma que el arreglo separó el campo de texto y el puerto.
- Mismo archivo, línea 11: «Packet Structure.cs:443 copia value.Length sin limitarlo a los 12 bytes disponibles». Es un riesgo previo señalado por el Juez, fuera del cambio local revisado.

Se citan solo los fragmentos necesarios, sin direcciones de red ni datos de cuentas. La propuesta no afirma que el defecto continúe en la versión actual.

## Diferencia respecto a lo existente

`montar-source-conquer-forja` pide identificar cliente, login y cifrado, pero no contiene este método de comprobación de campos. `juez-revision` exige evidencia general, sin detallar posiciones y capacidad de copia. Las demás skills y la propuesta archivada no cubren serialización binaria. La instrucción nueva corresponde a construcción y diagnóstico, no cambia el procedimiento de aprobación del Juez.

## Una prueba concreta para el Juez en Forja

**Una prueba A/B documental de un escritor de paquete sintético**, por lectura y cálculo de intervalos, sin ejecutar código inseguro ni usar red. No cargar el borrador como skill activa.

Caso común:

```text
Paquete: 32 bytes, índices 0 a 31.
Campo vecino: índices 12 a 15.
Campo de texto: índices 20 a 31, capacidad 12 bytes.
No hay terminador ni cola en este caso sintético.
Firma: Escribir(valor, longitud, posicion).
Llamada entregada: Escribir(valor, 12, 20).
Implementación entregada: copia todos los bytes de valor desde posicion,
sin comprobar longitud ni el final del paquete.
Valores ASCII de prueba: 'A' repetida 9, 12 y 13 veces.
```

- **A, sin el control propuesto:** comprobar solo el orden de argumentos y el valor de 9 bytes. Ocupa 20 a 28 y parece correcto. Este criterio deja pasar una implementación que no acota la copia.
- **B, con el control propuesto como objeto de evaluación:** revisar la implementación y los tres intervalos. Nueve bytes ocupan 20 a 28; doce, 20 a 31; trece, 20 a 32. Debe detectar que el último invade un índice inexistente y exigir un tratamiento válido del exceso antes de copiar. El campo vecino debe seguir intacto en los casos que caben; cambiar a la llamada invertida tampoco es una solución.

Éxito: B identifica el desbordamiento potencial que A omite y no declara seguro el escritor por el ejemplo corto. El Juez registra lo observado en ambas evaluaciones. La prueba acredita el control documental de límites; no ejecuta el escritor histórico ni certifica todo el protocolo.

Estado: prueba diseñada; evaluación independiente pendiente. No se afirma que esté superada.
