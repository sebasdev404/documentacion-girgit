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
| RF-51 | RF | Salud y enfermeria | Gestionar ficha medica del estudiante | Dato sensible; la diligencia el acudiente, la consulta enfermeria | ROL-12, ROL-09 | AC-26 | Media | Pendiente | RN-SA-001 |
| RF-52 | RF | Salud y enfermeria | Registrar atencion en enfermeria y suministro de medicamentos | Suministro solo con autorizacion vigente del acudiente | ROL-12 | AC-26 | Media | Pendiente | RN-SA-003 |
| RF-53 | RF | Salud y enfermeria | Generar remision a centro medico y notificar | Remision escala a Coordinacion de Convivencia y acudiente | ROL-12 | | Media | Pendiente | RN-SA-006 |
| RF-54 | RF | Bienestar y orientacion | Gestionar expediente y citas de orientacion | Expediente sensible; citas sin exponer motivo | ROL-12 | AC-26 | Media | Pendiente | RN-BW-001 |
| RF-55 | RF | Bienestar y orientacion | Gestionar remisiones y plan de apoyo con doble visibilidad | Remision externa exige consentimiento del acudiente | ROL-12 | AC-29 | Media | Pendiente | RN-BW-005 |
| RF-56 | RF | Biblioteca | Gestionar prestamos y devoluciones por ejemplar | Vencimiento calculado por configuracion; trazabilidad por ejemplar | ROL-12 | | Baja | Pendiente | RN-BI-001 |
| RF-57 | RF | Biblioteca | Gestionar reservas y multas | Multa configurable; puede integrar a la cartera unica del estudiante | ROL-12 | AC-27 | Baja | Pendiente | RN-BI-006 |
| RF-58 | RF | Transporte escolar | Definir rutas, paradas y asignar estudiantes | Una asignacion por sentido; valida cupo | ROL-06 | | Baja | Pendiente | RN-TR-001 |
| RF-59 | RF | Transporte escolar | Registrar abordajes y generar cobro recurrente | Abordaje/descenso notifica al acudiente; cobro a la cartera unica | ROL-06 | AC-27 | Baja | Pendiente | RN-TR-003 |
| RF-60 | RF | Restaurante y comedor | Configurar planes/menus y registrar consumo | Bloqueo por alergia severa; cobro a la cartera unica | ROL-06, ROL-12 | AC-27 | Baja | Pendiente | RN-RE-003 |
| RF-61 | RF | Inventario y activos | Registrar activos y gestionar prestamos a docentes | Placa unica por tenant; activo siempre localizado | ROL-06 | | Baja | Pendiente | RN-IV-001 |
| RF-62 | RF | Tienda y otros cobros | Generar cobros puntuales o masivos a la cartera unica | Otros cobros entran a la cartera unica del estudiante sin split | ROL-06 | AC-27 | Media | Pendiente | RR-17, RN-PP-120 |
| RF-63 | RF | Convivencia Ley 1620 | Reportar y clasificar casos (tipo I/II/III) | Clasificacion auditada; protocolo segun tipo | ROL-04, ROL-05 | | Alta | Pendiente | RR-20, RN-CVE-002 |
| RF-64 | RF | Convivencia Ley 1620 | Ejecutar la Ruta de Atencion Integral y escalar tipo III | Tipo III escala al Rector con constancia de reporte a autoridad | ROL-04, ROL-05, ROL-02 | | Alta | Pendiente | RR-20, RN-CVE-004 |
| RF-65 | RF | Convivencia Ley 1620 | Generar y firmar actas del Comite de Convivencia | Acta inmutable una vez firmada por el Rector | ROL-02 | | Media | Pendiente | RN-CVE-006 |
| RF-66 | RF | Reportes oficiales MEN | Generar archivo de matricula SIMAT con validacion previa | Validacion bloqueante contra catalogos oficiales | ROL-06 | AC-30 | Alta | Pendiente | RN-MO-001, RI-11 |
| RF-67 | RF | Reportes oficiales MEN | Generar formato DANE C-600 e inscripcion Saber (ICFES) | Edad a fecha de corte DANE; segmentado por codigo DANE de sede | ROL-06 | AC-30 | Media | Pendiente | RN-MO-008 |
| RF-68 | RF | Habeas Data | Capturar consentimientos granulares versionados | Casillas no premarcadas; atadas a version de politica vigente | ROL-09, ROL-06 | AC-29 | Alta | Pendiente | RR-19, RN-HD-002 |
| RF-69 | RF | Habeas Data | Gestionar solicitudes ARCO con plazos legales | Contador de vencimiento (10/15 dias habiles); retencion justificada | ROL-06 | AC-29 | Media | Pendiente | RN-HD-007 |
| RF-70 | RF | Admisiones | Registrar aspirantes con formulario y documentos | Aspirante no es usuario; codigo de aspirante unico | ROL-06 | | Media | Pendiente | RN-AM-002 |
| RF-71 | RF | Admisiones | Agendar pruebas/entrevistas y decidir admision | Decision justificada y auditada; cupo verificado | ROL-06, ROL-03 | | Media | Pendiente | RN-AM-007 |
| RF-72 | RF | Admisiones | Gestionar lista de espera y conversion a matricula | Emite PIN de matricula sin recobrar derecho de inscripcion | ROL-06 | | Media | Pendiente | RN-AM-008 |
| RF-73 | RF | Talento humano | Gestionar hoja de vida y contrato del docente | Expediente unico por docente; un contrato vigente | ROL-06, ROL-02 | | Media | Pendiente | RN-RH-001 |
| RF-74 | RF | Talento humano | Gestionar evaluacion de desempeno y novedades laborales | Evaluacion cerrada inmutable; novedad suspende disponibilidad | ROL-02, ROL-03 | | Media | Pendiente | RN-RH-004 |
| RF-75 | RF | Tareas y actividades | Publicar tareas y recibir entregas versionadas | Solo en asignacion activa; fecha limite obligatoria | ROL-07 | | Media | Pendiente | RN-TA-001 |
| RF-76 | RF | Tareas y actividades | Retroalimentar y proponer nota de la tarea | Propone nota; la nota oficial se confirma en Calificaciones | ROL-07 | | Media | Pendiente | RN-TA-005 |
| RF-77 | RF | Encuestas | Crear y consolidar encuestas institucionales | Anonimato irreversible; evaluacion docente siempre anonima | ROL-02, ROL-03 | | Baja | Pendiente | RN-EC-004 |
| RF-78 | RF | Eventos y reservas | Crear eventos y reservar espacios sin doble ocupacion | Salida exige autorizacion firmada electronicamente | ROL-02, ROL-03 | | Baja | Pendiente | RN-EV-002 |
| RF-79 | RF | Eventos y reservas | Gestionar cupo, lista de espera y cobro del evento | Cobro independiente de la pension; lista de espera por orden | ROL-02, ROL-03 | AC-27 | Baja | Pendiente | RN-EV-005 |
| RF-80 | RF | Valor agregado | App / Portal de acudientes con push y vista multi-hijo | Selector multi-hijo sin fusionar expedientes | Multiples | | Media | Pendiente | RN-VA-001 |
| RF-81 | RF | Valor agregado | Pagos sin friccion (medios locales + debito recurrente) | PSE, Nequi, Daviplata, link de pago; medios configurables | ROL-09 | | Media | Pendiente | RN-VA-002 |
| RF-82 | RF | Valor agregado | WhatsApp como canal oficial | Solo con opt-in y plantillas aprobadas | Multiples | | Media | Pendiente | RN-VA-003, RI-09 |
| RF-83 | RF | Valor agregado | Firma electronica de documentos | Sello de tiempo, hash y trazabilidad legal inmutable | ROL-09, ROL-06 | AC-29 | Media | Pendiente | RN-VA-004, RI-08 |
| RF-84 | RF | Valor agregado | Carne digital con QR y control de acceso | Lectura valida notifica ingreso/salida al acudiente | Multiples | | Baja | Pendiente | RN-VA-005 |
| RF-85 | RF | Valor agregado | Tablero ejecutivo en tiempo real para el Rector | Respeta alcance y permisos del rol | ROL-02 | | Baja | Pendiente | RN-VA-006 |
| RF-86 | RF | Valor agregado | Generador automatico de horarios | Propuesta en borrador; requiere aprobacion humana | ROL-03, ROL-05 | AC-28 | Baja | Pendiente | RN-VA-007 |
| RF-87 | RF | Valor agregado IA | Alertas tempranas de riesgo (scoring + explicacion IA) | Scoring determinista; IA solo redacta la explicacion | ROL-02, ROL-03 | AC-28 | Media | Pendiente | RN-VA-101, RI-10 |
| RF-88 | RF | Valor agregado IA | Asistente de redaccion de observaciones y boletin | Genera borradores; el docente edita y aprueba | ROL-07 | AC-28 | Media | Pendiente | RN-VA-102, RI-10 |
| RF-89 | RF | Valor agregado IA | Asistente conversacional para acudientes | Alcance por vinculo; escala a humano en temas sensibles | ROL-09 | AC-28 | Media | Pendiente | RN-VA-103, RI-10 |
| RNF-01 | RNF | Plataforma | Aislamiento total entre tenants a nivel BD | Schema separado por colegio | Todos | | Alta | Pendiente | RR-01 |
| RNF-02 | RNF | Plataforma | Verificacion de permisos en frontend y backend | | Todos | | Alta | Pendiente | RR-02 |
| RNF-03 | RNF | Plataforma | Auditoria de acciones sensibles | Logs inmutables | Todos | | Alta | Pendiente | RR-03 |
| RNF-04 | RNF | Plataforma | Acceso por subdominio del colegio | | Todos | | Alta | Pendiente | RR-06 |
| RNF-05 | RNF | Plataforma | Disponibilidad >= 99.5% mensual | | Todos | | Alta | Pendiente | |
| RNF-06 | RNF | Plataforma | Backup automatico diario del schema | Por tenant | Todos | | Alta | Pendiente | |
| RNF-07 | RNF | Plataforma | Cumplimiento Ley 1581 (proteccion de datos Colombia) | | Todos | | Alta | Pendiente | |
| RNF-08 | RNF | Valor agregado IA | Trazabilidad y aislamiento por tenant de las invocaciones de IA | Cada invocacion registra prompt/modelo/salida/solicitante/aprobador; contexto solo del tenant; sin entrenamiento con datos del menor | Todos | | Alta | Pendiente | RN-VA-112, RN-VA-113 |
| RR-01 | RR | Plataforma | Aislamiento total entre tenants | Ver [[07 - Reglas de Negocio]] | | | Alta | Pendiente | |
| RR-02 | RR | Plataforma | Verificacion de permisos frontend y backend | | | | Alta | Pendiente | |
| RR-03 | RR | Plataforma | Auditoria obligatoria | | | | Alta | Pendiente | |
| RR-04 | RR | Plataforma | Asignacion de roles por el rector | | | | Alta | Pendiente | |
| RR-05 | RR | Plataforma | Configurabilidad acotada de permisos | | | | Alta | Pendiente | |
| RR-06 | RR | Plataforma | Acceso por subdominio del colegio | | | | Alta | Pendiente | |
| RR-07 | RR | Notas | Notas se editan dentro del periodo abierto | Configurable post-cierre | | | Alta | Pendiente | |
| RR-08 | RR | Matricula | Bloqueo de documentos por pendientes | Configurable | | | Media | Pendiente | |
| RR-09 | RR | Roles | Director de Grupo solo opera sobre su grupo | Ver [[07 - Reglas de Negocio]] | ROL-08 | | Alta | Pendiente | |
| RR-10 | RR | Roles | Docente ve solo grupos y materias asignados | | ROL-07 | | Alta | Pendiente | |
| RR-11 | RR | Roles | El menor tiene una unica cuenta (Estudiante) | No existe rol Acudiente como usuario | ROL-09 | | Alta | Pendiente | |
| RR-12 | RR | Roles | Coordinador combinado excluye los separados | | ROL-03, ROL-04, ROL-05 | | Alta | Pendiente | |
| RR-13 | RR | Plataforma | Cambio de calendario A/B es del Superadmin | | ROL-01, ROL-02 | | Alta | Pendiente | |
| RR-14 | RR | Portal | Acudiente con varios hijos usa selector de estudiante | Sin fusionar expedientes ni pagos entre hermanos | ROL-09 | | Media | Pendiente | |
| RR-15 | RR | Reportes | Reporte SIMAT obligatorio | | ROL-06 | | Alta | Pendiente | |
| RR-16 | RR | Bienestar y servicios | Visibilidad triple del observador para Personal de Apoyo | Aportes del Personal de Apoyo usan RN-OB-081; por defecto interna | ROL-12 | AC-26 | Media | Pendiente | RN-OB-081 |
| RR-17 | RR | Tienda y otros cobros | Otros cobros entran a la cartera unica del estudiante sin split | Sin split entre hermanos ni acudientes | ROL-06 | AC-27 | Media | Pendiente | RN-PP-120 |
| RR-18 | RR | Valor agregado IA | IA siempre con humano en el bucle | Ninguna salida de IA surte efecto sin aprobacion humana | Todos | AC-28 | Alta | Pendiente | RN-VA-110 |
| RR-19 | RR | Habeas Data | Tratamiento de datos del menor exige consentimiento | Lo otorga el acudiente con patria potestad (Ley 1581) | ROL-09, ROL-06 | AC-29 | Alta | Pendiente | RN-HD-001 |
| RR-20 | RR | Convivencia Ley 1620 | Convivencia sigue la Ruta de Atencion Integral Ley 1620 | RAI con protocolo segun tipo; tipo III escala al Rector | ROL-04, ROL-05 | | Alta | Pendiente | RN-CVE-003 |
| RI-01 | RI | Pagos | Pasarelas de pago | | | | Alta | Pendiente | |
| RI-02 | RI | Reportes | SIMAT (MEN Colombia) | | | | Alta | Pendiente | |
| RI-03 | RI | Comunicaciones | Correo electronico | | | | Alta | Pendiente | |
| RI-04 | RI | Comunicaciones | SMS | | | | Media | Pendiente | |
| RI-05 | RI | Facturacion | DIAN (facturacion electronica) | | | | Alta | Pendiente | |
| RI-06 | RI | Plataforma | Almacenamiento en la nube | | | | Alta | Pendiente | |
| RI-07 | RI | Autenticacion | SSO Google/Microsoft (opcional) | | | | Baja | Pendiente | |
| RI-08 | RI | Valor agregado | Firma electronica | Sello de tiempo, hash y trazabilidad legal de documentos | | | Media | Pendiente | RN-VA-004 |
| RI-09 | RI | Comunicaciones | WhatsApp Business API | Canal oficial con plantillas aprobadas y opt-in | | | Media | Pendiente | RN-VA-003 |
| RI-10 | RI | Valor agregado IA | IA Claude (Anthropic) | Modelos Claude para alertas, redaccion y asistente conversacional | | | Media | Pendiente | RN-VA-118 |
| RI-11 | RI | Reportes | SIMAT / MEN (DANE / ICFES) | Cargue manual de archivos oficiales; no integracion en linea | | | Alta | Pendiente | RN-MO-001 |

---

## Notas

- Esta tabla es el indice maestro. El detalle de cada RR esta en [[07 - Reglas de Negocio]].
- Los AC se asignan en [[08 - Criterios de Aceptacion]].
- Los RFs marcados como "configurables" implican que un colegio puede activarlos o desactivarlos via configuracion del rol correspondiente.
