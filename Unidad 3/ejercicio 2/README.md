# Ejercicio 2: observación de HTTP, TLS y el handshake TCP

## Objetivo

El laboratorio permite observar con Wireshark la diferencia entre una conexión HTTP sin cifrado y una conexión HTTPS protegida con TLS. También muestra el establecimiento de una conexión TCP mediante los mensajes SYN, SYN-ACK y ACK.

La captura debe realizarse solamente sobre el tráfico propio. No se deben ingresar usuarios, contraseñas ni otros datos reales en un sitio HTTP.

## Sitios elegidos

- **Tráfico HTTP principal:** [BadSSL por HTTP](http://http.badssl.com/). Es una página de prueba que responde por el puerto 80 sin redirigir la solicitud.
- **Tráfico HTTPS:** [Example Domain](https://example.com/). Se utilizará para generar tráfico TLS fácil de reconocer.

El 28 de octubre de 2026 se comprobó con `curl` que `http://http.badssl.com/` devolvía `HTTP/1.1 200 OK` sin redirección. HTTP Forever se descartó porque, aunque respondió desde otras conexiones, no cargó correctamente en el entorno del estudiante.

## Antes de comenzar

1. Abrir Wireshark.
2. Identificar la interfaz que tiene actividad. En una notebook conectada por Wi-Fi normalmente será **Wi-Fi**; la gráfica pequeña se mueve cuando hay tráfico.
3. Cerrar descargas y aplicaciones que generen tráfico innecesario.
4. Preparar una ventana privada de Brave para reducir el efecto de la caché.
5. Hacer doble clic en la interfaz activa para iniciar la captura.

> La captura y el navegador deben ejecutarse en el mismo entorno. Si el navegador está en Windows, se captura la interfaz de Windows. Si se navega dentro de una máquina virtual, Wireshark debe ejecutarse dentro de esa VM o debe elegirse en el host la interfaz por la que pasa su tráfico.

## Evidencia 1: solicitud HTTP legible

### Procedimiento

1. Iniciar una captura nueva en Wireshark.
2. En la barra de direcciones del navegador escribir exactamente:

   ```text
   http://http.badssl.com/
   ```

   Es importante escribir `http://`; no se debe buscar el nombre del sitio en Google.
3. Volver a Wireshark y detener la captura con el botón rojo.
4. Aplicar este filtro de visualización:

   ```wireshark
   http.request && http.host contains "badssl"
   ```

5. Seleccionar el paquete cuya columna **Info** muestre algo parecido a `GET / HTTP/1.1`.
6. En **Packet Details**, expandir **Hypertext Transfer Protocol**.
7. Verificar que sean legibles campos como:
   - `Request Method: GET`
   - `Request URI: /`
   - `Host: http.badssl.com`
   - `User-Agent`

### Captura necesaria

Guardar la imagen como:

```text
capturas/01_http_get_texto_claro.png
```

La captura debe mostrar la barra del filtro, el paquete GET seleccionado y la sección **Hypertext Transfer Protocol** desplegada. Así queda demostrado que los metadatos de la solicitud se transmiten en texto claro.

### Si el navegador cambia automáticamente a HTTPS

- En Brave revisar **Settings > Privacy and security > Security > Always use secure connections** y desactivarlo temporalmente para este laboratorio.
- También se puede abrir una ventana privada y volver a escribir la URL completa.
- Como alternativa para generar el paquete sin enviar información sensible, ejecutar en PowerShell mientras Wireshark captura:

  ```powershell
  curl.exe http://http.badssl.com/ -o NUL
  ```

## Evidencia 2: datos protegidos con TLS

### Procedimiento

1. Limpiar la captura anterior con **File > Close** o iniciar otra mediante **Capture > Restart**.
2. Comenzar la captura sobre la misma interfaz.
3. Abrir una ventana privada y visitar:

   ```text
   https://example.com/
   ```

4. Detener la captura.
5. Aplicar el filtro:

   ```wireshark
   tls
   ```

6. Seleccionar un paquete cuya columna **Info** indique **Application Data**.
7. Expandir **Transport Layer Security** y observar **Packet Bytes**.

El contenido de la página y los datos de aplicación no aparecen como texto HTTP legible. Wireshark puede identificar que existe un registro TLS, pero su carga útil está cifrada.

### Captura necesaria

Guardar la imagen como:

```text
capturas/02_tls_application_data.png
```

La captura debe incluir el filtro `tls`, una fila **Application Data** seleccionada, el detalle TLS y la vista hexadecimal inferior.

### Si no aparecen paquetes con el filtro `tls`

Algunos navegadores usan HTTP/3 sobre QUIC, que funciona con UDP. Para este ejercicio conviene obtener una conexión TLS sobre TCP:

1. Cerrar la ventana privada.
2. Iniciar una captura nueva.
3. Abrir otra ventana privada y entrar nuevamente a `https://example.com/`.
4. Probar primero el filtro `tcp.port == 443` y luego `tls`.
5. Si el navegador insiste en usar QUIC, desactivarlo temporalmente o usar otro navegador solo para esta prueba.

## Evidencia 3: handshake de TCP

El filtro propuesto en el enunciado:

```wireshark
tcp.flags.syn == 1
```

sirve para encontrar SYN y SYN-ACK, pero excluye el ACK final porque ese paquete ya no tiene el bit SYN activo. Para observar los tres pasos se debe aislar una sola conversación TCP.

### Procedimiento recomendado

1. Iniciar una captura nueva.
2. Abrir `http://http.badssl.com/` en una ventana privada.
3. Detener la captura y aplicar:

   ```wireshark
   tcp.dstport == 80 && tcp.flags.syn == 1 && tcp.flags.ack == 0
   ```

4. Seleccionar el paquete SYN encontrado.
5. Hacer clic derecho y elegir **Follow > TCP Stream**.
6. Cerrar la ventana **Follow TCP Stream** sin borrar el filtro. Wireshark dejará un filtro similar a:

   ```wireshark
   tcp.stream eq 3
   ```

   El número puede ser diferente. La letra `N` utilizada en algunas explicaciones es solo un marcador: no debe escribirse literalmente. Por ejemplo, si el índice real es 3, el filtro correcto es `tcp.stream eq 3`.
7. En las primeras filas del flujo comprobar esta secuencia:
   1. Cliente a servidor: `[SYN]`
   2. Servidor a cliente: `[SYN, ACK]`
   3. Cliente a servidor: `[ACK]`

### Captura recomendada

Aunque el enunciado exige dos capturas, esta tercera evidencia mejora el trabajo. Guardarla como:

```text
capturas/03_tcp_handshake.png
```

La lista de paquetes debe mostrar juntos los tres mensajes y el filtro `tcp.stream eq N`.

## Qué debe verse en cada captura

| Archivo | Evidencia visible |
| --- | --- |
| `01_http_get_texto_claro.png` | GET HTTP, host y encabezados legibles |
| `02_tls_application_data.png` | Registro TLS Application Data y bytes cifrados |
| `03_tcp_handshake.png` | SYN, SYN-ACK y ACK del mismo flujo |

## Texto de análisis para la entrega

Si un atacante pudiera capturar los paquetes de una sesión HTTP en la que se introduce una contraseña, podría leerla directamente porque HTTP no cifra el contenido transmitido. También podría observar otros datos de la solicitud, reutilizar las credenciales para intentar acceder a la cuenta o modificar el tráfico durante su recorrido. En HTTPS, TLS cifra la información de aplicación, por lo que una captura equivalente muestra registros y bytes que no permiten leer directamente la contraseña. Por este motivo nunca se deben enviar credenciales mediante HTTP.

## Interpretación de los resultados

- **HTTP:** ofrece transporte web, pero no confidencialidad ni protección criptográfica de la integridad.
- **HTTPS:** encapsula HTTP dentro de TLS y protege el contenido durante el tránsito.
- **TCP:** establece primero una conexión lógica mediante el handshake de tres pasos; después circulan HTTP o TLS y los datos de la aplicación.
- **Candado del navegador:** confirma una conexión cifrada con el dominio indicado por el certificado, pero no garantiza por sí solo que el sitio sea legítimo.

## Próximo paso

Cuando las tres imágenes estén guardadas en `capturas/`, se incorporarán al reporte y se generará el PDF final del ejercicio.
