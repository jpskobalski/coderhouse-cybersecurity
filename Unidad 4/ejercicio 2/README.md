# Clasificador básico de malware

Este ejercicio implementa una función de Python que clasifica reportes escritos por usuarios como:

- `Ransomware`
- `Spyware`
- `RAT`
- `Desconocido`

## Funcionamiento

La función convierte la descripción a minúsculas con `lower()` y después utiliza condiciones `if` para buscar palabras clave.

```python
resultado = clasificar_malware(
    "Me pide dinero para recuperar mis archivos encryptados"
)
print(resultado)  # Ransomware
```

Se agregaron algunos sinónimos en español para que la función también reconozca las descripciones utilizadas en el enunciado, como `cifrado`, `bitcoin`, `contraseña`, `cámara` y `control remoto`.

## Ejecución

Desde PowerShell:

```powershell
python "Unidad 4/ejercicio 2/clasificar_malware.py"
```

## Decisión ante múltiples coincidencias

La función retorna la primera categoría que coincide. El orden aplicado es Ransomware, Spyware y RAT. Esta regla mantiene la lógica simple, como corresponde al alcance introductorio del ejercicio.
