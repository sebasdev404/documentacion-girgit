---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - rol/coord-combinado
  - acciones
aliases:
  - Acciones ROL-05
---

# Acciones del Usuario — Coordinador Academico y Convivencia

Tabla accion -> resultado. Cada accion sensible (notas, cierre, observador, clasificacion de convivencia, citaciones) genera entrada en el log de auditoria del tenant (RR-03).

## Academicas (heredadas del Coord. Academico)

| Accion | Resultado |
|---|---|
| Crea una materia en el plan de estudios | Sistema valida grado + intensidad + area · agrega la materia · la deja disponible para grupos y horarios · registra en log |
| Archiva una materia | Sistema verifica que no tenga grupos activos en el ano en curso · la marca archivada · la conserva en el historico · registra en log |
| Crea un grupo por grado y ano | Sistema crea el grupo · lo deja listo para asignacion docente y matricula · registra en log |
| Asigna un docente a materia x grupo | Sistema crea la asignacion · habilita al docente para ver ese grupo y materia (RR-10) · alimenta horarios y notas · registra en log |
| Designa un director de grupo | Sistema asigna el complemento al docente sobre ese grupo (RR-09) · habilita boletines y observador del grupo para ese docente · registra en log |
| Construye / edita un bloque de horario | Sistema valida choques de docente y de aula · si hay choque, bloquea y lo resalta · si no, guarda el bloque · registra en log |
| Publica el horario de un grupo | Sistema lo hace visible a docentes y estudiantes del grupo · registra en log |
| Consulta el consolidado de un grupo o de todos los grupos | Sistema muestra notas por estudiante x materia y faltantes · marca estudiantes en riesgo · no modifica datos |
| Ejecuta el cierre de un periodo | Sistema valida que los consolidados esten completos · congela las notas del periodo · genera automaticamente las nivelaciones de quienes perdieron materia (RN-NH-001) · notifica a docentes y directores · registra en log |
| Edita una nota despues del cierre | Sistema verifica el permiso configurable activado · exige justificacion (RR-07) · aplica el cambio · registra el antes/despues en log |
| Aprueba / firma un boletin | Sistema verifica el permiso configurable · marca el boletin como aprobado · lo habilita para publicacion a acudientes · registra en log |
| Devuelve un boletin con observacion | Sistema deja el boletin en estado "para correccion" · notifica al director de grupo · registra en log |

## Convivencia (heredadas del Coord. de Convivencia)

| Accion | Resultado |
|---|---|
| Registra una anotacion en el observador de un estudiante | Sistema crea la anotacion con su tipologia y nivel de visibilidad (RN-OB-081) · la acumula en el observador del ano · notifica segun visibilidad · registra en log |
| Define / edita una tipologia de anotacion | Sistema actualiza el catalogo del colegio · la deja disponible para autores del observador · registra en log |
| Anula una anotacion | Sistema exige justificacion · marca la anotacion como anulada conservando el historial (RN-OE-003) · registra en log |
| Recibe y clasifica un caso de convivencia (tipo I/II/III) | Sistema registra la clasificacion auditada (RN-CVE-002) · instancia el protocolo de la Ruta de Atencion Integral correspondiente con plazos y actuaciones · abre el caso con consecutivo · registra en log |
| Reclasifica un caso | Sistema exige justificacion · ajusta el protocolo al nuevo tipo · registra el cambio con autor y motivo (RN-CVE-002) |
| Marca un caso como tipo III (presunto delito) | Sistema escala automaticamente al Rector · restringe la visibilidad del caso · impide cerrarlo sin constancia de reporte a la autoridad (RN-CVE-004) |
| Cita formalmente a un acudiente | Sistema verifica el permiso configurable · genera la citacion con fecha/hora/lugar (sin exponer el motivo sensible) · notifica al acudiente por el canal habilitado · registra en log |
| Registra un acuerdo / compromiso del caso | Sistema lo asocia al caso · genera la anotacion correspondiente en el observador (RN-CVE-007) · pasa el caso a seguimiento · registra en log |
| Origina una remision a orientacion | Sistema crea la remision interna al area de bienestar · no expone el contenido sensible al cuerpo docente · registra en log |
| Genera un reporte de convivencia (por estudiante / grupo) | Sistema agrega anotaciones y casos respetando la visibilidad (RN-OE-005) · permite descargar PDF · registra la generacion |

## Transversales

| Accion | Resultado |
|---|---|
| Busca un estudiante / grupo / docente | Sistema devuelve resultados solo del propio tenant (RR-01) |
| Cierra sesion | Sistema invalida el token · registra logout en log |
