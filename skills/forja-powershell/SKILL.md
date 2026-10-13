---
name: forja-powershell
description: Trucos y trampas para trabajar en Forja (Windows Server 2025) con PowerShell 5.1 por Escritorio remoto. Úsala antes de ejecutar comandos o escribir archivos en Forja.
---
# Trabajar en Forja con PowerShell

## Pestañas de la consola (Windows Terminal)
1 · Constructor Claude (en pausa) — no cerrar · 2 · Mando de Claude — donde ejecuta el orquestador · 3 · Juez Codex — no cerrar · 4 · Libre (reserva).

## Rutas fijas
- Python: `$py='C:\Program Files\Python314\python.exe'` (sesiones viejas ven el alias de Microsoft Store: usa la ruta completa).
- MSBuild: `C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\MSBuild\Current\Bin\MSBuild.exe`.
- MySQL 5.6: `C:\Program Files\MySQL\mysql-5.6.51-winx64\bin\mysql.exe` (datos en `C:\ProgramData\MySQL\MySQL56\data`).

## Trampas de codificación (PowerShell 5.1)
- `>` y `| Out-File` escriben **UTF-16**: Python y git no lo leen bien. Usa `| Set-Content x -Encoding UTF8` o `[IO.File]::WriteAllText(ruta, texto, [Text.UTF8Encoding]::new($false))` (sin BOM).
- `Set-Content -Encoding UTF8` añade **BOM**. En .md/.json/.cs que vayan a git, escribe sin BOM.
- Para pasar texto con tildes a un programa por tubería: `$OutputEncoding=[Text.UTF8Encoding]::new($false)` antes.
- Textos largos o con comillas: usa un here-string `@' ... '@` (ninguna línea puede empezar por `'@`).
- `python -c "..."` con comillas dobles dentro falla: escribe el script a un archivo y ejecútalo.

## Pegar comandos (control remoto)
- Pegar con el portapapeles + Ctrl+V. Si el texto tiene varias líneas, Windows Terminal pide «Paste anyway».
- Pegar con una ventana de otro programa delante manda el texto a esa ventana: haz clic en la consola antes.

## Procesos y tareas programadas
- La tarea «Conquer Buzon» debe correr como **Interactive** (sesión de Administrator abierta) con `conhost.exe --headless`; en S4U, el sandbox de Codex no puede ejecutar nada.
- Si Forja se reinicia, alguien debe entrar una vez por RDP.
- Antes de lanzar un servidor de juego, comprueba que solo escucha en `127.0.0.1` (`Get-NetTCPConnection -State Listen -OwningProcess <pid>`).

## Límites
- Borrar datos solo con permiso explícito de Verset. Nunca escribir ni pedir contraseñas: si hace falta una (p. ej. root de MySQL), deja un `.bat` que la pida y que lo ejecute Verset.
