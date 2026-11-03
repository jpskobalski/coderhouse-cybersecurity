# Análisis de phishing y smishing

**Estudiante:** Juan Skobalski

**Curso:** Ciberseguridad

**Unidad:** 4 - Ejercicio 1

## Introducción

El phishing es una técnica de ingeniería social que intenta lograr que una persona realice voluntariamente una acción perjudicial, como abrir un enlace, entregar credenciales o efectuar un pago. Este reporte analiza dos casos ficticios desde la perspectiva de un analista junior: un correo que suplanta a Soporte Apple y un SMS que simula provenir de Correos.

## Caso A: correo de “Soporte Apple”

El mensaje afirma que el Apple ID del destinatario fue bloqueado y solicita acceder a `http://apple-id-security-check.info` para recuperarlo.

### Señales de alerta

1. **Dominio ajeno a Apple.** El dominio registrable es `apple-id-security-check.info`, no `apple.com`. Incluir la marca dentro del nombre no demuestra relación con la empresa.
2. **Uso de HTTP.** El enlace utiliza HTTP, por lo que la conexión no estaría cifrada. Aunque utilizara HTTPS, el candado solo probaría el cifrado de la conexión, no la legitimidad del propietario.
3. **Urgencia y miedo.** La supuesta cuenta bloqueada busca provocar una reacción rápida antes de que el usuario compruebe el mensaje.
4. **Identidad del remitente no verificada.** “Soporte Apple” es únicamente un nombre visible. Como el escenario no muestra la dirección real, no puede confirmarse que provenga de un dominio oficial.
5. **Ruta de recuperación insegura.** El mensaje dirige al usuario a un enlace incluido en el correo, en vez de recomendar el acceso independiente a la configuración oficial de la cuenta.

La combinación de estas señales es coherente con un intento de robo de credenciales. Si la víctima ingresara su Apple ID y contraseña, el atacante podría intentar tomar control de la cuenta y acceder a servicios vinculados.

## Caso B: smishing de un paquete retenido

El SMS informa que un paquete fue retenido por una deuda aduanera de 1,20 euros y presenta un enlace acortado para pagar.

El atacante combina **urgencia**, **miedo a perder una entrega** y una **cantidad deliberadamente pequeña**. Un importe bajo reduce la percepción de riesgo: la víctima puede considerar que verificar el reclamo demanda más esfuerzo que pagar. El enlace acortado impide evaluar el dominio antes de abrirlo y facilita que la víctima llegue a una página falsa. El objetivo podría no ser solamente cobrar 1,20 euros, sino obtener datos personales o de una tarjeta.

## Protocolo de respuesta para un familiar

1. **Detenerse y no interactuar.** No abrir el enlace, no responder, no descargar archivos y no ingresar información.
2. **Verificar por un canal independiente.** Abrir manualmente la aplicación o el sitio oficial, o llamar a un número obtenido fuera del mensaje. No utilizar enlaces ni teléfonos proporcionados por la comunicación sospechosa.
3. **Reportar y protegerse.** Marcar el mensaje como phishing o spam, bloquear al remitente y eliminarlo. Si ya se ingresaron datos, cambiar inmediatamente la contraseña desde el sitio oficial, cerrar sesiones, activar MFA y contactar al banco si se proporcionó información de pago.

## Conclusión

Los dos casos explotan emociones antes que vulnerabilidades técnicas. En el correo, la revisión del dominio, el protocolo y la identidad del remitente permite detectar la suplantación. En el SMS, la urgencia, la expectativa de recibir un paquete y el pago pequeño disminuyen la resistencia de la víctima. La respuesta más segura es interrumpir la interacción y verificar siempre por un canal independiente.
