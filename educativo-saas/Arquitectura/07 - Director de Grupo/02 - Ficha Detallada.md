---
tags:
  - arquitectura
  - rol/director-de-grupo
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-08
---

# Ficha Detallada — Director de Grupo

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

> Es un **complemento** del Docente (ROL-07). Todos los campos describen lo que se SUMA sobre el grupo dirigido; el resto del comportamiento es el del Docente.

| Campo | Valor |
|---|---|
| ID Rol | ROL-08 |
| Nombre | Director de Grupo |
| Alias | Director de grupo, DG, Titular del grupo |
| Tipo | Complemento — Tenant (NO es rol principal) |
| Tipo de usuario | Docente designado como director de un grupo especifico |
| Pre-requisito | La persona debe tener ya ROL-07 (Docente) |
| Reporta a | Coordinador Academico (ROL-03) y/o Coord. de Convivencia (ROL-04); Coordinador combinado (ROL-05) si el colegio usa ese esquema |
| Supervisa a | Estudiantes del grupo dirigido |
| Quien lo asigna | Coordinador Academico (ROL-03) o Rector (ROL-02) al designar el director del grupo |
| Ambito de datos | Su grupo dirigido + sus materias asignadas (RR-09, RR-10). Sin acceso a otros tenants (RR-01) |
| Cantidad por grupo | Tipicamente un unico director activo por grupo |
| Multi-grupo | Un docente puede dirigir uno o mas grupos (poco comun, permitido); usa selector de grupo |
| Modulos que usa | Inicio (grupo dirigido), Mi horario, Notas (mis materias), Asistencia, Consolidado del grupo, Boletines del grupo, Observador del grupo, Convivencia (Ley 1620), Citaciones, Comunicacion con acudientes, Bienestar y alertas |
| Permisos CRUD (adicionales) | Consolidado del grupo: Ver · Boletines del grupo: Reportar + observacion general (Editar) · Observador disciplinario del grupo: Editar · Asistencia del grupo: Ver · Convivencia: reportar + medidas tipo I |
| Permisos configurables | Editar notas que no dicta (def. desactivado); aprobar/firmar boletines; citar acudientes formalmente; ver promedios historicos; comunicarse con acudientes; editar notas tras cierre |
| Permisos negados | Aplicar permisos a otros grupos (RR-09); configuracion del colegio; usuarios y roles; documentos oficiales; matricula; clasificar tipo de convivencia; decidir tipo III |
| MFA | Segun politica del colegio (igual que el Docente) |
| Acceso | Subdominio del colegio (RR-06); mismo login que Docente |
| Dispositivo | Mobile + desktop |
| Frecuencia de uso | Diaria sobre el grupo; picos en cierre de periodo (boletines) y eventos disciplinarios |
| Dolor / Necesidad actual | Hoy el director consolida notas de varias materias a mano, persigue a los docentes por las notas faltantes, redacta observaciones en papel y no tiene trazabilidad del seguimiento de convivencia. Necesita ver el consolidado completo del grupo en un solo lugar, generar boletines con observacion general y dejar registro auditable de anotaciones y acuerdos |
| Notas UX / Recomendaciones | Bloque "Mi grupo dirigido" destacado en el inicio; selector de grupo si dirige varios; advertir notas faltantes antes de generar boletin; separar claramente "ver" (todo el grupo) de "editar" (solo sus materias) para evitar errores; en convivencia, dejar evidente que NO clasifica el tipo |
| Reglas asociadas | RR-09, RR-07, RR-10, RR-11, `RN-OB-081`, `RN-CVE-003`, `RN-CVE-004`, `RN-CVE-007` |

## Modulos y nivel de acceso (adicionales del complemento)

| Modulo | Nivel | Alcance |
|---|---|---|
| Consolidado del grupo | Ver | Todas las materias del grupo dirigido (RF-18) |
| Boletines del grupo | Reportar + Editar (observacion) | Generar (RF-38) y observar (RF-40) el grupo dirigido |
| Observador disciplinario | Editar | Estudiantes del grupo dirigido (RF-25) |
| Asistencia del grupo | Ver | Asistencia completa del grupo dirigido (RF-23) |
| Convivencia Ley 1620 | Reportar + medidas tipo I + seguimiento | Su grupo (`RN-CVE-003`) |
| Citaciones | Configurable | Acudientes del grupo |
| Aprobar/firmar boletines | Configurable | Grupo dirigido (RF-39) |

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Anotar o editar fuera del grupo dirigido | Backend restringe el scope al grupo (RR-02, RR-09); la UI no muestra estudiantes ajenos |
| Editar notas que no dicta sin autorizacion | Permiso configurable, por defecto desactivado; toda edicion queda auditada (RR-03, RR-07) |
| Tratar como tipo I una situacion que es delito | El director marca "presunto delito" y el sistema escala al Rector; el director no clasifica el tipo (`RN-CVE-004`) |
| Generar boletin con notas incompletas | El sistema advierte y lista materias faltantes antes de generar (RF-38) |
| Exposicion indebida del observador | Visibilidad por anotacion (`RN-OB-081`); el acudiente ve solo lo que le corresponde |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/07-director-de-grupo.md`
