---
titulo: Períodos académicos
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [periodos, ano-lectivo, calendario-academico]
---

# Períodos académicos

Año lectivo, bimestres, trimestres o semestres según el modelo del colegio.

## Estructura del año lectivo

Un año lectivo se compone de:

- **Una fecha de inicio y una fecha de cierre.**
- **N periodos académicos** consecutivos definidos por el colegio.
- Opcionalmente un **quinto periodo** que puede corresponder a una sumatoria de los anteriores u otro método de cálculo propio del colegio.
- Un **estado** del año lectivo: `Planificado`, `En curso`, `Cerrado`, `Archivado`.

El colegio define el número exacto de periodos en su [[../03-multi-tenancy/configuracion-por-colegio|configuración inicial]] (típicamente 4) y las fechas de inicio y cierre de cada uno.

## Tipos de período soportados

El sistema soporta dos tipos de calendario académico:

### Calendario A

- **Cobertura:** febrero a noviembre dentro de un mismo año calendario.
- **Identificación del año lectivo:** "2026" (año calendario simple).
- **Mercado típico:** colegios oficiales y muchos privados en Colombia.
- **No cruza** el cambio de año calendario.

### Calendario B

- **Cobertura:** septiembre a junio cruzando dos años calendario.
- **Identificación del año lectivo:** "2025-2026" — siempre con el formato "AAAA-AAAA". Nunca un año simple.
- **Mercado típico:** exclusivo de colegios privados.
- **Cruza el cambio de año calendario** (diciembre/enero).

La identificación "AAAA-AAAA" del Calendario B aplica en **toda la interfaz, reportes y documentos oficiales** generados por el sistema.

## Calendario B — cruce de años

### Periodos que cruzan diciembre y enero

Los periodos académicos que abarcan el cambio de año calendario se tratan como parte continua del mismo año lectivo. El sistema **no los divide ni los trata como pertenecientes a dos años distintos**. Las fechas, los reportes y la visualización respetan esta continuidad.

Ejemplo: un periodo que va del 15 de noviembre de 2025 al 15 de febrero de 2026 es **un solo periodo** del año lectivo "2025-2026".

### Reportes por año calendario vs año lectivo

Algunos reportes pueden requerirse filtrando por **año calendario** (enero a diciembre) en lugar de por año lectivo. El sistema soporta ambos criterios de filtro de manera independiente.

| Criterio | Caso de uso |
| --- | --- |
| Año lectivo ("2025-2026") | Reportes académicos completos: notas, asistencia, boletines, promoción. |
| Año calendario ("2026") | Reportes financieros, conciliación contable, reportes a entidades fiscales. |

### Coexistencia de procesos en junio

En el mes de junio, que es el mes de cierre del Calendario B, **coexisten dos procesos simultáneos**:

- **Cierre del año lectivo vigente:** proceso de promoción, generación de boletines finales y certificados.
- **Inicio del proceso de matrículas para el año lectivo siguiente.**

El sistema soporta que ambos procesos ocurran al mismo tiempo sin que interfieran entre sí. El año lectivo siguiente queda en estado `Planificado` mientras el actual se cierra; el proceso de matrícula opera contra el año `Planificado` y los procesos académicos contra el año `En curso`.

## Apertura y cierre de período

### Apertura

- Un periodo se abre automáticamente cuando llega su fecha de inicio configurada.
- El [[roles/02-coordinador-academico|Coordinador Académico]] puede adelantar la apertura manualmente si es necesario.
- A partir de la apertura, los docentes pueden registrar notas, asistencia y logros del periodo.

### Cierre

- El cierre de un periodo lo ejecuta el coordinador académico al finalizar las clases del periodo.
- Antes del cierre, el sistema valida que todos los docentes hayan registrado las notas finales de sus materias asignadas. Genera un reporte de pendientes.
- Al cierre del periodo:
  - Se calcula la nota final por materia según el método de aprobación configurado.
  - Se identifican los estudiantes que perdieron materias (candidatos a [[nivelaciones-y-habilitaciones|nivelación]]).
  - Quedan disponibles los boletines del periodo.
  - Se bloquea la edición de notas, asistencia y logros del periodo (excepto bajo intervención del superadmin con solicitud formal).

## Reglas para reportar fuera de período

- Una vez cerrado un periodo, ningún rol del tenant puede registrar notas, asistencia ni logros sobre fechas de ese periodo.
- La excepción es la apertura puntual de una **ventana de corrección** autorizada por el coordinador académico, que queda registrada en el log de auditoría con fecha de inicio, fecha de fin y motivo.

## Estados y transiciones

### Año lectivo

```
Planificado → En curso → Cerrado → Archivado
```

| Estado | Descripción |
| --- | --- |
| Planificado | Año lectivo configurado pero aún no iniciado. Permite preparación: plan de estudios, asignaciones, horarios, matrícula. |
| En curso | Año lectivo activo. Se registran notas, asistencia, observador y pagos. Solo puede haber un año lectivo `En curso` a la vez. |
| Cerrado | Proceso de promoción ejecutado. Datos inmutables. Sigue fácilmente accesible en la interfaz. |
| Archivado | Pasa cierta antigüedad definida por la plataforma. Modo de consulta más restringido pero nunca se elimina. |

### Periodo académico

```
Planificado → Abierto → Cerrado
```

| Estado | Descripción |
| --- | --- |
| Planificado | Periodo configurado pero aún no iniciado. |
| Abierto | Periodo en curso. Permite registro de notas, asistencia y logros. |
| Cerrado | Periodo finalizado. Datos inmutables. Boletines disponibles. |

## Reglas de negocio

- **RN-PA-001 — Un único año lectivo activo:** solo un año lectivo puede estar en estado `En curso` simultáneamente. El siguiente puede estar `Planificado` (caso Calendario B en junio).
- **RN-PA-002 — Calendario B usa formato AAAA-AAAA:** la identificación del año lectivo en Calendario B siempre se muestra con el formato "AAAA-AAAA" en interfaz, reportes y documentos oficiales.
- **RN-PA-003 — Periodos contiguos:** los periodos académicos son contiguos: la fecha de inicio del periodo N+1 es el día siguiente al cierre del periodo N.
- **RN-PA-004 — Cierre requiere notas completas:** el sistema alerta antes de cerrar un periodo si hay docentes con notas finales pendientes; el coordinador puede forzar el cierre asumiendo la responsabilidad.
- **RN-PA-005 — Cierre del año ejecuta promoción:** el cierre del año lectivo dispara el [[promocion-y-reprobacion|proceso de promoción automática]] que requiere validación del coordinador antes de quedar definitivo.
- **RN-PA-006 — Inmutabilidad post-cierre:** los datos de un periodo cerrado son inmutables; los datos de un año lectivo cerrado son **completamente inmutables** para todos los usuarios del tenant.
- **RN-PA-007 — Tipo de calendario inmutable:** el tipo de calendario (A o B) elegido en la configuración inicial no puede cambiarse mientras haya años lectivos activos o cerrados.
- **RN-PA-008 — Quinto periodo opcional:** el colegio decide si maneja un quinto periodo y su método de cálculo (sumatoria u otro). Esta configuración es por año lectivo.

## Notas y pendientes

- **[Configurable por colegio]** Antigüedad para que un año lectivo pase automáticamente de `Cerrado` a `Archivado`. Sugerencia inicial de la plataforma: 24 meses tras el cierre, modificable por el colegio.
- **[Resuelto en calificaciones.md]** La ventana de corrección tras cierre del periodo es configurable por colegio (activable, duración y alertas). Ver `RN-CL-030`.
