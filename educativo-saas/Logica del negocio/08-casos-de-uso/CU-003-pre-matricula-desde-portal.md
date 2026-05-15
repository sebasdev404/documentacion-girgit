---
titulo: "CU-003: Pre-matrícula desde portal"
modulo: 04-procesos-academicos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, pre-matricula, portal, acudiente]
---

# CU-003: Pre-matrícula desde portal

## Identificación

- **ID:** CU-003
- **Nombre:** Pre-matrícula desde portal
- **Módulo:** Procesos académicos
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** Acudiente / aspirante.
- **Secundarios:** [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica|Secretaría Académica]] (revisión).

## Descripción

Un acudiente o aspirante completa el formulario de pre-matrícula desde el portal del colegio, sube documentos y queda en cola para la revisión y confirmación por parte de secretaría (CU-002).

## Precondiciones

- El colegio tiene el período de admisiones / renovaciones abierto.
- El acudiente tiene acceso al portal o puede registrarse.

## Postcondiciones (éxito)

- Pre-matrícula creada en estado **Documentos pendientes** o **Documentos cargados**.
- Secretaría notificada para revisión.

## Flujo principal (camino feliz)

1. Acudiente entra al portal y selecciona \"Pre-matricular\".
2. Llena los datos del estudiante (o carga existente si renovación).
3. Sube los documentos requeridos según la lista del colegio.
4. Acepta el contrato / pagaré (firma electrónica simple).
5. Confirma envío.
6. Sistema valida estructura y antivirus.
7. Sistema registra la pre-matrícula y notifica a secretaría.

## Flujos alternativos

### A1. Pago de inscripción inicial

- Si el colegio cobra inscripción para iniciar admisión, el acudiente paga antes de poder enviar el formulario.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Documento infectado o no soportado. | Sistema rechaza el archivo con mensaje claro. |
| EX-2 | Cupos agotados en el grado. | Sistema permite enviar pero advierte que entra en lista de espera. |
| EX-3 | Sesión perdida a mitad de proceso. | El borrador se conserva y se puede retomar. |

## Reglas de negocio aplicables

- RN-MA-NNN, RN-AC-002 (antivirus), RN-GD-005 (documentos requeridos).

## Datos de entrada / salida

- **Entrada:** formulario y documentos.
- **Salida:** pre-matrícula registrada, número de radicado.

## Criterios de aceptación

- [ ] El acudiente puede retomar un formulario incompleto.
- [ ] La pre-matrícula queda visible para secretaría con todos los datos y archivos.
- [ ] El acudiente recibe acuse del envío con número de radicado.

## Notas y pendientes

- Validar si la pre-matrícula puede iniciarse sin tener todavía cuenta en el portal (por correo).
