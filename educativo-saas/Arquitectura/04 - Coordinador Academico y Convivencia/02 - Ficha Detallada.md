---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - rol/coord-combinado
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-05
---

# Ficha Detallada — Coordinador Academico y Convivencia

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

| Campo | Valor |
|---|---|
| ID Rol | ROL-05 |
| Nombre | Coordinador Academico y de Convivencia (combinado) |
| Alias | Coord. Combinado, Coordinacion unificada |
| Tipo | Principal — Tenant (un solo colegio) |
| Tipo de usuario | Personal directivo del colegio que asume ambas coordinaciones |
| Reporta a | Rector / Administrador del Colegio (ROL-02) |
| Supervisa a | Docentes (ROL-07) y Directores de Grupo (ROL-08) |
| Ambito de datos | Todo el tenant (no ve otros tenants — RR-01) |
| Cantidad sugerida | 1 por tenant (tipico en colegios pequenos / medianos) |
| Como se asigna | Lo asigna el Rector / Administrador del Colegio (RR-04) |
| Modulos que usa | Dashboard, Plan de estudios, Grupos y asignaciones, Horarios, Consolidados y cierre, Nivelaciones/Habilitaciones, Boletines, Observador, Convivencia (Ley 1620), Reportes de convivencia, Comunicaciones |
| Permisos CRUD | Plan de estudios: CRUD · Grupos: CRUD · Asignaciones docente: C/E · Horarios: CRUD · Consolidados: Ver · Cierre de periodo: Ejecutar · Observador (cualquier estudiante): C/E · Tipologias: C/E · Reportes de convivencia: Generar |
| Permisos configurables | Editar notas directamente (hereda ROL-03) · Aprobar/firmar boletines (hereda ROL-03) · Citaciones formales a acudientes (hereda ROL-04) · Definir sanciones formales (hereda ROL-04) |
| Permisos negados | Configuracion base del sistema (escala, jornadas, calendario, modelo pedagogico) · Documentos oficiales y SIMAT · Datos de otros tenants · Expediente clinico de bienestar |
| MFA | No obligatorio por defecto (configurable por el colegio) |
| Acceso | Subdominio del colegio (RR-06) — no URL de plataforma |
| Dispositivo | Desktop principalmente |
| Frecuencia de uso | Alta; cubre dos ambitos a la vez (academico + convivencia) |
| Dolor / Necesidad actual | En colegios pequenos / medianos no hay equipo para separar las dos coordinaciones; necesita gestionar estructura academica y seguimiento de convivencia desde un solo perfil, sin duplicar esfuerzo ni perder trazabilidad legal (Ley 1620) |
| Notas UX / Recomendaciones | Dashboard que combine ambos mundos (estado de cierre + casos de convivencia abiertos); justificacion obligatoria al editar nota tras cierre y al reclasificar un caso; deteccion de choques en horarios; visibilidad por anotacion en el observador; escalamiento automatico de tipo III al Rector |
| Reglas asociadas | RR-01, RR-03, RR-04, RR-05, RR-06, RR-07, RR-09, RR-10, RR-12, RN-OE-003, RN-OE-004, RN-OB-081, RN-NH-001, RN-NH-002, RN-CVE-002, RN-CVE-004, RN-CVE-005, RN-CVE-007 |

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Edicion de notas tras el cierre sin trazabilidad | Permiso configurable + justificacion obligatoria + log (RR-07) |
| Clasificacion erronea de un caso de convivencia | Clasificacion auditada; reclasificable solo con justificacion y autor (RN-CVE-002) |
| Cierre de un caso tipo III sin reporte legal | El sistema bloquea el cierre hasta registrar constancia de reporte a la autoridad (RN-CVE-004) |
| Coexistencia indebida con ROL-03 + ROL-04 | El sistema impide / advierte asignar los roles separados cuando el combinado esta activo (RR-12) |
| Exposicion de informacion sensible en notificaciones | Las citaciones informan fecha/hora/lugar, nunca el motivo clinico del caso |
| Anotacion del observador borrada por error | La anulacion preserva el historial con justificacion (RN-OE-003); ano cerrado inmutable (RN-OE-004) |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/04-coordinador-academico-y-convivencia.md`
