# Registro de entregas y decisiones hasta el 30 de septiembre de 2026

Este registro reúne el trabajo en las ramas `pedro-dev` del frontend y backend. No reemplaza la [matriz de verificación](11%20-%20Matriz%20de%20Verificacion.md) ni declara completos criterios que esa matriz mantiene parciales o pendientes.

| Módulo | Trabajo entregado | Límite |
|---|---|---|
| Provisionamiento y bienvenida | Colegio multitenant, contraseña temporal obligatoria, logo adaptable e información institucional previa al año. | Ensayo integral en PostgreSQL de staging pendiente. |
| Identidad, perfil y menú | Nombre, correo y plan reales; edición personal; secciones del menú conservadas; ajustes institucionales; MFA voluntario con QR/TOTP y recuperación. | Recuperación asistida de MFA pendiente. |
| Ciclo académico | Año lectivo, períodos por fechas y transición manual con permisos; sedes, jornadas, niveles, grados, grupos, bloques y espacios. | Inmaculada 2026 es demostración local. |
| Plan, horarios y SIEE | Áreas, materias, asignación, grupo obligatorio en horarios y filtros persistentes; currículo por grado, área derivada y peso editable. | Revisar reglas y carga real. |
| Evaluación y catálogos | Filtros y paginación desde servidor: hasta 20 filas completas; por encima de 20, tamaño inicial 20 y opciones 5 a 1000. | Mantener permisos y filtros en módulos nuevos. |
| Tiempo real | Reverb, actualización selectiva, filtros conservados y reconexión. | Procesos supervisados en despliegue. |
| Seguridad API | Cookies HttpOnly, CSRF, limpieza de almacenamiento sensible, selectores públicos y pruebas de aislamiento. | [Estado de sesión y selectores](11%20-%20Pendiente%20de%20seguridad%20de%20sesion%20web.md). |
| Archivos y operación | Permiso de carga, escaneo que falla cerrado, descargas firmadas, simulacro aislado de restauración y actualización de dependencias. | ClamAV real y respaldos externos antes de producción. |

La secuencia de commits y pruebas específicas está en cada repositorio. Las próximas entregas deben actualizar este registro y la matriz, distinguiendo verificación local de aptitud para producción.

## Adenda: ingreso estudiantil y correo — 7 de octubre de 2026

Matrículas por enlace, correo/PIN, requisitos configurables, archivos privados/versionados, correcciones, decisión, cuenta estudiantil y asignación de grupos. Sin pagos ni usuarios de acudiente. Permisos `ingreso.*` bajo `academico`. Guía y configuración Gmail en Ajustes institucionales, permiso exclusivo del rector `config.correo`, contraseña de aplicación cifrada por tenant y prueba antes de guardar. Incluye notificaciones de matrícula y recuperación de contraseña.

Validación local: pruebas API, cliente, build, recorrido de navegador con fixtures y migraciones PostgreSQL ensayadas en base nueva/restaurada, con respaldos. Detalle vigente, límites y procedimiento en [[../../Logica del negocio/04-procesos-academicos/matriculas]] y los runbooks `docs/INGRESO_ESTUDIANTIL.md` de backend/frontend. No se da por terminado el módulo futuro de admisiones/entrevistas ni se desplegó VPS.

### 8 de octubre: aprobación central de cambios de correo

Conexión guardada bloqueada, solicitud motivada, bandeja/notificación de Superadmin y aprobación de un uso/24 horas. Sin delegación por RBAC; también protege desconexión y posterior reconexión. Menú del usuario incorpora «Conexión de correo electrónico». Migración conserva bytes cifrados de la credencial real y datos académicos. Se verificó Inmaculada con un mensaje SMTP real al remitente ya guardado, aceptado por Google; no se alteraron credenciales ni se crearon solicitudes ficticias de aprobación. La revisión de recepción/spam sigue a cargo del titular del buzón.
