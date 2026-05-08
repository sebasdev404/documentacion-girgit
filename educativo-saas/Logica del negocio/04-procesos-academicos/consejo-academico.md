---
titulo: Consejo académico
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [consejo-academico, promocion, decisiones]
---

# Consejo académico

Reunión institucional al cierre del año lectivo donde se evalúan casos de estudiantes en situación límite y se toman decisiones sobre su promoción.

## Identificación de casos

Al cierre del año lectivo el sistema identifica automáticamente los estudiantes que se encuentran en situación límite:

- Aquellos que reprobaron pero cuyas notas están **muy cerca de la nota mínima** (umbral configurable por el colegio).
- Aquellos que tienen **circunstancias especiales** registradas durante el año (anotaciones disciplinarias relevantes, observaciones académicas, casos médicos, etc.).
- Aquellos que tienen el resultado de [[nivelaciones-y-habilitaciones|habilitación]] pendiente o no aprobada.

El sistema genera el listado de candidatos al consejo automáticamente, pero el [[roles/02-coordinador-academico|Coordinador Académico]] o el [[roles/01-rector-administrador-colegio|Rector]] pueden agregar o quitar casos manualmente.

## Convocatoria

- El [[roles/02-coordinador-academico|Coordinador Académico]] o el [[roles/01-rector-administrador-colegio|Rector]] convoca el consejo.
- El sistema permite registrar:
  - Fecha y hora de la reunión.
  - Lugar (físico o virtual).
  - Usuarios convocados (típicamente: rector, coordinaciones, directores de grupo de los casos involucrados, docentes titulares relevantes).

## Registro de decisiones

Para cada estudiante evaluado, el sistema permite registrar:

| Decisión | Descripción |
| --- | --- |
| Promovido | El estudiante pasa al grado siguiente. |
| Reprobado | El estudiante repite el grado. |
| Promovido con condición | El estudiante pasa al grado siguiente con un compromiso específico (firmado, con seguimiento). |

Junto a la decisión se registra:

- **Fecha de la reunión.**
- **Usuarios que participaron.**
- **Observaciones que justifican la decisión.**
- **Compromiso o condición** si la decisión es "Promovido con condición".

## Sobreescritura del resultado automático

La decisión del consejo puede **sobreescribir el resultado que el sistema calculó automáticamente**. Sin embargo:

- La sobreescritura queda completamente trazada en el log de auditoría.
- Se preserva tanto el resultado original del sistema como la decisión final del consejo.
- Se registra qué usuarios participaron en la decisión.

## Estados y transiciones

### Sesión del consejo

```
Convocada → En curso → Cerrada
```

### Decisión por estudiante

```
Pendiente → Tomada (Promovido / Reprobado / Promovido con condición)
```

## Reglas de negocio

- **RN-CO-001 — Identificación automática de candidatos:** el sistema identifica automáticamente los estudiantes en situación límite al cierre del año lectivo.
- **RN-CO-002 — Decisión registrada por estudiante:** cada decisión se registra individualmente con observaciones que la justifican.
- **RN-CO-003 — Sobreescritura auditada:** la decisión del consejo puede sobreescribir el cálculo automático, pero ambas versiones quedan registradas y la sobreescritura queda en el log de auditoría.
- **RN-CO-004 — Participantes auditados:** los usuarios que participan en la decisión quedan registrados explícitamente.
- **RN-CO-005 — Solo coordinador o rector convocan:** la convocatoria del consejo está restringida a estos roles.
- **RN-CO-006 — Inmutabilidad post-cierre del año:** las decisiones del consejo de años cerrados son inmutables.
- **RN-CO-007 — Promovido con condición exige compromiso:** si la decisión es "Promovido con condición", el sistema obliga a registrar el compromiso o condición específica.

## Acta del consejo

El sistema genera un PDF con el acta del consejo:

- Fecha, hora y lugar.
- Asistentes.
- Lista de estudiantes evaluados.
- Decisión de cada caso con su justificación.
- Resultado automático original y decisión final.

El acta se almacena asociada al año lectivo y consume cuota del tenant.

## Notas y pendientes

- **[Configurable por colegio]** Umbral en puntos por debajo de la nota mínima para considerar "situación límite". Cada colegio lo define en su configuración académica.
- **[Configurable por colegio]** Modalidad de decisión del consejo: votación registrada o consenso documentado. La plataforma soporta ambos formatos en el acta.
- **[Funcionalidad futura]** Firma digital del rector sobre el acta. Fuera de MVP.
