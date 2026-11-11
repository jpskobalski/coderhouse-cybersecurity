# Preentrega 5 — Mi bóveda y contenedor seguro

**Estudiante:** Juan Skobalski

**Estado:** reporte PDF generado con diez capturas recibidas, incluida la presencia de los archivos tras volver a montar Y:. Las comprobaciones privadas no visibles se explicitan en el reporte.

## Reporte disponible

- [PDF](output/pdf/Reporte_Boveda_Contenedor_Skobalski_Juan.pdf)
- [Fuente LaTeX](Reporte_Boveda_Contenedor_Skobalski_Juan.tex)

Las secciones siguientes conservan la guía de preparación. La tabla de planificación no sustituye la evaluación de evidencias del PDF, que documenta el estado actualizado.

## Objetivo y alcance

Documentar una bóveda con tres credenciales ficticias generadas y un contenedor VeraCrypt de 100 MB, AES y exFAT. Verificar escritura, desmontaje y respaldo externo de cabecera. No se afirma que las operaciones se hayan realizado hasta revisar las evidencias.

El PDF conservará la estructura de las preentregas anteriores: carátula, introducción y alcance, procedimiento con evidencias numeradas, resultados y conclusiones. Cada figura explicará qué se observa, qué requisito acredita y sus límites.

## Resolución de diferencias en la consigna

- Generar contraseñas de **20 caracteres**, distintas para las tres entradas: satisface el requisito de más de 16 caracteres.
- Frase maestra: al menos cuatro palabras aleatorias, al menos 12 caracteres y mezcla de tipos según el entregable. No usar la frase de ejemplo publicada.
- Crear **secreto.txt y evidencia.txt** dentro del volumen, pues aparecen ambos nombres en la consigna.
- Usar **exFAT**, aunque el ejercicio 1 permitiera FAT. No reformatear un contenedor existente con datos; crear uno nuevo para esta práctica si fuera necesario.
- MFA o archivo llave son controles complementarios; esta preentrega no los enumera como requisito obligatorio.

## Procedimiento y capturas

### 1. Bóveda

Elegir Bitwarden o KeePassXC. Crear o utilizar una bóveda propia, con la frase maestra indicada. Crear tres registros ficticios llamados Correo - Práctica, Campus - Práctica y Tienda - Práctica. Para cada entrada generar una contraseña nueva de 20 caracteres con letras, números y símbolos, y guardarla.

Capturar la lista de nombres como `01_boveda.png`. Capturar la configuración del generador como `02_generador.png`: longitud 20 y categorías habilitadas. Ocultar o recortar el valor generado. La lista acredita tres registros; el generador acredita la configuración, no demuestra por sí solo las tres contraseñas guardadas. Confirmar localmente que se generó una distinta para cada registro.

No compartir la frase maestra, secretos, semillas, códigos de recuperación ni QR de MFA. Declarar en el reporte que se cumplió la política de frase maestra sin revelar su contenido.

### 2. Creación de VeraCrypt

En Windows: Create Volume → Create an encrypted file container → Standard VeraCrypt volume. Elegir un archivo nuevo, por ejemplo PreEntrega5.hc, fuera del repositorio. Seleccionar AES; capturar `03_algoritmo.png`. Indicar 100 MB y capturar `04_tamano.png`. Asignar una frase diferente de la maestra, guardada de forma privada. En Volume Format seleccionar exFAT y capturar `05_exfat.png` antes de formatear, evitando mostrar el pool aleatorio u otros valores de claves. Mover el ratón según el asistente y completar Format.

Si el volumen ya existe y cumple todos los requisitos, pueden usarse sus propiedades y las propiedades de la unidad montada como evidencias equivalentes; no recrearlo solo para capturar pantallas.

### 3. Montaje y escritura

Seleccionar una letra libre, por ejemplo Z:, elegir el contenedor con Select File y pulsar Mount. Capturar la ventana principal como `06_montado.png` con la letra, ruta y tamaño visibles.

Abrir Z: en el Explorador y crear secreto.txt y evidencia.txt, habilitando la visualización de extensiones para evitar .txt.txt. Escribir un texto ficticio, por ejemplo: «Prueba académica de almacenamiento cifrado. Juan Skobalski. Preentrega 5. Sin datos personales reales». Guardar y capturar `07_archivos.png`, mostrando la ruta Z:, ambos archivos y el contenido de evidencia.txt si resulta legible.

Cerrar editores y ventanas que utilicen la unidad. Seleccionar Dismount. Capturar `08_desmontado.png` con la lista de VeraCrypt sin ese volumen y, si cabe en la imagen, This PC sin Z:. El contenedor .hc debe permanecer en su carpeta. Montarlo nuevamente y comprobar que los archivos siguen allí; desmontar al terminar.

### 4. Respaldo de cabecera

Con el contenedor seleccionado mediante Select File, abrir Tools → Backup Volume Header (también puede estar accesible desde Volume Tools según la versión). Elegir la función de respaldo, no Restore Volume Header. Seguir el asistente e introducir la contraseña en privado. Si consulta por un volumen oculto y se creó uno estándar sin volumen oculto, indicar que no existe.

Guardar el respaldo con un nombre como PreEntrega5_header.bak, fuera del contenedor y fuera del repositorio, preferentemente en otro medio de almacenamiento. Capturar el mensaje final de éxito como `09_header_backup.png` antes de cerrarlo. La confirmación debe acreditar que el respaldo se creó, no solo que se abrió el menú.

El respaldo de cabecera no contiene una copia de los archivos ni recupera una contraseña olvidada. Tampoco acredita una restauración probada. Conservar por separado una copia del contenedor y los medios de acceso necesarios.

## Criterios para el reporte

| Requisito | Evidencia prevista | Estado |
| --- | --- | --- |
| Bóveda y tres registros | 01 | Pendiente |
| Generador con más de 16 caracteres | 02 y confirmación de uso por registro | Pendiente |
| Frase maestra conforme a consigna | Declaración sin secreto | Pendiente |
| AES, 100 MB y exFAT | 03, 04 y 05 o propiedades equivalentes | Pendiente |
| Volumen montado | 06 | Pendiente |
| Texto guardado dentro del volumen | 07 | Pendiente |
| Desmontaje y persistencia | 08 y comprobación de reapertura | Pendiente |
| Respaldo externo de cabecera | 09 | Pendiente |

## Límites del control

El cifrado protege la confidencialidad en reposo. Mientras el volumen está montado, la sesión autorizada y aplicaciones con acceso pueden leer sus archivos. Las aplicaciones pueden dejar temporales fuera del volumen. Ver símbolos al abrir un contenedor con un editor no constituye una prueba suficiente del algoritmo ni de la seguridad; no guardar cambios sobre el .hc desde un editor. Esta práctica usa datos ficticios creados dentro del volumen para evitar originales sensibles sin cifrar fuera de él.

## Referencias

- [VeraCrypt: menú de herramientas y respaldo de cabecera](https://veracrypt.io/en/Program%20Menu.html).
- [VeraCrypt: ventana principal](https://veracrypt.io/en/Main%20Program%20Window.html).

## Entrega final

Una vez recibidas las evidencias, generar Reporte_Boveda_Contenedor_Skobalski_Juan.pdf en LaTeX, revisar cada página y completar los resultados exclusivamente con lo comprobado. Las capturas y el reporte se versionan; el contenedor, la bóveda y el respaldo de cabecera permanecen privados.
