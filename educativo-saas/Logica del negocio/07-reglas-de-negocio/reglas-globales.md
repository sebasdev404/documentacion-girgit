---
titulo: Reglas globales
modulo: reglas-de-negocio
tipo: regla
estado: borrador
tags: [reglas, globales]
---

# Reglas globales

Reglas que aplican transversalmente a todos los módulos del sistema, más allá de un proceso específico.

## Catálogo

| ID | Regla | Razón | Aplica a |
| --- | --- | --- | --- |
| RG-001 | Aislamiento estricto entre tenants. Ningún dato de un colegio es accesible desde otro. | Privacidad, cumplimiento legal, integridad operativa. | Multi-tenancy. |
| RG-002 | Toda acción relevante queda en el [[../11-plataforma-y-operacion/log-de-auditoria\|log de auditoría]]. | Trazabilidad, cumplimiento Habeas Data. | Todas las acciones de creación, edición y borrado. |
| RG-003 | El derecho a la educación no se bloquea por mora financiera: el estudiante mantiene acceso a sus notas, asistencia y observador. | Marco legal colombiano y ético. | Módulo financiero, módulo académico. |
| RG-004 | Las eliminaciones desde la aplicación son lógicas (soft-delete). El borrado físico ocurre tras la ventana de retención. | Recuperación ante errores humanos. | Todas las entidades con datos sensibles. |
| RG-005 | Los datos de un año lectivo cerrado son inmutables salvo reapertura formal. | Integridad académica. | Calificaciones, asistencia, observador, boletines. |
| RG-006 | La configuración se versiona por año lectivo. Cambios en el año vigente no afectan años cerrados. | Reimprimibilidad consistente. | Configuración académica. |
| RG-007 | Toda funcionalidad respeta la matriz de [[../02-usuarios-roles-y-permisos/matriz-de-permisos\|permisos]] del rol con el que el usuario actúa. | Seguridad y separación de funciones. | Todos los módulos. |
| RG-008 | Las contraseñas no se almacenan en texto plano; se usan algoritmos modernos (bcrypt / argon2). | Seguridad. | Módulo de autenticación. |
| RG-009 | Los archivos del tenant viven en su propio bucket; no se mezclan con archivos de otros colegios. | Aislamiento. | Módulo de almacenamiento. |
| RG-010 | Toda fecha y hora del sistema se almacena en UTC y se muestra en la zona horaria del colegio. | Consistencia y auditoría. | Todos los módulos. |
| RG-011 | Los identificadores expuestos al usuario no exponen secuencia interna; se usan UUID o códigos opacos. | Seguridad por oscuridad mínima. | APIs públicas. |
| RG-012 | El idioma por defecto es español; la plataforma debe permitir internacionalización. | Mercado objetivo y expansión. | Capa de presentación. |
| RG-013 | La moneda por defecto es la del país del colegio (COP en Colombia). Soporte futuro multi-moneda. | Modelo financiero. | Módulo monetario. |
| RG-014 | Las acciones críticas (eliminar registros, anular pagos, cerrar año) requieren confirmación explícita. | Prevención de errores irreversibles. | UI / UX. |
| RG-015 | Toda integración con terceros (pasarelas, correo, DIAN) usa credenciales por tenant cifradas en reposo. | Seguridad. | Módulo de integraciones. |
| RG-016 | El [[../02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma\|Superadmin]] solo accede a datos del tenant cuando es estrictamente necesario, con motivo registrado y notificando al administrador del colegio. | Privacidad del cliente. | Operación. |
| RG-017 | Las notificaciones críticas no son desactivables por el usuario. | Seguridad. | Módulo de notificaciones. |
| RG-018 | El sistema respeta el principio de menor privilegio: cada rol tiene solo los permisos mínimos necesarios. | Seguridad. | Modelo de roles. |

## Convención de identificadores

- `RG-NNN`: regla global (este archivo).
- `RT-N`: regla transversal de roles (ver [[../02-usuarios-roles-y-permisos/reglas-transversales-de-roles|Reglas transversales de roles]]).
- `RN-XX-NNN`: regla de módulo, donde `XX` es la abreviatura del módulo (CA = calificaciones, AS = asistencia, MA = matrícula, etc.).
- `CU-NNN`: caso de uso.

## Notas y pendientes

- Validar plan de internacionalización cuando se entre a un segundo país.
- Documentar el procedimiento de confirmación MFA para acciones críticas en el año 2.
