---
titulo: Boletines y reportes académicos
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [boletines, reportes, proceso]
---

# Boletines y reportes académicos

## Descripción

Proceso de generación del documento PDF que consolida el desempeño académico del estudiante en un periodo o al cierre del año lectivo. Es el documento más visible para acudientes y se entrega siempre tras cada cierre de periodo.

## Tipos de boletín

| Tipo | Descripción |
| --- | --- |
| Boletín parcial | Generado al cierre de cada periodo académico durante el año lectivo. |
| Boletín final | Generado al cierre del año lectivo, con la nota definitiva de cada materia y el resultado de promoción. |
| Consolidado | Documento que reúne todos los periodos en una vista única. |

## Plantillas

- El sistema ofrece un conjunto de **plantillas base** de boletín en HTML y CSS.
- El colegio selecciona una plantilla y la personaliza con su logo, colores institucionales y los campos que desea mostrar u ocultar.
- Si el colegio requiere una plantilla **completamente personalizada** con un diseño propio, se trata como servicio adicional: se diseña una vez y se carga en el sistema de ese tenant.

### Versionado de plantillas

Las plantillas y configuraciones del boletín se versionan. Esto garantiza que los boletines de años anteriores siempre se vean exactamente como se veían en el momento de su emisión original, con la plantilla y la configuración vigente en ese entonces, **no con la actual**.

## Contenido del boletín

Por defecto el boletín incluye:

- Datos del estudiante (nombre, documento, grado, grupo, foto).
- Periodo académico (o consolidado del año si es final).
- Cada materia con su nota final.
- Logros alcanzados por materia.
- Observaciones escritas por el docente de cada materia.
- Observación general escrita por el [[roles/07-director-de-grupo|Director de Grupo]].
- Registro de inasistencias por materia y total del periodo.
- Nota de comportamiento si el colegio la maneja.
- Logo y datos institucionales del colegio.

El colegio configura qué secciones aparecen y cuáles se ocultan.

## Generación del boletín

1. Al cierre del periodo, el sistema marca los boletines como "disponibles para generación".
2. El [[roles/07-director-de-grupo|Director de Grupo]] (con permiso) o el [[roles/02-coordinador-academico|Coordinador]] dispara la generación para todo el grupo.
3. El sistema arma cada boletín aplicando la plantilla, los datos del estudiante y la configuración vigente.
4. Genera el archivo PDF y lo almacena asociado al estudiante y al periodo.
5. Notifica al estudiante (y al acudiente) que su boletín está disponible.

## Aprobación / firma del boletín

- El director de grupo revisa el boletín antes de marcarlo como definitivo (opcional según configuración).
- El coordinador académico puede ejecutar una validación consolidada antes de la entrega masiva.
- Una vez marcado como entregado, el boletín queda accesible para descarga del estudiante.

## Confirmación digital del estudiante

Si el colegio lo exige, el estudiante debe **confirmar el boletín digitalmente** desde su portal antes de que quede como entregado. El sistema registra la fecha, hora e IP de esa confirmación.

## Bloqueo por paz y salvo

El sistema puede bloquear la disponibilidad del boletín si el estudiante tiene un [[../06-monetizacion-y-pagos/paz-y-salvo|paz y salvo]] pendiente, según la configuración del colegio.

## Distribución a padres y estudiantes

- El boletín está disponible en el portal del estudiante y del acudiente.
- El sistema envía notificación por correo y por portal cuando el boletín está disponible.
- El acudiente puede descargar el PDF en cualquier momento si no hay bloqueo por paz y salvo.

## Otros reportes académicos

Más allá del boletín por estudiante, el sistema genera:

- **Consolidado de notas por grupo** — PDF con todas las notas de todas las materias del grupo en un periodo. Para uso del director de grupo y coordinación.
- **Certificado de notas final del año** — documento oficial al cierre del año.
- **Constancia de estudio** — documento que acredita la matrícula activa del estudiante.

Ver [[../09-reportes-y-analitica/reportes-academicos|Reportes académicos]] y [[../11-plataforma-y-operacion/gestion-documental|Gestión documental]].

## Reglas de negocio

- **RN-BR-001 — Generación tras cierre del periodo:** los boletines parciales solo pueden generarse después del cierre del periodo correspondiente.
- **RN-BR-002 — Versionado fiel:** la regeneración de un boletín histórico usa la plantilla y configuración vigente al momento de su emisión original, no la actual.
- **RN-BR-003 — Bloqueo por paz y salvo configurable:** el bloqueo de boletín por paz y salvo es configurable por el colegio. Por defecto los boletines están disponibles.
- **RN-BR-004 — Confirmación digital opcional:** la confirmación digital del boletín por parte del estudiante es opcional, configurable por el colegio.
- **RN-BR-005 — PDF persistente:** los PDFs generados se almacenan y consumen cuota del tenant. Si el archivo se pierde, se regenera con fidelidad.
- **RN-BR-006 — Personalización total bajo servicio:** una plantilla completamente personalizada es servicio adicional fuera del autoservicio.

## Notas y pendientes

- Definir límites de personalización autoservicio (qué puede tocar el colegio sin servicio externo).
- Validar firma digital adicional para certificados oficiales (firma del rector, sellos).
