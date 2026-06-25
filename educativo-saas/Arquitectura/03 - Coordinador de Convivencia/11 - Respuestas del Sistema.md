---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-04
  - Coord. Convivencia Respuestas
---

# Respuestas del Sistema — Coordinador de Convivencia

Que responde el sistema ante cada evento.

| Evento | Respuesta del Sistema |
|---|---|
| Coordinador registra una anotacion en el observador | Guarda la anotacion con autor, tipo y nivel de visibilidad · si requiere confirmacion, la deja "Pendiente" y notifica al acudiente via portal · refleja la anotacion en la linea cronologica · registra en log (RR-03) |
| Acudiente confirma una anotacion | Cambia el estado a "Confirmada" · registra la confirmacion con fecha · notifica al coordinador |
| Coordinador anula una anotacion | Marca la anotacion como "Anulada" conservandola con su justificacion (RN-OE-003) · registra en log |
| Coordinador define una tipologia nueva | Agrega la tipologia al catalogo del colegio · la deja disponible para futuras anotaciones · no altera anotaciones historicas · registra en log |
| Docente o director de grupo reporta una situacion | Enruta el reporte a la bandeja del coordinador · genera notificacion · queda en estado "Reportado" hasta clasificarse |
| Coordinador clasifica un caso (tipo I/II/III) | Instancia el protocolo del tipo con plazos, responsables y actuaciones esperadas · abre el caso con consecutivo · registra la clasificacion auditada (RN-CVE-002) |
| Coordinador reclasifica un caso | Ajusta el protocolo al nuevo tipo · conserva el historial del tipo anterior · registra el cambio con motivo y autor |
| Caso se clasifica/escala a tipo III | Escala automaticamente al Rector · restringe la visibilidad del caso · bloquea el cierre hasta registrar el reporte a autoridad (RN-CVE-004) · notifica al Rector |
| Se registra dano al cuerpo en un caso | Marca la remision a EPS/urgencias como actuacion obligatoria · bloquea el cierre hasta registrarla (RN-CVE-005) · muestra alerta en el caso |
| Vence un plazo del protocolo sin actuacion | Genera alerta al coordinador y al Rector · marca la actuacion como vencida en el caso |
| Coordinador genera el acta del comite | Crea el acta con asistentes, hechos y compromisos · la deja pendiente de firma del Rector · al cargarse firmada queda inmutable (RN-CVE-006) |
| Coordinador registra acuerdos y compromisos | Guarda el acuerdo · genera automaticamente la anotacion correspondiente en el observador del estudiante (RN-CVE-007) · registra en log |
| Coordinador cierra un caso en seguimiento | Verifica que no haya actuaciones obligatorias pendientes · exige resolucion · cambia el estado a "Cerrado" · preserva el historial completo |
| Reincidencia o seguimiento incumplido | Reabre el caso o escala su tipo · notifica al coordinador · registra el evento |
| Coordinador cita formalmente a un acudiente | Programa la citacion · notifica fecha/hora/lugar por los canales habilitados sin revelar el motivo clinico (RN-BW-006) · registra en log |
| Coordinador genera un reporte de convivencia | Construye el reporte respetando el alcance del rol y la visibilidad de cada anotacion (RN-OE-005) · permite exportar a PDF · registra la consulta |
| Orientacion remite un caso a convivencia (configurable) | Enruta la remision a la bandeja del coordinador · muestra solo el contexto compartido · oculta el expediente clinico (RN-BW-002, RN-BW-008) |
| Alerta temprana de riesgo cruza el umbral | Enruta la alerta a convivencia (y/o orientacion) · muestra semaforo y recomendacion · no ejecuta accion automatica sobre el estudiante (RN-BW-007) |
| Intento de accion fuera de permiso (notas, otro tenant, expediente clinico) | Rechaza la accion en backend · muestra mensaje de permiso insuficiente · registra el intento en el log de seguridad (RR-02) |
| Login fallido del coordinador | Mensaje generico (no revela si el usuario existe) · incrementa contador de intentos · registra en log de seguridad |
| Cierre del ano lectivo | Vuelve inmutables los observadores y casos del ano · deja todo consultable · registra el cierre (RN-OE-004, RN-CVE-009) |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md` y `Logica del negocio/04-procesos-academicos/observador-del-estudiante.md`
