# Capturas requeridas

Toma las capturas dentro de la VM `ubuntu-coder` o desde VirtualBox según corresponda. Usa la herramienta Recortes de Windows (`Win + Shift + S`) y guarda cada archivo PNG con el nombre exacto.

## 1. Red NAT

1. Apaga completamente la VM.
2. En VirtualBox, selecciona `ubuntu-coder`.
3. Abre **Configuración > Red > Adaptador 1**.
4. Activa **Habilitar adaptador de red**.
5. En **Conectado a**, elige **NAT**.
6. En **Avanzadas > Reenvío de puertos**, verifica que la lista esté vacía.
7. Vuelve a la pantalla principal del adaptador y toma una captura donde se vean el nombre de la VM y el modo NAT.

Guárdala como `01-red-nat.png`.

## 2. Usuario sin privilegios administrativos

Desde la cuenta administradora de Ubuntu, crea una cuenta separada:

```bash
sudo adduser practicas
```

No agregues esa cuenta al grupo `sudo`. Cierra sesión, entra como `practicas` y ejecuta:

```bash
whoami
id
sudo -l
```

La salida de `id` no debe incluir el grupo `sudo`. El último comando debe indicar que `practicas` no puede ejecutar sudo. Toma la captura después de que aparezca el resultado; no captures el momento en que escribes la contraseña.

Guárdala como `02-usuario-sin-privilegios.png`.

## 3. Permisos con `ls -l`

En la sesión de `practicas`, ejecuta:

```bash
touch ~/evidencia-lab.txt
chmod 640 ~/evidencia-lab.txt
ls -l ~/evidencia-lab.txt
```

La línea debe comenzar con `-rw-r-----` y mostrar `practicas` como propietario. Amplía la terminal lo suficiente para que toda la salida resulte legible.

Guárdala como `03-permisos-ls-l.png`.

## 4. Ubuntu actualizado

Vuelve a la cuenta administradora y ejecuta:

```bash
sudo apt update
sudo apt full-upgrade
sudo apt update
```

Acepta la instalación si APT lo solicita. Toma la captura al finalizar la última consulta, cuando se vea que los paquetes están actualizados. Si Ubuntu está en inglés, es normal que el mensaje aparezca como `All packages are up to date`.

Guárdala como `04-apt-actualizado.png`.

## 5. Snapshot de hardening

1. Apaga la VM desde Ubuntu; no la dejes en estado guardado.
2. En VirtualBox, abre la vista **Instantáneas/Snapshots**.
3. Crea una instantánea llamada exactamente `Clean Install - Hardening applied`.
4. Como descripción puedes escribir `Hardening Inicial: NAT, usuario limitado, permisos y actualizaciones aplicadas`.
5. Toma una captura donde se vean la VM y el nombre completo de la instantánea.

Guárdala como `05-snapshot-hardening.png`.

## Revisión antes de copiar las imágenes

- Evita capturar contraseñas o cuadros de autenticación.
- No muestres tokens, claves SSH, direcciones de correo ni archivos personales.
- Conserva visible la aplicación o terminal que da contexto a cada evidencia.
- No recortes tanto que desaparezcan el nombre de la VM, el comando o el resultado.
- Usa PNG y evita fotos tomadas con el teléfono.
