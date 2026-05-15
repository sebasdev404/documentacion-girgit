---
tags:
  - arquitectura
  - modulos
aliases:
  - Por Modulo
---

# Requerimientos Por Modulo

Vista agrupada de los RFs por modulo del sidebar. Para el detalle completo ver [[03 - Tabla de Requerimientos]].

---

## Plataforma (panel del Superadmin)

Modulo cross-tenant para operacion del SaaS.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-01 | Crear tenant | ROL-01 | Alta |
| RF-02 | Asignar plan de licencia | ROL-01 | Alta |
| RF-03 | Cambiar calendario A/B del tenant | ROL-01 | Media |
| RF-50 | Acceder a logs globales de plataforma | ROL-01 | Alta |

---

## Configuracion del Colegio

Configuracion base del tenant. Solo el Rector la opera.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-04 | Configurar identidad institucional | ROL-02 | Alta |
| RF-05 | Configurar calendario y periodos | ROL-02 | Alta |
| RF-06 | Configurar jornadas y bloques horarios | ROL-02 | Alta |
| RF-07 | Configurar escala valorativa | ROL-02 | Alta |
| RF-08 | Configurar metodo de aprobacion | ROL-02 | Alta |
| RF-09 | Gestionar roles del tenant | ROL-02 | Alta |
| RF-10 | Crear y editar usuarios | ROL-02 | Alta |

---

## Plan de Estudios y Horarios

Estructura academica operativa.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-11 | Gestionar plan de estudios | ROL-03, ROL-05 | Alta |
| RF-12 | Crear y gestionar grupos | ROL-03, ROL-05 | Alta |
| RF-13 | Asignar docentes a materias y grupos | ROL-03, ROL-05 | Alta |
| RF-14 | Designar director de grupo | ROL-03, ROL-05 | Alta |
| RF-15 | Construir horarios de clase | ROL-03, ROL-05 | Alta |

---

## Notas y Consolidados

Registro y agregacion de calificaciones.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-16 | Registrar y editar notas en materia asignada | ROL-07 | Alta |
| RF-17 | Editar notas despues del cierre | ROL-02, ROL-03 | Media |
| RF-18 | Ver consolidados de notas por grupo | Multiples | Alta |
| RF-19 | Ver consolidado de todos los grupos | ROL-02, ROL-03, ROL-05 | Media |
| RF-20 | Cierre de periodo academico | ROL-02, ROL-03, ROL-05 | Alta |
| RF-21 | Gestion de nivelaciones y habilitaciones | ROL-02, ROL-03, ROL-05 | Media |

---

## Asistencia

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-22 | Registrar asistencia en clase propia | ROL-07 | Alta |
| RF-23 | Consultar asistencia del grupo dirigido | ROL-08 | Alta |

---

## Convivencia y Observador

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-24 | Registrar observacion academica en su materia | ROL-07 | Alta |
| RF-25 | Registrar anotacion en observador del grupo dirigido | ROL-08 | Alta |
| RF-26 | Registrar anotacion en observador de cualquier estudiante | ROL-04, ROL-05 | Alta |
| RF-27 | Definir tipologias de anotacion | ROL-04, ROL-05 | Media |
| RF-28 | Citar formalmente a acudientes | ROL-04, ROL-05 | Media |
| RF-29 | Generar reportes de convivencia | ROL-04, ROL-05 | Media |

---

## Matricula y Secretaria

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-30 | Registrar y editar estudiantes y acudientes | ROL-06 | Alta |
| RF-31 | Asignar estudiante a grupo | ROL-06, ROL-03 | Alta |
| RF-32 | Cargar y validar documentos de matricula | ROL-06 | Alta |
| RF-33 | Bloquear emision de documentos por pendientes | ROL-06 | Media |

---

## Documentos Oficiales

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-34 | Generar constancias de estudio | ROL-06 | Alta |
| RF-35 | Generar certificados de notas | ROL-06 | Alta |
| RF-36 | Generar paz y salvos | ROL-06 | Media |
| RF-37 | Reportar a SIMAT | ROL-06 | Alta |

---

## Boletines

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-38 | Generar boletin del grupo dirigido | ROL-08 | Alta |
| RF-39 | Aprobar / firmar boletines | ROL-02, ROL-03 | Alta |
| RF-40 | Agregar observacion general en boletin | ROL-08 | Media |
| RF-41 | Descargar boletin en PDF | Multiples | Alta |

---

## Comunicaciones

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-42 | Enviar comunicados al colegio entero | ROL-02 | Media |
| RF-43 | Comunicarse con acudientes via portal | Multiples | Media |
| RF-44 | Recibir notificaciones por correo | Todos | Alta |

---

## Portal Estudiantil / Acudientes

Solo consulta.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-45 | Consultar notas propias / del estudiante asociado | ROL-09 | Alta |
| RF-46 | Consultar horario | ROL-09 | Alta |
| RF-47 | Consultar boletines | ROL-09 | Alta |
| RF-48 | Consultar observador disciplinario | ROL-09 | Media |

---

## Auditoria

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-49 | Acceder a logs de auditoria del tenant | ROL-02 | Alta |
| RF-50 | Acceder a logs globales de plataforma | ROL-01 | Alta |

---

## Configuracion (Admin en pausa)

ROL-11 esta en pausa. Sus permisos se documentan pero no se implementan en MVP.

---

## No Funcionales (Transversal)

Ver RNF-01 a RNF-07 en [[03 - Tabla de Requerimientos]].

---

## Reglas de Negocio (resumen)

Ver [[07 - Reglas de Negocio]] para el detalle.

---

## Integraciones

| ID | Integracion | Modulo |
|---|---|---|
| RI-01 | Pasarelas de pago | Plataforma + Pagos |
| RI-02 | SIMAT | Documentos |
| RI-03 | Correo | Comunicaciones |
| RI-04 | SMS | Comunicaciones |
| RI-05 | DIAN | Facturacion |
| RI-06 | Almacenamiento | Plataforma |
| RI-07 | SSO | Autenticacion |
