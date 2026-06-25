---
tags:
  - arquitectura
  - rol/secretaria-academica
  - prd
aliases:
  - PRD-07
  - PRD Secretaria
---

# PRD — Secretaria Academica

| Campo | Valor |
|---|---|
| ID PRD | PRD-07 |
| HU | Como secretaria academica quiero gestionar la matricula y emitir los documentos oficiales del colegio con trazabilidad |
| Funcionalidad | Gestion administrativa del tenant: matricula, documentos y reporte oficial |
| Actor | ROL-06 Secretaria Academica |
| Dispositivo | Desktop (impresion de documentos, formularios extensos) |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Permitir que la secretaria registre estudiantes y sus acudientes operativos, lleve el proceso de matricula con control de documentos, emita constancias, certificados de notas y paz y salvos con consecutivo y trazabilidad, y prepare el reporte obligatorio al SIMAT, sin acceder a las notas como datos editables ni a la operacion academica del colegio.

## Flujo General

```
Inscripcion -> Crear ficha de estudiante + acudiente operativo + consentimiento habeas data
   -> Recepcion y validacion de documentos de matricula -> Asignacion de grupo -> Matricula completada
   -> Emision de documentos oficiales (constancia / certificado / paz y salvo) con consecutivo
   -> Reporte de novedades al SIMAT en la ventana del MEN
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-30 | Registrar y editar estudiantes y acudientes | Alta |
| RF-31 | Asignar estudiante a grupo | Alta |
| RF-32 | Cargar y validar documentos de matricula | Alta |
| RF-33 | Bloquear emision de documentos por pendientes | Media |
| RF-34 | Generar constancias de estudio | Alta |
| RF-35 | Generar certificados de notas | Alta |
| RF-36 | Generar paz y salvos | Media |
| RF-37 | Reportar a SIMAT | Alta |

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| RR-01 | Aislamiento total entre tenants | Solo ve estudiantes y datos de su colegio | Alta |
| RR-03 | Auditoria de acciones sensibles | Emision de documentos y cambios de matricula quedan en log | Alta |
| RR-05 | Configurabilidad acotada de permisos | El Rector activa/desactiva sus permisos configurables (cambio de grupo, comunicaciones, bloqueos) | Alta |
| RR-06 | Acceso solo por subdominio del colegio | Entra por el subdominio del tenant, no por panel de plataforma | Alta |
| RR-08 | Bloqueo de documentos por pendientes | Puede bloquear (o advertir) la emision cuando hay documentos o pagos pendientes | Media |
| RR-11 | El menor tiene una unica cuenta (Estudiante) | El acudiente no es usuario; sus datos viven en la ficha del estudiante (`RN-TU-410`) | Alta |
| RR-15 | Reporte SIMAT obligatorio | Debe generar el formato requerido por el MEN (`RN-MO-001`) | Alta |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Registrar / editar notas academicas | No participa en la operacion academica; solo las lee para certificados | Docente (ROL-07) |
| 2 | Registrar asistencia u observaciones disciplinarias | No es su ambito | Docente / Coordinador (ROL-04, ROL-05) |
| 3 | Aprobar / firmar boletines | Responsabilidad academica | Rector / Coordinador (ROL-02, ROL-03) |
| 4 | Configurar el colegio (identidad, calendario, escala) | Es del Rector | Rector (ROL-02) |
| 5 | Acceder al log global del tenant | Solo ve historial de los registros que opera (si esta activado) | Rector (ROL-02) |
| 6 | Acceder a datos de otro tenant | Aislamiento total (RR-01) | Nadie (excepto Superadmin auditado) |

## Dependencias

- Catalogo de grupos y grados del tenant (lo crean Coordinador / Rector).
- Consolidado de notas (lo producen los docentes) para emitir certificados — solo lectura.
- Estado de cartera / pagos (modulo de pagos) para el bloqueo configurable de paz y salvos (RR-08).
- Integracion SIMAT (RI-02) y formato oficial del MEN (`Logica del negocio/13-cumplimiento-colombia/reportes-oficiales-men.md`).
- Modulo de gestion documental para consecutivos y trazabilidad (`Logica del negocio/11-plataforma-y-operacion/gestion-documental.md`).
- Ver [[../_Globales/09 - Dependencias|Dependencias]].
