---
titulo: Logros e indicadores
modulo: procesos-academicos
tipo: referencia
estado: vigente en desarrollo local
tags: [logros, indicadores, desempeno]
---

# Logros e indicadores

Un indicador describe el aprendizaje esperado de una asignatura y un período, con alcance por grado o por grupo según el año lectivo. No se califica por separado para cada estudiante. El desempeño individual se expresa mediante las notas calculadas según el SIEE y las observaciones del boletín. La corrección de esta regla reemplaza las propuestas anteriores de escalas, caritas y estados «alcanzado / en proceso / no alcanzado» para indicadores.

## Alcance del texto

| Elemento | Comportamiento |
| --- | --- |
| Configuración anual | El rector o un rol con `indicadores.configurar` elige alcance por grado o por grupo y, solo en modo grupo, habilita si desea la escritura docente. Al pasar a grado se desactiva esa habilitación. |
| Por grado | Un indicador de grado, asignatura y período se muestra en todos los grupos de ese grado. |
| Por grupo | Cada grupo tiene una descripción de indicadores independiente por asignatura y período. Pueden redactarla roles autorizados o el docente realmente asignado a esa materia. |
| Histórico | Revisiones, actores y conversiones quedan auditados; el boletín emitido conserva el texto visible en su snapshot. |

El Rector o un rol autorizado con `indicadores.base.gestionar` administra los indicadores de todo el alcance seleccionado. Un docente o director con `indicadores.grupo.ver` y asignación activa puede consultar los indicadores **solo de su asignatura y grupo**. Para crearlos o editarlos en modo grupo necesita `indicadores.grupo.editar` **y** la política anual `docente_puede_editar` activa. La dirección de un grupo por sí sola no autoriza materias que dicta otra persona. La interfaz no muestra etiquetas «institucional» o «propio del grupo»; son indicadores del ámbito elegido, con autoría conservada únicamente en auditoría.

En modo grupo, la interfaz muestra una tabla con **asignatura** a la izquierda y **descripción** a la derecha, para todas las materias visibles al usuario en el grupo y período seleccionados. Cada celda se edita visualmente con negrita, cursiva, subrayado y listas con puntos o números; también permite revisar el código HTML. No ofrece títulos ni enlaces. El servidor limpia el HTML y conserva ese mismo formato en la vista previa, el boletín y el PDF. Las celdas se guardan con control de versión para detectar ediciones simultáneas. Una persona autorizada puede eliminar la descripción durante un período abierto: la celda queda vacía, los textos heredados no reaparecen y el boletín omite ese indicador. Los períodos cerrados muestran el motivo de bloqueo y quedan en consulta.

El cambio de grado a grupo copia cada texto a todos los grupos pertinentes y archiva los vínculos anteriores del grado. Así los textos empiezan iguales, pero pueden evolucionar por grupo. El cambio inverso conserva los indicadores de grupo como borradores reutilizables y deja el grado sin indicadores activos; un gestor selecciona un borrador o redacta el nuevo indicador de grado. Se avisa y se exige confirmación antes de cambiar con datos. La configuración es por año lectivo y no cambia automáticamente años cerrados.

## Relación con la evaluación y el boletín

El boletín presenta el texto descriptivo aplicable al período, grado, asignatura y grupo. La nota de la asignatura, la escala SIEE y la observación individual son datos distintos; ningún indicador tiene opción, número, porcentaje, estado de logro o umbral propio. Una asignatura reprobada se reconoce por su resultado académico, no por una supuesta valoración pendiente del indicador. La emisión individual no se bloquea por falta de una valoración inexistente.

## Reglas de negocio

- **RN-LI-001 — Alcance anual:** cada año opera por grado o por grupo. En años históricos que ya tengan ambos tipos, se conserva temporalmente el alcance mixto hasta que el rector confirme la conversión.
- **RN-LI-002 — Alcance docente:** la consulta y escritura exigen asignación real de asignatura y grupo. Crear o editar requiere además permiso efectivo, política anual activa y período abierto. La API verifica el alcance aunque la interfaz oculte controles.
- **RN-LI-006 — Conversión conservadora:** al pasar a grupo se copian los textos por grupo y se archiva el vínculo de grado. Al volver a grado se conservan los indicadores de grupo como borradores seleccionables y el grado parte vacío.
- **RN-LI-003 — Revisión histórica:** una redacción nueva no reescribe snapshots ya emitidos; las revisiones y el actor se auditan.
- **RN-LI-004 — Cierre:** no se modifica ordinariamente un indicador que afecte un período cerrado. Una corrección histórica exige un procedimiento auditado específico.
- **RN-LI-005 — Sin valoración independiente:** no existen escalas ni registros de logro por estudiante para indicadores; las notas siguen las reglas SIEE y las observaciones conservan su propio flujo.

La implementación local y la retirada de las tablas y permisos anteriores se describen en `colegio-saas-backend/docs/INDICADORES_ACADEMICOS.md`. Una implementación en otro entorno con datos antiguos de valoración debe respaldarlos y definir su tratamiento antes de aplicar la migración correctiva; esa migración se detiene si encuentra registros.

El 21 de octubre de 2026 se vació el contenido activo de indicadores en los cinco colegios del entorno local de desarrollo, a petición expresa y tras verificar respaldos PostgreSQL. Se conservaron la configuración del alcance, observaciones, auditoría y snapshots de boletines emitidos. Este saneamiento **no** debe ejecutarse implícitamente en migraciones ni en producción.
