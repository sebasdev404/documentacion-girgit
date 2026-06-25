---
tags:
  - arquitectura
  - rol/docente
  - acciones
aliases:
  - Acciones ROL-07
---

# Acciones del Usuario — Docente

Tabla accion -> resultado. Cada accion sensible (notas, asistencia, observaciones) genera entrada en el log de auditoria del tenant (RR-03).

| Accion | Resultado |
|---|---|
| Inicia sesion por el subdominio del colegio | Sistema infiere el tenant del subdominio · valida credenciales · carga el Home con las clases del dia segun el modelo pedagogico · registra el login en log |
| Click en una clase del Home | Sistema abre la clase con accion rapida "Tomar asistencia" e "Ir a notas" para ese grupo+materia |
| Abre "Mis grupos y estudiantes" | Sistema muestra solo los grupos y materias asignados (RR-10) · no devuelve grupos que no dicta |
| Registra una nota en la planilla | Sistema valida que la materia/grupo este asignado y el periodo abierto · guarda la nota · recalcula el acumulado del estudiante · registra en log |
| Edita una nota con el periodo abierto | Sistema actualiza la nota · recalcula el acumulado · registra el cambio con valor anterior y nuevo en log (RR-07) |
| Intenta editar una nota con el periodo cerrado | Sistema bloquea; si el colegio activo el permiso configurable, exige justificacion antes de permitir · registra el evento |
| Carga una evidencia de evaluacion (si esta activo) | Sistema adjunta el archivo a la evaluacion · descuenta de la cuota del tenant · registra en log |
| Toma asistencia de la clase del dia | Sistema guarda los estados P/A/T/E · marca la asistencia del dia como registrada · alimenta los conteos para alertas tempranas · registra en log |
| Edita el registro de asistencia del dia | Sistema actualiza estados · registra el cambio con autor y hora |
| Agrega una observacion academica a un estudiante | Sistema asocia la anotacion al estudiante en SU materia con la visibilidad configurada · notifica segun configuracion · registra en log |
| Consulta su horario | Sistema muestra la vista semanal/diaria en solo lectura · permite exportar |
| Abre "Salud (alertas de aula)" | Sistema muestra unicamente las alergias/condiciones criticas autorizadas por el acudiente (RN-SA-007) · no muestra la ficha medica completa |
| Remite un estudiante a enfermeria | Sistema crea el reporte de remision · notifica al Personal de Apoyo · registra en log |
| Reporta una situacion de convivencia | Sistema crea el reporte y lo enruta al Coordinador de Convivencia para clasificacion · NO permite al docente clasificar el tipo (RN-CVE-002) · registra en log |
| Marca "presunto delito" en un reporte | Sistema escala de inmediato al Rector · restringe la visibilidad del caso · registra evento (RN-CVE-004) |
| Inicia/responde un mensaje a un acudiente (si esta habilitado) | Sistema entrega el mensaje al acudiente del estudiante · registra la comunicacion · si el permiso esta desactivado, oculta la accion |
| Recibe notificacion de cierre de periodo proximo | Sistema muestra alerta y lista de notas pendientes por cargar antes del cierre |
| Cierra sesion | Sistema invalida el token · registra logout en log |

## Relacionado

- [[10 - Validaciones]] — que bloquea el sistema en cada accion
- [[11 - Respuestas del Sistema]] — eventos y respuestas
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
