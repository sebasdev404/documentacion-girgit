---
tags:
  - arquitectura
  - rol/docente
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-07
---

# Respuestas del Sistema — Docente

Que responde el sistema ante cada evento.

| Evento | Respuesta del Sistema |
|---|---|
| Docente inicia sesion por el subdominio | Infiere el tenant del subdominio · valida credenciales · arma el Home con las clases del dia segun el modelo pedagogico · registra el login en log del tenant |
| Docente registra una nota | Valida asignacion y periodo abierto · guarda la nota · recalcula el acumulado del estudiante en la materia · si el promedio cae bajo el minimo, lo refleja en la planilla · registra en log (RR-03) |
| Docente edita una nota (periodo abierto) | Actualiza el valor · recalcula el acumulado · registra el cambio con valor anterior y nuevo (RR-07) |
| Docente intenta editar nota con periodo cerrado | Bloquea; si el colegio activo el permiso, exige justificacion y registra el cambio como excepcion auditada |
| Docente toma asistencia | Guarda los estados P/A/T/E · marca la clase como registrada · registra en log |
| Inasistencia reiterada de un estudiante | El sistema NO se lo notifica al docente de materia; refleja la inasistencia en la vista consolidada del Director de Grupo / Coordinador |
| Docente agrega una observacion academica | Asocia la anotacion al estudiante en su materia con la visibilidad configurada · notifica al acudiente segun configuracion · registra en log |
| Docente remite un estudiante a enfermeria | Crea el reporte de remision · notifica al Personal de Apoyo (enfermeria) · registra en log |
| Docente reporta una situacion de convivencia | Crea el reporte y lo enruta al Coordinador de Convivencia para clasificacion · deja el caso en estado "Reportado" · registra en log (RN-CVE-002) |
| Docente marca "presunto delito" | Escala el caso de inmediato al Rector · restringe la visibilidad a coordinacion y rectoria · registra evento (RN-CVE-004) |
| Docente abre las alertas de salud de un estudiante | Devuelve solo las alergias/condiciones criticas autorizadas por el acudiente · oculta el resto de la ficha clinica (RN-SA-007) |
| Docente envia un mensaje a un acudiente (habilitado) | Entrega el mensaje por el portal · notifica al acudiente · registra la comunicacion |
| Coordinador cambia las asignaciones del docente | El sistema actualiza los grupos y materias visibles para el docente · retira de su vista lo que ya no dicta (RR-10) |
| Se aproxima el cierre de periodo | Notifica al docente · muestra la lista de notas pendientes por cargar antes del cierre |
| El Rector/Coordinador cierra el periodo | Bloquea la edicion de notas del docente · muestra mensaje de periodo cerrado en la planilla (RR-07) |
| Docente activa el complemento Director de Grupo (designacion del Coordinador) | El sistema le habilita, SOLO sobre el grupo dirigido, el consolidado del grupo, el observador disciplinario del grupo y los boletines del grupo (RR-09); en sus demas grupos sigue siendo solo Docente |
| Login fallido del docente | Mensaje generico (no revela si el usuario existe) · incrementa contador de intentos · registra en log de seguridad |
| Colegio suspendido por el Superadmin | Bloquea el login del docente · muestra pantalla "colegio suspendido" |
| Docente intenta una accion sin permiso (consolidados, configuracion, boletines) | El modulo no aparece en su sidebar; si llega por ruta directa, el backend rechaza y registra el intento (RR-02) |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/02-usuarios-roles-y-permisos/roles/06-docente.md`
