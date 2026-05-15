---
titulo: "CU-013: Crear publicación en agenda"
modulo: 05-comunicacion
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, agenda, publicacion, docente]
---

# CU-013: Crear publicación en agenda

## Identificación

- **ID:** CU-013
- **Nombre:** Crear publicación en agenda
- **Módulo:** Comunicación
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** Docente, director de grupo, coordinador, rector, secretaría.
- **Secundarios:** Estudiantes / acudientes (audiencia).

## Descripción

Publicación unidireccional en el muro institucional dirigida a estudiantes o acudientes de un alcance específico.

## Precondiciones

- Autor con permiso de publicación a un alcance dado.
- Alcance dentro de su autoridad (docente: solo sus grupos; admin: cualquier alcance).

## Postcondiciones (éxito)

- Publicación visible para la audiencia.
- Notificación según el flag de urgencia y preferencias del usuario.

## Flujo principal

1. Autor entra a \"Agenda\" y crea nueva publicación.
2. Selecciona alcance y audiencia (estudiantes, acudientes, ambos).
3. Llena título, cuerpo, adjuntos.
4. Marca si es urgente.
5. Define fecha de publicación (inmediata o programada) y fecha de expiración opcional.
6. Confirma. Sistema valida permisos y publica.

## Flujos alternativos

### A1. Edición posterior

- El autor edita su propia publicación. Versión previa queda en historial.

### A2. Eliminación por administrador

- Rector / admin elimina publicación de cualquiera con motivo. Queda archivada.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Alcance fuera de autoridad. | Sistema bloquea con mensaje. |
| EX-2 | Cuota de almacenamiento llena. | Sistema bloquea adjuntos. |

## Reglas de negocio aplicables

- RN-AG-001..009, RN-AC-005.

## Criterios de aceptación

- [ ] La audiencia ve la publicación en su muro.
- [ ] La urgencia dispara notificación inmediata sin agrupar.
- [ ] La expiración la retira del muro vigente, conservándola en el histórico.

## Notas y pendientes

- Validar si los borradores se sincronizan entre sesiones del autor.
