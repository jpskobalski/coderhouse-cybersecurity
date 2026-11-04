# Mi bóveda y contenedor seguro fundamental

**Estudiante:** Juan Skobalski

**Materia:** Ciberseguridad · Unidad 5 · Ejercicio 1

**Estado:** guía preparada; configuración y evidencias pendientes de realización.

## Objetivo y alcance

Proteger credenciales con un gestor y una protección adicional, y almacenar un archivo de práctica dentro de un contenedor cifrado. Se trabajará en Windows con datos ficticios. Esta documentación describe el procedimiento previsto: no acredita configuraciones todavía no verificadas.

La consigna requiere README y capturas. El recorrido principal usa Bitwarden con MFA; KeePassXC con archivo llave es una alternativa válida. No hace falta implementar ambas opciones ni configurar passkeys para cumplir este ejercicio.

## 1. Bóveda de identidad

1. Instalar Bitwarden desde su [sitio oficial](https://bitwarden.com/download/) y crear la cuenta, o utilizar una cuenta propia ya disponible.
2. Elegir una frase maestra con al menos cuatro palabras seleccionadas aleatoriamente. No copiar ejemplos de internet ni escribirla en el reporte.
3. Crear tres elementos de tipo **Login** con nombres `Correo - Práctica`, `Campus - Práctica` y `Tienda - Práctica`. Usar un usuario ficticio, como `alumno@example.com`; no es necesario crear cuentas en servicios externos.
4. Generar una contraseña diferente para cada elemento, de al menos 16 caracteres, con números y símbolos. Guardarlas en la bóveda sin revelarlas en capturas.
5. En la bóveda web, buscar **Settings → Security → Two-step login** y configurar **Authenticator app**. Los nombres pueden variar con la versión. Escanear el QR desde una aplicación autenticadora independiente y confirmar el código solicitado.
6. Guardar el código de recuperación de MFA en un lugar seguro accesible si la bóveda queda bloqueada. No conservar su única copia dentro de esa misma bóveda. Este código permite recuperar el acceso al segundo factor; no sustituye la contraseña maestra ni descifra la bóveda.
7. Comprobar el acceso en una sesión nueva con contraseña y autenticador antes de cerrar la sesión de configuración. Desbloquear una sesión existente no necesariamente solicita MFA.

**Justificación:** las contraseñas distintas reducen el impacto de la reutilización; el gestor facilita su generación y almacenamiento. MFA agrega un factor al inicio de sesión. Los códigos TOTP todavía pueden ser robados por phishing en tiempo real: la protección no es absoluta.

### Alternativa: KeePassXC

Crear una base `.kdbx`, asignar una frase maestra y añadir un archivo llave como requisito adicional. Crear los mismos tres registros y probar la reapertura con ambos componentes. Mantener copias de respaldo y guardar el archivo llave separado de la base. La captura debe mostrar que la base requiere el archivo, sin revelar su contenido. No equivale a una llave física FIDO2 ni vuelve inaccesible una base ya desbloqueada.

## 2. Contenedor cifrado con VeraCrypt

1. Descargar e instalar VeraCrypt desde su [sitio oficial](https://veracrypt.io/).
2. Abrir **Create Volume → Create an encrypted file container → Standard VeraCrypt volume**.
3. En **Select File**, elegir una ubicación privada fuera del repositorio y un nombre nuevo, por ejemplo `LaboratorioUnidad5.hc`. No seleccionar un archivo existente: se creará y formateará el contenedor.
4. En **Encryption Options**, seleccionar **AES** y **SHA-512**, conforme a la consigna. Verificar los valores aunque la versión muestre otros predeterminados. AES cifra los datos; SHA-512 es el algoritmo hash seleccionado para la derivación de claves.
5. En **Volume Size**, ingresar **100 MB**.
6. Establecer una frase diferente de la contraseña maestra. Guardarla como un elemento adicional en el gestor y verificar que pueda recuperarse.
7. En **Volume Format**, elegir un sistema de archivos apropiado para este volumen pequeño, como FAT. Mover el ratón dentro del asistente durante el proceso de recolección de aleatoriedad y pulsar **Format**. Esperar la finalización y salir del asistente.

**Justificación:** el contenedor protege la confidencialidad de los archivos almacenados cuando está desmontado. No reemplaza un respaldo ni protege el contenido frente a malware con acceso a la sesión mientras está montado.

## 3. Montaje, uso y comprobación

1. En la ventana principal, seleccionar una letra libre, por ejemplo **Z:**.
2. Pulsar **Select File**, elegir el contenedor y luego **Mount**. Introducir la frase en privado.
3. Abrir **This PC → Z:** en el Explorador. Crear allí `aprendizajes.txt`, comprobando que no termine como `.txt.txt`.
4. Escribir y guardar estos tres aprendizajes con tus propias palabras, o utilizar el siguiente texto de práctica:

```text
1. Una contraseña única por servicio limita el daño de una filtración; el gestor permite generar y conservar claves robustas.
2. MFA añade una barrera al inicio de sesión, y su recuperación debe planificarse antes de perder el autenticador.
3. El contenedor cifrado protege los archivos cuando está desmontado; mientras está montado, la sesión autorizada puede leerlos.
```

5. Cerrar el editor y los archivos abiertos en Z:. Seleccionar el volumen en VeraCrypt y pulsar **Dismount**.
6. Comprobar que Z: ya no aparece como unidad accesible. El archivo `.hc` permanece: desmontar no lo borra.
7. Montar de nuevo, verificar que `aprendizajes.txt` conserva el contenido y desmontar al terminar.

## 4. Evidencias requeridas

Usar **Win + Shift + S** para capturar la ventana relevante y guardar en `capturas/` con estos nombres:

| Archivo | Qué debe verse | Qué acredita |
| --- | --- | --- |
| `01_boveda.png` | Lista con los tres nombres ficticios, sin abrir sus secretos | Existencia de los registros |
| `02_proteccion_adicional.png` | MFA habilitado en Bitwarden o configuración de archivo llave en KeePassXC | Protección adicional configurada |
| `03_veracrypt_montado.png` | Ventana principal con volumen, tamaño y letra de unidad | Contenedor montado |

Antes de compartir, comprobar que no aparezcan contraseñas, QR de MFA, semillas TOTP, códigos de recuperación ni datos reales. Para MFA, capturar el estado habilitado después de terminar el asistente, no la pantalla del QR.

Las capturas de la lista no demuestran longitud ni aleatoriedad de las contraseñas: esos requisitos deben verificarse localmente en el generador. Como complemento opcional, puede adjuntarse `04_aprendizajes.png` con el archivo abierto dentro de Z:, sin secretos.

## 5. Registro de resultados

Completar únicamente después de ejecutar y verificar cada operación.

| Comprobación | Estado actual |
| --- | --- |
| Gestor elegido y frase maestra de cuatro palabras aleatorias o más | Pendiente |
| Tres registros con contraseñas distintas de al menos 16 caracteres | Pendiente |
| MFA o archivo llave y acceso de prueba | Pendiente |
| Recuperación y respaldo planificados | Pendiente |
| Contenedor estándar de 100 MB, AES y SHA-512 | Pendiente |
| Archivo con tres aprendizajes guardado dentro del volumen | Pendiente |
| Desmontaje y reapertura comprobados | Pendiente |
| Tres capturas requeridas revisadas y adjuntadas | Pendiente |

## Fuentes de apoyo

- [Bitwarden: métodos de autenticación en dos pasos](https://bitwarden.com/help/setup-two-step-login/).
- [Bitwarden: código de recuperación](https://bitwarden.com/help/two-step-recovery-code/).
- [VeraCrypt: tutorial de creación, montaje y desmontaje](https://veracrypt.io/en/Beginner%27s%20Tutorial.html).

## Cierre previsto

La práctica quedará completa cuando se verifique la protección de la bóveda, se compruebe la persistencia del archivo tras volver a montar el contenedor y se incorporen las evidencias. Hasta entonces no se afirma que los controles estén implementados.
