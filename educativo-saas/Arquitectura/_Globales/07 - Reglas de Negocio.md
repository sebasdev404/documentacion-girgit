---
tags:
  - arquitectura
  - reglas-de-negocio
aliases:
  - Reglas de Negocio
---

# Reglas de Negocio

Reglas RR-NN consolidadas. Cada regla viene de la fuente de verdad en `Logica del negocio/`.

---

## Reglas transversales

| ID | Regla | Descripcion |
|---|---|---|
| RR-01 | Aislamiento total entre tenants | Ningun rol puede acceder a datos de otro tenant. Aislamiento a nivel BD (schema separado) y autenticacion (subdominio). Unica excepcion: ROL-01 (Superadmin) con acceso auditado |
| RR-02 | Verificacion de permisos en frontend y backend | Cada accion se valida tanto en UI (oculta/deshabilita) como en backend (rechaza llamadas). No es posible saltarse un permiso por interfaz |
| RR-03 | Auditoria de acciones sensibles | Toda accion sensible (notas, documentos, configuracion, cambios de roles, accesos del Superadmin) registra: quien, que, cuando, IP, registro afectado. Los logs son inmutables |
| RR-04 | Asignacion de roles por el Administrador del Colegio | Los roles del tenant solo los asigna ROL-02 (Rector). El rol del Rector lo entrega el Superadmin al crear el tenant. Un usuario tiene un solo rol principal |
| RR-05 | Configurabilidad acotada de permisos | El colegio no puede crear permisos nuevos. Solo puede activar/desactivar permisos configurables existentes. Los permisos estructurales no se pueden desactivar |
| RR-06 | Acceso al sistema solo por subdominio del colegio | Un usuario de un tenant no puede autenticarse en el portal de otro tenant, aunque use las mismas credenciales. El tenant_id se infiere del subdominio antes de validar credenciales |

---

## Reglas operativas

| ID | Regla | Descripcion |
|---|---|---|
| RR-07 | Notas se editan dentro del periodo abierto | Una vez cerrado el periodo, la edicion de notas requiere permiso configurable activado + justificacion |
| RR-08 | Bloqueo de documentos por pendientes | La secretaria puede ser configurada para bloquear emision de constancias/certificados/paz y salvos cuando hay documentos de matricula o pagos pendientes |
| RR-09 | Director de Grupo solo opera sobre su grupo | Los permisos extra del complemento Director de Grupo aplican solo sobre el grupo dirigido. En otros grupos sigue siendo solo Docente sobre sus materias |
| RR-10 | Docente ve solo grupos y materias asignados | Un docente nunca ve datos de grupos o materias que no le han sido asignados explicitamente por el Coordinador Academico |
| RR-11 | Estudiante y Acudiente comparten rol | Comparten el mismo rol con scope distinto. Estudiante ve sus propios datos; acudiente ve los datos de los estudiantes vinculados a el |
| RR-12 | Coordinador combinado excluye los separados | Un tenant elige: o usa Coord. Academico + Coord. de Convivencia separados, o usa el Coordinador combinado. No ambos esquemas simultaneamente |
| RR-13 | Cambio de calendario A/B es del Superadmin | El Rector elige el calendario dentro de los habilitados por el plan, pero solo el Superadmin puede cambiar el calendario habilitado para un tenant |
| RR-14 | Acudiente accede solo a datos de estudiantes vinculados | Un acudiente con varios hijos en el colegio ve los datos de todos sus hijos vinculados, no de otros estudiantes |
| RR-15 | Reporte SIMAT obligatorio | Los colegios estan obligados a reportar matricula al SIMAT (Ministerio de Educacion Nacional). El sistema debe generar el formato requerido |

---

## Referencias cruzadas

- Fuente de verdad de las reglas transversales: `Logica del negocio/02-usuarios-roles-y-permisos/reglas-transversales-de-roles.md`.
- Las reglas operativas (RR-07 a RR-15) provienen de los archivos individuales de rol en `Logica del negocio/02-usuarios-roles-y-permisos/roles/`.
- Cuando una regla aplique solo a un modulo especifico, ver el archivo de ese modulo en `Logica del negocio/`.

---

## Documentos relacionados

- [[03 - Tabla de Requerimientos|Tabla de Requerimientos]] — referencias RR-XX en la columna Notas.
- [[06 - Matriz de Permisos|Matriz de Permisos]] — los permisos configurables vienen de RR-05.
- [[08 - Criterios de Aceptacion|Criterios de Aceptacion]] — cada AC referencia la RR que cubre.
