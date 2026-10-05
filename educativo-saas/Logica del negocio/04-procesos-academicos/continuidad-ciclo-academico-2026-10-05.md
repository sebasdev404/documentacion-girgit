---
titulo: Continuidad del ciclo académico — decisiones de octubre de 2026
modulo: procesos-academicos
tipo: plan-de-continuidad
estado: planificado
tags: [siee, boletines, promocion, asistencia, continuidad]
---

# Continuidad del ciclo académico — 5 de octubre de 2026

Este documento sirve para retomar el trabajo en otro ordenador. **Registra decisiones y pendientes; no certifica que las funciones planificadas estén implementadas.** Las reglas detalladas permanecen en [[boletines-y-reportes-academicos|Boletines]], [[promocion-y-reprobacion|Promoción]], [[asistencia|Asistencia]], [[admisiones|Admisiones]] y [[matriculas|Matrícula]].

## Estado comprobado

- El boletín existente es una **vista previa**. Las planillas y el SIEE calculan las definitivas con precisión interna; solo se redondea el valor publicado. La regla vigente deja el cinco exacto hacia abajo al mostrar un decimal: `3.650 → 3.6`, mientras que `3.66875 → 3.7`.
- En el tenant **local** de Inmaculada, la revisión de 195 matrículas activas comprobó 2.145 definitivas anuales de asignatura y 1.800 de área sin inconsistencias frente a los valores exactos y los pesos configurados. Promediar las cifras de período ya mostradas con un decimal produciría un resultado distinto en 305 definitivas de asignatura; **no se cambió la fórmula ni las notas**.
- La valoración por imágenes/caritas de preescolar ya existe en el código de trabajo y en la base local, pero debe publicarse, instalarse en el otro entorno y verificarse allí antes de considerarla disponible en ese ordenador.
- Los datos de auditoría de Inmaculada son **sintéticos y locales**. El cuarto período permanece abierto; hay actividades de auditoría fechadas después del 3 de octubre de 2026. Los scripts de carga no son migraciones ni deben ejecutarse automáticamente para otros colegios. Git transporta los scripts, **no** los registros PostgreSQL ni los respaldos locales.

## Siguientes entregas acordadas

1. **Boletín preliminar:** mostrar el peso anual en cada encabezado de período (`Primer período · 25 %`). Solo mostrar peso de asignatura dentro del área si el SIEE usa promedio ponderado; con promedio simple no hay porcentajes por asignatura. No añadir el desglose técnico de valores internos del P5.
2. **Revisión de promoción:** ordenar la selección de materias no reprobables en una tabla clara, con selección individual y «Seleccionar todas»; filtrar matrículas activas por grupo. Conservar los permisos y reglas de revisión actuales.
3. **Ensayo aislado del cierre académico:** comprobar recuperación/nivelación, política de promoción, decisiones y transición del año de extremo a extremo en datos controlados. No cerrar el cuarto período activo de Inmaculada únicamente para hacer una prueba.
4. **Boletín oficial:** diseñar plantillas configurables, revisión/aprobación, PDF persistente y versiones históricas. La aprobación confirma el documento que se publicará; no edita las notas. Faltan decisiones sobre alcance de aprobación (individual/grupo/lote) y responsabilidades concretas entre Rector, dirección de grupo y coordinación.
5. **Asistencia:** configurar y registrar por franja/clase del horario, también sin bloques fijos. Dos franjas de la misma materia con dos ausencias generan dos inasistencias. Definir por colegio los umbrales, períodos de acumulación, justificaciones, tardanzas y efectos sobre aprobación, boletín y promoción.
6. **Admisiones y matrícula integral:** mantener aparte del próximo lote. La matrícula académica actual solo relaciona estudiante, grupo y año; el flujo integral de solicitud, documentos, admisión y pago todavía no está acordado para implementación.

## Antes de trabajar en el otro ordenador

- Sincronizar por separado las ramas publicadas de `colegio-saas-backend` y `colegio-saas-frontend` (`pedro-dev`) y de `documentacion-girgit` (`main`). No interpretar este plan como código ya desplegado.
- Aplicar las migraciones tenant pendientes con el procedimiento normal de respaldo y despliegue; verificar tanto colegios existentes como el alta de uno nuevo. No ejecutar scripts de auditoría de Inmaculada sobre otra institución.
- Si se necesitan los **mismos registros** de Inmaculada en el otro ordenador, transferir/restaurar un respaldo de PostgreSQL por un canal seguro. Clonar Git por sí solo no los transporta.
- Antes de llamar «oficial» a un boletín, exigir pruebas de permisos, cálculo, cierre, PDF, histórico y corrección auditada. No publicar datos sintéticos como resultados académicos reales.
