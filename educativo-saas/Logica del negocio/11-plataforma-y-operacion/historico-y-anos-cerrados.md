---
titulo: Histórico y años cerrados
modulo: 11-plataforma-y-operacion
tipo: regla
estado: borrador
tags: [historico, cierre-de-año, archivado, inmutabilidad]
---

# Histórico y años cerrados

## Descripción

Cómo la plataforma trata la información de **años lectivos cerrados**: qué se preserva, qué se puede modificar, quién puede consultar y bajo qué condiciones.

## Cierre de año

El cierre de año lectivo es un proceso explícito que ejecuta el [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Administrador del Colegio]] cuando todos los procesos académicos del año han concluido:

1. Se confirma la promoción / reprobación de todos los estudiantes (ver [[../04-procesos-academicos/promocion-y-reprobacion|Promoción y reprobación]]).
2. Se generan los boletines finales y los certificados.
3. Se cierran los pagos y la conciliación financiera.
4. Se ejecuta el cierre formal: el sistema marca el año como **cerrado**.

Tras el cierre, los datos del año se vuelven **inmutables** salvo excepciones autorizadas.

## Datos preservados

Tras el cierre se preservan:

- Matrículas y estados de matrícula.
- Calificaciones por periodo y consolidadas.
- Asistencia y justificaciones.
- Observador del estudiante.
- Boletines emitidos.
- Pagos realizados, anulados, en mora.
- Comunicaciones, agenda y citaciones del año.
- Configuración vigente del año (escalas, áreas, asignaturas, plan de estudios, calendario).

## Inmutabilidad

- No se modifican notas, asistencia ni observaciones de un año cerrado.
- Las correcciones excepcionales requieren reapertura formal del año (ver siguiente sección).
- La consulta sigue habilitada para todos los roles autorizados.

## Reapertura excepcional

- Solo el [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Administrador del Colegio]] puede solicitarla.
- Requiere motivo escrito y acta del [[../04-procesos-academicos/consejo-academico|Consejo Académico]] cuando la modificación es académica.
- La reapertura es **acotada**: solo a un estudiante o a un proceso puntual; no se reabre todo el año.
- Toda modificación durante una reapertura queda en el [[log-de-auditoria|log]] con el motivo y los soportes.
- Tras aplicar la corrección, el año se vuelve a cerrar.

## Configuración por año

- La plataforma versiona la configuración relevante por año: escalas de calificación, áreas, plan de estudios, periodos, calendario, plantillas de boletín.
- Un cambio aplicado en el año vigente NO afecta los años cerrados.
- Esto garantiza que un boletín reimpreso de un año cerrado conserve los criterios originales.

## Acceso a información histórica

| Rol | Acceso |
| --- | --- |
| Administrador / Rector | Total, todos los años. |
| Secretaría | Total, todos los años. |
| Coordinación | Total, todos los años para los que estuvo activa. |
| Docente | Sus propios datos: grupos en los que enseñó, observaciones que registró. |
| Director de grupo | Datos del grupo dirigido en cada año. |
| Estudiante (operado por su acudiente) | Datos del estudiante: notas, asistencia, boletines, pagos. |
| Egresado | Acceso al portal con sus datos históricos (boletines y certificados). |

## Egresados

- Al graduarse, el estudiante pasa al rol de [[../02-usuarios-roles-y-permisos/roles/14-egresado\|Egresado]].
- Conserva acceso a su histórico (boletines, certificados, paz y salvo).
- Puede solicitar certificaciones desde su portal sin necesidad de presentarse físicamente.

## Reglas de negocio

- **RN-HA-001 — Cierre formal y único:** un año lectivo se cierra una vez; el cierre es explícito y registrado.
- **RN-HA-002 — Inmutabilidad por defecto:** los datos del año cerrado no se modifican.
- **RN-HA-003 — Reapertura motivada:** la reapertura requiere motivo, autorización y queda en log.
- **RN-HA-004 — Configuración versionada por año:** un cambio en la configuración no altera años cerrados.
- **RN-HA-005 — Egresados con portal:** los egresados conservan acceso a su histórico.
- **RN-HA-006 — Boletines reimprimibles:** la reimpresión de boletines de años anteriores usa la configuración del año, no la actual.

## Notas y pendientes

- **[Decisión tomada]** **Reapertura tras cierre**:
  - Un **periodo académico** puede reabrirse dentro de una **ventana configurable** definida por rectoría o coordinación académica (sugerencia inicial: **15 días** posteriores al cierre del periodo).
  - Una vez el **año lectivo completo** se cierra de forma **definitiva**, **no se permite reapertura operativa**, salvo **intervención extraordinaria del superadministrador de plataforma** con auditoría y trazabilidad completa.
  Regla: **RN-HC-280 — Reapertura intra-ventana por rol con permiso; reapertura post-cierre anual solo por superadmin con auditoría**.
- **[Decisión tomada]** **Solicitudes de certificados de egresados**: el sistema soporta **cobro por certificado** a egresados, **configurable por colegio** (precio y modalidad: incluido en convenio, cobrado al egresado, o gratuito). Regla: **RN-HC-281 — Certificados de egresados con tarifa y modalidad configurables por colegio**.
