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

## Bienestar y Servicios

Servicios de apoyo al estudiante. La mayoria son modulos configurables que el colegio activa segun su oferta. El Personal de Apoyo (ROL-12) opera Salud, Bienestar o Biblioteca segun su perfil.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-51 | Gestionar ficha medica del estudiante | ROL-12, ROL-09 | Media |
| RF-52 | Registrar atencion en enfermeria y suministro de medicamentos | ROL-12 | Media |
| RF-53 | Generar remision a centro medico y notificar | ROL-12 | Media |
| RF-54 | Gestionar expediente y citas de orientacion | ROL-12 | Media |
| RF-55 | Gestionar remisiones y plan de apoyo con doble visibilidad | ROL-12 | Media |
| RF-56 | Gestionar prestamos y devoluciones por ejemplar | ROL-12 | Baja |
| RF-57 | Gestionar reservas y multas | ROL-12 | Baja |
| RF-58 | Definir rutas, paradas y asignar estudiantes | ROL-06 | Baja |
| RF-59 | Registrar abordajes y generar cobro recurrente | ROL-06 | Baja |
| RF-60 | Configurar planes/menus y registrar consumo | ROL-06, ROL-12 | Baja |
| RF-61 | Registrar activos y gestionar prestamos a docentes | ROL-06 | Baja |
| RF-62 | Generar cobros puntuales o masivos a la cartera unica | ROL-06 | Media |

---

## Cumplimiento Colombia

Modulos de obligatorio cumplimiento normativo: convivencia escolar (Ley 1620), reportes oficiales al MEN (SIMAT / DANE / Saber) y proteccion de datos (Habeas Data, Ley 1581).

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-63 | Reportar y clasificar casos (tipo I/II/III) | ROL-04, ROL-05 | Alta |
| RF-64 | Ejecutar la Ruta de Atencion Integral y escalar tipo III | ROL-04, ROL-05, ROL-02 | Alta |
| RF-65 | Generar y firmar actas del Comite de Convivencia | ROL-02 | Media |
| RF-66 | Generar archivo de matricula SIMAT con validacion previa | ROL-06 | Alta |
| RF-67 | Generar formato DANE C-600 e inscripcion Saber (ICFES) | ROL-06 | Media |
| RF-68 | Capturar consentimientos granulares versionados | ROL-09, ROL-06 | Alta |
| RF-69 | Gestionar solicitudes ARCO con plazos legales | ROL-06 | Media |

---

## Admisiones

Proceso previo a la matricula. El aspirante no es usuario del sistema.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-70 | Registrar aspirantes con formulario y documentos | ROL-06 | Media |
| RF-71 | Agendar pruebas/entrevistas y decidir admision | ROL-06, ROL-03 | Media |
| RF-72 | Gestionar lista de espera y conversion a matricula | ROL-06 | Media |

---

## Talento Humano

Gestion del expediente y desempeno del personal docente.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-73 | Gestionar hoja de vida y contrato del docente | ROL-06, ROL-02 | Media |
| RF-74 | Gestionar evaluacion de desempeno y novedades laborales | ROL-02, ROL-03 | Media |

---

## Tareas, Encuestas y Eventos

Procesos academicos y de comunicacion complementarios.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-75 | Publicar tareas y recibir entregas versionadas | ROL-07 | Media |
| RF-76 | Retroalimentar y proponer nota de la tarea | ROL-07 | Media |
| RF-77 | Crear y consolidar encuestas institucionales | ROL-02, ROL-03 | Baja |
| RF-78 | Crear eventos y reservar espacios sin doble ocupacion | ROL-02, ROL-03 | Baja |
| RF-79 | Gestionar cupo, lista de espera y cobro del evento | ROL-02, ROL-03 | Baja |

---

## Valor Agregado

Diferenciadores estandar (RF-80..86) y funciones con IA selectiva (RF-87..89, proveedor Claude/Anthropic). Toda salida de IA requiere aprobacion humana (RR-18).

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-80 | App / Portal de acudientes con push y vista multi-hijo | Multiples | Media |
| RF-81 | Pagos sin friccion (medios locales + debito recurrente) | ROL-09 | Media |
| RF-82 | WhatsApp como canal oficial | Multiples | Media |
| RF-83 | Firma electronica de documentos | ROL-09, ROL-06 | Media |
| RF-84 | Carne digital con QR y control de acceso | Multiples | Baja |
| RF-85 | Tablero ejecutivo en tiempo real para el Rector | ROL-02 | Baja |
| RF-86 | Generador automatico de horarios | ROL-03, ROL-05 | Baja |
| RF-87 | Alertas tempranas de riesgo (scoring + explicacion IA) | ROL-02, ROL-03 | Media |
| RF-88 | Asistente de redaccion de observaciones y boletin | ROL-07 | Media |
| RF-89 | Asistente conversacional para acudientes | ROL-09 | Media |

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
| RI-08 | Firma electronica | Valor Agregado |
| RI-09 | WhatsApp Business API | Comunicaciones |
| RI-10 | IA Claude (Anthropic) | Valor Agregado IA |
| RI-11 | SIMAT / MEN (DANE / ICFES) | Cumplimiento Colombia |
