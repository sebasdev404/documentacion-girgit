---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-12
---

# Ficha Detallada — Personal de Apoyo

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

| Campo | Valor |
|---|---|
| ID Rol | ROL-12 |
| Nombre | Personal de Apoyo |
| Alias | Apoyo, Orientador, Enfermeria, Bibliotecario |
| Tipo | Principal — Servicio no docente, bajo privilegio |
| Tipo de usuario | Funcionario no docente con interaccion directa con el estudiante |
| Perfiles concretos | Orientador/Psicologo (`RN-BW`) · Enfermeria (`RN-SA`) · Bibliotecario (`RN-BI`) · Otros (solo nucleo) |
| Reporta a | Rector (ROL-02) o coordinacion designada por el colegio (`RN-TU-008`) |
| Supervisa a | — |
| Ambito de datos | Un solo tenant; ficha acotada del estudiante (no expediente completo) |
| Cantidad sugerida | Grupo pequeno de funcionarios (segun servicios contratados) |
| Como se asigna | El Rector crea la cuenta y selecciona el perfil **antes** de activarla (`RN-TU-003`) |
| Modulos que usa | Nucleo: Inicio del servicio, Buscar estudiante (ficha acotada), Aportes al observador, Mi agenda. Mas el modulo del perfil: Bienestar / Salud / Biblioteca |
| Permisos CRUD | Ficha del estudiante: Ver (acotada) · Observador: Crear/editar aporte propio (no borra) · Modulo del perfil: CRUD acotado a su servicio · Otros perfiles de servicio: — |
| Permisos negados | Notas, calificaciones, boletines, consolidados, documentos oficiales, pagos/cartera, configuracion del tenant, gestion de roles/grupos/horarios, modulo de un perfil ajeno, datos de otros tenants |
| Visibilidad observador | Solo las anotaciones que `RN-OB-081` le permita; sus aportes salen en nivel **interna** por defecto |
| Alertas tempranas (`RN-VA-101`) | Configurable por el colegio (default desactivado) |
| MFA | Segun politica del tenant |
| Acceso | Subdominio del colegio (RR-06) |
| Dispositivo | Desktop / tablet (mostrador, enfermeria, consultorio) |
| Frecuencia de uso | Diaria durante la jornada escolar |
| Dolor / Necesidad actual | Necesita ubicar rapido al estudiante y su contacto sin exponer datos academicos; registrar atenciones/citas/prestamos con trazabilidad; dejar constancia en el observador con la confidencialidad adecuada; remitir casos que exceden su servicio |
| Notas UX / Recomendaciones | Preseleccionar visibilidad **interna** en aportes al observador (`RN-TU-005`); ocultar por completo modulos academicos/financieros; bloquear suministro de medicamento sin autorizacion vigente (`RN-SA-003`); en biblioteca calcular vencimiento por configuracion, no a mano (`RN-BI-002`); en bienestar separar la parte interna del plan de la parte visible (`RN-BW-008`) |
| Reglas asociadas | `RN-TU-001` a `RN-TU-010`, `RN-OB-081`, `RN-VA-101`, `RN-BW-*`, `RN-SA-*`, `RN-BI-*`, RR-03, RR-05, RR-06 |

## Perfiles y su modulo de servicio

| Perfil | Modulo habilitado | Prefijo RN | Objeto principal |
|---|---|---|---|
| Orientador / Psicologo | Bienestar y orientacion | `RN-BW` | Expediente de bienestar (transversal al ano), citas, planes |
| Enfermeria | Salud y enfermeria | `RN-SA` | Ficha medica, atenciones, suministro, vacunas, remisiones |
| Bibliotecario | Biblioteca | `RN-BI` | Catalogo, ejemplares, prestamos, reservas, multas |
| Otros perfiles | Sin modulo dedicado | — | Solo nucleo: ficha acotada + aporte al observador |

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Acceso a datos sensibles del menor mas alla de lo necesario | Ficha **acotada**, no expediente completo (`RN-TU-006`); auditoria de cada consulta (`RN-TU-009`) |
| Cruce de informacion entre perfiles | Cada perfil solo ve su propio modulo (`RN-TU-004`) |
| Exposicion de motivo clinico en notificaciones | Notificaciones de cita/remision sin motivo sensible (`RN-BW-006`) |
| Suministro de medicamento no autorizado | Bloqueo sin autorizacion vigente del acudiente (`RN-SA-003`) |
| Que el rol tome decisiones que no le competen | Solo remite, no decide sanciones/promocion (`RN-TU-010`) |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo.md`
