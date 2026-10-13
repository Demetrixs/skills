---
name: montar-source-conquer-forja
description: Pasos para evaluar y montar una source (servidor) de Conquer Online con su cliente en Forja, aislada y en local. Úsala al probar o cambiar la base del servidor.
---
# Montar una source de Conquer en Forja

## Principios
- Base elegida por ser la **más avanzada en contenido** (lo que pide la comunidad), no la más fácil. Debe correr en **PCs viejos**.
- Todo empieza **aislado**: `C:\Conquer\_pruebas\<nombre>`. Nada se mezcla con otra base hasta aprobar.
- Nunca abrir al público, puertos ni firewall: servidor solo en `127.0.0.1`.

## Pasos
1. **Bajar** la source (git clone o archivo) dentro de la carpeta aparte y **escanearla**: `Start-MpScan -ScanType CustomScan -ScanPath <carpeta>`. Descargas de foros solo en Forja.
2. **Auditar** con Codex en solo lectura + compilación (skill `codex-constructor-windows`): compila, qué cliente espera (versión, paquete de login, cifrado Blowfish/CAST, puertos), estado de la base de datos y de los sistemas (terminado / a medias / falta), riesgos y veredicto.
3. **Cliente**: conseguir la versión exacta (archive.org guarda instaladores oficiales; catálogos de cooldown.dev). Escanear antes de instalar. Preparar una copia para pruebas que apunte a `127.0.0.1` (Server.dat / herramientas RSA de la comunidad); a los jugadores se les da el original.
4. **Base de datos**: crear una **nueva y aparte** en MySQL (permiso de Verset; la contraseña root la pone él con un `.bat`). Importar el volcado de la source.
5. **Encender** el servidor con `Start-Process` (ventana minimizada; no cerrar su ventana) y comprobar los puertos en 127.0.0.1. Abrir el cliente y dejar que **Verset entre** (sus credenciales las escribe él).
6. Bitácora: qué se hizo, dónde y cómo probarlo.

## Trampas conocidas
- Avisos de «Program Compatibility Assistant»: inofensivos; Verset marca «Don't show this message again».
- Clientes antiguos con login en Flash o DLL de OpenSSL de otra arquitectura (x86/x64): revisar primero DLLs.
- Procesos como TQAT.exe bloquean el borrado de la carpeta del cliente: pararlos antes.
