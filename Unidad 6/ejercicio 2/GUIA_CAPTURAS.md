# Guía de evidencias en Zen

## Preparar la sesión

1. Abrir una pestaña nueva en Zen. Usar únicamente una página pública de prueba, sin iniciar sesión ni ingresar datos personales.
2. Abrir **Network** con `Ctrl + Shift + E`, o pulsar `F12` y elegir **Network**.
3. Escribir explícitamente `http://neverssl.com` en la barra y presionar Enter. Recargar con `Ctrl + R` si no aparecen solicitudes.
4. Si el navegador cambia a HTTPS o la página no carga, registrar lo ocurrido. No modificar globalmente la seguridad del navegador. Se puede probar `http://http.badssl.com/` como alternativa y documentar el cambio de sitio.
5. Seleccionar la solicitud del documento HTML, no un favicon ni una imagen. Si hubo redirecciones, conservar la solicitud inicial y la del documento final.

## Captura 1: solicitud y respuesta

Abrir **Headers** en el panel de detalles de la solicitud. Aumentar el tamaño de las herramientas arrastrando su borde si hace falta.

Guardar como `capturas/01_solicitud_http.png`, mostrando:

- Barra de direcciones y solicitud seleccionada.
- **Request URL**, **Request Method**, **Status** y **Version**, según los rótulos disponibles.
- Host real, visible en la URL o en el encabezado `Host`.

El esquema HTTP determina la ausencia de TLS; la versión HTTP/1.1, por sí sola, no permite concluirlo.

## Captura 2: encabezados enviados

En la misma solicitud, desplegar **Request Headers** y guardar `capturas/02_encabezados_http.png`. Mostrar el método o la URL junto a encabezados como `Host`, `User-Agent`, `Accept` o `Accept-Language`, si aparecen. No enviar cookies, tokens ni encabezados de otras sesiones personales.

Si todos los datos son legibles en una sola captura, esa imagen puede cubrir ambos puntos. DevTools puede mostrar contenido descifrado de HTTPS: la evidencia de HTTP requiere que se vea el esquema de la solicitud.

## Qué enviar para completar el reporte

Enviar las capturas y aclarar si se utilizó VPN durante esta sesión. No hace falta repetir Wireshark, conectarse a una cafetería ni realizar una prueba de VPN para cumplir esta consigna. No se necesita un PDF: el formato solicitado es README en Markdown dentro de un repositorio público llamado `practica-wifi-segura`.
