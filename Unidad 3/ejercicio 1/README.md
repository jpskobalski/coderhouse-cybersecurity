# Observando redes en mi entorno cotidiano

**Estudiante:** Juan Skobalski  
**Curso:** Ciberseguridad  
**Unidad:** 3  
**Ejercicio:** 1

## Objetivo

Identificar dispositivos conectados a la red doméstica, distinguir cuáles pueden comunicarse dentro de la red local y cuáles necesitan acceso a internet, y describir el posible recorrido de los datos durante una acción cotidiana.

## Entorno observado

Los dispositivos se conectan por Wi-Fi al router doméstico. El router funciona como punto central de la red local: les asigna direcciones IP privadas, permite que se comuniquen entre sí cuando corresponde y dirige hacia internet el tráfico destinado a servicios externos.

## Inventario de dispositivos

| Dispositivo | Conexión habitual | Comunicación dentro de la red local | Uso de internet |
| --- | --- | --- | --- |
| MacBook Air M5 | Wi-Fi | Puede enviar documentos a la impresora y comunicarse con otros equipos autorizados de la casa. | Necesita internet para navegar, usar servicios en la nube, descargar actualizaciones y realizar videollamadas. |
| iPhone 17 | Wi-Fi o red móvil | Puede descubrir la impresora, enviar contenido a equipos compatibles y controlar dispositivos inteligentes, según la aplicación utilizada. | Necesita internet para mensajería, navegación, copias en la nube, redes sociales y contenido multimedia. |
| Impresora HP Inkjet con Wi-Fi | Wi-Fi | Puede recibir trabajos de impresión directamente desde la MacBook o el iPhone mediante la red doméstica. | La impresión local no necesariamente requiere internet. La conexión externa puede utilizarse para actualizaciones, servicios del fabricante o impresión remota. |
| Lámpara inteligente Smart Home | Wi-Fi | Puede recibir órdenes desde el teléfono dentro de la casa si el producto y la aplicación admiten control local. | Puede necesitar internet cuando las órdenes pasan por la nube del fabricante o se realizan desde fuera del hogar. |
| Lavarropas Midea con Wi-Fi | Wi-Fi | La aplicación puede detectar o configurar el equipo desde la red doméstica, según el diseño del fabricante. | Normalmente utiliza internet para control remoto, notificaciones, integración con la cuenta del fabricante y actualizaciones. |

## ¿Cómo se comunican entre sí?

Cada dispositivo se asocia al punto de acceso Wi-Fi del router y recibe una dirección IP privada, por ejemplo `192.168.1.10`. Esa dirección permite identificarlo dentro de la red doméstica.

Cuando dos dispositivos se comunican localmente, como la MacBook y la impresora, los datos permanecen dentro de la LAN y el router o su switch integrado los dirige al destino correspondiente. La conexión a internet del proveedor no es indispensable para transportar un trabajo de impresión local.

Cuando un dispositivo necesita un servicio externo, envía los paquetes al router. El router traduce la dirección privada mediante NAT y reenvía el tráfico hacia el proveedor de internet. La respuesta realiza el recorrido inverso hasta el dispositivo que inició la comunicación.

Los equipos inteligentes pueden tener comportamientos distintos según su fabricante. Algunos aceptan comandos locales; otros envían la orden a un servidor en internet y esperan que ese servidor se comunique con el dispositivo. Por eso, aunque el teléfono y la lámpara estén conectados al mismo Wi-Fi, ciertas funciones podrían dejar de operar si se interrumpe internet.

## Acción elegida: reproducir un video de YouTube en el iPhone

El recorrido posible de los datos es el siguiente:

1. El usuario abre YouTube en el iPhone y selecciona un video.
2. El iPhone se comunica por Wi-Fi con el router doméstico.
3. La aplicación consulta la dirección del servicio y establece una conexión cifrada con los servidores de YouTube.
4. El router envía los paquetes al proveedor de internet mediante la conexión doméstica.
5. Los paquetes atraviesan distintas redes intermedias hasta llegar a un servidor de YouTube o a un servidor de distribución de contenido cercano.
6. El servidor responde enviando el video dividido en múltiples partes y paquetes.
7. La respuesta vuelve por internet al proveedor, llega al router y este la entrega al iPhone.
8. El iPhone ordena los datos recibidos, reconstruye cada parte del contenido y reproduce el video mientras continúa descargando las siguientes partes.

```mermaid
flowchart LR
    A[iPhone 17] -->|Wi-Fi| B[Router doméstico]
    B --> C[Proveedor de internet]
    C --> D[Redes intermedias]
    D --> E[Servidor de YouTube o CDN]
    E -->|Paquetes de respuesta| D
    D --> C
    C --> B
    B -->|Wi-Fi| A
```

## ¿Por qué los datos se dividen en paquetes?

Dividir la información en paquetes permite que la red transporte datos de muchas comunicaciones al mismo tiempo. En lugar de reservar todo el medio para un único mensaje, los paquetes de distintos dispositivos pueden intercalarse y avanzar por la infraestructura disponible.

Este sistema ofrece varias ventajas:

- **Uso eficiente de la red:** diferentes usuarios y aplicaciones comparten los enlaces de comunicación.
- **Recuperación ante pérdidas:** si se pierde una parte de la información, puede volver a enviarse solamente el paquete afectado.
- **Elección de rutas:** los paquetes pueden atravesar distintos caminos según la disponibilidad de las redes intermedias.
- **Reconstrucción ordenada:** la información de control permite identificar el origen, el destino y el orden necesario para reconstruir los datos.
- **Escalabilidad:** la misma infraestructura puede transportar páginas web, mensajes, audio, video y archivos para millones de dispositivos.

## Conclusión

La red doméstica combina comunicaciones locales y conexiones con servicios externos. La impresora puede funcionar principalmente dentro de la LAN, mientras que el iPhone, la computadora y los dispositivos inteligentes utilizan internet para muchas de sus funciones. El router vincula ambos espacios: organiza el tráfico local y actúa como salida hacia otras redes. La división de la información en paquetes hace posible compartir esa infraestructura de forma eficiente, recuperar partes perdidas y entregar los datos al destino correcto.
