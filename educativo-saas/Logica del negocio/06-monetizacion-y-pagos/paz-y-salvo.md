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

- **[Decisión tomada]** **Generación del paz y salvo es configurable por colegio**. Modalidades soportadas:
  1. **Generación automática** al detectar saldo cero, descargable por el acudiente cuando lo necesite.
  2. **Bajo solicitud explícita** del acudiente, opcionalmente con **aprobación administrativa**.
  3. **Pago previo del costo del certificado**: si el colegio cobra por el documento de paz y salvo, el acudiente debe primero pagar ese cargo. **Mientras exista deuda principal, ni siquiera puede generarse el cargo del certificado**, evitando que se pague el certificado sobre una cuenta morosa.
  Regla: **RN-PYS-150 — Tres modalidades de generación configurables por colegio (automática, por solicitud, con pago previo del certificado)**.
- **[Decisión tomada]** **Conciliación previa obligatoria**: antes de emitir el paz y salvo, el sistema **valida que el último pago esté efectivamente conciliado** con la pasarela o banco. Si está pendiente de confirmación: el documento queda en estado **"pendiente de conciliación"** o se emite con **advertencia temporal**, configurable por colegio. Esto evita emitir paz y salvos sobre pagos reversables. Regla: **RN-PYS-151 — Validación de conciliación efectiva antes de emitir paz y salvo**.
