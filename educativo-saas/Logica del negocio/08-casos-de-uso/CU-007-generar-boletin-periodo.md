---
titulo: "CU-007: Generar boletín de periodo"
modulo: 04-procesos-academicos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, boletin, coordinacion]
---

# CU-007: Generar boletín de periodo

## Identificación

- **ID:** CU-007
- **Nombre:** Generar boletín de periodo
- **Módulo:** Procesos académicos
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** [[../02-usuarios-roles-y-permisos/roles/02-coordinador-academico|Coordinador Académico]].
- **Secundarios:** Docente, secretaría, acudiente (consumidor).

## Descripción

Generación masiva de boletines del periodo aplicando la plantilla del colegio para todos los estudiantes de uno o varios grupos.

## Precondiciones

- Periodo cerrado.
- Calificaciones de todas las asignaturas del periodo cerradas.
- Plantilla de boletín configurada.

## Postcondiciones (éxito)

- Boletines (PDF) generados, almacenados y disponibles para los estudiantes / acudientes.
- Notificaciones enviadas a los acudientes.

## Flujo principal

1. Coordinador entra y selecciona año, periodo y grupos.
2. Sistema valida que todas las notas estén cerradas.
3. Coordinador inicia generación.
4. Sistema genera PDFs en lote y los almacena en el bucket del tenant.
5. Sistema publica los boletines en el portal y notifica.

## Flujos alternativos

### A1. Plantilla personalizada por grupo

- Si el colegio usa varias plantillas, el sistema selecciona la correcta según el grado / nivel.

### A2. Generación individual

- Coordinador genera el boletín de un solo estudiante (corrección puntual).

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Notas faltantes. | Sistema bloquea y lista las asignaturas pendientes. |
| EX-2 | Cuota de almacenamiento llena. | Sistema notifica al administrador y permite reintentar tras liberar espacio. |

## Reglas de negocio aplicables

- RN-BO-NNN, RG-005 (inmutabilidad año cerrado), RN-AC-005 (cuota).

## Criterios de aceptación

- [ ] El boletín respeta la plantilla del colegio del periodo.
- [ ] El acudiente recibe notificación con enlace al boletín.
- [ ] Reimprimir un boletín da el mismo PDF (idempotente para datos no modificados).

## Notas y pendientes

- Validar si los boletines se firman digitalmente desde la fase 1.
