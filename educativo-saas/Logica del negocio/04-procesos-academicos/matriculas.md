---
titulo: Matrículas
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [matricula, proceso]
---

# Matrículas

## Descripción

Proceso por el cual una persona externa al colegio (aspirante) se inscribe a un grado de un año lectivo, paga el valor de la matrícula, diligencia el formulario, sube los documentos requeridos, y —una vez aprobado— queda creado automáticamente como estudiante del colegio.

El proceso está diseñado para que el aspirante **no necesite tener un usuario previo en el sistema**.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| Aspirante | Persona externa que se inscribe. No tiene usuario en el sistema hasta el cierre del proceso. |
| [[roles/05-secretaria-academica\|Secretaría Académica]] | Revisa documentos y confirma la matrícula. |
| [[roles/01-rector-administrador-colegio\|Administrador del Colegio]] | Configura el proceso, los conceptos cobrables y los documentos requeridos. |
| [[roles/02-coordinador-academico\|Coordinador Académico]] | Asigna grupo al estudiante recién matriculado. |
| Pasarela de pago | Procesa el pago del valor de la matrícula. |

## Precondiciones

- El año lectivo destino existe en el sistema (estado `Planificado` o `En curso`).
- El colegio ha configurado:
  - Conceptos cobrables (incluyendo el valor de la matrícula).
  - Documentos requeridos por nivel educativo.
  - Vigencia del PIN.
  - Cupos por grado.
  - Pasarela de pago habilitada.
- El colegio ha habilitado las matrículas para ese año lectivo.

## Flujo principal

### Etapa 1 — Inscripción y pago

1. El aspirante (o su acudiente) ingresa al portal del colegio.
2. Selecciona el grado al que aspira.
3. El sistema muestra la **disponibilidad de cupos**.
   - Si hay cupo: continúa.
   - Si no hay cupo: el aspirante puede registrarse en lista de espera.
4. El aspirante ingresa datos básicos (nombre, correo, teléfono).
5. Paga el valor de la matrícula a través de la pasarela configurada.
6. La pasarela confirma el pago.
7. El sistema genera automáticamente un **PIN único** asociado al pago.
8. El sistema envía al correo registrado:
   - El PIN.
   - El enlace al formulario de matrícula.
   - La fecha de vencimiento del PIN.

### Etapa 2 — Diligenciamiento del formulario

1. El aspirante ingresa al formulario con su PIN.
2. El formulario muestra los campos configurados por el colegio (obligatorios y opcionales).
3. El aspirante diligencia los datos y sube los documentos requeridos:
   - Fotocopia del documento de identidad.
   - Registro civil.
   - Foto del estudiante.
   - Certificado de notas del año anterior.
   - Carné de vacunas.
   - Otros documentos personalizados que el colegio haya agregado.
4. El aspirante envía la solicitud.
5. El sistema notifica al personal autorizado (secretaría).

### Etapa 3 — Revisión

1. El personal autorizado revisa la solicitud documento por documento.
2. Para cada documento puede:
   - Aprobar.
   - Rechazar con observación.
3. Si rechaza algún documento, el sistema notifica al aspirante indicando cuál fue rechazado y por qué.
4. El aspirante corrige y vuelve a subir el documento rechazado.
5. Este ciclo puede repetirse hasta que **todos los documentos estén aprobados**.

### Etapa 4 — Confirmación

1. Una vez todos los documentos están aprobados, el personal autorizado confirma la matrícula.
2. El sistema:
   - Crea automáticamente el usuario estudiante usando el correo registrado en el proceso.
   - Genera una contraseña temporal automática.
   - Envía al correo las credenciales de acceso con instrucciones para cambiar la contraseña en el primer ingreso.
   - Asigna al estudiante al grado correspondiente.
   - Lo deja en lista de espera de grupo hasta que el [[roles/02-coordinador-academico|Coordinador Académico]] realice la asignación.
   - Crea las cuentas de los acudientes registrados en el formulario y las vincula al estudiante.

## Flujos alternativos

### A1. PIN vencido

- Si el PIN vence sin que el aspirante complete el proceso, el colegio define si el pago es reembolsable o no.
- El sistema marca el PIN como `Vencido` y registra la situación.
- El aspirante debe iniciar un nuevo proceso si quiere reintentar.

### A2. Sin cupo — lista de espera

- Si no hay cupos disponibles en el grado, el aspirante se registra en lista de espera con un orden de llegada.
- Si se libera un cupo, el sistema notifica al primer aspirante en la lista para que proceda con el pago.

### A3. Documento rechazado múltiples veces

- No hay límite definido por defecto, pero el colegio puede configurar un máximo de reintentos.
- Si se alcanza el máximo, la solicitud queda en estado `Rechazada definitivamente` y se notifica al aspirante.

## Reglas de negocio

- **RN-MA-001 — Cupos limitados:** el sistema verifica disponibilidad de cupos antes de permitir el pago. Si los cupos se agotan entre la consulta y el pago (carrera), el sistema garantiza que solo se asignan cupos por orden de pago confirmado.
- **RN-MA-002 — PIN único por pago:** cada pago confirmado genera exactamente un PIN, asociado a un grado y un correo del aspirante.
- **RN-MA-003 — PIN con vigencia configurable:** el PIN tiene una vigencia configurable por el colegio (default 15 días).
- **RN-MA-004 — Reembolso fuera de la plataforma:** la política de reembolso por PIN vencido es del colegio. La plataforma registra el evento pero no ejecuta automáticamente el reembolso.
- **RN-MA-005 — Documentos por nivel:** los documentos requeridos varían por nivel educativo según la configuración del colegio.
- **RN-MA-006 — Confirmación exige todos los documentos aprobados:** la matrícula no puede confirmarse si hay algún documento rechazado o pendiente.
- **RN-MA-007 — Creación automática del usuario:** al confirmar la matrícula se crea automáticamente el usuario estudiante. La asignación a grupo es un paso posterior.
- **RN-MA-008 — Cuota de almacenamiento:** los documentos subidos por el aspirante consumen cuota del tenant.
- **RN-MA-009 — Auditoría completa:** todas las acciones (pago, rechazo de documento, confirmación, creación de usuario) quedan en el log.

## Estados y transiciones

### Solicitud de matrícula

```
Iniciada → Pago confirmado (PIN emitido)
        → Formulario enviado
        → En revisión
        → Documentos rechazados (loop hasta corregir)
        → Documentos aprobados
        → Matrícula confirmada (usuario creado)
        → PIN vencido
        → Rechazada definitivamente
```

### PIN

```
Emitido → Usado (formulario diligenciado)
        → Vencido (sin uso dentro del plazo)
```

## Datos involucrados

- Aspirante (datos personales antes de ser usuario).
- Pago (monto, pasarela, referencia, fecha).
- PIN.
- Documentos subidos.
- Estados de aprobación por documento.
- Usuario estudiante creado al cierre.
- Acudientes asociados.

## Documentos requeridos

Lista típica configurada por el colegio (varía por nivel):

- Fotocopia del documento de identidad.
- Registro civil de nacimiento.
- Foto reciente del estudiante.
- Certificado de notas del año anterior.
- Carné de vacunas.
- Paz y salvo del colegio anterior (si aplica).
- Otros documentos personalizados con nombre y descripción.

## Notas y pendientes

- Definir el máximo de reintentos por documento rechazado y si es configurable.
- Validar el comportamiento si el aspirante quiere matricular hermanos: ¿un pago por hermano o agrupado?
- Definir si el sistema soporta descuentos en matrícula (ver [[../06-monetizacion-y-pagos/descuentos-y-becas|Descuentos y becas]]).
