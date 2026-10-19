---
titulo: Plan de acceso docente y filtros por asignación
fecha: 2026-10-19
estado: planificado; sin implementación
---

# Acceso docente y filtros por asignación

Este documento recoge las correcciones solicitadas al revisar la cuenta de un docente de Inmaculada. Se publica como plan: **no concede permisos ni modifica todavía las pantallas, las API o los datos**. La implementación comenzará después de publicar el corte actual de frontend, backend y documentación.

## 1. Matriz como fuente de autorización

- Levantar una tabla de rutas, elementos de navegación y operaciones API por permiso efectivo, rol y asignación vigente. No usar el nombre del rol como sustituto de la matriz ni mostrar una opción solo porque exista una pantalla.
- Ocultar para un docente sin permiso las entradas administrativas de años lectivos, estructura, plan de estudios, parámetros académicos, configuración SIEE, personalización de plantillas de boletín y reportes financieros. Ocultar también un menú padre si no conserva ningún destino autorizado.
- Mantener la validación de servidor aunque una opción no se vea. Una URL escrita manualmente debe seguir devolviendo 403 cuando corresponda. Los datos se restringen al colegio y a los grupos/asignaturas efectivamente asignados; no basta con ocultar filas en el navegador.
- Separar permiso de **consulta** de permiso de **gestión**. La carga de un año o período necesario para planilla, asistencia, calendario y boletín debe poder consultarse con acceso académico válido, sin habilitar edición de parámetros institucionales.
- Reconciliar la matriz documental, `PermissionMatrix`, los permisos efectivos del tenant y las guardas de frontend/API. Las celdas históricas que niegan consulta docente del boletín completo deben revisarse según el alcance aprobado abajo; no se hereda por ello derecho a emitir o publicar.

## 2. Indicadores y boletín del docente

- Mostrar al docente los indicadores descriptivos de su asignatura, grado, período y grupo asignados, aunque no tenga permiso de gestionar el catálogo institucional. Su variante de grupo solo será editable si el Rector habilita la política y el rol tiene el permiso específico.
- Permitirle consultar el **boletín completo en modo lectura** únicamente de estudiantes de sus grupos asignados. Esto no concede edición de calificaciones ajenas, gestión de plantillas, preparación, aprobación, publicación ni acceso a documentos privados fuera del alcance autorizado. Conservar las reglas propias de visibilidad de una emisión oficial y distinguirla de la vista preliminar.
- Comprobar tanto el listado como el detalle/API con un docente de un grupo, uno de varios grupos y otro no asignado; verificar que jamás puedan enumerarse matrículas de otro grupo.

## 3. Selecciones dependientes de la asignación

- Si la cuenta tiene **un solo grupo distinto** en el año seleccionado, fijarlo automáticamente y no mostrar un selector de grupo redundante. Esto aplica a planilla de notas, boletines, asistencia, calendario y cualquier otra vista con el mismo patrón. Dos asignaturas en el mismo grupo siguen contando como un grupo.
- Si tiene dos o más grupos distintos, mostrar el selector solo con los grupos asignados. Al cambiar año o asignación, descartar la selección anterior si ya no pertenece al alcance. No persistir en caché privada una selección de otro usuario o colegio.
- En asistencia, cargar directamente el único grupo y conservar selección de asignatura y período cuando hay varias opciones. En planilla/boletín, traer los datos del grupo único sin exigir un clic adicional.
- En calendario, retirar “Todos los grupos” como filtro para el docente de grupo único. Con varios grupos, conservar el filtro limitado a sus grupos; los eventos de todo el colegio que pueda consultar no amplían por sí solos sus asignaciones docentes.
- Mostrar el filtro de estado solo si hay más de un estado relevante y efectivamente seleccionable en ese contexto. No ofrecer controles vacíos ni opciones que conduzcan a consultas no autorizadas.

## 4. Verificación y criterios de aceptación

1. Auditar el conjunto real de permisos del docente de prueba y reproducir los 403 y el fallo de carga del año señalados en las capturas. Distinguir falta de permiso de un error de carga genuino.
2. Probar navegación, acceso directo por URL y API para docente con uno/varios grupos, rector y usuario sin asignación. El menú no muestra destinos prohibidos; el servidor los sigue bloqueando.
3. Probar cambio de año, revocación de asignación y sesión/tenant distintos para que filtros y caché no muestren datos residuales.
4. Probar indicadores, planilla, asistencia, calendario y boletín preliminar/emitido con datos del grupo propio y ajeno. El docente consulta el boletín completo de su grupo conforme a la política acordada, sin adquirir permisos de emisión o diseño.
5. Revisar diseño responsive y accesibilidad de los selectores condicionales, y actualizar matriz, documentación y pruebas automatizadas antes de cerrar el bloque.
