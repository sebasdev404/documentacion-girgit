---
titulo: Onboarding de usuarios
modulo: usuarios-roles-y-permisos
tipo: proceso
estado: borrador
tags: [onboarding, usuarios]
---

# Onboarding de usuarios

Flujos por los que entran al sistema los distintos tipos de usuario.

## Onboarding de un colegio nuevo (tenant)

1. El [[roles/00-superadministrador-plataforma|Superadministrador de la Plataforma]] crea el tenant manualmente desde el panel de administración global.
2. El sistema provisiona automáticamente:
   - Base de datos exclusiva del tenant.
   - Subdominio `<slug>.<dominio>`.
   - Usuario administrador inicial con contraseña temporal autogenerada.
3. El sistema envía al correo institucional del colegio un mensaje con la URL del subdominio y las credenciales del administrador.
4. El tenant queda en estado `Configurando` hasta que el administrador complete la configuración inicial.

## Onboarding del admin del colegio

1. El administrador (rector) recibe el correo con sus credenciales.
2. Ingresa al subdominio del colegio.
3. Cambia su contraseña temporal en el primer ingreso.
4. Completa la configuración inicial obligatoria (ver [[../03-multi-tenancy/configuracion-por-colegio|Configuración por colegio]]).
5. Una vez completada la configuración mínima, el tenant pasa a estado `Activo` y el resto de funcionalidades quedan disponibles.

## Onboarding masivo de docentes

1. El administrador del colegio (o la secretaría con permiso) crea docentes manualmente desde la administración de usuarios, **o** sube un archivo plantilla con los datos de varios docentes.
2. El sistema valida el archivo (formato, campos obligatorios, correos no duplicados dentro del tenant).
3. Cada docente se crea en estado `Pendiente` con contraseña temporal.
4. El sistema envía a cada docente un correo con sus credenciales y la URL del subdominio.
5. Cuando el docente ingresa por primera vez, cambia su contraseña y pasa a `Activo`.
6. Posteriormente, el coordinador académico crea las asignaciones (materia × grupo) del docente. Sin asignaciones el docente puede iniciar sesión pero no ve ningún grupo.

## Onboarding masivo de estudiantes

El onboarding de estudiantes ocurre, en la mayoría de casos, a través del [[../04-procesos-academicos/matriculas|proceso de matrícula]] que crea automáticamente la cuenta del estudiante al cierre del proceso.

Flujo alterno (carga masiva, ej. al migrar desde otro sistema):

1. El administrador o secretaría sube un archivo plantilla con datos de estudiantes ya inscritos.
2. El sistema valida formato y duplicados.
3. Cada estudiante se crea en estado `Pendiente`.
4. Los **datos de acudiente operativo** se cargan **dentro de la ficha del estudiante** (no como usuarios aparte; `RN-TU-410`).
5. Notificación por correo al **estudiante** con credenciales temporales; en la práctica el correo registrado suele ser el del acudiente operativo.

## Notificación al acudiente operativo

El acudiente **no tiene cuenta propia en la plataforma** (`RN-TU-410`). Las comunicaciones dirigidas "al acudiente" se enrutan a los datos de contacto registrados en la ficha del estudiante (correo, teléfono) y/o se entregan vía el portal usando la cuenta del estudiante. No existe un onboarding separado para acudientes.

## Reglas de negocio

- **RN-OB-001 — Configuración inicial obligatoria:** el tenant no es operable hasta que el administrador complete la configuración inicial mínima.
- **RN-OB-002 — Credenciales por correo:** todo usuario nuevo recibe sus credenciales temporales por el correo registrado al momento de su creación.
- **RN-OB-003 — Validación de duplicados en tenant:** dentro de un mismo tenant, el correo electrónico de un usuario es único.
- **RN-OB-004 — Carga masiva valida formato:** el sistema rechaza la carga masiva si hay errores de formato o validaciones básicas; ofrece reporte de líneas con error sin importar las correctas (transacción atómica).
- **RN-OB-005 — Estudiante creado al cierre de matrícula:** el estudiante se crea automáticamente al confirmar la matrícula y queda en lista de espera de asignación de grupo hasta que el coordinador académico le asigne uno.

## Notas y pendientes

- **[Decisión tomada]** **Formato de carga masiva**: soporta **CSV y Excel**. La plataforma provee una **plantilla descargable** con columnas fijas + columnas opcionales documentadas, y **valida cabeceras de forma estricta** antes de iniciar el procesamiento. Regla: **RN-OU-390 — CSV/Excel con plantilla y validación estricta de cabeceras**.
- **[Decisión tomada]** **Modo de carga masiva dual**:
  - **Transaccional (todo o nada)**: por defecto en procesos críticos que requieren integridad total (matrículas, planes de estudio).
  - **Tolerante**: opcional, procesa registros válidos y reporta errores por fila para que el usuario corrija solo los errados.
  Regla: **RN-OU-391 — Carga masiva dual transaccional/tolerante seleccionable por flujo y por usuario**.
