---
tags:
  - arquitectura
  - rol/secretaria-academica
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-06
  - Secretaria Ficha Detallada
---

# Ficha Detallada — Secretaria Academica

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

| Campo | Valor |
|---|---|
| ID Rol | ROL-06 |
| Nombre | Secretaria Academica |
| Alias | Secretaria, Secretaria Academica |
| Tipo | Principal — Tenant (colegio) |
| Tipo de usuario | Personal administrativo del colegio |
| Reporta a | Rector (ROL-02) |
| Supervisa a | — |
| Ambito de datos | Un solo tenant (su colegio); ve todos los estudiantes del tenant (RR-01) |
| Cantidad sugerida | 1 a 3 personas por tenant |
| Como se asigna | El Rector (ROL-02) lo asigna y ajusta sus permisos configurables (RR-04) |
| Modulos que usa | Inicio, Estudiantes, Matricula, Documentos de matricula, Documentos oficiales, SIMAT / Reportes MEN, Habeas Data / Consentimientos, Comunicaciones (configurable), Historial / Auditoria (configurable) |
| Permisos CRUD | Estudiantes y acudientes: CRUD · Asignar a grupo: editar · Cambiar grupo post-matricula: configurable · Documentos de matricula: editar · Constancias / certificados / paz y salvos: reportar (generar) · SIMAT: reportar · Notas: solo lectura para certificados |
| Permisos configurables | Bloqueo de emision por documentos pendientes (default activado) · Bloqueo por pagos pendientes · Cambiar grupo post-matricula · Paz y salvo sin pasar por contabilidad · Ver notas consultables · Comunicarse con acudientes · Enviar comunicados al colegio · Ver historial de cambios |
| Permisos negados | Registrar/editar notas, registrar asistencia, observador disciplinario, configuracion base del colegio, log global del tenant, datos de otros tenants |
| MFA | No obligatorio (segun politica del colegio) |
| Acceso | Subdominio del colegio (RR-06); no entra por panel de plataforma |
| Dispositivo | Desktop principalmente (impresion de documentos, formularios extensos) |
| Frecuencia de uso | Diaria; picos en epoca de matricula (inicio del ano) y al cierre (certificados, paz y salvos, SIMAT) |
| Dolor / Necesidad actual | Hoy lleva matricula y consecutivos en hojas sueltas o Excel; reportar al SIMAT es manual y propenso a errores; emitir certificados exige consolidar notas a mano; no hay trazabilidad clara de quien emitio que documento |
| Notas UX / Recomendaciones | Checklist visual de documentos de matricula; bloqueo/advertencia claro antes de emitir cuando hay pendientes; consecutivo automatico y no editable; validacion previa del archivo SIMAT antes de exportar; certificado de notas en solo lectura sobre el consolidado; plantillas de aviso de documentos vencidos |
| Reglas asociadas | RR-01, RR-03, RR-05, RR-06, RR-08, RR-11, RR-15, `RN-TU-410`, `RN-GD-001`, `RN-GD-270`, `RN-PZ-002`, `RN-MO-001`, `RN-MO-004`, `RN-HD-001` |
| Requerimientos | RF-30, RF-31, RF-32, RF-33, RF-34, RF-35, RF-36, RF-37 |
| Integraciones | RI-02 (SIMAT), RI-05 (DIAN — facturacion), RI-03 (correo, para avisos) |

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Emitir documento con pendientes no resueltos | Bloqueo configurable (RR-08); en modo advertencia, sello visible + registro en log |
| Consecutivo duplicado o saltado en documentos oficiales | Consecutivo automatico, unico y no editable por tipo de documento (`RN-GD-001`) |
| Reporte SIMAT con datos inconsistentes | Validacion previa obligatoria antes de exportar (`RN-MO-004`); marca de "enviado" para trazabilidad |
| Tratar datos del menor sin autorizacion | Captura y verificacion del consentimiento de habeas data en matricula (`RN-HD-001`, `RN-HD-002`) |
| Cambio indebido de grupo post-matricula | Accion configurable; puede restringirse al Coordinador Academico (RR-05) |
| Acceso a datos de otro colegio | Aislamiento total por tenant; entra por subdominio (RR-01, RR-06) |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/05-secretaria-academica.md`
