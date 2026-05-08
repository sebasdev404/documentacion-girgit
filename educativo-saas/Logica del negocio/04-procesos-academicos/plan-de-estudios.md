---
titulo: Plan de estudios
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [plan-de-estudios, materias, areas]
---

# Plan de estudios

El plan de estudios define qué materias o asignaturas existen en el colegio por grado y año lectivo. Es la base estructural sobre la que se construyen las asignaciones de docentes, los horarios y la registración de notas.

## Conceptos

### Área del conocimiento

Agrupación de materias relacionadas (ej. Ciencias Naturales, Matemáticas, Humanidades, Educación Física). Sirve para:

- Calcular promedios por área cuando el método de aprobación lo requiere.
- Estructurar el boletín en bloques temáticos.
- Permitir reportes agrupados por área.

### Materia / asignatura

Unidad pedagógica concreta (ej. Matemáticas 9, Inglés 9, Biología 9). Cada materia tiene:

| Atributo | Descripción |
| --- | --- |
| Nombre | Nombre visible de la materia. |
| Código | Identificador interno opcional. |
| Área del conocimiento | A qué área pertenece. |
| Niveles educativos | A qué niveles aplica (Preescolar, Primaria, Secundaria, Media). |
| Grados aplicables | A qué grados específicos aplica. |
| Intensidad horaria semanal | Número de horas semanales por grado. |
| Año lectivo | El plan de estudios se versiona por año lectivo. |

## Requisito previo

El plan de estudios debe existir **antes** de poder:

- Asignar docentes (ver [[asignacion-docentes|Asignación de docentes]]).
- Construir horarios (ver [[horarios|Horarios]]).
- Registrar notas (ver [[calificaciones|Calificaciones]]).

## Versionado por año lectivo

- Cada año lectivo tiene su propio plan de estudios.
- Al iniciar un nuevo año lectivo, el sistema permite **clonar** el plan del año anterior como punto de partida y luego ajustar.
- El plan de estudios de un año cerrado es inmutable.

## Reglas de negocio

- **RN-PE-001 — Plan obligatorio antes de operación:** no se pueden asignar docentes ni construir horarios sin un plan de estudios definido para el año lectivo activo.
- **RN-PE-002 — Una materia por grado:** dentro del mismo grado y año lectivo, no pueden existir dos materias con el mismo nombre.
- **RN-PE-003 — Intensidad horaria positiva:** la intensidad horaria semanal debe ser mayor que cero.
- **RN-PE-004 — Inmutabilidad histórica:** el plan de estudios de un año lectivo cerrado no puede modificarse.
- **RN-PE-005 — Clonación al cambio de año:** el sistema ofrece clonar el plan del año anterior al crear el nuevo año lectivo, pero no es obligatorio.
- **RN-PE-006 — Eliminación condicionada:** no se puede eliminar una materia que ya tiene asignaciones de docentes, horarios o notas registradas en el año lectivo activo.

## Quién gestiona

- **Crear / editar:** [[roles/02-coordinador-academico|Coordinador Académico]] o [[roles/01-rector-administrador-colegio|Administrador del Colegio]].
- **Consultar:** todos los roles del tenant.

## Notas y pendientes

- Definir si el sistema soporta materias optativas que el estudiante elige individualmente, o si todas las materias del grado son obligatorias para todo el grupo.
- Definir si las áreas del conocimiento son catálogo cerrado del sistema o cada colegio define las suyas.
