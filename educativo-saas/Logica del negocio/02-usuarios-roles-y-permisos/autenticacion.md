---
titulo: Autenticación
modulo: usuarios-roles-y-permisos
tipo: proceso
estado: borrador
tags: [autenticacion, login, seguridad]
---

# Autenticación

## Métodos de autenticación soportados

- **Usuario y contraseña** sobre el subdominio o dominio del colegio. Método principal en el lanzamiento.
- **SSO con Google / Microsoft** (futuro, plan premium): permite a un colegio habilitar inicio de sesión con cuentas corporativas de su dominio.
- **MFA opcional** activable por usuario o por el colegio para roles administrativos (futuro).

## Flujo de login

1. El usuario abre el portal del colegio en su subdominio (`<slug>.<dominio>`) o dominio propio.
2. El sistema resuelve el tenant a partir del host.
3. El usuario ingresa correo y contraseña.
4. El sistema valida las credenciales **contra el tenant resuelto**. Credenciales válidas en otro tenant **no funcionan**.
5. Si el usuario es nuevo (creado automáticamente al cierre de la matrícula o por el administrador), se le exige cambio de contraseña en el primer ingreso.
6. El sistema crea la sesión y redirige al portal correspondiente al rol del usuario.

## Recuperación de contraseña

1. El usuario solicita recuperación desde la pantalla de login indicando su correo.
2. El sistema envía al correo registrado en el tenant un enlace de recuperación con expiración corta (ej. 30 minutos).
3. El enlace solo es válido en el subdominio del tenant que lo emitió.
4. El usuario define una contraseña nueva que cumpla la política de complejidad.
5. La acción queda registrada en el log de auditoría.

## Sesiones y expiración

- Sesión activa con token de duración configurable por la plataforma (default 8 horas).
- Cierre automático de sesión por inactividad prolongada (default 30 minutos).
- El usuario puede cerrar sesión manualmente desde cualquier dispositivo y/o cerrar todas sus sesiones activas.
- El administrador del colegio puede forzar el cierre de sesiones de un usuario sospechoso.

## Multi-factor (MFA)

- MFA por TOTP (apps tipo Authenticator) disponible como opción en una fase posterior.
- El colegio puede exigir MFA obligatorio para roles administrativos (rector, coordinadores, secretaría).
- Recuperación de MFA: códigos de respaldo entregados al activar; en caso de pérdida total, intervención del administrador del colegio.

## Bloqueo por intentos fallidos

- Tras N intentos fallidos consecutivos (default 5), la cuenta se bloquea temporalmente por T minutos (default 15).
- Notificación automática al correo del usuario informando del bloqueo.
- El administrador del colegio puede desbloquear manualmente.

## Reglas de negocio

- **RN-AU-001 — Login por subdominio:** la autenticación está ligada al tenant resuelto por el subdominio. Credenciales de otro tenant **nunca** autentican.
- **RN-AU-002 — Cambio obligatorio de contraseña inicial:** todo usuario recién creado debe cambiar su contraseña temporal en el primer ingreso.
- **RN-AU-003 — Política de complejidad mínima:** la contraseña debe cumplir un mínimo de longitud y mezcla de caracteres definido por la plataforma.
- **RN-AU-004 — Bloqueo por intentos fallidos:** el sistema bloquea automáticamente cuentas tras intentos fallidos consecutivos.
- **RN-AU-005 — Sesión vinculada a tenant:** una sesión autenticada en un tenant no es válida en otro tenant; el cambio de tenant requiere nuevo login.
- **RN-AU-006 — Acceso al portal del estudiante deshabilitable:** el colegio puede desactivar completamente el portal del estudiante en su configuración.
- **RN-AU-007 — Auditoría de eventos de autenticación:** logins exitosos y fallidos, recuperaciones de contraseña, bloqueos y cambios de contraseña quedan registrados.

## Notas y pendientes

- Definir valor exacto de la política de complejidad mínima.
- Definir si el sistema soporta cuentas inactivas con caducidad automática.
