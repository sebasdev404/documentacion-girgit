---
titulo: "CU-006: Justificar inasistencia"
modulo: 04-procesos-academicos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, asistencia, justificacion, acudiente]
---

# CU-006: Justificar inasistencia

## Identificación

- **ID:** CU-006
- **Nombre:** Justificar inasistencia
- **Módulo:** Procesos académicos
- **Prioridad:** media
- **Versión:** 0.1

## Actores

- **Primario:** Acudiente o estudiante mayor de edad.
- **Secundarios:** Director de grupo, coordinación de convivencia.

## Descripción

Acudiente sube soporte para justificar una inasistencia registrada. El sistema enruta la solicitud al rol responsable, que aprueba o rechaza.

## Precondiciones

- Existe inasistencia registrada en estado **No justificada**.
- La solicitud cae dentro de la ventana de justificación configurada.

## Postcondiciones (éxito)

- Inasistencia queda **Justificada** o **Rechazada con motivo**.
- Acudiente recibe notificación.

## Flujo principal

1. Acudiente entra al portal y ve las inasistencias del estudiante.
2. Selecciona la inasistencia y elige \"Justificar\".
3. Llena motivo (categorías predefinidas: salud, calamidad, etc.).
4. Sube soporte (incapacidad, etc.).
5. Confirma. Sistema crea solicitud en estado **Pendiente**.
6. Director de grupo o coordinador revisa, aprueba o rechaza con comentario.
7. Sistema notifica al acudiente.

## Flujos alternativos

### A1. Justificación sin soporte

- Configurable por el colegio: algunos casos no requieren soporte (calamidad declarada).

### A2. Fuera de ventana

- Sistema impide la justificación; el caso requiere autorización del coordinador.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Soporte demasiado grande. | Sistema rechaza con mensaje de tamaño máximo. |
| EX-2 | Soporte infectado. | Sistema rechaza por antivirus. |

## Reglas de negocio aplicables

- RN-AS-NNN, RN-AC-002, RG-002.

## Criterios de aceptación

- [ ] La justificación queda visible en el observador y la asistencia.
- [ ] El estado de la inasistencia se actualiza al aprobarse / rechazarse.
- [ ] El acudiente recibe notificación con el resultado.

## Notas y pendientes

- Validar si una justificación retroactiva fuera de ventana puede aprobarse manualmente con motivo registrado.
