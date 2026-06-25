---
tags:
  - arquitectura
  - rol/director-de-grupo
  - acciones
aliases:
  - Acciones ROL-08
---

# Acciones del Usuario — Director de Grupo

Tabla accion -> resultado del complemento sobre el grupo dirigido. Cada accion sensible (observador, boletin, convivencia, citacion, edicion de notas) genera entrada en el log del tenant (RR-03).

> Las acciones como Docente (calificar sus materias, registrar asistencia de sus clases) se documentan en [[../06 - Docente/08 - Acciones del Usuario|Acciones del Docente]]. Aqui solo lo adicional.

| Accion | Resultado |
|---|---|
| Abre "Inicio — Mi grupo dirigido" | Sistema carga tarjetas resumen del grupo (estudiantes, estado del periodo, boletines pendientes, alertas) · si dirige varios grupos muestra el selector |
| Cambia de grupo en el selector del header | Sistema conmuta el contexto de toda la pantalla al nuevo grupo dirigido |
| Abre el consolidado del grupo (RF-18) | Sistema muestra todas las materias del grupo con notas (solo lectura) · permite filtrar por periodo/materia/estudiante |
| Descarga el consolidado en PDF | Sistema genera el PDF del consolidado con marca de quien y cuando descargo · registra en log |
| Consulta la asistencia del grupo (RF-23) | Sistema muestra inasistencia por estudiante y materia con semaforo de alerta |
| Click en "Generar boletines del grupo" (RF-38) | Sistema valida que las notas del periodo esten cerradas · si faltan notas advierte y lista los faltantes · genera los boletines · registra en log |
| Escribe una observacion general en el boletin de un estudiante (RF-40) | Sistema guarda la observacion asociada al estudiante y al periodo · queda visible en el boletin · registra en log |
| Click en "Aprobar / firmar boletin" (RF-39, si esta activado) | Sistema marca el boletin como firmado por el director · lo deja disponible para el acudiente · registra en log |
| Descarga un boletin en PDF | Sistema genera el PDF del boletin · registra en log |
| Registra una anotacion en el observador del grupo (RF-25) | Sistema guarda la anotacion sobre el estudiante del grupo · aplica la visibilidad configurada (RN-OB-081) · si requiere confirmacion, notifica al acudiente · registra en log |
| Adjunta evidencia a una anotacion | Sistema asocia el archivo a la anotacion sujeto a cuota del tenant · registra en log |
| Edita una nota de una materia que no dicta (configurable) | Si el permiso esta activado: exige justificacion · aplica el cambio · registra en log con valor anterior y nuevo (RR-09) · si no esta activado: bloquea la accion |
| Edita una nota despues del cierre (RF-17, configurable) | Si esta activado: exige justificacion · aplica el cambio · registra en log (RR-07) · si no: bloquea |
| Reporta una situacion de convivencia del grupo | Sistema crea el reporte y lo envia al Coord. de Convivencia para clasificar · queda en estado "Reportado" · registra en log |
| Aplica una medida pedagogica tipo I en el aula | Sistema registra la medida como actuacion tipo I · genera la anotacion correspondiente en el observador (RN-CVE-007) · registra en log |
| Marca un reporte como "presunto delito" | Sistema escala automaticamente al Rector · restringe la visibilidad del caso · notifica al Rector (RN-CVE-004) |
| Registra el seguimiento de un acuerdo de convivencia | Sistema actualiza el estado del seguimiento · si el acuerdo se incumple deja el caso disponible para reapertura · registra en log |
| Cita formalmente a un acudiente (configurable) | Si esta activado: crea la citacion · notifica al acudiente · registra en log · si no: ofrece "solicitar citacion al Coordinador" |
| Solicita una citacion al Coordinador (cuando no tiene permiso directo) | Sistema envia la solicitud al Coord. de Convivencia · registra en log |
| Envia un mensaje a un acudiente del grupo (configurable) | Sistema entrega el mensaje por el portal/canal habilitado · registra la comunicacion · el acudiente opera la cuenta del Estudiante (RR-11) |
| Intenta abrir el consolidado/observador de un grupo que NO dirige | Sistema no lo muestra; backend rechaza por scope (RR-09, RR-02) |
| Cierra sesion | Sistema invalida token · registra logout en log |

## Relacionado

- [[10 - Validaciones]] — que bloquea el sistema en cada accion
- [[11 - Respuestas del Sistema]] — eventos y respuestas
- [[09 - Campos del Formulario]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
