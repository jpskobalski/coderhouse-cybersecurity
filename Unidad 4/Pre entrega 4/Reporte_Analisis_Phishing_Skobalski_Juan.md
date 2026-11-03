# Reporte de análisis de phishing universitario

**Estudiante:** Juan Skobalski

**Curso:** Ciberseguridad

**Unidad:** 4 - Pre entrega 4

## Introducción

Este reporte analiza un correo simulado que informa a un profesor sobre una supuesta bonificación por investigación y le solicita iniciar sesión en `portal-universitario-pagos.net` antes de las 17:00 para confirmar datos bancarios. El análisis considera señales de ingeniería social, riesgos para la persona y la universidad, respuesta inmediata y defensa multicapa.

## Señales de alerta

1. **Dominio no institucional:** `portal-universitario-pagos.net` no demuestra relación con el dominio oficial de la universidad.
2. **Urgencia artificial:** el plazo “antes de las 5:00 PM” busca reducir el tiempo de análisis.
3. **Beneficio económico inesperado:** la bonificación crea entusiasmo y predispone a obedecer.
4. **Solicitud de datos sensibles:** un enlace recibido por correo pide credenciales y datos bancarios.
5. **Saludo genérico:** “Estimado docente” no identifica al destinatario.
6. **Procedimiento atípico:** una bonificación legítima debería verificarse en los sistemas administrativos oficiales.

El caso combina spoofing de identidad, un dominio parecido y un pretexto de autoridad. Aunque el sitio utilizara HTTPS, el cifrado no demostraría legitimidad.

## Exposición de riesgos

Si el profesor introduce información, podrían producirse robo de credenciales, fraude bancario, toma de la cuenta institucional, suplantación para atacar a otros empleados, acceso a servicios conectados y filtración de información. Una contraseña reutilizada aumentaría el alcance. El atacante también podría utilizar la cuenta comprometida como acceso inicial a la red institucional.

## Plan de acción inmediato

1. **Contener y preservar:** bloquear el dominio y el remitente, poner en cuarentena mensajes similares y conservar el correo con sus encabezados como evidencia.
2. **Investigar y proteger identidades:** localizar destinatarios, revisar clics e inicios de sesión y, si hubo interacción, restablecer credenciales, revocar sesiones y aplicar MFA.
3. **Comunicar y prevenir:** alertar a la comunidad, distribuir indicadores del ataque, reforzar el reporte de phishing y recordar el acceso por canales oficiales.

## Defensa multicapa

- **Personas:** capacitación y técnica de la lupa sobre el enlace.
- **Correo:** filtros, reputación y SPF/DKIM/DMARC para reducir suplantaciones.
- **Identidad:** MFA, contraseñas únicas y control de sesiones.
- **Red y navegación:** bloqueo DNS/web del dominio malicioso.
- **Monitoreo y respuesta:** registros, alertas y procedimiento documentado.

## Boletín preventivo (83 palabras)

Antes de abrir un enlace, coloca el cursor sobre él sin hacer clic. Compara la dirección mostrada con el dominio oficial de la universidad. En este caso, portal-universitario-pagos.net no pertenece al dominio institucional: combina palabras confiables para parecer legítimo. Si el destino es diferente, está acortado o solicita credenciales o datos bancarios, no ingreses. Abre el portal escribiendo manualmente la dirección oficial o desde la aplicación institucional. Reporta el mensaje a Soporte. La urgencia y una promesa de dinero nunca reemplazan la verificación.

## Conclusión

El correo presenta señales suficientes para clasificarlo como phishing. La protección eficaz depende de detener la interacción, verificar de forma independiente y aplicar controles complementarios de correo, identidad, red, monitoreo y capacitación.
