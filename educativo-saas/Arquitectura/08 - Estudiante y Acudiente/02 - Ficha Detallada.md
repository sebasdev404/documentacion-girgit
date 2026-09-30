---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - rol/estudiante-acudiente
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-09
  - Estudiante y Acudiente Ficha Detallada
---

# Ficha Detallada — Estudiante / Acudiente

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

| Campo | Valor |
|---|---|
| ID Rol | ROL-09 |
| Nombre | Estudiante / Acudiente |
| Alias | Estudiante, Acudiente, Padre de familia (operativo) |
| Tipo | Principal — Tenant (solo consulta) |
| Tipo de usuario | Estudiante matriculado. El acudiente opera la misma cuenta de hecho, sin credenciales propias (RN-TU-410) |
| Reporta a | — (no participa en jerarquia operativa del colegio) |
| Supervisa a | — |
| Ambito de datos | Un unico estudiante en contexto dentro de un solo tenant (RR-01, RR-14) |
| Cantidad | 1 cuenta por estudiante matriculado |
| Como se asigna | Se crea en la matricula por la Secretaria Academica (RF-30). Un estudiante = una cuenta. Los datos del acudiente se registran como contacto del estudiante, no como usuario (RN-TU-410) |
| Primer ingreso | Contrasena temporal con cambio obligatorio (RN-AU-360) |
| Modulos que usa | Inicio, Notas, Horario, Asistencia, Boletines, Observador (configurable), Comunicaciones, Pagos y estado de cuenta, Documentos, Citas |
| Permisos CRUD | Notas: Ver · Horario: Ver · Asistencia: Ver + Justificar (queda pendiente) · Boletines: Ver + Confirmar + Descargar (configurable) · Observador: Ver + Confirmar (configurable) · Comunicaciones: Ver + Mensaje a docente (configurable) · Pagos: Ver + Pagar + Descargar comprobante · Documentos: Cargar requeridos + Solicitar oficiales · Citas: Solicitar |
| Permisos negados | Modificar notas, asistencia, observador, boletines o cualquier dato del sistema; ver datos de otros estudiantes; acceder a configuracion del colegio; acceder a otros tenants (RN-PE-002, RR-14, RR-01) |
| MFA | Opcional, igual que para el Superadministrador |
| Acceso | Subdominio del colegio (RR-06). Configurable: el colegio puede desactivar el portal por completo (RN-PE-001) |
| Selector multi-estudiante | Si el correo esta vinculado a varios estudiantes del mismo colegio, el portal ofrece selector; no fusiona expedientes, permisos ni pagos (RR-14, RN-CP-002, RN-PP-120) |
| Dispositivo | Mobile principalmente; desktop para descargas de boletines y comprobantes |
| Frecuencia de uso | Variable; picos en publicacion de notas, boletines y vencimiento de cuotas |
| Dolor / Necesidad actual | Quiere ver notas, horario, boletines y deuda sin depender de la secretaria; pagar en linea y descargar comprobantes; justificar inasistencias y solicitar documentos sin desplazarse al colegio |
| Notas UX / Recomendaciones | Movil primero; selector de estudiante muy visible para acudientes con varios hijos; estados claros en justificaciones, pagos y documentos (pendiente/aprobado/rechazado); avisos accionables en Inicio; mensajes explicitos cuando una descarga esta bloqueada por paz y salvo o pago |
| Reglas asociadas | RR-01, RR-06, RR-11, RR-14, RN-TU-410, RN-CP-002, RN-AU-360, RN-PE-001, RN-PE-002, RN-PE-003, RN-PE-004, RN-PE-005, RN-PE-006, RN-OB-080, RN-OB-081, RN-MI-180, RN-GD-270, RN-PP-120, RN-PP-121, RN-PP-003, RN-PP-006, RN-PYS-150, RN-PZ-006, RN-NO-004 |

## Scope por tipo de usuario

| Tipo de usuario | Scope |
|---|---|
| Estudiante | Sus propios datos unicamente |
| Acudiente (operativo) | Los datos del estudiante cuya cuenta opera; con varios hijos, uno a la vez via selector, sin fusionar (RR-14) |

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Acceso a datos de otro estudiante | Scope estricto al estudiante en contexto; aislamiento por tenant (RR-01, RR-14); el selector no fusiona expedientes (RN-CP-002) |
| Intento de modificar notas/asistencia/observador | Solo lectura forzada en backend (RN-PE-002, RR-02); toda interaccion queda auditada |
| Descarga indebida de documento con deuda | Bloqueo por paz y salvo / pago previo (RN-PE-003, RN-PE-006, RN-PYS-150) |
| Confirmacion de boletin no trazable | Confirmacion registra fecha, hora e IP asociada al usuario (RN-PE-004) |
| Justificacion tomada como aprobada automaticamente | La justificacion queda pendiente hasta revision del docente/coordinador (RN-PE-005) |
| Suplantacion en pagos | Estado del pago lo define el webhook de la pasarela, no el navegador (RN-PP-003); doble registro de transaccion prohibido (RN-PP-004) |

## Fuente

- `Logica del negocio/02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente.md`
- `Logica del negocio/02-usuarios-roles-y-permisos/portal-del-estudiante.md`
