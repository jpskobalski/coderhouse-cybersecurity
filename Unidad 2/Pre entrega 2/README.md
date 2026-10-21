# Preentrega 2: laboratorio seguro con Ubuntu

**Estudiante:** Juan Skobalski  
**Curso:** Ciberseguridad  
**Máquina virtual:** `ubuntu-coder`  
**Sistema invitado:** Ubuntu Linux

## Objetivo

Documentar una máquina virtual preparada para prácticas iniciales de ciberseguridad mediante aislamiento de red, menor privilegio, permisos de archivos, actualización del sistema y una instantánea de recuperación.

El reporte se genera desde [`Reporte_Laboratorio_Seguro_Skobalski_Juan.tex`](Reporte_Laboratorio_Seguro_Skobalski_Juan.tex). Las imágenes se insertan automáticamente al guardarlas en [`capturas`](capturas/) con los nombres indicados.

## Evidencias necesarias

| Archivo | Qué debe demostrar |
| --- | --- |
| `01-red-nat.png` | Adaptador 1 de VirtualBox conectado a **NAT**. |
| `02-usuario-sin-privilegios.png` | Usuario `practicas`, sus grupos y ausencia de autorización para usar `sudo`. |
| `03-permisos-ls-l.png` | Salida de `ls -l` para `evidencia-lab.txt` con permisos `-rw-r-----`. |
| `04-apt-actualizado.png` | Consulta de repositorios y estado actualizado después de ejecutar APT. |
| `05-snapshot-hardening.png` | Snapshot denominado **Clean Install - Hardening applied**. |

Las capturas anteriores de **Solo-Anfitrión** e **Instalación Base Limpia** documentan el ejercicio 1, pero no satisfacen literalmente la configuración ni el nombre pedidos en esta preentrega. Deben tomarse nuevamente.

## Guía rápida

Las instrucciones completas para preparar cada pantalla están en [`capturas/README.md`](capturas/README.md). No deben aparecer contraseñas, tokens, claves privadas ni información personal innecesaria.

## Estado del documento

Mientras falte una captura, la carátula mostrará **BORRADOR - EVIDENCIAS PENDIENTES** y el lugar correspondiente aparecerá como un recuadro. Cuando existan las cinco imágenes, cambiará automáticamente a **REPORTE CON EVIDENCIAS COMPLETAS**.

## Salida

El PDF final se guarda en:

`output/pdf/Reporte_Laboratorio_Seguro_Skobalski_Juan.pdf`

## Checklist

- [x] La red de VirtualBox figura en modo NAT.
- [ ] No existen reglas de reenvío de puertos.
- [x] El usuario de prácticas no pertenece al grupo `sudo`.
- [x] La captura de permisos muestra `ls -l` y `-rw-r-----`.
- [x] APT finalizó la actualización y documentó 15 paquetes diferidos por `phasing`.
- [x] El snapshot tiene el nombre solicitado.
- [x] Las cinco capturas son legibles y no exponen secretos.
- [x] El PDF final fue revisado y exportado.
