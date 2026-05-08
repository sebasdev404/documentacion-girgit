---
titulo: Promoción y reprobación
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [promocion, reprobacion, cierre-de-ano]
---

# Promoción y reprobación

Proceso ejecutado al cierre del año lectivo que determina, para cada estudiante, si avanza al grado siguiente o si repite el grado actual.

## Proceso automático

Al cierre del año lectivo el sistema ejecuta el proceso de promoción automática. Evalúa a cada estudiante según las reglas configuradas por el colegio:

- **Cuántas materias puede perder y aún ser promovido.**
- **Si existen materias que no se pueden perder bajo ninguna circunstancia** (ej. el colegio puede definir que perder Matemáticas implica reprobación automática).
- **El promedio general mínimo requerido** para pasar.

El sistema toma como insumo:

- Las notas finales de cada materia.
- Los resultados de [[nivelaciones-y-habilitaciones|nivelaciones y habilitaciones]].
- Las decisiones del [[consejo-academico|consejo académico]] cuando aplican.

## Validación antes del cierre

El sistema genera un **listado completo de estudiantes promovidos y reprobados** para revisión del [[roles/02-coordinador-academico|Coordinador Académico]] **antes** de hacer el proceso definitivo.

El coordinador puede:

- Consultar el detalle de cada caso.
- Ver los que pasaron por consejo académico.
- Validar caso por caso o aceptar el listado completo.

**Solo después de que el coordinador valida el listado**, el proceso queda cerrado.

## Cierre del año y preparación del siguiente

Una vez cerrado el año:

- El sistema prepara la estructura del año lectivo siguiente.
- Los estudiantes promovidos avanzan al grado siguiente y quedan en **espera de asignación de grupo**.
- Los reprobados quedan registrados en el mismo grado para el año siguiente.
- Los datos del año cerrado quedan en **modo histórico inmutable** (ver [[../11-plataforma-y-operacion/historico-y-anos-cerrados|Histórico y años cerrados]]).

## Estados y transiciones

### Año lectivo (vista parcial centrada en este proceso)

```
En curso → Cierre iniciado → Promoción calculada (borrador) → Validada → Cerrado
```

### Resultado por estudiante

```
Pendiente → Calculado automáticamente → Validado / sobreescrito por consejo → Definitivo
```

## Datos involucrados

- Notas finales del año por materia y estudiante.
- Resultados de habilitaciones.
- Decisiones del consejo académico.
- Reglas de promoción configuradas por el colegio.
- Resultado por estudiante (Promovido / Reprobado / Promovido con condición).
- Compromiso si aplica (Promovido con condición).
- Grado destino para el año siguiente.

## Estudiantes egresados

Los estudiantes que terminan el último grado del colegio (típicamente Undécimo en Colombia) y aprueban quedan marcados como **Egresados**:

- No se les asigna grado para el año siguiente.
- Pueden seguir consultando su histórico (boletines, certificados) según la configuración del colegio.
- El colegio puede generar el certificado de bachillerato u otro documento equivalente.

## Reglas de negocio

- **RN-PR-001 — Cálculo automático con reglas configurables:** el cálculo respeta las reglas del colegio (materias máximas perdibles, materias intransigibles, promedio mínimo).
- **RN-PR-002 — Validación obligatoria del coordinador:** el proceso no queda cerrado hasta que el coordinador valida el listado.
- **RN-PR-003 — Decisión del consejo prevalece:** las decisiones del consejo académico sobre casos individuales sobreescriben el cálculo automático.
- **RN-PR-004 — Cierre dispara preparación del año siguiente:** al cerrar el año, el sistema crea la estructura del año siguiente con los estudiantes promovidos y reprobados ya distribuidos por grado.
- **RN-PR-005 — Inmutabilidad del año cerrado:** una vez cerrado, el año lectivo y todos sus datos son inmutables (excepto bajo intervención del superadmin con solicitud formal documentada).
- **RN-PR-006 — Asignación de grupo posterior:** los estudiantes promovidos quedan en espera de asignación de grupo; el coordinador académico asigna grupos antes del inicio del año siguiente.
- **RN-PR-007 — Egresados sin grado destino:** los estudiantes que terminan el último grado y aprueban quedan marcados como egresados, sin asignación al año siguiente.
- **RN-PR-008 — Cierre sin habilitaciones pendientes:** el sistema bloquea el cierre definitivo del año si hay habilitaciones pendientes de registrar.

## Notas y pendientes

- **[Decisión tomada]** El sistema ofrece **plantillas predefinidas de reglas de promoción** (ej. "máximo N materias perdidas", "ninguna materia con nota inferior a X", "promedio mínimo Y") y permite a cada colegio definir una **regla custom** combinable. Regla: **RN-PR-100 — Plantillas predefinidas + regla custom por colegio**.
- **[Decisión tomada]** La **reapertura del cierre académico** por error material la puede ejecutar **cualquier rol con el permiso `cierre.reabrir`** (rector, coordinador académico, secretaria u otro definido por la matriz de permisos del colegio), siempre con **justificación obligatoria** y **log inmutable** de auditoría. No se restringe al superadmin de plataforma. Regla: **RN-PR-101 — Reapertura por permiso, no por rol fijo, con justificación y log inmutable**.
- **[Pendiente — producto]** Comportamiento si un estudiante egresado quiere matricularse nuevamente al colegio: debería reactivarse su expediente histórico (no crearse uno nuevo) y matricularlo en el grado correspondiente, conservando todo el historial.
