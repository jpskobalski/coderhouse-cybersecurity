# Pre entrega 3: análisis de tráfico e identificación de protocolos inseguros

## Objetivo

Documentar una captura controlada de tráfico propio con Wireshark para reconocer DNS, TCP, HTTP y TLS; comparar tráfico web en texto claro y cifrado; e identificar el three-way handshake de TCP.

Para el tráfico HTTP se utilizará `http://http.badssl.com/`, porque NeverSSL no cargó correctamente en la conexión del estudiante. BadSSL es una página de prueba que permite generar una solicitud HTTP sin ingresar datos reales. Para HTTPS se utilizará `https://www.wikipedia.org/`.

> No se deben introducir usuarios, contraseñas ni datos personales en ninguna página HTTP.

## Evidencias necesarias

| N.º | Archivo | Qué debe demostrar |
| --- | --- | --- |
| 1 | `capturas/01_inventario_protocolos.png` | Jerarquía de protocolos con al menos DNS, TCP, HTTP y TLS |
| 2 | `capturas/02_dns_resolucion.png` | Consulta, dominio consultado y respuesta con dirección IP |
| 3 | `capturas/03_http_solicitud_get.png` | Método GET, host y URI visibles en texto claro |
| 4 | `capturas/04_http_respuesta_200.png` | Respuesta HTTP y código de estado |
| 5 | `capturas/05_tls_application_data.png` | Datos de aplicación TLS cifrados |
| 6 | `capturas/06_tcp_handshake.png` | SYN, SYN-ACK y ACK de un mismo flujo TCP |

## Preparación de una captura limpia

1. Cerrar descargas y aplicaciones que generen tráfico innecesario.
2. Abrir una ventana privada de Brave.
3. En Brave, comprobar temporalmente:
   - **Settings > Privacy and security > Security > Use secure DNS:** desactivado, para que Wireshark pueda observar la consulta DNS tradicional.
   - **Settings > Privacy and security > Security > Always use secure connections:** desactivado, para evitar que Brave cambie la URL HTTP a HTTPS.
4. Abrir PowerShell y ejecutar antes de iniciar la navegación:

   ```powershell
   ipconfig /flushdns
   ```

5. Iniciar Wireshark y hacer doble clic en la interfaz **Wi-Fi** activa.
6. Mientras la captura está en curso, visitar en este orden:

   ```text
   http://http.badssl.com/
   https://www.wikipedia.org/
   ```

7. Esperar unos segundos y detener la captura.
8. Guardar también la captura original como `captura_entregable_3.pcapng` para conservar la evidencia completa.
9. Al terminar el laboratorio, restaurar las opciones de seguridad de Brave que se hayan modificado.

## 1. Inventario de protocolos

1. Con la captura detenida, abrir **Statistics > Protocol Hierarchy**.
2. Expandir las ramas necesarias hasta que se vean DNS, TCP, HTTP y TLS.
3. Tomar una captura en la que se lea el nombre de cada protocolo.
4. Guardarla como `capturas/01_inventario_protocolos.png`.

## 2. Resolución DNS

1. Cerrar la ventana de jerarquía y aplicar:

   ```wireshark
   dns.qry.name contains "badssl"
   ```

2. Elegir una fila cuya columna **Info** indique `Standard query response`.
3. En **Packet Details**, expandir **Domain Name System (response)** y luego **Answers**.
4. Verificar que se vean el dominio y el registro `A` o `AAAA` con la IP obtenida.
5. Guardar la captura como `capturas/02_dns_resolucion.png`.

Si no aparece ninguna consulta DNS, iniciar una captura nueva después de desactivar **Use secure DNS**, ejecutar nuevamente `ipconfig /flushdns` y volver a abrir el sitio en una ventana privada.

## 3. Solicitud HTTP en texto claro

1. Aplicar:

   ```wireshark
   http.request && http.host contains "badssl"
   ```

2. Seleccionar `GET / HTTP/1.1`.
3. Expandir **Hypertext Transfer Protocol**.
4. Comprobar que se lean:
   - `Request Method: GET`
   - `Request URI: /`
   - `Host: http.badssl.com`
5. Guardar la captura como `capturas/03_http_solicitud_get.png`.

La imagen debe incluir la barra del filtro, la fila seleccionada, el detalle HTTP y, si es posible, el panel de bytes.

## 4. Respuesta y código HTTP

1. Sobre el paquete GET, hacer clic derecho y seleccionar **Follow > TCP Stream**.
2. Cerrar la ventana del flujo. Wireshark dejará un filtro similar a `tcp.stream eq 9`; el número será el de la captura real.
3. Añadir `&& http`, por ejemplo:

   ```wireshark
   tcp.stream eq 9 && http
   ```

4. Seleccionar la respuesta `HTTP/1.1 200 OK`.
5. Expandir **Hypertext Transfer Protocol** y verificar `Status Code: 200`.
6. Guardar la captura como `capturas/04_http_respuesta_200.png`.

No se debe escribir literalmente `N` en `tcp.stream eq N`; debe usarse el número que indique Wireshark.

## 5. Tráfico HTTPS protegido con TLS

1. Aplicar:

   ```wireshark
   tls.handshake.type == 1
   ```

2. Buscar un **Client Hello** relacionado con Wikipedia y seleccionarlo.
3. Hacer clic derecho en ese paquete y elegir **Follow > TCP Stream**.
4. Cerrar la ventana y conservar el número de flujo que aparece en el filtro.
5. Aplicar, reemplazando el número por el real:

   ```wireshark
   tcp.stream eq 15 && tls.record.content_type == 23
   ```

6. Seleccionar una fila **Application Data**.
7. Expandir **Transport Layer Security** para que se vea **Encrypted Application Data**.
8. Guardar la captura como `capturas/05_tls_application_data.png`.

Si Brave usa HTTP/3 y no aparecen paquetes TLS sobre TCP, se puede desactivar QUIC temporalmente en `brave://flags/#enable-quic`, reiniciar Brave y repetir la captura. Después del laboratorio debe restaurarse el valor original.

## 6. Three-Way Handshake de TCP

El filtro `tcp.flags.syn == 1` ayuda a localizar el comienzo, pero no muestra el ACK final porque ese paquete ya no tiene activo el bit SYN.

1. Aplicar:

   ```wireshark
   tcp.dstport == 80 && tcp.flags.syn == 1 && tcp.flags.ack == 0
   ```

2. Seleccionar el SYN dirigido a `http.badssl.com`.
3. Hacer clic derecho y elegir **Follow > TCP Stream**.
4. Cerrar la ventana del flujo y conservar `tcp.stream eq <número>`.
5. Ordenar la columna **No.** de menor a mayor.
6. Confirmar que las tres primeras filas del establecimiento sean:
   1. Cliente a servidor: `[SYN]`
   2. Servidor a cliente: `[SYN, ACK]`
   3. Cliente a servidor: `[ACK]`
7. Ajustar la altura de la lista para que se vean juntas y guardar `capturas/06_tcp_handshake.png`.

## Criterio de calidad de las capturas

- Debe verse la barra del filtro utilizada.
- La columna **Protocol** y la columna **Info** deben ser legibles.
- La fila relevante debe estar seleccionada.
- El panel de detalles debe estar desplegado en DNS, HTTP o TLS según corresponda.
- No deben aparecer contraseñas, tokens, correos personales ni otros datos sensibles.

## Próximo paso

Cuando estén disponibles las seis imágenes, se incorporarán al reporte en LaTeX y se generará el PDF final con introducción, inventario, análisis de seguridad, conclusiones y recomendaciones.
