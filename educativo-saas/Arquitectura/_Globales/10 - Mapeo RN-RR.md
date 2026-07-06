---
tags:
  - arquitectura
  - trazabilidad
  - mapeo
aliases:
  - Mapeo RN-RR
  - Trazabilidad Logica-Arquitectura
---

# Mapeo RN <-> RR (Trazabilidad entre capas)

> **Proposito:** cerrar el hueco de trazabilidad bidireccional entre las dos capas. La capa `Logica del negocio/` identifica reglas como `RN-XX-NNN` (modulo + correlativo); la capa `Arquitectura/` usa `RR-NN`/`RF-NN`. Esta tabla permite, dado un `RR` o un `RN`, saber su contraparte. Cuando se cree una nueva `RR`, agregar aqui su origen `RN`.

> Fuente de verdad: siempre `Logica del negocio/`. Si una `RR` y su `RN` divergen, gana el `RN`.

---

## 1. RR -> RN (origen de cada regla de Arquitectura)

| RR | Regla (Arquitectura) | Origen en Logica del negocio (RN / archivo) |
|---|---|---|
| RR-01 | Aislamiento total entre tenants | `RN-AI-001`..`RN-AI-005` · `03-multi-tenancy/aislamiento-de-datos.md` |
| RR-02 | Verificacion de permisos en frontend y backend | `RN-VL-430` · `07-reglas-de-negocio/validaciones.md` |
| RR-03 | Auditoria de acciones sensibles | `RN-LA-001`, `RN-LA-002`, `RN-RT-400`, `RN-RT-401` · `11-plataforma-y-operacion/log-de-auditoria.md` |
| RR-04 | Asignacion de roles por el Rector | `RT-4` · `02-usuarios-roles-y-permisos/reglas-transversales-de-roles.md` |
| RR-05 | Configurabilidad acotada de permisos | `RT-5`, `RN-RG-018` (menor privilegio) · `reglas-transversales-de-roles.md`, `07-reglas-de-negocio/reglas-globales.md` |
| RR-06 | Acceso solo por subdominio del colegio | `RN-AU-001`, `RN-AU-005`, `RN-AU-006` · `02-.../autenticacion.md` |
| RR-07 | Notas se editan dentro del periodo abierto | `RN-CA-005`, `RN-CL-030`, `RN-CL-031` · `04-.../calificaciones.md` |
| RR-08 | Bloqueo de documentos por pendientes | `RN-GD-270`, `RN-BR-003`, `RN-CM-004` · `11-.../gestion-documental.md`, `06-.../paz-y-salvo.md` |
| RR-09 | Director de Grupo solo opera sobre su grupo | `roles/07-director-de-grupo.md` (scope del complemento) |
| RR-10 | Docente ve solo grupos y materias asignados | `RN-AD-001` · `04-.../asignacion-docentes.md`, `roles/06-docente.md` |
| RR-11 | El menor tiene una unica cuenta (Estudiante) | `RN-TU-410`, `RN-CP-001` · `02-.../tipos-de-usuario.md`, `05-.../comunicacion-con-padres.md` |
| RR-12 | Coordinador combinado excluye los separados | `roles/04-coordinador-academico-y-convivencia.md` |
| RR-13 | Cambio de calendario A/B es del Superadmin | `RN-CE-001`..`RN-CE-004` · `04-.../calendario-escolar.md`, `roles/00-superadministrador-plataforma.md` |
| RR-14 | Acudiente con varios hijos usa selector | `RN-CP-002`, `RN-PP-120`, `RN-TU-410` · `05-.../comunicacion-con-padres.md`, `06-.../pagos-de-pensiones.md` |
| RR-15 | Reporte SIMAT obligatorio | `RN-MO-001` · `13-cumplimiento-colombia/reportes-oficiales-men.md` |
| RR-16 | Visibilidad triple del observador para Personal de Apoyo | `RN-OB-081`, `RN-TU-005` · `04-.../observador-del-estudiante.md`, `02-.../roles/09-personal-de-apoyo.md` |
| RR-17 | Otros cobros entran a la cartera unica del estudiante sin split | `RN-PP-120`, `RN-TI-001` · `06-.../pagos-de-pensiones.md`, `12-bienestar-y-servicios/tienda-y-otros-cobros.md` |
| RR-19 | Tratamiento de datos del menor exige consentimiento | `RN-HD-001`, `RN-HD-002` · `13-cumplimiento-colombia/habeas-data-y-consentimientos.md` |
| RR-20 | Convivencia sigue la Ruta de Atencion Integral Ley 1620 | `RN-CVE-003`, `RN-CVE-004` · `13-cumplimiento-colombia/convivencia-ley-1620.md` |

---

## 2. Catalogos RN sin RR dedicada (cobertura pendiente)

Estas familias de reglas de la Logica **no tienen aun una `RR` espejo** en Arquitectura. No estan "perdidas" (viven en la fuente de verdad y muchas aparecen como `RNF` en `03 - Tabla de Requerimientos`), pero conviene crearles `RR` o `RNF` cuando se propaguen los modulos. Ver [[../../_PLAN MAESTRO DE COMPLETADO#A. Decisiones de saneamiento (resuelven inconsistencias)|Plan Maestro, D-06]].

| Familia RN | Tema | Donde vive | Estado de cobertura en Arquitectura |
|---|---|---|---|
| `RN-RG-001..018` | Reglas globales del sistema (no bloqueo por mora, soft-delete, UTC, hashing, moneda por pais, menor privilegio, notificaciones criticas) | `07-reglas-de-negocio/reglas-globales.md` | Parcial: algunas como `RNF`; faltan RR espejo |
| `RN-LA-001..006`, `RN-LA-290` | Log de auditoria append-only, diff JSON, retencion legal | `11-.../log-de-auditoria.md` | Cubierto via RR-03 (parcial) |
| `RN-PE-001..005`, `RN-PE-350/351` | Idempotencia y seguridad de pasarela | `10-.../pasarelas-de-pago-externas.md` | Pendiente RR/RI |
| `RN-MN-001..003` | Doble flujo de monetizacion, comisiones | `06-.../modelo-de-negocio.md` | Pendiente RR |
| `RN-RG-420/421`, `RN-VL-430` | i18n, MFA obligatorio, validacion dual | `07-.../reglas-globales.md`, `validaciones.md` | RR-02 (validacion); MFA pendiente RR/RNF |

---

## 3. Convencion para nuevas reglas

1. Toda regla nace primero como `RN-XX-NNN` en `Logica del negocio/`.
2. Al propagarla a Arquitectura se le asigna `RR-NN` (regla) o `RF-NN` (requerimiento funcional) y se registra la fila aqui.
3. El correlativo `RR`/`RF` es unico en todo el proyecto (continua desde el maximo actual: ver [[../../_PLAN MAESTRO DE COMPLETADO#D. Asignacion de rangos de ID (anti-colision para escritura paralela)|Plan Maestro, seccion D]]).

---

## Documentos relacionados

- [[07 - Reglas de Negocio|07 - Reglas de Negocio]] — catalogo RR-NN.
- [[03 - Tabla de Requerimientos|03 - Tabla de Requerimientos]] — RF/RNF/RR/RI.
- [[../../_PLAN MAESTRO DE COMPLETADO|Plan Maestro de Completado]] — gobernanza del completado.
