---
tags:
  - arquitectura
  - criterios-aceptacion
aliases:
  - Criterios de Aceptacion
---

# Criterios de Aceptacion

Condiciones que se deben cumplir para considerar el sistema "terminado". Cada criterio es verificable (si/no) y referencia la RR o RF que cubre.

---

| # | Criterio | Cubre |
|---|---|---|
| AC-01 | El Superadmin puede crear un tenant nuevo. Al crearlo, el sistema provisiona schema PostgreSQL, semillas base, subdominio y deja al primer Rector con acceso a configurar | RF-01, RR-01 |
| AC-02 | Un usuario autenticado en un tenant no puede acceder a datos de otro tenant. Cualquier intento (manipulando subdominio, IDs o tokens) es rechazado en backend | RR-01, RR-06, RNF-01 |
| AC-03 | Cada accion sensible genera un registro de auditoria con quien, que, cuando, IP, registro afectado. El log es consultable por el Rector | RR-03, RF-49, RNF-03 |
| AC-04 | El Rector puede configurar el calendario y los periodos lectivos. El sistema valida que los periodos no se traslapen y cubran el ano lectivo completo | RF-05 |
| AC-05 | El Rector puede definir la escala valorativa, ya sea numerica (rango configurable) o por imagenes (preescolar). El sistema usa esa escala para todas las notas de ese tenant | RF-07 |
| AC-06 | El Coordinador Academico puede asignar docentes a materias y grupos. Un docente solo ve los grupos y materias asignados | RF-13, RR-10 |
| AC-07 | Un docente registra notas solo en sus materias asignadas. El sistema bloquea intentos de registrar notas en materias no asignadas (frontend y backend) | RF-16, RR-02, RR-10 |
| AC-08 | Despues del cierre de periodo, el sistema bloquea la edicion de notas para Docentes. El permiso solo se puede dar via configuracion explicita del rol | RR-07, RF-17 |
| AC-09 | El Director de Grupo ve el consolidado completo de su grupo (todas las materias). En otros grupos solo ve sus materias asignadas como Docente | RR-09 |
| AC-10 | El Coordinador de Convivencia gestiona el observador disciplinario de cualquier estudiante. No tiene acceso al modulo de notas salvo que el colegio lo configure | RF-26 |
| AC-11 | La Secretaria genera constancias, certificados y paz y salvos. El sistema asigna consecutivo y deja trazabilidad por documento | RF-34, RF-35, RF-36 |
| AC-12 | Si el colegio tiene activado el bloqueo por pendientes, la secretaria no puede emitir documentos para un estudiante con documentos de matricula o pagos pendientes | RR-08, RF-33 |
| AC-13 | El reporte SIMAT se genera en el formato requerido por el Ministerio de Educacion Nacional. Permite descarga directa | RF-37, RI-02 |
| AC-14 | El estudiante / acudiente puede consultar notas, horario, boletines y observaciones del estudiante asociado. No puede modificar nada | RF-45, RF-46, RF-47, RF-48, RR-11, RR-14 |
| AC-15 | El acudiente con varios hijos ve los datos de todos sus hijos vinculados. No ve datos de otros estudiantes del colegio | RR-14 |
| AC-16 | El sistema no permite asignar simultaneamente Coord. Academico + Coord. de Convivencia separados Y Coord. combinado en un mismo tenant | RR-12 |
| AC-17 | El sistema solo permite asignar el complemento Director de Grupo a un usuario que ya tiene el rol Docente | RR-09 |
| AC-18 | Cada rol distingue permisos estructurales (no modificables) y permisos configurables. El sistema no permite desactivar un permiso estructural | RR-05 |
| AC-19 | Disponibilidad del sistema >= 99.5% mensual medido sobre 30 dias rodantes | RNF-05 |
| AC-20 | Backup automatico diario por tenant. Restauracion completa probada al menos una vez por semestre | RNF-06 |
| AC-21 | El sistema cumple con los requisitos de la Ley 1581 (proteccion de datos personales en Colombia): consentimiento, finalidad, derecho al olvido, etc. | RNF-07 |
| AC-22 | El cambio de calendario A/B de un tenant solo lo puede hacer el Superadmin. El Rector ve cual esta activo pero no lo cambia | RR-13, RF-03 |
| AC-23 | El boletin generado puede ser firmado/aprobado segun el flujo configurado (director, coordinador o rector). Solo despues de aprobado se distribuye | RF-39 |
| AC-24 | La matriz de permisos del UI siempre refleja el estado real de configuracion del tenant. No hay desfase entre lo que se ve y lo que el backend valida | RR-02, RR-05 |
| AC-25 | El portal funciona en mobile y desktop con misma cobertura funcional para los roles de consulta (ROL-09) | RNF-05 |

---

## Notas

- Los AC se actualizan a medida que se descubren casos limite durante implementacion.
- Cada AC debe poder verificarse manualmente o con un test automatizado.
- Los AC marcados con RNF requieren validacion en ambientes de stress (carga, fallos, datos a escala).
