---
titulo: Validaciones
modulo: reglas-de-negocio
tipo: regla
estado: borrador
tags: [validaciones, reglas]
---

# Validaciones

Catálogo de validaciones que el sistema aplica en formularios y flujos. Las validaciones triviales de campo (no vacío, longitud máxima) se omiten salvo cuando tienen un límite de negocio relevante.

## Por entidad

### Estudiante

| Campo | Validación | Mensaje |
| --- | --- | --- |
| Identificación | Única dentro del tenant. | "Ya existe un estudiante con esta identificación". |
| Fecha de nacimiento | Coherente con el grado al que se matricula según rangos de edad configurados (advertencia, no bloqueo por defecto). | "La edad sugiere otro grado". |
| Acudiente | Al menos un acudiente con datos completos. | "Debe registrar al menos un acudiente". |
| EPS / tipo de sangre | Requeridos en colegios que lo configuran. | "Campo requerido por su colegio". |

### Acudiente

| Campo | Validación | Mensaje |
| --- | --- | --- |
| Correo | Formato de email + único por usuario en la plataforma o reutilizable según política. | "Correo no válido o ya registrado". |
| Teléfono | Formato del país. | "Teléfono no válido". |
| Identificación | Única dentro del tenant. | "Ya existe un acudiente con esta identificación". |

### Docente

| Campo | Validación | Mensaje |
| --- | --- | --- |
| Asignación a asignatura | El docente debe tener perfil habilitado para el área. | "El docente no está habilitado para esta área". |
| Carga horaria | No supera la máxima configurada por el colegio. | "Carga horaria excedida". |

### Calificación

| Campo | Validación | Mensaje |
| --- | --- | --- |
| Valor de la nota | Dentro del rango de la escala vigente. | "La nota debe estar entre {min} y {max}". |
| Suma de pesos por área | Igual a 100% (con tolerancia 0.01). | "La suma de pesos no es 100%". |
| Edición tras cierre del periodo | Bloqueada salvo permiso. | "El periodo está cerrado". |

### Asistencia

| Campo | Validación | Mensaje |
| --- | --- | --- |
| Fecha de la inasistencia | No futura. | "No se permiten inasistencias futuras". |
| Tipo de inasistencia | Dentro del catálogo configurado. | "Tipo no válido". |
| Justificación | Dentro de la ventana configurada (ej. 5 días). | "Fuera de la ventana de justificación". |

### Matrícula

| Campo | Validación | Mensaje |
| --- | --- | --- |
| Documentos requeridos | Todos cargados antes de confirmar. | "Faltan documentos requeridos". |
| Paz y salvo del año anterior | Vigente, salvo excepción. | "No tiene paz y salvo vigente". |
| Cupo del grupo | No supera el máximo configurado. | "El grupo no tiene cupo". |

### Pago

| Campo | Validación | Mensaje |
| --- | --- | --- |
| Monto | Mayor que cero, exacto al cobro generado salvo abonos permitidos. | "Monto no válido". |
| `transactionId` de pasarela | Único. | "Pago duplicado". |
| Anulación | Solo si está en estado válido para anular y con motivo. | "No se puede anular este pago". |

### Comunicado / publicación

| Campo | Validación | Mensaje |
| --- | --- | --- |
| Alcance vs rol del autor | El autor solo puede dirigirse a alcances permitidos por su rol. | "No tiene permiso para publicar a este alcance". |
| Tamaño de adjuntos | Dentro del límite y de la cuota disponible. | "Adjunto demasiado grande o cuota agotada". |

### Configuración del colegio

| Campo | Validación | Mensaje |
| --- | --- | --- |
| Periodos académicos | No se solapan; suman 100% del año. | "Los periodos no son consistentes". |
| Pesos por área / asignatura | Suman 100%. | "Los pesos no suman 100%". |
| Escalas de calificación | Rangos contiguos sin huecos ni traslapes. | "La escala tiene huecos o solapes". |

## Validaciones cruzadas (entre campos)

- **Sede + Grado + Grupo:** el grupo seleccionado debe pertenecer al grado y la sede.
- **Periodo + Fecha de calificación:** la fecha de captura está dentro del rango del periodo o de su ventana extendida.
- **Estudiante + Grupo:** el estudiante está matriculado en ese grupo en el año lectivo vigente.
- **Concepto + Estudiante + Beca:** la beca cubre los conceptos correctos antes de generar la cuota.
- **Acudiente + Estudiante:** un acudiente solo recibe / paga por estudiantes que tiene vinculados.

## Validaciones de negocio (no triviales)

- **Cupo del grupo:** matricular un nuevo estudiante no excede el máximo del grupo (configurable).
- **Carga del docente:** asignar una asignatura no excede la carga máxima del docente.
- **Choque de horarios:** una clase no puede solapar la franja del mismo docente o del mismo grupo.
- **Choque de espacios:** un aula / laboratorio no puede tener dos clases simultáneas.
- **Promoción:** un estudiante con áreas reprobadas por encima del límite no puede promocionarse automáticamente.
- **Cierre de año:** no se cierra el año si quedan calificaciones, asistencia o pagos en estados intermedios.

## Notas y pendientes

- Centralizar los mensajes de validación en un catálogo de internacionalización.
- Definir cuáles validaciones se ejecutan en frontend y cuáles solo en backend (defensa en profundidad).
