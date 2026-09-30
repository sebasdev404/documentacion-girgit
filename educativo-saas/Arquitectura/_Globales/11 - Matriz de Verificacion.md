---
tags: [arquitectura, aceptacion, evidencia]
aliases: [Matriz de Verificacion, Estado verificable del producto]
---

# Matriz de verificación

**Actualización del 30 de septiembre de 2026:** el [registro de entregas](12%20-%20Registro%20de%20entregas%202026-09.md) y el [estado de sesión y selectores](11%20-%20Pendiente%20de%20seguridad%20de%20sesion%20web.md) incorporan la migración a cookies HttpOnly/CSRF, selectores públicos en API académica y plataforma, permisos de archivos y verificaciones locales (206 pruebas backend, 1443 aserciones y 20 frontend). Estos avances amplían la evidencia de AC-02, AC-18 y AC-24, que siguen **parciales** porque requieren cobertura de todos los módulos y validación de despliegue. AC-20 también sigue parcial: el simulacro no equivale a respaldos externos y restauraciones operativas.

Las cifras de ejecución y hashes del corte del 29 de septiembre que siguen abajo son una instantánea histórica de esa entrega, no resultados del corte del 30.

**Corte:** 29 de septiembre de 2026. Repositorios: frontend y backend `pedro-dev`, documentación `main`. Base previa: frontend `2aae193`, backend `e488f59`, documentación `8e318e0`; esta matriz incluye la entrega de perfil/MFA, confirmada después en frontend (`5f12ede`) y backend (`d224a29`).

**Cobertura documental:** los 29 criterios vigentes de [[08 - Criterios de Aceptacion]] tienen una fila. AC-28 permanece retirado; no se reutiliza. Los estados se refieren al criterio completo, no al porcentaje de archivos escritos.

| Estado | Significado |
|---|---|
| Verificado local | El comportamiento delimitado tiene prueba local reproducible. No certifica producción ni todas las combinaciones de datos |
| Parcial | Hay implementación o evidencia de una parte; el criterio completo tiene brechas explícitas |
| Pendiente | No se encontró un flujo completo y verificable para cumplirlo |
| Futuro | Fuera de la entrega inicial por el corte de alcance; conserva su ID y dependencia |

## Matriz de aceptación

| AC | Criterio resumido | Entrega / prioridad | Estado | Evidencia localizada | Falta para aceptar el criterio completo |
|---|---|---|---|---|---|
| AC-01 | Crear colegio, base, semillas, subdominio y Rector | Base / P0 | Parcial | E01: provisionamiento, migraciones y pruebas de onboarding | Prueba de provisionamiento PostgreSQL completa reproducible en integración, fallos/reintentos y reversión; las pruebas automatizadas habituales usan SQLite |
| AC-02 | Aislamiento por tenant en acceso y datos | Base / P0 | Parcial | E01, E02, E03: identificación, tokens opacos ligados al tenant, autenticación de canales y descargas firmadas | Extender negativos a todos los endpoints y archivos, jobs, sedes y restauraciones; una URL opaca no sustituye autorización |
| AC-03 | Auditoría sensible consultable por Rector | Base / P0 | Parcial | E04: logs, redacción, inmutabilidad y vista de auditoría de Plataforma | Consulta tenant autorizada para Rector, cobertura de todos los eventos sensibles, retención y resistencia operacional a manipulación |
| AC-04 | Fechas/períodos válidos y cobertura del año | Académico / P1 | Parcial | E05: estados por fechas, período actual, transición de año y duplicación | Prueba dedicada de cobertura exacta/contigüidad, huecos y límites de calendario; distinguir fecha del año de tipo A/B institucional |
| AC-05 | Escala numérica o por imágenes usada en las notas | Académico / P1 | Parcial | E05, E06: SIEE anual, cálculo exacto, escalas y validación de notas | Flujo de captura, cálculo y documento final con escala por imágenes; extremos de redondeo para todas las configuraciones |
| AC-06 | Coordinador asigna; docente ve lo asignado | Académico / P1 | Parcial | E05: asignación, propagación a clases y visibilidad de horarios del docente | Prueba completa de interfaz con coordinador y docente, sedes y año cerrado; validar todo el catálogo, no solo horarios |
| AC-07 | Docente solo registra notas de sus materias | Académico / P1 | Parcial | E05: `wrong_teacher_and_other_students_cannot_read_gradebooks_or_reports`, escritura y concurrencia | Prueba de escritura HTTP negativa con docente ajeno y comprobación de interfaz para todas las rutas de planillas |
| AC-08 | Período cerrado bloquea; reapertura autorizada explícita | Académico / P0 | Verificado local | E05: `closed_periods_block_grade_writes`, Rector sin permiso rechazado, coordinador sin transición, reapertura manual persiste | Mantener regresiones; ventana de solicitudes futura no está implementada ni autoriza escribir cerrado |
| AC-09 | Director ve consolidado del grupo y solo sus materias fuera | Académico / P1 | Parcial | E05, E07: catálogo de roles y restricciones generales de evaluación | Asignación efectiva director↔grupo y prueba positiva/negativa del consolidado multiasignatura con un director real |
| AC-10 | Convivencia gestiona observador con acceso acotado a notas | Operación / P1 | Pendiente | E07, E08: permisos catalogados; rutas de convivencia todavía en «Próximamente» | Observador persistente, visibilidad, autorización por ficha, acciones y pruebas de convivencia |
| AC-11 | Secretaría emite documentos oficiales con consecutivo | Operación / P1 | Pendiente | E08; E05 solo demuestra vista previa de boletín | Emisión oficial, numeración concurrente, firma, registro y trazabilidad de constancias/certificados/paz y salvo |
| AC-12 | Bloqueo de documentos por pendientes | Operación / P1 | Pendiente | E08: sin integración completa de documentos, matrícula y cartera | Política institucional, comprobación backend al emitir, excepciones autorizadas y auditoría |
| AC-13 | Exportación SIMAT descargable | Operación / P1 | Pendiente | E08: reporte oficial sin flujo completo | Implementar con requisitos adicionales de AC-30; una exportación genérica no es formato oficial válido |
| AC-14 | Estudiante consulta solo su información | Operación / P1 | Parcial | E05: horarios/eventos por matrícula y restricción de boletines | Portal completo de observaciones y boletines publicados, permisos efectivos y pruebas de identidad/matrícula en todos los módulos |
| AC-15 | Portal multihijo con vínculos autorizados | Ampliación / P2 | Futuro | RN-TU-410 y [[../../Logica del negocio/01-vision-y-alcance/corte-de-alcance-2026-09-29|corte de alcance]] | Diseñar identidad delegada/vínculos comprobados antes del selector; el mismo correo de contacto no concede acceso |
| AC-16 | Excluir esquemas de coordinación incompatibles | Base / P1 | Parcial | E07: catálogo y validación de alta por rol | Validación conjunta a nivel tenant de coordinadores combinados/separados; pruebas al crear, editar y cambiar de sede |
| AC-17 | Director de grupo solo como complemento de Docente | Base / P1 | Parcial | E07: catalogado como complemento | El alta aún usa rol principal; falta modelar y probar el complemento ligado al grupo y prohibir asignarlo sin docente |
| AC-18 | Permisos estructurales inmutables y configurables diferenciados | Base / P0 | Parcial | E07: matriz, overrides y controladores RBAC | Matriz de pruebas por celda estructural/configurable, plan y sede; no equiparar existencia del catálogo con protección de cada acción futura |
| AC-19 | Disponibilidad ≥99,5% en 30 días rodantes | Operación / P0 | Pendiente | E08: aplicación ejecutable local; no serie de medición operacional | Monitor externo, definición de ventana/exclusiones, alertas y 30 días de mediciones reales |
| AC-20 | Copia diaria por tenant y restore completo trimestral | Base / P0 | Parcial | E09: simulacro PostgreSQL con cifrado, integridad, archivo y alteración rechazada | Automatización, destino externo, claves, retención, WAL/snapshots para RPO, tenant completo y medición de RTO; el simulacro sintético no completa el AC |
| AC-21 | Protección de datos y atención de derechos | Base / P0 | Pendiente | E02/E04 son controles técnicos parciales | Consentimiento y propósito, retención/eliminación, solicitudes y evidencia de operación; requiere revisión especializada, no se declara cumplimiento legal por pruebas de código |
| AC-22 | Solo Plataforma cambia tipo de calendario A/B | Base / P1 | Parcial | E01, E05: configuración central y años basados en el calendario del tenant | Prueba HTTP de intento del Rector y restricciones por años activos/cerrados, incluida suplantación |
| AC-23 | Boletín aprobado/firmado antes de distribuir | Operación / P0 | Pendiente | E05: resultado con tipo `VISTA_PREVIA` | Versionado de emisión oficial, aprobación, firma, congelación y distribución; no publicar vista previa como documento oficial |
| AC-24 | Matriz UI coincide con autorización efectiva | Base / P0 | Parcial | E07/E10: permisos de transición y actualización Reverb | Recorrido por rol, plan y sede en toda acción implementada; etiquetar permisos de funciones futuras; no aceptar solo ocultar botones |
| AC-25 | Misma cobertura de consulta en móvil/escritorio | Operación / P1 | Parcial | E10/E11: navegación, institucional y perfil 320/390 px; horarios con filtros | Pruebas del portal completo del estudiante; queda registrada la regresión previa de copia de horario por toque móvil |
| AC-26 | Apoyo ve ficha/servicio limitado y observador autorizado | Ampliación / P2 | Pendiente | E07/E08: rol y permisos definidos, servicios sin flujo completo | Implementar servicio, expediente mínimo, privacidad y pruebas de cada perfil de apoyo |
| AC-27 | Cobros adicionales en cartera única por estudiante | Ampliación / P2 | Pendiente | E08: módulos de pagos/servicios sin integración | Ledger único, idempotencia, conciliación, devoluciones y prueba de no mezclar deudas de hermanos |
| AC-29 | Consentimiento granular versionado y bloqueante | Base / P0 | Pendiente | E08: ausencia de flujo integral de consentimiento en rutas implementadas | Registro de representante, versión, finalidades sin preselección, revocación y bloqueo backend del uso sensible |
| AC-30 | SIMAT/DANE validado con catálogos y aprobación Rector | Operación / P1 | Pendiente | E08: reporte oficial sin flujo completo | Catálogos oficiales versionados, validación bloqueante, aprobación y muestras de archivos aceptadas por el proceso oficial |

## Evidencia reproducible

Los vínculos de código suponen los tres repositorios vecinos dentro de `School_SASS`. Los nombres de prueba son localizables en los archivos citados. No se ejecutaron nuevamente todas las pruebas históricas de navegador.

| Ref. | Código / prueba | Resultado de este corte |
|---|---|---|
| E01 | [TenantProvisioner](../../../../colegio-saas-backend/app/Services/TenantProvisioner.php), [TenantProvisioningTest](../../../../colegio-saas-backend/tests/Feature/TenantProvisioningTest.php), [TenantOnboardingTest](../../../../colegio-saas-backend/tests/Feature/TenantOnboardingTest.php), [tenancy](../../../../colegio-saas-backend/config/tenancy.php) | Incluidos en suite backend; PostgreSQL por base configurado |
| E02 | [StoragePipelineTest](../../../../colegio-saas-backend/tests/Feature/StoragePipelineTest.php), [SecurityFlowsTest](../../../../colegio-saas-backend/tests/Feature/SecurityFlowsTest.php) | Incluidos en suite backend |
| E03 | [RealtimeHttpTest](../../../../colegio-saas-backend/tests/Feature/RealtimeHttpTest.php), [RealtimeSyncTest](../../../../colegio-saas-backend/tests/Feature/RealtimeSyncTest.php) | Incluidos en suite backend |
| E04 | [AuditLoggerTest](../../../../colegio-saas-backend/tests/Feature/AuditLoggerTest.php), [AuditRequests](../../../../colegio-saas-backend/app/Http/Middleware/AuditRequests.php) | Incluidos en suite backend; consulta de Plataforma, no Rector |
| E05 | [AcademicModulesTest](../../../../colegio-saas-backend/tests/Feature/AcademicModulesTest.php), [EvaluacionController](../../../../colegio-saas-backend/app/Http/Controllers/Api/Academico/EvaluacionController.php) | Incluidos en suite backend; especificaciones concretas en nombres de pruebas |
| E06 | [GradeCalculationServiceTest](../../../../colegio-saas-backend/tests/Unit/GradeCalculationServiceTest.php) | Incluido en suite backend |
| E07 | [PermissionMatrix](../../../../colegio-saas-backend/app/Rbac/PermissionMatrix.php), [UserController](../../../../colegio-saas-backend/app/Http/Controllers/Api/UserController.php), [RoleController](../../../../colegio-saas-backend/app/Http/Controllers/Api/RoleController.php) | Inspección de implementación; pendientes no cubiertos por prueba específica |
| E08 | [PrivateRoutes](../../../../colegio-saas-frontend/src/app/routing/PrivateRoutes.tsx), [tenant_academico](../../../../colegio-saas-backend/routes/tenant_academico.php), [api](../../../../colegio-saas-backend/routes/api.php) | Inspección de rutas reales y destinos de demostración/pendientes |
| E09 | [backup-restore-drill.php](../../../../colegio-saas-backend/tests/Support/backup-restore-drill.php), [[../../Logica del negocio/11-plataforma-y-operacion/procedimiento-respaldo-restauracion|procedimiento]] | Simulacro local correcto; dos registros, hash de archivo, rechazo por manipulación, limpieza |
| E10 | [browser-smoke.mjs](../../../../colegio-saas-frontend/scripts/browser-smoke.mjs), [WebSocketManager](../../../../colegio-saas-frontend/src/app/modules/auth/core/WebSocketManager.ts) | Institución y Reverb reejecutados correctamente; menú actualiza el plan, filtros se preservan, reconexión y permisos correctos; copia móvil pendiente del corte anterior |
| E11 | [ProfileMfaPolicyTest](../../../../colegio-saas-backend/tests/Feature/ProfileMfaPolicyTest.php), [AccountTest](../../../../colegio-saas-backend/tests/Feature/AccountTest.php), [Navbar](../../../../colegio-saas-frontend/src/_metronic/layout/components/header/Navbar.tsx), [AccountHeader](../../../../colegio-saas-frontend/src/app/modules/accounts/AccountHeader.tsx) | Perfil, política MFA y pruebas `browser-smoke.mjs --account` correctos; capturas locales revisadas en escritorio, 390 y 320 px |

## Entrega de perfil y MFA

| Comportamiento | Estado | Evidencia / límite |
|---|---|---|
| Nombre/correo/plan reales y acceso a ajustes desde menú | Verificado local | Datos de API, escape HTML y navegador; Reverb real con API aislada actualiza el plan sin F5. La prueba no modifica un plan comercial real |
| Guardar nombre/teléfono sin F5 y mantener identidad | Verificado local | `--account`, `AccountTest`; nombre y correo de estudiante protegidos también en API |
| Menú conserva secciones futuras sin datos ficticios | Verificado local | Proyectos, suscripción y estados de cuenta permanecen visibles; no hay contador de muestra ni preferencias que simulen guardar |
| MFA opcional sin bloqueo de navegación | Verificado local | Superadministrador y Rector entran sin MFA; sesiones limitadas anteriores se normalizan; el Rector sigue del cambio de contraseña a la configuración institucional. No se exige MFA al actor de una suplantación válida |
| Códigos de recuperación | Verificado local | Ocho valores aleatorios, hashes en reposo, consumo transaccional único; descarga/confirmación de guardado en UI |
| MFA activado voluntariamente | Verificado local | QR generado en el navegador, clave manual alternativa, confirmación TOTP; inicio de sesión exige código únicamente después de la activación; desactivación requiere contraseña y código |
| Recuperación asistida y renovación de autenticador | Pendiente | Falta asistencia auditada por pérdida total y renovación del autenticador |
| Verificación de correo / SSO | Pendiente / futuro | Cambiar correo lo deja sin verificar; vinculación Google no demuestra existencia de SSO |

## Ejecuciones de la entrega

| Verificación | Resultado |
|---|---|
| Backend: `php artisan test --compact` | 139 pruebas, 767 aserciones; correctas después de hacer MFA opcional |
| Frontend: `npm test` | 18 pruebas; correctas |
| Traducciones: `npm run check:i18n` | ES/EN completas; sin claves faltantes ni textos alternativos incrustados |
| Compilación TypeScript/Vite | Correcta |
| Navegador: `--account` | Dashboard accesible sin MFA, perfil sin F5, QR opcional, códigos de recuperación y restricciones estudiante; escritorio, 390 y 320 px |
| Navegador: `--institutional` | Flyout, rutas, enlaces anteriores y pantallas móviles correctos |
| Navegador: `--realtime` | Reverb real; plan, años, horarios, permisos y reconexión correctos con API aislada |
| Respaldo/restauración | Simulacro local correcto; alcance limitado descrito en E09 |
| Coherencia documental | 29 AC únicos y completos; 40 vínculos de los documentos nuevos resueltos |

No se ejecutó el modo completo de horarios en esta entrega: su prueba de copia móvil del corte anterior continúa pendiente. Tampoco se midieron disponibilidad, carga productiva ni recuperación de datos reales.

## Cómo actualizar esta matriz

1. Localizar el AC y la regla vigente antes de implementar; resolver contradicciones en `Logica del negocio`.
2. Incorporar evidencia de código y una prueba de éxito y rechazo relevante. Anotar entorno, resultado y límites.
3. Cambiar el estado solo si se cubre el criterio completo. Mantener lo pendiente, incluso cuando ya exista pantalla o permiso.
4. Para criterios operativos adjuntar ejecución real, fecha y mediciones. No sustituir RPO/RTO, disponibilidad o restore con pruebas unitarias.

Prioridades y decisiones: [[../../Logica del negocio/01-vision-y-alcance/corte-de-alcance-2026-09-29]].
