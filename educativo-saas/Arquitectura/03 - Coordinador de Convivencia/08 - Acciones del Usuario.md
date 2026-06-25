---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
  - acciones
aliases:
  - Acciones ROL-04
  - Coord. Convivencia Acciones
---

# Acciones del Usuario — Coordinador de Convivencia

Tabla accion -> resultado. Cada accion sensible genera entrada en el log de auditoria del tenant (RR-03).

| Accion | Resultado |
|---|---|
| Busca un estudiante y abre su observador | Sistema verifica alcance (cualquier estudiante del tenant, RR-01) · muestra la linea cronologica de anotaciones del ano lectivo |
| Click en "Registrar anotacion" y completa el formulario (RF-26) | Sistema valida campos · guarda la anotacion con tipo, autor y nivel de visibilidad (RN-OB-081) · si requiere confirmacion, la marca "Pendiente de confirmacion" y notifica al acudiente · registra en log |
| Edita una anotacion propia dentro del periodo abierto | Sistema aplica el cambio · conserva version anterior en historial · registra en log |
| Anula una anotacion | Sistema exige justificacion · marca la anotacion como Anulada sin borrarla (RN-OE-003) · registra en log |
| Cierra / archiva una anotacion | Sistema cambia el estado a cerrada · la deja consultable · registra en log |
| Solicita confirmacion del acudiente | Sistema notifica via portal · queda en estado Pendiente hasta que el acudiente confirme · registra la confirmacion cuando ocurre |
| Define o edita una tipologia de anotacion (RF-27) | Sistema valida nombre unico · agrega/actualiza el catalogo del colegio · no afecta anotaciones historicas ya creadas · registra en log |
| Recibe un reporte de situacion y lo clasifica en tipo I/II/III | Sistema exige la clasificacion antes de avanzar (RN-CVE-002) · instancia el protocolo del tipo con plazos y actuaciones · abre el caso con consecutivo · registra clasificacion en log |
| Reclasifica un caso | Sistema exige motivo · ajusta el protocolo al nuevo tipo · registra el cambio con autor y fecha en log |
| Marca un caso como "presunto delito" (tipo III) | Sistema escala automaticamente al Rector · restringe la visibilidad del caso · bloquea el cierre hasta registrar el reporte a autoridad (RN-CVE-004) |
| Registra dano al cuerpo en un caso | Sistema marca la remision a EPS/urgencias como actuacion obligatoria · bloquea el cierre hasta registrarla (RN-CVE-005) |
| Registra una actuacion del protocolo | Sistema marca la actuacion como cumplida con responsable y fecha · recalcula los plazos restantes · registra en log |
| Convoca el Comite Escolar y genera el acta | Sistema crea la sesion con asistentes y compromisos · genera el acta · queda pendiente de firma del Rector (RN-CVE-006) |
| Registra acuerdos y compromisos firmados | Sistema guarda el acuerdo · genera la anotacion correspondiente en el observador del estudiante (RN-CVE-007) · registra en log |
| Cierra un caso en seguimiento | Sistema verifica que no haya actuaciones obligatorias pendientes · exige resolucion · cambia estado a Cerrado · registra en log |
| Cita formalmente a un acudiente (RF-28, configurable) | Sistema programa la citacion · notifica fecha/hora/lugar sin revelar el motivo sensible (RN-BW-006) · registra en log |
| Genera un reporte de convivencia (RF-29) | Sistema construye el reporte por estudiante/grupo/tipo/fechas respetando visibilidad (RN-OE-005) · permite exportar a PDF · registra la consulta |
| Genera el informe disciplinario consolidado (multi-ano) | Sistema reune anotaciones de varios anos lectivos · produce PDF · registra la generacion |
| Recibe una remision interna de Orientacion (configurable) | Sistema enruta la remision a su bandeja · muestra solo el contexto compartido, no el expediente clinico (RN-BW-002, RN-BW-008) |
| Envia un comunicado de convivencia (configurable) | Sistema valida el permiso configurable · entrega por los canales habilitados · registra en log |
| Cierra sesion | Sistema invalida el token · registra logout en log |

## Relacionado

- [[10 - Validaciones]] — que bloquea el sistema en cada accion
- [[11 - Respuestas del Sistema]] — eventos y respuestas
- [[09 - Campos del Formulario]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
