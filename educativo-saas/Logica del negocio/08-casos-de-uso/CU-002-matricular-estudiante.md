---
titulo: "CU-002: Aprobar y matricular un estudiante nuevo"
modulo: 04-procesos-academicos
tipo: caso-de-uso
estado: implementado-local
tags: [caso-de-uso, matricula, ingreso]
---

# CU-002: Aprobar y matricular un estudiante nuevo

Versión del 7 de octubre de 2026. Sustituye el borrador que exigía pago y cuentas de acudiente. Referencia: [[../04-procesos-academicos/matriculas|Matrículas por enlace]]. La matrícula académica manual de usuarios existentes conserva su flujo independiente.

## Actores y precondiciones

Rector o personal delegado con `ingreso.ver`, `ingreso.revisar`, `ingreso.decidir` y/o `ingreso.asignar`, según la acción. Capacidad `academico`, año válido y solicitud enviada desde CU-003. No requiere cuenta del aspirante ni pago.

## Flujo

1. Abrir bandeja y expediente.
2. Revisar última versión de documentos: aprobar o solicitar corrección con motivo.
3. Aspirante corrige y reenvía.
4. Aprobar grado solicitado o diferente con `ingreso.cambiar_grado`, motivo y requisitos completos del nuevo grado.
5. Validar documentos, envío, consentimiento, cupo, límite del plan y ausencia de cuenta/documento duplicado.
6. Crear cuenta estudiantil con contraseña temporal obligatoria de cambiar y notificar; estado `aprobada`, sin grupo.
7. Seleccionar grupo o generar propuesta automática y revisarla.
8. Confirmar revalida cupos y crea matrícula activa del año/grupo; notifica y pasa a `matriculada`.

## Alternativas y aceptación

- No aprobar con documentos pendientes, rechazados o correcciones sin reenviar.
- Sin cupo: espera explícita, sin cuenta nueva ni reserva automática.
- Rechazo: motivo en seguimiento y correo.
- Cupo ocupado después de proponer: rechazar confirmación completa, sin matrículas parciales.
- Repetir aprobación/asignación: sin duplicados.
- Cuenta existente: bloqueo, gestionar matrícula académica/renovación independiente.
- Primer acceso estudiantil: solo contraseña, no configuración institucional.
- Sin cuotas, contratos firmados, pagos ni usuarios de acudiente.

Verificado por `EnrollmentIntakeTest` y `npm run test:ui:ingreso`. La segunda usa API simulada; no acredita entrega SMTP.
