---
titulo: "CU-011: Registrar anotación en observador"
modulo: 04-procesos-academicos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, observador, disciplina, docente]
---

# CU-011: Registrar anotación en observador

## Identificación

- **ID:** CU-011
- **Nombre:** Registrar anotación en observador
- **Módulo:** Procesos académicos / Disciplina
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** Docente, director de grupo o coordinador.
- **Secundarios:** Acudiente, estudiante (consumidores).

## Descripción

Registro de una anotación (positiva, académica o disciplinaria) en el observador del estudiante, con seguimiento si aplica.

## Precondiciones

- Estudiante activo en el año vigente.
- Autor con autoridad para registrar (según matriz de permisos).

## Postcondiciones (éxito)

- Anotación creada en el observador.
- Notificación al acudiente si la anotación lo requiere.

## Flujo principal

1. Autor entra al observador del estudiante.
2. Selecciona tipo (positiva, académica, disciplinaria) y subtipo.
3. Describe el hecho con fecha, lugar, contexto.
4. Adjunta evidencia si aplica.
5. Marca si requiere confirmación del acudiente.
6. Confirma. Sistema persiste y dispara notificación.

## Flujos alternativos

### A1. Compromiso disciplinario

- Para faltas graves, el flujo incluye creación de un compromiso firmado por el acudiente.

### A2. Acción posterior (apelación)

- El acudiente puede apelar; entra al flujo de revisión por coordinación de convivencia.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Adjunto demasiado grande. | Sistema rechaza; recomienda compresión. |
| EX-2 | Estudiante en otro tenant. | Imposible: aislamiento estricto. |

## Reglas de negocio aplicables

- RN-OE-NNN, RN-DI-NNN, RG-002, RG-005 (inmutabilidad histórica).

## Criterios de aceptación

- [ ] La anotación queda con autor, fecha y evidencia adjunta si la hay.
- [ ] El acudiente la ve en el portal y recibe notificación si aplica.
- [ ] Las anotaciones de años cerrados no se editan.

## Notas y pendientes

- Validar el flujo cuando una anotación debe retirarse por decisión de comité (queda como modificación con motivo, no borrado).
