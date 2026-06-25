---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - rol/estudiante-acudiente
  - prd
aliases:
  - PRD-10
  - PRD Estudiante y Acudiente
---

# PRD — Estudiante / Acudiente

| Campo | Valor |
|---|---|
| ID PRD | PRD-10 |
| HU | Como estudiante (o acudiente que opera su cuenta) quiero consultar mi informacion academica y financiera y gestionar lo propio sin depender de la secretaria |
| Funcionalidad | Portal de consulta y autogestion del estudiante |
| Actor | ROL-09 Estudiante / Acudiente |
| Dispositivo | Mobile principalmente; desktop para descargas |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Permitir que el estudiante y, en la practica, su acudiente, consulten de forma autonoma notas, horario, asistencia, boletines, observador y estado de cuenta del estudiante, y gestionen lo propio (justificar inasistencias, pagar, confirmar boletines, cargar documentos, solicitar certificados y citas), reduciendo la carga administrativa del colegio, sin modificar ningun dato academico, disciplinario o administrativo del sistema (RN-PE-002).

## Flujo General

```
Login por subdominio (RR-06) -> [si varios hijos: selector de estudiante (RR-14)]
   -> Dashboard del estudiante en contexto
   -> Consulta (notas / horario / asistencia / boletines / observador)
   -> Autogestion (justificar inasistencia / pagar / confirmar boletin /
                   cargar documento / solicitar certificado o cita)
   -> Sistema valida, registra y notifica el resultado
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-45 | Consultar notas propias / del estudiante asociado | Alta |
| RF-46 | Consultar horario | Alta |
| RF-47 | Consultar boletines (y confirmar/descargar segun configuracion) | Alta |
| RF-48 | Consultar observador disciplinario (configurable) | Media |
| RF-44 | Recibir notificaciones por correo (configurable) | Alta |
| RF-23 | Consultar registro de asistencia y justificar inasistencias | Alta |
| RF-43 | Comunicarse con docentes/coordinacion via portal (configurable) | Media |
| RF-41 | Descargar boletin en PDF | Alta |
| RF-32 | Cargar documentos requeridos de matricula | Alta |
| RF-34 | Solicitar constancia de estudio | Media |
| RF-35 | Solicitar certificado de notas | Media |
| RF-36 | Solicitar paz y salvo | Media |

> Nota: los RF-23/RF-32/RF-34/RF-35/RF-36/RF-41/RF-43 se listan aqui por la cara que el estudiante toca del flujo (consulta, justificacion, cargue, solicitud, descarga). El registro y la emision oficial pertenecen a otros roles (Docente, Secretaria). No se crean IDs nuevos.

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| RR-11 | El menor tiene una unica cuenta (Estudiante) | El acudiente no es usuario; opera la cuenta del estudiante de hecho (RN-TU-410) | Alta |
| RR-14 | Acudiente con varios hijos usa selector | Selector de estudiante por correo comun; sin fusionar expedientes, permisos ni pagos (RN-CP-002, RN-PP-120) | Alta |
| RR-01 | Aislamiento total entre tenants | Nunca ve datos de otro estudiante ni de otro colegio | Alta |
| RR-06 | Acceso por subdominio del colegio | Entra por el dominio del colegio, no por URL de plataforma | Alta |
| RN-PE-001 | Acceso desactivable | El colegio puede apagar el portal por completo | Alta |
| RN-PE-002 | Solo lectura academica/disciplinaria | Nunca modifica notas, asistencia ni observador | Alta |
| RN-PE-003 | Bloqueo de documentos por paz y salvo | Descarga de boletines/certificados puede bloquearse por configuracion de paz y salvo | Media |
| RN-PE-004 | Confirmacion de boletin auditada | Registra fecha, hora e IP asociada al usuario | Media |
| RN-PE-005 | Justificaciones requieren revision | La inasistencia justificada queda pendiente hasta aprobacion/rechazo | Alta |
| RN-PE-006 | Pago obligatorio antes de descarga | Conceptos cobrables requieren pago confirmado antes de habilitar la descarga | Media |
| RN-OB-081 | Observador configurable en portal | Algunos colegios no exponen el observador en el portal | Media |
| RN-GD-270 | Flujo de revision de documentos | El documento cargado pasa por revision administrativa (aprobado/rechazado) | Media |
| RN-PP-120 | Deuda unica por estudiante | Sin split entre acudientes; el colegio puede dividir en cuotas | Alta |
| RN-PP-003 | Webhook como fuente de verdad del pago | El estado del pago lo confirma la pasarela, no el navegador | Alta |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Modificar notas | Rol de solo consulta (RN-PE-002) | Docente (ROL-07) |
| 2 | Modificar asistencia (solo la justifica) | La justificacion requiere revision (RN-PE-005) | Docente (ROL-07) / Coordinador |
| 3 | Editar o eliminar anotaciones del observador | Documento institucional de solo lectura para el estudiante | Coordinador de Convivencia / Director de Grupo |
| 4 | Ver datos de otros estudiantes | Scope estricto y aislamiento (RR-14, RR-01) | — (nadie fuera de su alcance) |
| 5 | Emitir documentos oficiales (los solicita, no los emite) | Responsabilidad del colegio | Secretaria (ROL-06) |
| 6 | Acceder a configuracion del colegio | Fuera de su ambito | Rector (ROL-02) |
| 7 | Iniciar sesion si el colegio desactivo el portal | RN-PE-001 | — |

## Dependencias

- Pasarelas de pago configuradas por el colegio (RI-01).
- Servicio de correo para notificaciones (RI-03).
- Modulo de paz y salvo y conciliacion de pagos para habilitar descargas (RN-PYS-150, RN-PYS-151).
- Flujos de origen operados por otros roles: registro de notas (ROL-07), revision de justificaciones (ROL-07/ROL-08), emision de documentos (ROL-06).
- Ver [[../_Globales/09 - Dependencias|Dependencias]].

## Relacionado

- [[00 - Arquitectura Estudiante y Acudiente|Wireframe]]
- [[05 - Requerimientos]]
- [[../_Globales/02 - PRD - Plataforma|PRD Plataforma]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente.md`
