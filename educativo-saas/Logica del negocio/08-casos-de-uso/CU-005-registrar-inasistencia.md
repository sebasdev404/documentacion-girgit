---
titulo: "CU-005: Registrar inasistencia"
modulo: 04-procesos-academicos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, asistencia, docente]
---

# CU-005: Registrar inasistencia

## Identificación

- **ID:** CU-005
- **Nombre:** Registrar inasistencia
- **Módulo:** Procesos académicos
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** [[../02-usuarios-roles-y-permisos/roles/06-docente|Docente]] o [[../02-usuarios-roles-y-permisos/roles/07-director-de-grupo|Director de grupo]].
- **Secundarios:** [[../02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia|Coordinador de Convivencia]].

## Descripción

Registro diario de inasistencias por sesión / clase. Configurable según política del colegio: por jornada o por asignatura.

## Precondiciones

- Existe la sesión (clase) en el calendario.
- Docente está asignado a esa sesión.

## Postcondiciones (éxito)

- Inasistencia registrada con tipo (ausencia, retardo, justificada / no).
- Notificación al acudiente según configuración.

## Flujo principal

1. Docente abre la sesión del día.
2. Sistema muestra la lista del grupo.
3. Docente marca presentes / ausentes / retardos.
4. Confirma. Sistema persiste y agenda notificaciones.

## Flujos alternativos

### A1. Captura por director de grupo (jornada completa)

- Si el colegio configura asistencia por jornada, solo el director de grupo o un rol asignado registra.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Fecha futura. | Sistema rechaza. |
| EX-2 | Sesión ya registrada. | Sistema permite editar dentro de la ventana configurada. |

## Reglas de negocio aplicables

- RN-AS-NNN, RG-002.

## Criterios de aceptación

- [ ] Solo el docente asignado puede registrar para su sesión.
- [ ] Las notificaciones llegan al acudiente según configuración del colegio.
- [ ] El sistema bloquea el registro de fechas futuras.

## Notas y pendientes

- Definir ventana de edición posterior (sugerido 24-48h).
