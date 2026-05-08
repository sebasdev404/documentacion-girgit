---
titulo: "CU-004: Capturar calificaciones de un periodo"
modulo: 04-procesos-academicos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, calificaciones, docente]
---

# CU-004: Capturar calificaciones de un periodo

## Identificación

- **ID:** CU-004
- **Nombre:** Capturar calificaciones de un periodo
- **Módulo:** Procesos académicos
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** [[../02-usuarios-roles-y-permisos/roles/06-docente|Docente]].
- **Secundarios:** [[../02-usuarios-roles-y-permisos/roles/02-coordinador-academico|Coordinador Académico]] (cierre).

## Descripción

El docente registra las calificaciones de los estudiantes de sus grupos / asignaturas asignados, en los logros e indicadores definidos para el periodo activo.

## Precondiciones

- El periodo está abierto para captura.
- El docente tiene asignación vigente al grupo y asignatura.
- El plan de estudios y los indicadores están configurados.

## Postcondiciones (éxito)

- Calificaciones guardadas en estado **Borrador** o **Cerradas del periodo**.
- Sistema calcula la nota final del periodo aplicando los pesos.

## Flujo principal (camino feliz)

1. Docente entra al portal y selecciona el grupo y la asignatura.
2. Ve la lista de estudiantes con los indicadores del periodo.
3. Captura la nota de cada indicador / actividad.
4. Sistema valida que la nota esté en el rango de la escala.
5. Docente guarda. Sistema persiste como borrador.
6. Docente repite hasta tener todas las notas.
7. Docente \"cierra\" el periodo en su asignatura. Sistema marca como **Cerradas**.
8. Coordinación valida y publica los boletines (CU-007).

## Flujos alternativos

### A1. Modificación tras cierre

- Solo con permiso especial. Sistema registra valor previo y nuevo en log con motivo.

### A2. Carga masiva por Excel

- Docente descarga plantilla, llena, sube. Sistema valida y aplica.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Nota fuera de la escala. | Sistema rechaza con mensaje del rango. |
| EX-2 | Pesos no suman 100%. | Sistema advierte y no permite cerrar el periodo. |
| EX-3 | Periodo cerrado. | Sistema bloquea captura, ofrece flujo de excepción. |

## Reglas de negocio aplicables

- RN-CA-NNN, validaciones de escala y pesos, RG-005 (inmutabilidad), RG-002 (auditoría).

## Datos de entrada / salida

- **Entrada:** notas por estudiante e indicador.
- **Salida:** notas almacenadas, nota final del periodo calculada.

## Criterios de aceptación

- [ ] Docente solo ve sus grupos / asignaturas.
- [ ] El sistema calcula automáticamente la nota final del periodo.
- [ ] Una vez cerrado, el docente no edita salvo permiso especial.

## Notas y pendientes

- Validar si la captura permite asistencia de un asistente / suplente del docente con permiso especial.
