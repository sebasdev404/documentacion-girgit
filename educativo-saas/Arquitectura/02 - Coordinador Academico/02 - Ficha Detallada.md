---
tags:
  - arquitectura
  - rol/coord-academico
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-03
---

# Ficha Detallada — Coordinador Academico

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

| Campo | Valor |
|---|---|
| ID Rol | ROL-03 |
| Nombre | Coordinador Academico |
| Alias | Coord. Academico, CA |
| Tipo | Principal — Tenant (un solo colegio) |
| Tipo de usuario | Personal directivo del colegio con responsabilidad academica |
| Reporta a | Rector / Administrador del Colegio (ROL-02) |
| Supervisa a | Docentes (ROL-07) en lo academico; Directores de grupo (ROL-08) en la designacion |
| Ambito de datos | Un solo tenant — todos los grupos, materias, docentes y estudiantes del colegio |
| Cantidad sugerida | 1 a 3 por tenant segun el tamano del colegio |
| Como se asigna | Lo asigna el Rector / Administrador del Colegio (RR-04) |
| Modulos que usa | Dashboard academico, Plan de estudios, Grupos, Asignacion docente, Horarios, Consolidados de notas, Cierre de periodo, Nivelaciones, Boletines, Comunicaciones |
| Permisos CRUD | Plan de estudios: CRUD · Grupos: CRUD · Horarios: CRUD · Asignacion docente: editar · Director de grupo: designar · Consolidados: ver (todo el tenant) · Cierre de periodo: editar · Nivelaciones: editar |
| Permisos configurables | Editar notas directamente · Editar notas despues del cierre · Aprobar / firmar boletines · Crear anos lectivos · Asignar/cambiar estudiante de grupo · Citar acudientes · Mensajear acudientes · Ver historial de cambios |
| Permisos negados | Configuracion base (escala, jornadas, modelo pedagogico, calendario) · Observador disciplinario · Documentos oficiales (constancias, certificados, paz y salvos, SIMAT) · Datos de otros tenants · Logs de auditoria del tenant |
| MFA | Configurable por el colegio (no obligatorio para este rol) |
| Acceso | Subdominio del colegio (RR-06) |
| Dispositivo | Desktop principalmente |
| Frecuencia de uso | Alta al inicio del ano (plan, grupos, asignacion, horarios) y en cada cierre de periodo; media en operacion estable |
| Dolor / Necesidad actual | Necesita armar y mantener la estructura academica de todo el colegio sin tocar la configuracion base; detectar a tiempo grupos con notas incompletas y estudiantes en riesgo; cerrar periodos limpios; trazabilidad de quien cargo/edito notas |
| Notas UX / Recomendaciones | Validacion de cruces (docente/aula/grupo) antes de publicar horarios; panel de cierre con semaforo de grupos completos/incompletos; advertencia clara al cerrar (bloquea edicion de notas) y al reabrir (puede requerir Rector); separar visualmente lo estructural de lo configurable |
| Reglas asociadas | RR-01, RR-03, RR-04, RR-05, RR-06, RR-07, RR-09, RR-10, RR-12 |

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Cierre de periodo prematuro (notas incompletas) | Panel de cierre exige consolidados completos; advierte grupos/docentes pendientes antes de activar el cierre |
| Edicion indebida de notas | Edicion directa es permiso configurable (default restringido al docente); toda edicion queda auditada (RR-03, RR-07) |
| Reapertura de periodo cerrado | Puede requerir intervencion del Rector segun configuracion; toda reapertura queda en log |
| Horario con cruces | El sistema valida docente/aula/grupo en el mismo bloque antes de publicar |
| Acceso a datos academicos fuera de su tenant | Aislamiento total por tenant (RR-01); el coordinador solo ve su colegio |
| Asignacion docente que abre acceso indebido | El docente solo ve lo asignado (RR-10); el complemento Director de Grupo aplica solo sobre el grupo dirigido (RR-09) |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/02-coordinador-academico.md`
