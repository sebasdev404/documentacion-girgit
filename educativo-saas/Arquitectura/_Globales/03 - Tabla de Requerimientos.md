---
tags:
  - arquitectura
  - requerimientos
aliases:
  - Tabla Requerimientos
---

# Tabla de Requerimientos

| Documento | Tabla de Requerimientos |
|---|---|
| Version | 0.1 |
| Estado | Borrador |
| Relacionado a | [[02 - PRD - Plataforma]] |

---

## Tipos de Requerimiento

| Prefijo | Tipo | Define |
|---|---|---|
| RF | Funcional | QUE hace el sistema |
| RNF | No Funcional | COMO lo hace |
| RR | de Negocio | POR QUE existe |
| RI | de Integracion | CON QUE conecta |

## Prioridad

| Codigo | Significado |
|---|---|
| Alta | Bloqueante para arrancar |
| Media | Necesario en MVP |
| Baja | Mejora |

## Estado

| Codigo | Significado |
|---|---|
| Pendiente | No iniciado |
| En curso | En desarrollo |
| Bloqueado | Esperando dependencia |
| Listo | Implementado y aprobado |

---

## Tabla maestra

| ID | Tipo | Modulo | Requerimiento | Descripcion | Rol(es) | AC | Prioridad | Estado | Notas |
|---|---|---|---|---|---|---|---|---|---|
| RF-01 | RF | Plataforma | Crear tenant | Superadmin crea un colegio nuevo, provisionando schema y semillas | ROL-01 | AC-01 | Alta | Pendiente | |
| RF-02 | RF | Plataforma | Asignar plan de licencia | Superadmin asigna plan basico/estandar/premium a un tenant | ROL-01 | | Alta | Pendiente | |
| RF-03 | RF | Plataforma | Cambiar calendario A/B del tenant | Superadmin cambia el calendario habilitado de un tenant | ROL-01 | | Media | Pendiente | |
| RF-04 | RF | Configuracion colegio | Configurar identidad institucional | Rector define nombre, logo, NIT, resolucion MEN | ROL-02 | | Alta | Pendiente | |
| RF-05 | RF | Configuracion colegio | Configurar calendario y periodos | Rector elige A o B y define fechas de cada periodo lectivo | ROL-02 | | Alta | Pendiente | |
| RF-06 | RF | Configuracion colegio | Configurar jornadas y bloques horarios | Rector crea jornadas (Manana, Tarde) y bloques de clase | ROL-02 | | Alta | Pendiente | |
| RF-07 | RF | Configuracion colegio | Configurar escala valorativa | Rector define escala numerica o por imagenes (preescolar) | ROL-02 | | Alta | Pendiente | |
| RF-08 | RF | Configuracion colegio | Configurar metodo de aprobacion | Rector elige promedio / ponderado / sumatoria + nota minima | ROL-02 | | Alta | Pendiente | |
| RF-09 | RF | Usuarios y roles | Gestionar roles del tenant | Rector activa/desactiva permisos configurables, renombra roles | ROL-02 | | Alta | Pendiente | |
| RF-10 | RF | Usuarios y roles | Crear y editar usuarios | Rector crea cuentas de todos los actores internos | ROL-02 | | Alta | Pendiente | |
| RF-11 | RF | Plan de estudios | Gestionar plan de estudios | Materias por grado, intensidad horaria, areas | ROL-03, ROL-05 | | Alta | Pendiente | |
| RF-12 | RF | Plan de estudios | Crear y gestionar grupos | Por grado y ano lectivo | ROL-03, ROL-05 | | Alta | Pendiente | |
| RF-13 | RF | Plan de estudios | Asignar docentes a materias y grupos | | ROL-03, ROL-05 | | Alta | Pendiente | |
| RF-14 | RF | Plan de estudios | Designar director de grupo | | ROL-03, ROL-05 | | Alta | Pendiente | |
| RF-15 | RF | Horarios | Construir horarios de clase | Docente / materia / aula / bloque / dia | ROL-03, ROL-05 | | Alta | Pendiente | |
| RF-16 | RF | Notas | Registrar y editar notas en materia asignada | | ROL-07 | | Alta | Pendiente | |
| RF-17 | RF | Notas | Editar notas despues del cierre | Configurable; con justificacion | ROL-02, ROL-03 | | Media | Pendiente | RR-07 |
| RF-18 | RF | Notas | Ver consolidados de notas por grupo | | ROL-02, ROL-03, ROL-05, ROL-08 | | Alta | Pendiente | |
| RF-19 | RF | Notas | Ver consolidado de todos los grupos | | ROL-02, ROL-03, ROL-05 | | Media | Pendiente | |
| RF-20 | RF | Notas | Cierre de periodo academico | | ROL-02, ROL-03, ROL-05 | | Alta | Pendiente | |
| RF-21 | RF | Notas | Gestion de nivelaciones y habilitaciones | | ROL-02, ROL-03, ROL-05 | | Media | Pendiente | |
| RF-22 | RF | Asistencia | Registrar asistencia en clase propia | | ROL-07 | | Alta | Pendiente | |
| RF-23 | RF | Asistencia | Consultar asistencia del grupo dirigido | | ROL-08 | | Alta | Pendiente | |
| RF-24 | RF | Convivencia | Registrar observacion academica en su materia | | ROL-07 | | Alta | Pendiente | |
| RF-25 | RF | Convivencia | Registrar anotacion en observador del grupo dirigido | | ROL-08 | | Alta | Pendiente | |
| RF-26 | RF | Convivencia | Registrar anotacion en observador de cualquier estudiante | | ROL-04, ROL-05 | | Alta | Pendiente | |
| RF-27 | RF | Convivencia | Definir tipologias de anotacion | Leve / grave / gravisima, etc. | ROL-04, ROL-05 | | Media | Pendiente | |
| RF-28 | RF | Convivencia | Citar formalmente a acudientes | Configurable | ROL-04, ROL-05 | | Media | Pendiente | |
| RF-29 | RF | Convivencia | Generar reportes de convivencia | | ROL-04, ROL-05 | | Media | Pendiente | |
| RF-30 | RF | Matricula | Registrar y editar estudiantes y acudientes | | ROL-06 | | Alta | Pendiente | |
| RF-31 | RF | Matricula | Asignar estudiante a grupo | Configurable: secretaria o coordinador | ROL-06, ROL-03 | | Alta | Pendiente | |
| RF-32 | RF | Matricula | Cargar y validar documentos de matricula | | ROL-06 | | Alta | Pendiente | |
| RF-33 | RF | Matricula | Bloquear emision de documentos por pendientes | Configurable | ROL-06 | | Media | Pendiente | RR-08 |
| RF-34 | RF | Documentos | Generar constancias de estudio | | ROL-06 | | Alta | Pendiente | |
| RF-35 | RF | Documentos | Generar certificados de notas | | ROL-06 | | Alta | Pendiente | |
| RF-36 | RF | Documentos | Generar paz y salvos | | ROL-06 | | Media | Pendiente | |
| RF-37 | RF | Documentos | Reportar a SIMAT | | ROL-06 | | Alta | Pendiente | RI-02 |
| RF-38 | RF | Boletines | Generar boletin del grupo dirigido | | ROL-08 | | Alta | Pendiente | |
| RF-39 | RF | Boletines | Aprobar / firmar boletines | Configurable | ROL-02, ROL-03 | | Alta | Pendiente | |
| RF-40 | RF | Boletines | Agregar observacion general en boletin | | ROL-08 | | Media | Pendiente | |
| RF-41 | RF | Boletines | Descargar boletin en PDF | | Multiples | | Alta | Pendiente | |
| RF-42 | RF | Comunicaciones | Enviar comunicados al colegio entero | Configurable | ROL-02 | | Media | Pendiente | |
| RF-43 | RF | Comunicaciones | Comunicarse con acudientes via portal | Configurable | Multiples | | Media | Pendiente | |
| RF-44 | RF | Comunicaciones | Recibir notificaciones por correo | | Todos | | Alta | Pendiente | RI-03 |
| RF-45 | RF | Portal | Consultar notas propias / del estudiante asociado | | ROL-09 | | Alta | Pendiente | |
| RF-46 | RF | Portal | Consultar horario | | ROL-09 | | Alta | Pendiente | |
| RF-47 | RF | Portal | Consultar boletines | | ROL-09 | | Alta | Pendiente | |
| RF-48 | RF | Portal | Consultar observador disciplinario | Configurable | ROL-09 | | Media | Pendiente | |
| RF-49 | RF | Auditoria | Acceder a logs de auditoria del tenant | | ROL-02 | | Alta | Pendiente | RR-03 |
| RF-50 | RF | Auditoria | Acceder a logs globales de plataforma | | ROL-01 | | Alta | Pendiente | |
| RNF-01 | RNF | Plataforma | Aislamiento total entre tenants a nivel BD | Schema separado por colegio | Todos | | Alta | Pendiente | RR-01 |
| RNF-02 | RNF | Plataforma | Verificacion de permisos en frontend y backend | | Todos | | Alta | Pendiente | RR-02 |
| RNF-03 | RNF | Plataforma | Auditoria de acciones sensibles | Logs inmutables | Todos | | Alta | Pendiente | RR-03 |
| RNF-04 | RNF | Plataforma | Acceso por subdominio del colegio | | Todos | | Alta | Pendiente | RR-06 |
| RNF-05 | RNF | Plataforma | Disponibilidad >= 99.5% mensual | | Todos | | Alta | Pendiente | |
| RNF-06 | RNF | Plataforma | Backup automatico diario del schema | Por tenant | Todos | | Alta | Pendiente | |
| RNF-07 | RNF | Plataforma | Cumplimiento Ley 1581 (proteccion de datos Colombia) | | Todos | | Alta | Pendiente | |
| RR-01 | RR | Plataforma | Aislamiento total entre tenants | Ver [[07 - Reglas de Negocio]] | | | Alta | Pendiente | |
| RR-02 | RR | Plataforma | Verificacion de permisos frontend y backend | | | | Alta | Pendiente | |
| RR-03 | RR | Plataforma | Auditoria obligatoria | | | | Alta | Pendiente | |
| RR-04 | RR | Plataforma | Asignacion de roles por el rector | | | | Alta | Pendiente | |
| RR-05 | RR | Plataforma | Configurabilidad acotada de permisos | | | | Alta | Pendiente | |
| RR-06 | RR | Plataforma | Acceso por subdominio del colegio | | | | Alta | Pendiente | |
| RR-07 | RR | Notas | Notas se editan dentro del periodo abierto | Configurable post-cierre | | | Alta | Pendiente | |
| RR-08 | RR | Matricula | Bloqueo de documentos por pendientes | Configurable | | | Media | Pendiente | |
| RI-01 | RI | Pagos | Pasarelas de pago | | | | Alta | Pendiente | |
| RI-02 | RI | Reportes | SIMAT (MEN Colombia) | | | | Alta | Pendiente | |
| RI-03 | RI | Comunicaciones | Correo electronico | | | | Alta | Pendiente | |
| RI-04 | RI | Comunicaciones | SMS | | | | Media | Pendiente | |
| RI-05 | RI | Facturacion | DIAN (facturacion electronica) | | | | Alta | Pendiente | |
| RI-06 | RI | Plataforma | Almacenamiento en la nube | | | | Alta | Pendiente | |
| RI-07 | RI | Autenticacion | SSO Google/Microsoft (opcional) | | | | Baja | Pendiente | |

---

## Notas

- Esta tabla es el indice maestro. El detalle de cada RR esta en [[07 - Reglas de Negocio]].
- Los AC se asignan en [[08 - Criterios de Aceptacion]].
- Los RFs marcados como "configurables" implican que un colegio puede activarlos o desactivarlos via configuracion del rol correspondiente.
