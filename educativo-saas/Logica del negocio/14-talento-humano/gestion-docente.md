---
titulo: Gestión del talento humano docente
modulo: talento-humano
tipo: proceso
estado: borrador
tags: [docentes, talento-humano, contratos, evaluacion-docente, capacitaciones, novedades]
---

# Gestión del talento humano docente

## Descripción

Proceso por el cual el colegio administra el expediente laboral del docente más allá de su asignación académica: hoja de vida, datos de contrato, títulos y certificaciones, evaluación de desempeño por periodo, capacitaciones y novedades laborales (incapacidades, permisos, licencias). Estas novedades se cruzan con la asignación y la asistencia para reflejar ausencias del docente y disparar reemplazos.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Rector / Administrador del colegio]] | Aprueba contratos, cierra evaluaciones de desempeño y autoriza novedades de alto impacto. |
| [[../02-usuarios-roles-y-permisos/roles/02-coordinador-academico\|Coordinador Académico]] | Evalúa el desempeño del docente, gestiona la reasignación de carga ante novedades y aprueba capacitaciones. |
| [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica\|Secretaría Académica]] | Mantiene la hoja de vida, registra contratos, novedades y carga los soportes documentales. |
| [[../02-usuarios-roles-y-permisos/roles/06-docente\|Docente]] | Consulta su expediente, actualiza datos personales y radica solicitudes de permiso o soporte de incapacidad. |

## Alcance del expediente docente

| Bloque | Contenido | Editable por |
| --- | --- | --- |
| Hoja de vida | Datos personales, contacto, formación académica, experiencia previa. | Secretaría; el docente puede sugerir cambios. |
| Contrato | Tipo de vinculación, fechas de inicio/fin, jornada, escalafón/categoría, valor. | Secretaría / Rector. |
| Títulos y certificaciones | Diplomas, escalafón docente, manipulación de alimentos, primeros auxilios, vencimientos. | Secretaría (con soporte adjunto). |
| Evaluación de desempeño | Resultado por periodo, evaluador, plan de mejoramiento. | Coordinación / Rector. |
| Capacitaciones | Cursos internos y externos, horas, constancia. | Secretaría / Coordinación. |
| Novedades | Incapacidades, permisos, licencias, vacaciones. | Secretaría (registra), Docente (radica solicitud). |

## Flujo principal

1. Secretaría crea el expediente del docente y registra su hoja de vida y datos de contrato.
2. Carga los títulos y certificaciones con su soporte adjunto y, cuando aplica, la fecha de vencimiento.
3. Al cierre de cada periodo académico, la coordinación abre la evaluación de desempeño del docente.
4. El docente recibe el resultado; si está por debajo del umbral, se genera un plan de mejoramiento con seguimiento.
5. Durante el año, las novedades (incapacidades, permisos) se radican y aprueban, afectando temporalmente su asignación y asistencia.
6. El expediente se mantiene como histórico aun cuando el docente sale del colegio (soft-delete).

## Novedades y su efecto en asignación/asistencia

1. El docente radica una solicitud de permiso, o Secretaría registra una incapacidad con soporte (EPS).
2. La novedad define un rango de fechas y un tipo (incapacidad, permiso remunerado, licencia, calamidad).
3. Mientras la novedad está activa, el sistema marca al docente como **no disponible** en ese rango.
4. Las sesiones del horario del docente en ese rango quedan señaladas para reemplazo; la asistencia de esas sesiones no se le exige al titular.
5. La coordinación asigna un docente reemplazo temporal o reprograma; el reemplazo registra asistencia y notas sobre esas sesiones.
6. Al terminar la novedad, el docente recupera su disponibilidad y su asignación original.

## Estados y transiciones

### Contrato

```
Borrador → Vigente → Por vencer → Finalizado
                    → Suspendido (novedad de larga duración)
```

### Novedad

```
Solicitada → En revisión → Aprobada → En curso → Cerrada
                         → Rechazada
```

### Evaluación de desempeño

```
No iniciada → En curso → Cerrada → (si bajo umbral) Plan de mejoramiento → Seguimiento
```

## Configurabilidad por colegio

- El colegio define el **modelo de evaluación de desempeño**: rúbrica, dimensiones evaluadas, escala y umbral de aprobación.
- Define qué **tipos de novedad** existen y cuáles cuentan como inasistencia laboral del docente.
- Configura la **periodicidad** de la evaluación (por periodo académico, semestral o anual).
- Define qué **certificaciones son obligatorias** y su política de alerta por vencimiento (ej. 30 días antes).
- Decide si el docente puede **autogestionar** la radicación de permisos o si todo pasa por Secretaría.

## Datos involucrados

- Expediente del docente (1:1 con el usuario docente).
- Contrato vigente e histórico de contratos.
- Catálogo de títulos y certificaciones con vencimientos.
- Evaluaciones de desempeño por periodo y evaluador.
- Registro de capacitaciones con horas y constancia.
- Novedades con rango de fechas, tipo, soporte y estado.

## Integraciones con otros módulos

- **Asignación de docentes:** el soft-delete y la reasignación obligatoria de asignaciones huérfanas se rigen por [[../04-procesos-academicos/asignacion-docentes#Reglas de negocio\|RN-AD-011]].
- **Asistencia:** las novedades suspenden la exigencia de registro de asistencia del titular en el rango afectado.
- **Observador del estudiante:** la evaluación de desempeño no se mezcla con el expediente del estudiante; son dominios separados.
- **Log de auditoría:** todo cambio de contrato, evaluación y novedad queda registrado con autor, fecha y valores.

## Reglas de negocio

- **RN-RH-001 — Expediente único por docente:** cada docente tiene un único expediente de talento humano vinculado 1:1 a su usuario; no se duplica entre años lectivos.
- **RN-RH-002 — Contrato vigente único:** un docente solo puede tener un contrato en estado `Vigente` a la vez; al iniciar uno nuevo el anterior pasa a `Finalizado` y queda en el histórico.
- **RN-RH-003 — Certificación con soporte y vencimiento:** registrar una certificación obligatoria exige adjuntar el soporte; si tiene fecha de vencimiento, el sistema alerta según la ventana configurada por el colegio.
- **RN-RH-004 — Evaluación por periodo cerrada e inmutable:** una evaluación de desempeño cerrada no se edita; correcciones requieren una nueva versión que conserva la anterior en auditoría.
- **RN-RH-005 — Plan de mejoramiento bajo umbral:** si la evaluación queda por debajo del umbral configurado, el sistema obliga a crear un plan de mejoramiento con responsable y fecha de seguimiento antes de cerrar el proceso.
- **RN-RH-006 — Novedad suspende disponibilidad:** mientras una novedad está `En curso`, el docente queda no disponible en su rango; las sesiones afectadas se marcan para reemplazo y no exigen asistencia al titular.
- **RN-RH-007 — Novedad no borra la asignación:** una incapacidad o permiso no elimina la asignación materia × grupo del titular; solo suspende su disponibilidad temporalmente y la restituye al cerrar la novedad.
- **RN-RH-008 — Soft-delete con reasignación obligatoria:** al desvincular un docente se aplica soft-delete; conserva todo su expediente e historial, pero sus asignaciones quedan huérfanas y deben reasignarse explícitamente (cruza [[../04-procesos-academicos/asignacion-docentes#Reglas de negocio\|RN-AD-011]]).
- **RN-RH-009 — Aislamiento por tenant:** el expediente docente, contratos y evaluaciones residen en la BD del colegio; nunca se comparten entre tenants aunque la persona trabaje en varios colegios de la plataforma.
- **RN-RH-010 — Auditoría de datos sensibles:** cambios en contrato, valor, evaluación de desempeño y novedades de salud quedan en el log de auditoría con autor, fecha, valor anterior y nuevo.

## Notas y pendientes

- **[Decisión tomada]** El expediente docente es **multi-tenant aislado**: si una persona enseña en dos colegios de la plataforma, tiene un expediente independiente en cada tenant (RN-RH-009).
- **[Decisión tomada]** La desvinculación de un docente con asignaciones activas usa **soft-delete con reasignación obligatoria**, coherente con `RN-AD-011`; el coordinador académico recibe la lista de asignaciones huérfanas pendientes.
- **[Pendiente — producto]** Definir si las incapacidades incluyen datos de salud reservados (diagnóstico EPS) y cómo se restringe su visibilidad bajo Habeas Data (Ley 1581); cruza con [[../13-cumplimiento-colombia/habeas-data-y-consentimientos\|Habeas Data y consentimientos]].
- **[Pendiente — producto]** Validar si la evaluación de desempeño docente alimenta el [[../09-reportes-y-analitica/reportes-academicos\|tablero del rector]] o queda como reporte aparte de talento humano.

## Documentos relacionados

- [[../04-procesos-academicos/asignacion-docentes|Asignación de docentes]]
- [[../04-procesos-academicos/asistencia|Asistencia]]
- [[../02-usuarios-roles-y-permisos/roles/06-docente|Rol Docente]]
- [[../02-usuarios-roles-y-permisos/roles/02-coordinador-academico|Rol Coordinador Académico]]
- [[../02-usuarios-roles-y-permisos/ciclo-de-vida-de-usuario|Ciclo de vida de usuario]]
- [[../13-cumplimiento-colombia/habeas-data-y-consentimientos|Habeas Data y consentimientos]]
- [[../11-plataforma-y-operacion/log-de-auditoria|Log de auditoría]]
