---
tags:
  - arquitectura
  - matriz-permisos
aliases:
  - Matriz de Permisos
---

# Matriz de Permisos

Quien puede hacer que, modulo por modulo, accion por accion.

Para el detalle granular de cada rol ver `Arquitectura/[NN - Rol]/04 - Permisos Detallados.md`.

Para los simbolos ver [[05 - Leyenda]].

Convenciones cortas usadas en esta matriz:
- `Crear` / `Ver` / `Editar` / `CRUD` / `Aprobar` / `Configurable` / `Auto` / `—` / `En pausa`
- `Auto*` significa que el sistema lo ejecuta automaticamente para este rol.

---

## Plataforma (cross-tenant)

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Plataforma** | Crear / eliminar tenant | CRUD | — | — | — | — | — | — | — | — |
| | Asignar plan de licencia | Editar | — | — | — | — | — | — | — | — |
| | Cambiar calendario A/B del tenant | Editar | — | — | — | — | — | — | — | — |
| | Definir subdominio del tenant | Editar | — | — | — | — | — | — | — | — |
| | Gestionar almacenamiento del tenant | Editar | — | — | — | — | — | — | — | — |
| | Acceso cross-tenant para soporte | Ver | — | — | — | — | — | — | — | — |
| | Acceder a logs globales de plataforma | Ver | — | — | — | — | — | — | — | — |

---

## Configuracion del Colegio

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Identidad** | Configurar logo, NIT, MEN | — | Editar | — | — | — | — | — | — | — |
| **Calendario** | Definir periodos lectivos | — | Editar | — | — | — | — | — | — | — |
| | Cambiar calendario A/B | — | Ver | — | — | — | — | — | — | — |
| **Jornadas** | Configurar jornadas y bloques | — | Editar | — | — | — | — | — | — | — |
| **Modelo pedagogico** | Configurar por nivel | — | Editar | — | — | — | — | — | — | — |
| **Escala valorativa** | Configurar escala (numerica / imagenes) | — | Editar | — | — | — | — | — | — | — |
| **Aprobacion** | Configurar metodo y nota minima | — | Editar | — | — | — | — | — | — | — |

---

## Usuarios y Roles

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Usuarios** | Crear / editar / desactivar usuarios | — | CRUD | — | — | — | — | — | — | — |
| | Asignar roles | — | Editar | — | — | — | — | — | — | — |
| | Ajustar permisos configurables | — | Editar | — | — | — | — | — | — | — |

---

## Plan Academico y Horarios

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Plan de estudios** | Gestionar materias por grado | — | CRUD | CRUD | — | CRUD | — | — | — | — |
| **Grupos** | Crear / gestionar grupos | — | CRUD | CRUD | — | CRUD | — | — | — | — |
| **Asignacion** | Asignar docentes a materias/grupos | — | Editar | Editar | — | Editar | — | — | — | — |
| | Designar director de grupo | — | Editar | Editar | — | Editar | — | — | — | — |
| **Horarios** | Construir / editar horarios | — | CRUD | CRUD | — | CRUD | — | — | — | — |
| | Consultar horario propio | — | Ver | Ver | Ver | Ver | Ver | Ver | Ver | Ver |

---

## Notas y Consolidados

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Notas** | Registrar/editar notas en materia asignada | — | Editar | Configurable | — | Configurable | — | Editar | Editar | — |
| | Editar notas que no dicta | — | Editar | Configurable | — | Configurable | — | — | Configurable | — |
| | Editar notas despues del cierre | — | Editar | Configurable | — | Configurable | — | Configurable | Configurable | — |
| **Consolidados** | Ver consolidado del grupo dirigido | — | Ver | Ver | — | Ver | — | — | Ver | — |
| | Ver consolidado de todos los grupos | — | Ver | Ver | — | Ver | — | — | — | — |
| | Ver notas propias / del estudiante asociado | — | Ver | Ver | — | Ver | Configurable | — | — | Ver |
| **Periodo** | Coordinar cierre de periodo | — | Editar | Editar | — | Editar | — | — | — | — |
| | Gestionar nivelaciones / habilitaciones | — | Editar | Editar | — | Editar | — | — | — | — |

---

## Asistencia

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Asistencia** | Registrar en sus clases | — | Editar | — | — | — | — | Editar | Editar | — |
| | Consultar del grupo dirigido | — | Ver | Ver | — | Ver | — | — | Ver | — |
| | Consultar propia / del estudiante asociado | — | Ver | Ver | Ver | Ver | Ver | — | — | Ver |

---

## Convivencia y Observador

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Observador academico** | Registrar observacion en su materia | — | Editar | — | — | — | — | Editar | Editar | — |
| **Observador disciplinario** | Anotacion en grupo dirigido | — | Editar | — | Editar | Editar | — | — | Editar | — |
| | Anotacion en cualquier estudiante | — | Editar | — | Editar | Editar | — | — | — | — |
| **Configuracion** | Definir tipologias de anotacion | — | Editar | — | Editar | Editar | — | — | — | — |
| **Citaciones** | Citar formalmente a acudientes | — | Editar | Configurable | Configurable | Configurable | — | — | Configurable | — |
| | Definir sanciones formales | — | Editar | — | Configurable | Configurable | — | — | — | — |
| **Reportes** | Generar reportes de convivencia | — | Ver | — | Reportar | Reportar | — | — | — | — |
| **Consulta** | Ver observador propio / del estudiante | — | Ver | — | Ver | Ver | — | — | Ver | Configurable |

---

## Matricula y Secretaria

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Estudiantes** | Registrar / editar estudiantes y acudientes | — | CRUD | — | — | — | CRUD | — | — | — |
| | Asignar a grupo (matricula) | — | Editar | Configurable | — | Configurable | Editar | — | — | — |
| | Cambiar grupo post-matricula | — | Editar | Configurable | — | Configurable | Configurable | — | — | — |
| **Documentos matricula** | Cargar y validar | — | Ver | — | — | — | Editar | — | — | — |

---

## Documentos Oficiales

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Constancias** | Generar constancias de estudio | — | Reportar | — | — | — | Reportar | — | — | — |
| **Certificados** | Generar certificados de notas | — | Reportar | — | — | — | Reportar | — | — | — |
| **Paz y salvos** | Emitir paz y salvos | — | Reportar | — | — | — | Reportar | — | — | — |
| **SIMAT** | Reportar a SIMAT | — | Reportar | — | — | — | Reportar | — | — | — |
| **Bloqueos** | Bloquear emision por pendientes | — | Configurable | — | — | — | Configurable | — | — | — |

---

## Boletines

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Boletines** | Generar boletin del grupo dirigido | — | Reportar | Reportar | — | Reportar | — | — | Reportar | — |
| | Aprobar / firmar boletines | — | Aprobar | Configurable | — | Configurable | — | — | Configurable | — |
| | Agregar observacion general | — | Editar | — | — | — | — | — | Editar | — |
| | Consultar propio / del estudiante | — | Ver | Ver | — | Ver | Ver | — | — | Ver |
| | Descargar PDF | — | Ver | Ver | — | Ver | Ver | — | Ver | Configurable |

---

## Comunicaciones y Portal

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Comunicados** | Enviar al colegio entero | — | Editar | Configurable | Configurable | Configurable | Configurable | — | — | — |
| **Mensajes** | Comunicarse con acudientes via portal | — | Editar | Configurable | Configurable | Configurable | Configurable | Configurable | Configurable | — |
| **Notificaciones** | Recibir por correo | — | Auto | Auto | Auto | Auto | Auto | Auto | Auto | Configurable |
| **Portal** | Acceder al portal | — | Ver | Ver | Ver | Ver | Ver | Ver | Ver | Configurable |

---

## Auditoria

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Auditoria** | Acceder a logs del tenant | — | Ver | — | — | — | — | — | — | — |
| | Ver historial de cambios de un registro | — | Ver | Configurable | Configurable | Configurable | Configurable | — | — | — |

---

## Notas clave

> **Permisos estructurales vs configurables.** Las marcas "Configurable" indican que el colegio puede activar o desactivar el permiso desde la pantalla de configuracion del rol. Las marcas firmes (CRUD/Editar/Ver/Reportar/Aprobar/Auto/—) son **estructurales**, no se pueden modificar.

> **Director de Grupo (ROL-08) es complemento, no rol principal.** Solo se asigna sobre un usuario que ya tenga ROL-07 (Docente). Los permisos de ROL-08 listados aqui son ADICIONALES sobre el grupo dirigido; conserva todos los permisos de ROL-07 sobre sus materias asignadas.

> **Coordinador combinado (ROL-05) es excluyente con ROL-03 + ROL-04.** El colegio elige el esquema. No se asignan ambos esquemas simultaneamente.

> **Aislamiento por tenant (RR-01) aplica a todos los roles del tenant.** Nadie ve datos de otro colegio.

> **Auditoria (RR-03) aplica a todas las acciones sensibles** sin importar el rol.

> **Fuente de verdad del detalle:** `Logica del negocio/02-usuarios-roles-y-permisos/matriz-de-permisos.md`. Esta matriz es la **interpretacion UX** de esa.
