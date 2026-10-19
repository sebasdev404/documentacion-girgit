---
titulo: Promoción y reprobación
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [promocion, reprobacion, cierre-de-ano]
---

# Promoción y reprobación

> **Actualización vigente (15-10-2026):** la promoción se determina por notas y reglas configuradas por el colegio. No se decide por consenso ni votación y un consejo académico no puede sobreescribir el cálculo. Las propuestas históricas de esta página sobre consejo decisorio, promoción condicionada o traslado automático al año siguiente no están aprobadas para implementación. La revisión autorizada valida los insumos, sin cambiar el resultado. El traslado al año siguiente requiere un proceso explícito posterior.

> **Corrección vigente (15-10-2026):** se descartó la marca de «grado de egreso» por confundir resultado académico con salida institucional. La propuesta de promoción calcula exclusivamente `promovido` o `reprobado` y su revisión no puede sustituirlos por `egresado`. Una persona puede dejar el colegio tras cualquier grado; su salida y posible renovación pertenecen a un flujo de trayectoria estudiantil separado. La columna local introducida para grado terminal se elimina mediante migración correctiva, sin alterar notas ni matrículas. Las referencias históricas de esta página que vinculen egreso al último grado no son reglas vigentes.

Proceso ejecutado al cierre del año lectivo que determina, para cada estudiante, si avanza al grado siguiente o si repite el grado actual.

## Proceso automático

Al cierre del año lectivo el sistema ejecuta el proceso de promoción automática. Evalúa a cada estudiante según las reglas configuradas por el colegio:

- **Cuántas materias puede perder y aún ser promovido.**
- **Si existen materias que no se pueden perder bajo ninguna circunstancia** (ej. el colegio puede definir que perder Matemáticas implica reprobación automática).
- **El promedio general mínimo requerido** para pasar.

El sistema toma como insumo:

- Las notas finales de cada materia.
- Los resultados de [[nivelaciones-y-habilitaciones|nivelaciones y habilitaciones]].

## Validación antes del cierre

El sistema genera un **listado completo de estudiantes promovidos y reprobados** para revisión del [[roles/02-coordinador-academico|Coordinador Académico]] **antes** de hacer el proceso definitivo.

El coordinador puede:

- Consultar el detalle de cada caso.
- Ver las notas efectivas, recuperaciones y reglas que explican el resultado.
- Validar caso por caso o aceptar el listado completo.

**Solo después de que el coordinador valida el listado**, el proceso queda cerrado.

### Interfaz de revisión — decisión de producto del 5 de octubre de 2026

- En la política de promoción, presentar las **materias que no se pueden reprobar** en filas y columnas legibles, con selección individual y un control **Seleccionar todas**. El control debe permitir deshacer la selección masiva antes de guardar; no modifica la política sin confirmación.
- En el listado de **matrículas activas**, ofrecer un filtro por **grupo** que muestre a sus estudiantes. Es un filtro de revisión, no una modificación de matrícula ni de la propuesta académica.
- **Estado:** mejoras de interfaz pendientes. El cálculo y la revisión de promoción existentes no deben confundirse con promoción automática al año siguiente o cierre académico oficial.

## Cierre del año y preparación del siguiente

Una vez cerrado el año:

- El sistema prepara la estructura del año lectivo siguiente.
- Los estudiantes promovidos tienen un **grado destino recomendado** para la renovación; no se crea todavía una matrícula ni se modifica su usuario.
- Los reprobados conservan su resultado y podrán solicitar renovación para repetir el grado que corresponda.
- Los datos del año cerrado quedan en **modo histórico inmutable** (ver [[../11-plataforma-y-operacion/historico-y-anos-cerrados|Histórico y años cerrados]]).

## Estados y transiciones

### Año lectivo (vista parcial centrada en este proceso)

```
En curso → Cierre iniciado → Promoción calculada (borrador) → Validada → Cerrado
```

### Resultado por estudiante

```
Pendiente → Calculado automáticamente → Revisado sin cambio del resultado → Definitivo
```

## Datos involucrados

- Notas finales del año por materia y estudiante.
- Resultados de habilitaciones.
- Reglas de promoción configuradas por el colegio.
- Resultado académico por estudiante (Promovido / Reprobado; Pendiente mientras falten insumos).
- Grado destino para el año siguiente.

## Estudiantes que dejan el colegio

`Egresado` describe a quien no continúa en la institución, no un grado ni una nota. Puede haber sido promovido o reprobado; ambos datos deben conservarse por separado. Lo marca manualmente una persona con `estudiantes.egreso.gestionar`; nunca se deduce del último grado ni de la falta de matrícula futura. El acceso a la plataforma se revoca y se conservan expediente, boletines y certificados históricos. Si regresa, el proceso de reincorporación deberá verificar su identidad y reutilizar el mismo usuario.

## Reglas de negocio

- **RN-PR-001 — Cálculo automático con reglas configurables:** el cálculo respeta las reglas del colegio (materias máximas perdibles, materias intransigibles, promedio mínimo).
- **RN-PR-002 — Validación obligatoria del coordinador:** el proceso no queda cerrado hasta que el coordinador valida el listado.
- **RN-PR-003 — Resultado reglado:** ninguna votación, consenso ni acta puede sobreescribir el cálculo. Una diferencia se resuelve corrigiendo los insumos o la política autorizada y recalculando, con auditoría.
- **RN-PR-004 — Cierre y preparación del año siguiente:** el cierre conserva resultados y puede preparar la estructura del año siguiente, pero no distribuye estudiantes ni genera matrículas automáticamente. La renovación explícita utiliza el grado destino y conserva el mismo usuario.
- **RN-PR-005 — Inmutabilidad del año cerrado:** una vez cerrado, el año lectivo y todos sus datos son inmutables y **no admiten edición directa**. La única vía de modificación es una **reapertura formal y auditada** según el modelo de dos niveles de `RN-PR-101` (intra-ventana por permiso `cierre.reabrir`; fuera de ventana, exclusiva del superadministrador — ver `RN-HC-281`).
- **RN-PR-006 — Asignación de grupo posterior:** solo tras una renovación revisada y aprobada se asigna grupo para el nuevo año lectivo.
- **RN-PR-007 — Separación de trayectoria:** la promoción no marca egreso. La salida del colegio se gestiona fuera del cálculo de notas y no altera su resultado; no se crea una matrícula del siguiente año por el mero hecho de aprobar.
- **RN-PR-008 — Cierre sin habilitaciones pendientes:** el sistema bloquea el cierre definitivo del año si hay habilitaciones pendientes de registrar.

## Notas y pendientes

- **[Decisión tomada]** El sistema ofrece **plantillas predefinidas de reglas de promoción** (ej. "máximo N materias perdidas", "ninguna materia con nota inferior a X", "promedio mínimo Y") y permite a cada colegio definir una **regla custom** combinable. Regla: **RN-PR-100 — Plantillas predefinidas + regla custom por colegio**.
- **[Decisión tomada]** La **reapertura del cierre académico** sigue un **modelo de dos niveles**: (1) **intra-ventana** (dentro del periodo de gracia configurable tras el cierre) la ejecuta **cualquier rol con el permiso `cierre.reabrir`** (rector, coordinador académico, secretaria u otro definido por la matriz del colegio), con **justificación obligatoria** y **log inmutable**; (2) **fuera de ventana / post-cierre definitivo** queda **exclusivamente en manos del superadministrador de plataforma** (ver `RN-HC-281`). Regla: **RN-PR-101 — Reapertura en dos niveles: por permiso intra-ventana, superadministrador fuera de ventana, siempre con justificación y log inmutable**.
- **[Pendiente — producto]** Comportamiento si un estudiante egresado quiere matricularse nuevamente al colegio: debería reactivarse su expediente histórico (no crearse uno nuevo) y matricularlo en el grado correspondiente, conservando todo el historial.
