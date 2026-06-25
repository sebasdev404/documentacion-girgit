---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-04
  - Coord. Convivencia Ficha Detallada
---

# Ficha Detallada — Coordinador de Convivencia

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

| Campo | Valor |
|---|---|
| ID Rol | ROL-04 |
| Nombre | Coordinador de Convivencia |
| Alias | Coordinador Disciplinario, Coord. Convivencia |
| Tipo | Principal — Tenant (un solo colegio) |
| Tipo de usuario | Personal directivo del colegio con responsabilidad sobre disciplina y convivencia escolar |
| Reporta a | Rector / Administrador del Colegio (ROL-02) |
| Supervisa a | Directores de grupo (ROL-08) en lo disciplinario |
| Ambito de datos | Su tenant (RR-01). No ve datos de otros colegios |
| Cantidad sugerida | 1 a 2 por tenant segun tamano del colegio |
| Como se asigna | Lo asigna el Rector (RR-04). Un usuario tiene un solo rol principal |
| Excluyente con | ROL-05 Coordinador combinado (RR-12); no coexisten en el mismo tenant |
| Modulos que usa | Dashboard de Convivencia, Observador del estudiante, Casos de convivencia (Ley 1620), Comite Escolar de Convivencia, Tipologias y catalogos, Citaciones a acudientes, Reportes de convivencia, Bienestar/Orientacion (config), Comunicados (config) |
| Permisos CRUD | Observador: Ver (cualquier estudiante) + Editar (registrar/cerrar/anular anotaciones) · Tipologias: Editar · Casos 1620: clasificar/operar/cerrar · Reportes de convivencia: generar/exportar |
| Permisos configurables | Acceso al modulo academico (notas) — default desactivado · Citaciones formales a acudientes · Definir sanciones formales · Comunicados al colegio · Mensajes via portal · Ver historial de cambios de un registro |
| Permisos negados | Registrar/editar notas academicas · Plan de estudios y horarios · Emitir documentos oficiales · Acceso al expediente clinico de bienestar · Datos de otros tenants |
| MFA | Segun politica del tenant (no obligatorio como en ROL-01) |
| Acceso | Subdominio del colegio (RR-06); no entra por URL de plataforma |
| Dispositivo | Desktop principalmente; mobile para anotaciones rapidas |
| Frecuencia de uso | Diaria. Picos en cierres de periodo y ante casos de convivencia |
| Dolor / Necesidad actual | Necesita un registro unico, trazable y oportuno del comportamiento; clasificar casos de la Ley 1620 sin perder plazos; coordinar con directores de grupo y orientacion; preparar actas del comite y reportes consolidados para auditoria/SIUCE sin trabajo manual disperso |
| Notas UX / Recomendaciones | Anotacion rapida desde mobile; nivel de visibilidad explicito al crear (publica/docentes/interna); recordatorio de plazos de protocolo; bloqueo de cierre de caso tipo III sin constancia de reporte; banner de "caso con dano al cuerpo" hasta registrar remision a salud; anulacion con justificacion (no borrado) |
| Reglas asociadas | RR-01, RR-03, RR-04, RR-05, RR-06, RR-12, RN-OE-001..005, RN-OB-080, RN-OB-081, RN-CVE-001..010, RN-BW-002, RN-BW-006, RN-BW-008 |

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Caso tipo III cerrado sin reportar a autoridad | El sistema bloquea el cierre hasta registrar entidad, fecha y radicado (RN-CVE-004) |
| Cierre de caso con dano al cuerpo sin atencion en salud | El cierre se bloquea hasta registrar la remision a EPS/urgencias (RN-CVE-005) |
| Exposicion de informacion sensible | Visibilidad por anotacion en 3 niveles (RN-OB-081); notificaciones sin motivo clinico (RN-BW-006) |
| Borrado de anotaciones | Anulacion preserva historial con justificacion (RN-OE-003); inmutabilidad post-cierre (RN-OE-004, RN-CVE-009) |
| Plazos de protocolo por debajo de la ley | El sistema valida el tope minimo al parametrizar (RN-CVE-010) |
| Asignar a la vez esquema separado y combinado | El sistema impide ROL-04 + ROL-05 en el mismo tenant (RR-12) |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia.md`
