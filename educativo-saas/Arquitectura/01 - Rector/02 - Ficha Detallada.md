---
tags:
  - arquitectura
  - rol/rector
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-02
  - Rector Ficha Detallada
---

# Ficha Detallada — Rector / Administrador del Colegio

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

| Campo | Valor |
|---|---|
| ID Rol | ROL-02 |
| Nombre | Rector / Administrador del Colegio |
| Alias | Rector, Administrador del Colegio, Director General |
| Tipo | Principal — Tenant (maximo acceso dentro del colegio) |
| Tipo de usuario | Personal directivo del colegio |
| Reporta a | Superadmin (ROL-01) en lo contractual; junta/propietario del colegio fuera del producto |
| Supervisa a | Todos los roles internos del tenant (ROL-03 a ROL-09) |
| Ambito de datos | Un solo tenant (todo el colegio); sin visibilidad cross-tenant (RR-01) |
| Cantidad sugerida | Minimo 1, maximo configurable. Default: 1 activo + 1 respaldo opcional |
| Como se asigna | El Superadmin lo asigna al crear el tenant (primer Rector = contacto del colegio). Relevos posteriores los hace el Rector saliente o el Superadmin |
| Acceso | Subdominio del colegio (RR-06); el tenant_id se infiere antes de validar credenciales |
| Configurable por el colegio | Parcial: el colegio puede renombrar el rol, pero los permisos estructurales no se quitan (RR-05) |
| Modulos que usa | Dashboard, Identidad, Calendario y periodos, Jornadas, Modelo pedagogico, Escala valorativa, Aprobacion, Usuarios, Roles, Auditoria, Plan de estudios, Grupos, Horarios, Notas, Asistencia, Boletines, Observador, Convivencia Ley 1620, Matricula y admisiones, Documentos oficiales, Bienestar (salud, orientacion, biblioteca, transporte, restaurante), Financiero (pensiones, becas, paz y salvo), Comunicaciones, Reportes y KPIs |
| Permisos CRUD | Configuracion institucional: CRUD · Usuarios: CRUD · Roles/permisos configurables: editar · Academico (plan, grupos, horarios, notas): CRUD/editar · Boletines: aprobar/firmar · Convivencia: editar · Matricula/documentos: respaldo de Secretaria · Auditoria del tenant: ver · Reportes: ver/exportar |
| Permisos negados | Crear/eliminar tenants · Cambiar calendario A/B habilitado · Acceder a datos de otros colegios · Impersonar usuarios · Ver logs globales de plataforma |
| MFA | Recomendado, no obligatorio (a diferencia del Superadmin). Configurable por el colegio |
| Dispositivo | Desktop principalmente (configuracion y gestion); mobile para consulta y aprobaciones puntuales |
| Frecuencia de uso | Alta al inicio del ano lectivo y en cambios de configuracion; media-baja en operacion estable |
| Dolor / Necesidad actual | Necesita configurar el colegio rapido al arrancar; visibilidad consolidada del estado academico, de convivencia y financiero; capacidad de delegar sin perder control; trazabilidad de quien hizo que |
| Notas UX / Recomendaciones | Asistente de configuracion guiado en el primer ingreso; advertencias al cambiar configuracion que afecta datos ya calculados (escala, metodo de aprobacion); confirmacion + justificacion al editar notas post-cierre; banner de "configuracion incompleta" hasta cubrir lo minimo para operar; delegacion expresada como ampliar permisos al otro rol, no quitarselos al Rector |
| Reglas asociadas | RR-01, RR-02, RR-03, RR-04, RR-05, RR-06, RR-07, RR-08, RR-12, RR-13, RR-15, RNF-02, RNF-03, RNF-07 |

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Configuracion errada que se propaga (NIT, escala, aprobacion) | Asistente guiado + advertencias antes de aplicar cambios que afectan datos calculados o documentos oficiales |
| Edicion indebida de notas tras el cierre | Permiso configurable + justificacion obligatoria + auditoria (RR-07, RR-03) |
| Desactivacion accidental de un usuario clave | La desactivacion no borra historial; reactivacion posible; queda auditado |
| Delegacion mal entendida (quitar permisos al Rector) | El modelo solo permite ampliar permisos a otros roles; los estructurales del Rector son fijos (RR-05) |
| Manejo de datos sensibles (menores, salud) | Cumplimiento Habeas Data / Ley 1581 (RNF-07); acceso auditado (RR-03) |
| Intento de operar fuera del tenant | Aislamiento total a nivel BD y subdominio (RR-01, RR-06) |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio.md`
