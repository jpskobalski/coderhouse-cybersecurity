# Guía de Autoprotección Digital

**Estudiante:** Juan Skobalski  
**Curso:** Ciberseguridad · Unidad 6 · Ejercicio 1  
**Estado:** reporte final de cuatro páginas.

## Entrega

- [PDF](output/pdf/Guia_Autoproteccion_Digital_Skobalski_Juan.pdf)
- [Fuente LaTeX editable](Guia_Autoproteccion_Digital_Skobalski_Juan.tex)
- [Captura de la práctica](capturas/01_privado_extension.png)

## Alcance y resultados

La práctica se realizó con **Zen, basado en Firefox**, y **Privacy Badger**. El reporte incluye una comparación entre navegación privada y VPN, sus límites, la evidencia visual y el análisis de una operación bancaria desde una red Wi-Fi pública.

La captura muestra el indicador de navegación privada, el icono de la extensión fijado en la barra y su panel activo, con un posible rastreador bloqueado. El estudiante confirmó que la visita privada no se agregó al historial y que también realizó la prueba con VPN. No se adjuntaron capturas de la comparación de IP: el reporte no atribuye direcciones, proveedor ni ubicación de salida.

## Estructura del reporte

1. Carátula.
2. Introducción, alcance y comparación de seis aspectos, incluidos IP y cifrado.
3. Evidencia, configuración reproducible y resultados.
4. Análisis del caso, recomendaciones, conclusión y referencias.

## Compilación

Desde esta carpeta, con una distribución LaTeX que incluya los paquetes del documento:

```powershell
pdflatex -interaction=nonstopmode -halt-on-error -output-directory=output/pdf Guia_Autoproteccion_Digital_Skobalski_Juan.tex
```

El PDF fue compilado y sus cuatro páginas se revisaron visualmente.
