# Propuesta: verificar la identidad antes de automatizar pruebas

Tipo: **nueva**, `verificar-identidad-prueba`.
Estado: borrador del Bibliotecario, pendiente del Juez; no instalar ni repartir.

## Lección y umbral

La cuenta prevista en el encargo puede diferir de la usada por una ventana o herramienta. Las teclas ignoradas y una ruta equivocada produjeron accesos con otra identidad. Hay dos tareas distintas con ese tropiezo y un hallazgo del Juez. Una comprobación antes del envío y otra antes de actuar evitan dar por buena la identidad solo por intención.

## Evidencia local depurada

- `C:\Conquer\_pruebas\codex-tareas\T14\VEREDICTO-GEMINI.md:8`: «Las pruebas de pulsaciones simuladas dispararon 2 logins no previstos». El Juez registra un efecto sobre el último acceso; se omite la identidad real.
- `C:\Conquer\_pruebas\codex-tareas\T14\INFORME-T14.md:37`: «porque mis teclas no entraron en los campos». El constructor describe el uso accidental de los valores que ya estaban en el cliente. Es el mismo incidente anterior, no otro caso.
- `C:\Conquer\_pruebas\codex-tareas\T27\INFORME-T27.md:75`: «una ruta mal copiada». El constructor reconoce que la primera ejecución entró con una cuenta de prueba distinta de la prevista. Se omiten nombres y números de cuentas.

## Diferencia respecto a lo existente

`montar-source-conquer-forja` reserva la entrada personal al usuario, y `forja-powershell` advierte sobre el foco al pegar comandos en consolas. No definen la comprobación de identidad efectiva de una herramienta o formulario de pruebas. La propuesta cubre ese paso específico, sin cambiar quién puede autorizar cuentas o sesiones. La propuesta archivada sobre revisión de skills tampoco lo cubre.

## Una prueba concreta para el Juez en Forja

**Una prueba A/B documental de selección de cuenta**, realizada por lectura, sin contraseñas, conexiones, pulsaciones ni cambios de cuentas. No cargar el borrador como skill activa.

Caso común, con alias totalmente ficticios:

```text
Encargo: probar una compra únicamente con PRUEBA-A.
Ventana: instancia de pruebas correcta.
Formulario actual: identificador PRUEBA-B.
La automatización intentó escribir PRUEBA-A, pero el cliente ignoró las teclas.
Estado comprobable antes de Enter: el formulario sigue mostrando PRUEBA-B.
Acción pendiente: enviar Enter y, tras conectar, efectuar la compra.
```

- **A, sin la comprobación propuesta:** continuar porque la automatización ya intentó escribir el identificador. En el caso descrito se enviaría PRUEBA-B: falla la condición de identidad del encargo, aunque la ventana sea la correcta.
- **B, con el control propuesto como objeto de evaluación:** cotejar el estado efectivo antes de Enter. Debe detectar la discrepancia y detener el envío y la compra hasta poder verificar PRUEBA-A dentro del alcance autorizado. No debe concederse permiso para PRUEBA-B ni corregir su cuenta.

Éxito: B bloquea el acceso equivocado antes del primer envío; no basta con descubrirlo después de comprar. El Juez registra el resultado de A y B. A representa la práctica fallida observada, no el comportamiento inevitable de cualquier agente sin la skill. Esta prueba acredita el control documental; no acredita automatización real del cliente.

Estado: prueba diseñada; evaluación independiente pendiente. No se afirma que esté superada.
