---
tags: [academico, siee, avance, evidencia]
aliases: [Avance del ciclo académico 2026-09-30]
---

# Avance del ciclo académico — 30 de septiembre de 2026

## Actualización posterior: 1 de octubre de 2026

**Estado más reciente (1 de octubre):** 247 pruebas backend/1827 aserciones y 32 pruebas frontend correctas; compilación frontend aprobada. El resultado visible usa un decimal con empate hacia abajo (`3.15 → 3.1`) también para años históricos, sin reescribir calificaciones capturadas. La migración tenant `2026_10_01_000001` se aplicó a cinco tenants locales; conservó sin configurar los SIEE que estaban en `NULL`. Se verificó una instalación PostgreSQL nueva y una actualización restaurada. Los respaldos anteriores a la actualización están en el directorio temporal documentado por backend. La emisión oficial de boletines y el resto del ciclo siguen pendientes.

Verificación del corte: **237 pruebas backend / 1711 aserciones**, **31 pruebas frontend**, build y auditoría i18n aprobados (1096 claves, sin faltantes es/en ni fallbacks inline). Recorridos de navegador de notas/preinformes, paginación y navegación general aprobados con API simulada; migraciones PostgreSQL comprobadas separadamente como se detalla abajo. Esto no certifica emisión oficial de boletines ni los módulos pendientes del ciclo completo.

El propietario redefinió la evaluación: el rector configura preinformes opcionales por año/período; el docente define actividades y sus porcentajes en una planilla tipo Excel. **La preparación de actividades desde currículo ya no es un paso obligatorio del flujo nuevo.** El currículo conserva grado–materia–área, con peso de área exclusivamente cuando el SIEE lo requiere.

Implementado: menú separado Evaluación y notas, cuadrícula con pegado/tabulación/flechas, edición de columnas, subtotales por preinforme, decimal normalizado (coma a punto, sin ceros sobrantes), permisos de acción/delegación y capacidad de plan `preinformes` (Estándar/Premium o plan personalizado). Sin preinformes hay notas directas simples o ponderadas. Los pesos de actividades, preinformes y períodos son niveles distintos y no se mezclan; cada conjunto ponderado suma 100 %. Los datos anteriores se preservan, sin redistribución automática de notas.

Las migraciones central 000006 y tenant 000010–000011 ya se aplicaron a los cinco tenants locales, con respaldo de central/tenants, prueba de esquema PostgreSQL desde cero y actualización de una restauración aislada de Inmaculada. Se verificó conservación de usuarios, actividades y valores de notas. Las bases temporales se retiraron; respaldo conservado en Temp, según documento backend. La copia de períodos incorpora configuración de preinformes, nunca actividades, docentes ni notas.

Evidencia y detalle operativo en los documentos `docs/CICLO_ACADEMICO_AVANCE.md` de backend/frontend y pruebas `FlexibleGradingTests`, `AcademicPermissionMigrationTest`, `browser-smoke.mjs --grading` y `--pagination`. El resto de la tabla inferior es el corte histórico: no acredita emisión oficial de boletines, consejo ni cierre del ciclo completo.

## Corte del 30 de septiembre

Referencia de alcance: `PLAN_COMPLETAR_CICLO_ACADEMICO.md` en la raíz del proyecto. Este registro separa lo **implementado y probado** de lo que aún falta. El propietario autorizó posteriormente cinco cuentas ficticias en Inmaculada para pruebas locales; no acredita operación real de un colegio.

| Fase del plan | Estado al corte | Evidencia / siguiente condición |
|---|---|---|
| 1. Inventario y matriz | Parcial | Se contrastaron plan, especificación SIEE, corte Girgit y código vigente. La matriz AC se actualiza sin marcar completo un criterio por una pantalla. |
| 2. Calendario, currículo y preparación | Parcial | Revisión previa de cierre, cobertura/contigüidad de períodos y preparación de componentes/actividades sin docentes ni estudiantes. Restan indicadores integrales del currículo, restricciones de cambios históricos y recorrido PostgreSQL de migraciones. |
| 3. Planillas, manuales y escalas | Parcial | La preparación se aplica explícitamente a la planilla existente sin mezclar componentes; falta captura manual por ámbito, escala por imágenes y UX completa de edición/concurrencia. |
| 4. Recuperaciones | Operativa para escala numérica | Expediente persistente por matrícula, materia y período/año; candidatos de resultado reprobado completo, nota original intacta, política SIEE, resultado efectivo, autorización, auditoría, anulación y vista en boletín preliminar. Faltan escalas por imágenes y validación visual interactiva. |
| 5. Promoción, consejo y cierre | Parcial | Política anual, propuesta explicable, aprobación del Rector con huella/versionado y cierre con decisiones vigentes ya funcionan. Sin notas completas no hay propuesta; faltan consejo, condicionados y congelación/emisión de históricos. |
| 6. Asistencia, logros y director | Pendiente | Requiere modelos, permisos de alcance y bloqueos en período cerrado. |
| 7. Editor de boletines | Pendiente | Usar capacidad efectiva `boletines_personalizables` desde Estándar y permiso de Rector; falta editor, versiones y vista previa aislada. |
| 8. Emisión oficial y PDF | Pendiente | El boletín actual es `VISTA_PREVIA`, no un documento aprobado o distribuible. |
| 9. Recorrido integral | Parcial | Migraciones 000007 y 000008 aplicadas a cinco tenants PostgreSQL locales y verificación de la consulta que fallaba. Dos docentes y estudiantes ficticios recorren planilla y boletín preliminar; no hay promoción ni emisión oficial. |

## Contratos y decisiones preservadas

- Los selectores de año, grado, materia, período y asignación en las rutas nuevas son opacos; las tablas usan claves internas exclusivamente del lado servidor.
- La preparación pertenece a materia curricular y período, con componentes, actividades, versión optimista y marca persistente de primera aplicación. La aplicación a una asignación materia–grupo es explícita, idempotente y auditada. No depende de crear un docente o estudiante, no toca notas existentes y no se sobrescribe tras aplicarse.
- El SIEE numérico del año sigue gobernando los pesos y la escala; una preparación incompleta se puede guardar, pero no aplicar. Esto no habilita aún escala por imágenes ni el modo `MANUAL` de resultados.
- La API rechaza una **nueva** selección de resultado `MANUAL` para materia, área o anual mientras no haya captura persistente y autorizada; mantiene sin reescribir configuraciones históricas. La política de recuperación `MANUAL` es otra regla y no se cambia en esta entrega.
- El cierre no ejecuta promoción de forma implícita. Distingue año vacío, año con solo matrículas retiradas y año con matrículas activas; estas últimas exigen decisiones de promoción aprobadas y vigentes. Los períodos pueden cerrarse aun con notas pendientes, pero esas pendientes no se convierten en cero ni permiten aprobar promoción.
- La duplicación anual incluye definiciones preparatorias cuando están presentes currículo y períodos homólogos; no copia planillas, personas ni notas. Una copia posterior permite completar secciones omitidas sin sobrescribir una definición local.
- La reapertura anual exclusiva de Plataforma y la reapertura explícita del período no se cambiaron. Por autorización posterior se añadieron únicamente cinco cuentas ficticias a Inmaculada, no a los otros tenants.

## Evidencia y límites de despliegue

Última verificación: **228 pruebas backend, 1621 aserciones; 29 pruebas frontend**, compilación y auditoría de traducciones correctas. Las cifras de los párrafos siguientes documentan cortes anteriores.

Backend: `php artisan test --compact` pasó con **220 pruebas y 1545 aserciones** en el corte; `AcademicModulesTest` cubre revisión de cierre, año vacío/con matrícula, copia posterior, preparación sin personas, conflictos de versión, aplicación repetida, aislamiento de selectores y conservación de la marca aplicada. Frontend: compilación, auditoría de traducciones y 29 pruebas de scripts pasaron; falta prueba visual interactiva del panel nuevo.

**Corte posterior:** tras implementar recuperación numérica, la suite backend pasó con **223 pruebas y 1580 aserciones**; la compilación y auditoría de traducciones del frontend también pasaron. La nueva migración `000008` se aplicó a los cinco tenants, tras respaldarlos de nuevo en `C:\Users\Pedro\AppData\Local\Temp\colegio-academico-20260930-230518`; una simulación posterior confirmó que no quedan migraciones pendientes. El índice de selectores opacos se corrigió para admitir tablas creadas más tarde durante el alta de un tenant nuevo. Los respaldos en Temp no equivalen a retención segura ni se ha ensayado una restauración PostgreSQL.

**Actualización posterior del 30 de septiembre:** el fallo SQL por ausencia de `preparaciones_evaluacion` confirmó que el código nuevo estaba activo antes de la migración en Inmaculada. Se respaldaron y verificaron cinco bases locales PostgreSQL, se aplicó `2026_09_30_000007_prepare_curriculum_evaluation.php` a los cinco tenants y una segunda simulación informó «Nothing to migrate» en todos. En Inmaculada se verificaron las tres tablas y el enlace en `componentes_evaluacion`; una lectura de preparación ya devuelve un estado vacío válido. Los respaldos quedaron en `C:\Users\Pedro\AppData\Local\Temp\colegio-academico-20260930-224740`; por ser un directorio temporal, no es una política de retención. Falta la comprobación de restauración y de provisionamiento nuevo en PostgreSQL aislado.

Con autorización expresa para cuentas temporales, en Inmaculada se crearon dos docentes, dos estudiantes y una cuenta de coordinación con nombres verosímiles, correos institucionales reservados bajo `.example` y contraseñas temporales cifradas, visibles para el Rector mediante gestión de usuarios. Los correos iniciales `.test` se reemplazaron mediante cinco cambios auditados para evitar rótulos de prueba en los datos visibles, sin hacerlos entregables a personas ajenas. Se vincularon los docentes a Matemáticas y Lengua Castellana del grupo Primero 01A y se matricularon los dos estudiantes allí. Se registraron cuatro actividades y ocho calificaciones en el cuarto período, actualmente abierto. Las notas de los períodos cerrados no se alteraron. Se comprobaron roles, asignaciones, matrículas, resultados calculados y auditoría. Son identidades ficticias locales, no personas reales ni demostración de un año académico concluido.

Comprobación puntual con estas identidades: el docente de Matemáticas recibió 200 al abrir su planilla del cuarto período; el docente de Lengua Castellana recibió 403 al intentar abrir esa misma planilla; un estudiante recibió 200 al consultar su propia vista preliminar de boletín. El informe contiene 11 materias y dos resultados calculados para el cuarto período; el resto permanece pendiente. No hay candidatos de recuperación en esas cuentas porque el período de las notas creadas sigue abierto. Esa vista no constituye emisión oficial.

**Corte de promoción revisada:** la migración tenant `2026_09_30_000009_create_promociones_academicas.php` creó políticas por año y decisiones por matrícula con actor, motivo, versión, huella e insumos. Las cinco bases PostgreSQL se respaldaron y verificaron en `C:\Users\Pedro\AppData\Local\Temp\colegio-academico-20260930-232420` antes de migrar; tras la aplicación, las cinco informaron «Nothing to migrate». El Rector puede configurar la política, consultar propuestas pendientes/calculadas y aprobar con grado destino explícito. Una política o nota cambiada vuelve obsoleta la decisión y bloquea el cierre. Solo se aprueba una propuesta igual al cálculo —o egreso de alguien promovido—; cualquier excepción requiere el consejo académico pendiente. No se creó promoción ni se cerró Inmaculada, cuyos períodos anteriores siguen sin notas de estas matrículas. Estos datos ficticios tienen nombres y actividades escolares verosímiles, sin etiquetas «Demo» o «Prueba» en los registros visibles; los correos `.example` siguen siendo no entregables por seguridad.

La nueva interfaz pasó un smoke aislado en navegador (`node scripts/browser-smoke.mjs --promotion`): se guardó la política, se aprobó una propuesta y se revisó que el modal no desbordara el ancho a 390/320 px. Usa API simulada; no constituye una prueba visual con los datos reales del tenant.

Contratos de API y migración: `colegio-saas-backend/docs/CICLO_ACADEMICO_AVANCE.md`. Recorrido de Rector y estados vacíos: `colegio-saas-frontend/docs/CICLO_ACADEMICO_AVANCE.md`.

## Dependencias para la siguiente entrega

1. Completar validadores de currículo, pesos por grado/área y protección ante históricos.
2. Resolver persistencia de resultados manuales y variación de escala por nivel sin reinterpretar SIEE existente.
3. Probar visualmente nivelaciones/habilitaciones y resultados efectivos con un período cerrado en un tenant aislado antes de calcular promoción; en Inmaculada no se cerró prematuramente el cuarto período.
4. Completar consejo académico, resultados condicionados y actas antes de admitir excepciones a la propuesta de promoción. La política/propuesta/aprobación ordinaria ya persisten.
5. Preparar asistencia, logros y director de grupo con permisos verificables.
6. Construir editor de diseños con permiso Rector y capacidad real de plan; luego emisión aprobada, PDF inmutable e histórico.
7. Probar migraciones PostgreSQL, aislamiento/roles y recorrido con identidades temporales en entorno de prueba, sin poblar colegios reales.
