# Reporte de Hardening en Windows

**Estudiante:** Juan Skobalski  
**Curso:** Ciberseguridad  
**Estado:** preparación de evidencias

## Objetivo

Aplicar medidas básicas de endurecimiento en una máquina virtual de Windows y documentar cómo cada cambio reduce la superficie de ataque o limita el impacto de una cuenta comprometida.

> La práctica debe realizarse dentro de una VM de Windows. Las evidencias de la entrega anterior corresponden a Ubuntu y no demuestran los controles solicitados en esta consigna.

## Controles que deben aplicarse

### 1. Usuario estándar

Crear una cuenta denominada `UsuarioSeguro` —o un nombre equivalente— y comprobar que su tipo sea **Usuario estándar**, sin privilegios de administrador.

**Fundamento:** una cuenta de uso diario con permisos limitados aplica el principio de menor privilegio. Si una aplicación maliciosa se ejecuta en esa sesión, no obtiene automáticamente permisos administrativos sobre todo el sistema.

**Evidencia requerida:** captura de *Configuración > Cuentas > Otros usuarios* donde se vean el usuario y su tipo de cuenta. No incluir contraseñas, preguntas de recuperación ni otra información sensible.

### 2. Windows Update

Abrir Windows Update, buscar actualizaciones e instalar las que correspondan. Reiniciar la VM si Windows lo solicita.

**Fundamento:** las actualizaciones corrigen vulnerabilidades conocidas y reducen la posibilidad de que un atacante aproveche fallas para las que ya existe un parche.

**Evidencia requerida:** captura donde se vea que Windows está buscando actualizaciones o que el sistema se encuentra actualizado.

### 3. Desactivación de SMB 1.0/CIFS

Abrir **Activar o desactivar las características de Windows**, localizar **Compatibilidad con el protocolo para compartir archivos SMB 1.0/CIFS** y comprobar que la casilla esté desmarcada.

**Fundamento:** SMB 1.0 es un protocolo heredado que aumenta la superficie de ataque. Si ninguna aplicación antigua lo requiere, mantenerlo deshabilitado evita exponer funciones innecesarias de compartición de archivos.

**Evidencia requerida:** captura legible de la ventana de características de Windows donde SMB 1.0/CIFS aparezca desmarcado.

## Evidencias pendientes

Guardar las imágenes dentro de [`capturas`](capturas/) usando estos nombres:

1. `01-usuario-estandar.png`
2. `02-windows-update.png`
3. `03-smb1-deshabilitado.png`

## Entregable final

El reporte se genera desde:

`Reporte_Hardening_Skobalski_Juan.tex`

El archivo LaTeX inserta automáticamente las capturas cuando se guardan con los nombres indicados. Mientras falte alguna imagen, el PDF se identifica como borrador y muestra un recuadro de evidencia pendiente.

El documento de entrega se guarda como:

`Reporte_Hardening_Skobalski_Juan.pdf`

El reporte final incluirá una carátula, una introducción breve, las tres evidencias con su explicación técnica y una conclusión sobre la reducción de la superficie de ataque.

## Checklist

- [x] La práctica fue realizada en una VM de Windows y no en el equipo host.
- [x] Existe una cuenta estándar separada de la cuenta administradora.
- [x] Windows Update fue ejecutado y documentado.
- [x] SMB 1.0/CIFS aparece deshabilitado.
- [x] Las capturas son legibles y no exponen contraseñas ni datos sensibles.
- [x] Cada captura está acompañada por una explicación del cambio y su propósito.
- [x] El documento final fue exportado a PDF con la nomenclatura indicada.

## Precaución operativa

Antes de cambiar usuarios o características del sistema, conviene crear una instantánea de la VM y confirmar que la contraseña de la cuenta administradora funciona. La cuenta administradora no debe eliminarse ni degradarse durante esta práctica.
