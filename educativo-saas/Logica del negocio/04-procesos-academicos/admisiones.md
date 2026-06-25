---
titulo: Admisiones
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [admisiones, aspirantes, proceso]
---

# Admisiones

## Descripción

Proceso por el cual una persona externa al colegio (aspirante) postula a un grado de un año lectivo, presenta las pruebas y entrevistas que el colegio defina, es evaluado, y recibe una decisión de admisión. El aspirante admitido habilita el inicio del proceso de [[matriculas|Matrícula]]; admisiones **no crea estudiante ni cobra matrícula**, solo selecciona.

Es un proceso distinto de la matrícula: admisiones decide **a quién se acepta**; la matrícula formaliza **el ingreso y el pago** del aspirante ya admitido.

## Objetivo del proceso

Seleccionar a los aspirantes que ingresarán al colegio según los criterios definidos por la institución, gestionar la lista de espera cuando el cupo es insuficiente, y entregar al aspirante admitido el medio para iniciar la matrícula sin requerir un usuario previo en el sistema.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| Aspirante / Acudiente | Persona externa que postula. No tiene usuario en el sistema; el acudiente diligencia y hace seguimiento. |
| [[roles/05-secretaria-academica\|Secretaría Académica]] | Recibe inscripciones, agenda pruebas y entrevistas, registra resultados y notifica la decisión. |
| [[roles/02-coordinador-academico\|Coordinador Académico]] | Define criterios de admisión, evalúa pruebas y participa en el comité de admisiones. |
| [[roles/03-coordinador-convivencia\|Coordinador de Convivencia]] | Realiza la entrevista psicosocial o de convivencia cuando el colegio la exige. |
| [[roles/01-rector-administrador-colegio\|Administrador del Colegio]] | Configura el proceso (etapas, cobro de inscripción, cupos) y aprueba la decisión final cuando aplica. |
| Pasarela de pago | Procesa el derecho de inscripción cuando el colegio lo cobra. Ver [[../06-monetizacion-y-pagos/pasarelas-de-pago\|Pasarelas de pago]]. |

## Precondiciones

- El año lectivo destino existe (`Planificado` o `En curso`) y tiene grados con cupos definidos.
- El colegio configuró la convocatoria de admisiones: fechas de apertura/cierre, grados ofertados y etapas exigidas (prueba, entrevista, ambas o ninguna).
- Si el colegio cobra derecho de inscripción, hay pasarela habilitada y el concepto está creado.
- El formulario de inscripción está parametrizado (campos y documentos requeridos por grado/nivel).

## Disparadores (cuándo arranca)

- Un aspirante abre el formulario público de inscripción del colegio durante la convocatoria abierta.
- Secretaría registra manualmente a un aspirante que postuló por canal externo (presencial, teléfono).

## Flujo principal

### Etapa 1 — Inscripción del aspirante

1. El aspirante (o su acudiente) ingresa al formulario público del colegio y selecciona el grado al que postula.
2. El sistema muestra la **disponibilidad de cupos** del grado para ese año lectivo.
3. El aspirante diligencia datos básicos (nombre del aspirante, datos del acudiente, correo, teléfono, colegio de procedencia) y adjunta los documentos exigidos en esta etapa.
4. Si el colegio cobra **derecho de inscripción**, el aspirante paga por la pasarela; la inscripción se confirma al recibir el pago. Si no se cobra, la inscripción se confirma al enviar el formulario.
5. El sistema registra al aspirante con estado `Inscrito` y le asigna un **código de aspirante** único en el tenant.
6. El sistema notifica al aspirante el recibido y a secretaría la nueva inscripción.

### Etapa 2 — Agendamiento de pruebas y entrevistas

1. Secretaría (o el aspirante, si el colegio habilita autoagendamiento) selecciona fecha, hora y espacio para la prueba y/o entrevista entre los cupos disponibles.
2. El sistema reserva el [[espacios-fisicos\|espacio físico]] y evita choques de agenda del evaluador.
3. El sistema notifica al aspirante la cita con fecha, hora, lugar e instrucciones; el aspirante pasa a estado `En evaluación`.

### Etapa 3 — Registro de pruebas y entrevistas

1. El día de la cita el evaluador registra la asistencia del aspirante.
2. El evaluador registra el resultado de la prueba (puntaje por área) y/o el concepto de la entrevista (observaciones cualitativas).
3. El sistema consolida los resultados en el expediente del aspirante.

### Etapa 4 — Evaluación y decisión

1. El comité de admisiones (o el rol con permiso) revisa el consolidado de resultados de cada aspirante.
2. Registra la decisión: **Admitido**, **No admitido** o **En lista de espera**.
3. Toda decisión exige una justificación que queda en el log de auditoría.
4. El sistema notifica al aspirante la decisión por los canales configurados.

### Etapa 5 — Conversión del aspirante admitido a matrícula

1. Para el aspirante `Admitido`, el sistema habilita el inicio de la matrícula y emite el **PIN de matrícula** asociado a su grado y correo, sin que el aspirante deba pagar de nuevo el derecho de inscripción.
2. El aspirante recibe el PIN y el enlace para continuar en el proceso de [[matriculas|Matrícula]].
3. El aspirante pasa a estado `Convertido a matrícula`. Admisiones no crea el usuario estudiante; eso ocurre al confirmar la matrícula (`RN-MA-007`).

## Flujos alternativos

### A1. Sin cupo — lista de espera

- Si al cerrar la decisión el aspirante cumple criterios pero no hay cupo, queda `En lista de espera` con un orden (por puntaje o por orden de inscripción, según configuración).
- Si se libera un cupo, el sistema propone al primer aspirante elegible de la lista y notifica a secretaría para que confirme su admisión.

### A2. Aspirante no se presenta a la cita

- Si el aspirante no asiste a la prueba o entrevista, el evaluador lo marca como `No presentado`.
- El colegio define si permite reagendar (con o sin recargo) o si la inscripción queda `Desistida`.

### A3. Aspirante desiste

- El aspirante o el acudiente puede desistir en cualquier etapa previa a la conversión. El estado pasa a `Desistido` y libera la reserva de cita si la tenía.

## Estados y transiciones

### Aspirante

```
Inscrito → En evaluación → Admitido → Convertido a matrícula
                         → No admitido
                         → En lista de espera → Admitido (al liberarse cupo)
                                              → No admitido (cierre de convocatoria)
Inscrito / En evaluación → No presentado → (reagenda) En evaluación
                                         → Desistido
Cualquier estado previo a conversión → Desistido
```

### Derecho de inscripción (si se cobra)

```
Pendiente → Pagado (inscripción confirmada)
         → No pagado (inscripción no confirmada / expira)
```

## Configurabilidad por colegio

- Etapas exigidas: solo formulario, formulario + prueba, formulario + entrevista, o las tres.
- Cobro del derecho de inscripción: activado o no; monto; política de reembolso (no automática).
- Criterio de orden de la lista de espera: por puntaje de prueba o por orden de inscripción.
- Autoagendamiento de citas por el aspirante: habilitado o gestionado solo por secretaría.
- Quién toma la decisión final: comité, coordinador académico o rector.
- Campos y documentos requeridos del formulario por grado/nivel.

## Datos involucrados

- Aspirante (datos personales y de contacto antes de ser usuario) y su código de aspirante.
- Acudiente que postula.
- Grado y año lectivo de destino.
- Pago del derecho de inscripción (monto, referencia, fecha) si aplica.
- Citas agendadas (fecha, espacio, evaluador).
- Resultados de prueba (puntaje por área) y concepto de entrevista.
- Decisión de admisión y justificación.
- Referencia al PIN de matrícula emitido al convertir.

## Integraciones con otros módulos

- [[matriculas|Matrícula]]: la admisión emite el PIN que da inicio a la matrícula; sin admisión aprobada no debería iniciarse matrícula cuando el colegio exige proceso de admisiones.
- [[espacios-fisicos|Espacios físicos]]: reserva de salones para pruebas y entrevistas.
- [[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación y recibos]]: recibo del derecho de inscripción.
- [[observador-del-estudiante|Observador del estudiante]]: el expediente de admisión no se vuelve observador hasta que el aspirante es estudiante matriculado.
- [[../09-reportes-y-analitica/reportes-academicos|Reportes académicos]]: embudo de admisiones (inscritos, evaluados, admitidos, convertidos) y ocupación de cupos.

## Reglas de negocio

- **RN-AM-001 — Admisión distinta de matrícula:** admisiones selecciona aspirantes pero no crea estudiante ni cobra matrícula; la creación del usuario ocurre solo al confirmar la matrícula (`RN-MA-007`).
- **RN-AM-002 — Código de aspirante único:** cada inscripción genera un código de aspirante único dentro del tenant, independiente del futuro usuario estudiante.
- **RN-AM-003 — Derecho de inscripción opcional y configurable:** el colegio decide si cobra el derecho de inscripción y su monto; la inscripción solo se confirma con el pago cuando el cobro está activo. El reembolso es política del colegio, no se ejecuta automáticamente.
- **RN-AM-004 — Etapas configurables por colegio:** las etapas exigidas (prueba, entrevista, ambas o ninguna) son parametrizables; el aspirante no avanza a decisión sin completar las etapas exigidas.
- **RN-AM-005 — Cupo verificado en la decisión:** un aspirante solo puede pasar a `Admitido` si hay cupo disponible en el grado; si no lo hay, la única transición válida desde elegible es `En lista de espera`.
- **RN-AM-006 — Lista de espera ordenada y configurable:** el orden de la lista de espera sigue el criterio configurado por el colegio (puntaje u orden de inscripción) y se respeta al liberarse un cupo.
- **RN-AM-007 — Decisión justificada y auditada:** toda decisión de admisión (admitido, no admitido, en espera) exige justificación y queda en el log con autor, fecha y valor.
- **RN-AM-008 — Conversión emite PIN de matrícula:** al marcar `Admitido` y convertir, el sistema emite el PIN de matrícula del aspirante (`RN-MA-002`) sin recobrar el derecho de inscripción ya pagado.
- **RN-AM-009 — Sin reproceso de pago en conversión:** el derecho de inscripción y el valor de matrícula son conceptos distintos; convertir un admitido no descuenta ni duplica el cobro de matrícula.
- **RN-AM-010 — Documentos consumen cuota del tenant:** los documentos adjuntos en la inscripción consumen la cuota de almacenamiento del colegio aun antes de existir el estudiante.

## Notas y pendientes

- **[Decisión tomada]** Admisiones y matrícula son procesos separados con cobros independientes: el derecho de inscripción no se descuenta ni se transfiere al valor de matrícula. Regla: **RN-AM-009**.
- **[Decisión tomada]** El expediente de admisión no se convierte en observador del estudiante; solo al matricularse se inicia el observador. Ver [[observador-del-estudiante|Observador del estudiante]].
- **[Pendiente — producto]** Definir si el aspirante en `Lista de espera` recibe un ranking visible o solo la confirmación de estar en espera, por sensibilidad de la información entre familias.
- **[Pendiente — producto]** Validar el autoagendamiento de citas durante el piloto: control de no-shows y política de recargo por reagendamiento.
- **[Pendiente — producto]** Decidir si un colegio puede operar matrícula directa (sin proceso de admisiones) y, en ese caso, cómo se concilia con `RN-AM-001`.

## Documentos relacionados

- [[matriculas|Matrícula]]
- [[espacios-fisicos|Espacios físicos]]
- [[observador-del-estudiante|Observador del estudiante]]
- [[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarelas de pago]]
- [[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación y recibos]]
- [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica|Secretaría Académica]]
- [[../02-usuarios-roles-y-permisos/roles/02-coordinador-academico|Coordinador Académico]]
- [[../09-reportes-y-analitica/reportes-academicos|Reportes académicos]]
