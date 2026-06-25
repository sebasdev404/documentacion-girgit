---
tags:
  - arquitectura
  - rol/rector
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-02
  - Rector Respuestas
---

# Respuestas del Sistema — Rector / Administrador del Colegio

Que responde el sistema ante cada evento. Toda accion sensible queda en el log de auditoria del tenant (RR-03).

| Evento | Respuesta del Sistema |
|---|---|
| Rector ingresa por primera vez (tenant recien creado) | Detecta configuracion vacia · abre el asistente de configuracion institucional · muestra checklist de pasos minimos para operar |
| Rector guarda la identidad institucional | Valida NIT y resolucion MEN · persiste los datos · habilita la emision de documentos oficiales · registra en log |
| Rector define calendario y periodos | Verifica que el calendario este habilitado por el plan · crea la estructura de periodos y fechas de cierre · habilita el registro de notas · registra en log |
| Rector define la escala valorativa | Persiste la escala · si hay notas previas, recalcula consolidados tras confirmacion · registra en log |
| Rector cambia el metodo de aprobacion | Aplica la nueva formula · advierte y recalcula consolidados afectados tras confirmacion · registra en log |
| Rector crea un usuario | Valida unicidad de correo/documento · crea la cuenta · asigna el rol (RR-04) · envia correo de acceso · registra en log |
| Rector hace carga masiva de usuarios | Procesa fila por fila · crea los validos · devuelve el listado de rechazados con su motivo · registra el lote en log |
| Rector desactiva un usuario | Bloquea su login · conserva todo su historial · invalida sus sesiones activas · registra en log |
| Rector activa/desactiva un permiso configurable | Aplica el cambio a todos los usuarios de ese rol · respeta los permisos estructurales · registra en log (RR-05) |
| Rector elige el esquema de coordinacion (RR-12) | Habilita un esquema y deshabilita el otro · impide convivencia de ambos · registra en log |
| Rector coordina el cierre de un periodo | Valida completitud de notas · bloquea la edicion ordinaria · habilita la generacion de boletines · notifica a docentes y coordinadores · registra en log |
| Rector edita una nota post-cierre (RR-07) | Exige justificacion · aplica el cambio · conserva el valor anterior en el historial · notifica al docente responsable · registra en log |
| Rector aprueba/firma un boletin (RF-39) | Marca el boletin como aprobado con autor y fecha · habilita su entrega oficial a las familias · registra la firma en log |
| Rector registra una anotacion en el observador (RF-26) | Guarda la anotacion con su tipologia · notifica al director de grupo y al acudiente segun configuracion · registra en log |
| Rector cita formalmente a un acudiente (RF-28) | Genera la citacion · la entrega por portal/correo · la agenda · registra en log |
| Rector emite un documento oficial (constancia/certificado/paz y salvo) | Verifica pendientes si el bloqueo esta activo (RR-08) · genera el PDF con la identidad institucional · registra la emision en log |
| Rector genera el reporte SIMAT (RR-15) | Construye el formato exigido por el MEN · valida completitud · marca el reporte como generado · registra en log |
| Rector envia un comunicado al colegio (RF-42) | Resuelve la audiencia · entrega por los canales elegidos (portal/correo/SMS) · registra el envio en log |
| Rector consulta el log de auditoria del tenant (RF-49) | Devuelve resultados filtrados, solo de su tenant (RR-01) · permite exportar · registra la exportacion |
| Login fallido del Rector | Mensaje generico (no revela si el usuario existe) · incrementa contador de intentos · registra en log de seguridad · bloquea tras N intentos |
| El Superadmin ejecuta una accion sobre el tenant (cambio de calendario, plan, suspension) | Notifica al Rector del cambio (RN-LA-002) · refleja el nuevo estado/configuracion · registra en el log del tenant |
| El Superadmin suspende el tenant | Bloquea el login del Rector y de todos los usuarios · muestra pantalla "colegio suspendido" · notifica al Rector por correo |
| Un servicio de bienestar (salud, transporte, etc.) registra una incidencia | Genera alerta en el dashboard del Rector · permite ver el detalle del servicio · registra en log |
| Un estudiante/grupo entra en mora (financiero) | Refleja el estado en cartera · si el bloqueo por pendientes esta activo, condiciona la emision de documentos (RR-08) · notifica segun politica |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio.md`
