---
titulo: Jerarquía organizacional
modulo: multi-tenancy
tipo: referencia
estado: borrador
tags: [multi-tenancy, jerarquia, organizacion]
---

# Jerarquía organizacional

Estructura interna de un colegio: sedes, jornadas, niveles, grados, grupos.

## Niveles jerárquicos

| Nivel | Descripción | Ejemplo |
| --- | --- | --- |
| Colegio (tenant) | Institución completa. Contiene toda la jerarquía interna. | "Colegio San José" |
| Sede | Ubicación física del colegio cuando hay más de una. Opcional para colegios de sede única. | "Sede Principal", "Sede Norte" |
| Jornada | Bloque horario de operación diaria. Tiene hora de inicio y fin propias y bloques horarios definidos. | Mañana, Tarde, Única |
| Nivel educativo | Etapa pedagógica. Cada nivel tiene su propio modelo pedagógico configurado. | Preescolar, Primaria, Secundaria, Media |
| Grado | Curso dentro del nivel. | Transición, Primero, ..., Décimo, Undécimo |
| Grupo / curso | Sección dentro del grado. Si el colegio no maneja secciones, el grupo coincide con el grado. | 9A, 9B, 9C |

## Reglas de pertenencia

- Un grupo pertenece a **exactamente un grado** y a **un año lectivo** específico.
- Un grado pertenece a **un nivel educativo**.
- Una jornada pertenece a **una sede** (o al colegio directamente si no hay múltiples sedes).
- Un grupo puede tener **un salón fijo asignado** (espacio físico) o ninguno si los estudiantes se desplazan a aulas especializadas.
- Un grupo puede tener **un Director de Grupo** asignado, que es un docente con el complemento de rol correspondiente.
- Un estudiante pertenece a **un único grupo dentro de un año lectivo**. En el siguiente año lectivo es reasignado.

## Reasignaciones (cambio de grupo, traslado de sede)

- Durante el año lectivo activo, el coordinador académico puede mover un estudiante de un grupo a otro dentro del mismo grado.
- El movimiento queda registrado en el log de auditoría con fecha, motivo, usuario y grupo origen/destino.
- Las notas y asistencia ya registradas en el grupo origen se mantienen en el historial del estudiante.
- Años lectivos cerrados son inmutables: no se puede cambiar el grupo de un estudiante en un año cerrado (ver [[../11-plataforma-y-operacion/historico-y-anos-cerrados|Histórico y años cerrados]]).
- El traslado de un estudiante entre sedes implica un cambio de grupo y posiblemente de jornada; sigue las mismas reglas de auditoría.

## Reglas de negocio

- **RN-JO-001 — Pertenencia exclusiva a un grupo:** un estudiante no puede pertenecer a más de un grupo en el mismo año lectivo.
- **RN-JO-002 — Grupo asociado a año lectivo:** los grupos son entidades por año lectivo. "9A 2026" y "9A 2027" son grupos distintos aunque compartan el nombre.
- **RN-JO-003 — Director de grupo único:** un grupo tiene como máximo un director de grupo. El mismo docente puede ser director de varios grupos si así lo decide el colegio.
- **RN-JO-004 — Sede opcional:** los colegios de sede única no requieren modelar sede; las jornadas se asocian directamente al colegio.
- **RN-JO-005 — Jornada con bloques horarios:** una jornada debe tener al menos un bloque horario configurado para poder construir horarios.

## Notas y pendientes

- **[Decisión tomada]** **Catálogo base de niveles educativos por país** (en Colombia: Preescolar / Primaria / Secundaria / Media). Cada colegio puede **agregar niveles o variantes propias** si su modelo pedagógico lo requiere (ej. Materno, Pre-jardín, Bachillerato Internacional). Regla: **RN-JO-230 — Catálogo base por país + niveles custom por colegio**.
- **[Decisión tomada]** **Repetición de grado entre sedes del mismo colegio**: **configurable por colegio**. Por defecto se permite el **traslado interno entre sedes** bajo **autorización administrativa o rectoral**, manteniendo el **historial académico centralizado** del estudiante (no se duplica el expediente). Regla: **RN-JO-231 — Traslado entre sedes con autorización y expediente centralizado**.
