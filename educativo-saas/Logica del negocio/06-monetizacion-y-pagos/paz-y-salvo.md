---
titulo: Paz y salvo
modulo: 06-monetizacion-y-pagos
tipo: proceso
estado: borrador
tags: [paz-y-salvo, financiero, certificado]
---

# Paz y salvo

## Descripción

Documento que certifica que un estudiante / acudiente está al día con sus obligaciones financieras y/o documentales con el colegio. Es requisito para procesos como: matrícula del año siguiente, traslado a otro colegio, expedición de boletines finales o de constancias.

## Alcances de un paz y salvo

| Alcance | Verifica |
| --- | --- |
| Financiero | No deuda en pensiones, matrícula, transporte, alimentación ni otros conceptos. |
| Documental | Carpeta de matrícula completa (documentos requeridos firmados / cargados). |
| Material | Devolución de libros de biblioteca, equipos prestados, uniformes. |
| Disciplinario | Sin sanciones pendientes. |
| **Integral** | Suma de todos los anteriores. |

El colegio define qué alcances usa.

## Quién emite

- [[roles/05-secretaria-academica|Secretaría Académica]] (financiero y documental).
- [[roles/01-rector-administrador-colegio|Administrador del Colegio]] (cualquier alcance).
- Otros roles según configuración del colegio (bibliotecario para material, coordinador de convivencia para disciplinario).

## Cuándo se exige

- Antes de iniciar el proceso de [[../04-procesos-academicos/matriculas|matrícula]] del siguiente año.
- Al solicitar traslado a otro colegio.
- Al solicitar entrega del boletín final del año.
- Al pedir certificados oficiales (de estudios, de notas).
- Al cierre de año, para egresar del último grado.

## Flujo de emisión

1. El acudiente o estudiante solicita el paz y salvo desde el portal.
2. El sistema valida automáticamente las condiciones según los alcances configurados:
   - Cartera vencida.
   - Documentos faltantes.
   - Materiales no devueltos.
3. Si todo está al día → emite el paz y salvo en PDF con firma del responsable y QR de verificación.
4. Si hay pendientes → muestra al solicitante el detalle de lo que debe resolver.
5. El responsable puede emitir manualmente con justificación (excepción), siempre auditada.

## Vigencia

- El paz y salvo tiene fecha de emisión y, opcionalmente, fecha de vigencia (ej. válido por 30 días).
- Si después de emitido se generan nuevas deudas u obligaciones, el paz y salvo emitido no se invalida retroactivamente; pero un nuevo paz y salvo no se puede emitir.

## Verificación

- Cada paz y salvo lleva un identificador único y un QR.
- El receptor (otro colegio, entidad pública) puede verificar la autenticidad escaneando el QR o ingresando el identificador en una página pública.

## Reglas de negocio

- **RN-PZ-001 — Validación automática:** la emisión normal valida automáticamente todos los alcances configurados.
- **RN-PZ-002 — Excepción auditada:** la emisión por excepción (con pendientes) requiere rol con permiso y motivo registrado.
- **RN-PZ-003 — Documento inmutable:** una vez emitido, el paz y salvo no se modifica. Se puede revocar (con motivo) y emitir uno nuevo.
- **RN-PZ-004 — QR de verificación:** todo paz y salvo lleva mecanismo de verificación pública.
- **RN-PZ-005 — Bloqueo de matrícula:** la matrícula del siguiente año no se aprueba sin paz y salvo vigente, salvo excepción registrada.
- **RN-PZ-006 — No bloquea derecho a la educación durante el año en curso:** el paz y salvo no se exige para que el estudiante asista a clases o consulte notas durante el año en curso.

## Notas y pendientes

- Definir si el paz y salvo se genera automáticamente al pagar la última cuota o requiere solicitud.
- Validar el flujo cuando un acudiente paga una deuda en mora justo antes de solicitar el paz y salvo (asegurar que el sistema detecte el pago antes de validar).
