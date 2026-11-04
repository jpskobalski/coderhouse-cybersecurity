# Automatización del acceso a un contenedor VeraCrypt

**Estudiante:** Juan Skobalski

**Materia:** Ciberseguridad · Unidad 5 · Ejercicio 2

## Objetivo

Completar los comandos de montaje y desmontaje con la sintaxis Linux proporcionada por la consigna. Esta es una resolución escrita; los comandos no fueron ejecutados ni se verificó un contenedor real.

## Solución

```bash
# 1. Montar el contenedor
veracrypt --text --mount datos_confidenciales.hc /media/boveda --password="MiPasswordSuperSecreto" --pim=0 --keyfiles="" --protect-hidden=no

# 2. Desmontar el contenedor
veracrypt --text --dismount datos_confidenciales.hc
```

## Explicación

- `--text`: utiliza la interfaz de terminal.
- `--mount`: monta el archivo indicado en `/media/boveda`.
- `--password`: utiliza la contraseña ficticia suministrada por el ejercicio.
- `--pim=0`: utiliza el valor predeterminado del multiplicador de iteraciones.
- `--keyfiles=""`: indica que no se utilizan archivos llave.
- `--protect-hidden=no`: no activa la protección de un volumen oculto.
- `--dismount`: desmonta el contenedor indicado. No borra el archivo ni los datos almacenados.

La ruta del contenedor es relativa al directorio de trabajo. Estos comandos corresponden a Linux, no a la sintaxis de VeraCrypt para Windows.

## Consideración de seguridad

La contraseña publicada es exclusivamente la del ejemplo de clase. En uso real conviene introducir el secreto cuando la herramienta lo solicite, evitando dejarlo en la línea de comandos o en el historial. Antes de desmontar, deben cerrarse los archivos y aplicaciones que estén utilizando el volumen.
