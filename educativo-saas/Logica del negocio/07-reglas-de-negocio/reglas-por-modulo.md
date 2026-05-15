---
titulo: Reglas por módulo
modulo: reglas-de-negocio
tipo: regla
estado: borrador
tags: [reglas, modulo]
---

# Reglas por módulo

Índice de reglas específicas agrupadas por módulo. El detalle de cada regla vive en la página del proceso correspondiente; aquí se concentra el listado para búsqueda y referencia rápida.

> **Convención:** `RN-XX-NNN`, donde `XX` es la abreviatura del submódulo.

## Usuarios y roles

Ver [[../02-usuarios-roles-y-permisos/reglas-transversales-de-roles|reglas transversales]] (RT-1 a RT-3) y reglas específicas en cada [[../02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma|página de rol]].

- Autenticación: ver [[../02-usuarios-roles-y-permisos/autenticacion]].
- Ciclo de vida del usuario: ver [[../02-usuarios-roles-y-permisos/ciclo-de-vida-de-usuario]].
- Onboarding: ver [[../02-usuarios-roles-y-permisos/onboarding-de-usuarios]].

## Multi-tenancy

Ver [[../03-multi-tenancy/modelo-de-tenants]], [[../03-multi-tenancy/aislamiento-de-datos]], [[../03-multi-tenancy/configuracion-por-colegio]] y [[../03-multi-tenancy/jerarquia-organizacional]].

## Procesos académicos

### Estructura

- Plan de estudios: `RN-PE-NNN`.
- Asignación de docentes: `RN-AD-NNN`.
- Horarios: `RN-HO-NNN`.
- Espacios físicos: `RN-EF-NNN`.
- Logros e indicadores: `RN-LI-NNN`.

### Matrículas

- Pre-matrícula y matrícula: `RN-MA-NNN` (ver [[../04-procesos-academicos/matriculas]]).

### Asistencia

- `RN-AS-NNN` (ver [[../04-procesos-academicos/asistencia]]).

### Calificaciones

- `RN-CA-NNN` (ver [[../04-procesos-academicos/calificaciones]]).
- Periodos: `RN-PR-NNN` (ver [[../04-procesos-academicos/periodos-academicos]]).
- Calendario escolar: `RN-CE-NNN` (ver [[../04-procesos-academicos/calendario-escolar]]).
- Boletines: `RN-BO-NNN` (ver [[../04-procesos-academicos/boletines-y-reportes-academicos]]).
- Nivelaciones y habilitaciones: `RN-NH-NNN`.
- Promoción y reprobación: `RN-PR-NNN` (ver [[../04-procesos-academicos/promocion-y-reprobacion]]).
- Consejo académico: `RN-CO-NNN`.

### Disciplina y observador

- Disciplina y observaciones: `RN-DI-NNN` (ver [[../04-procesos-academicos/disciplina-y-observaciones]]).
- Observador del estudiante: `RN-OE-NNN`.

## Comunicación

- Circulares y comunicados: `RN-CC-COM-NNN` (ver [[../05-comunicacion/circulares-y-comunicados]]).
- Comunicación con padres: `RN-CP-NNN`.
- Mensajería interna: `RN-MI-NNN`.
- Notificaciones: `RN-NO-NNN`.
- Agenda y publicaciones: `RN-AG-NNN`.

## Monetización y pagos

### Modelo y planes

- Modelo de negocio: `RN-MN-NNN`.
- Planes y suscripciones: `RN-PS-NNN`.

### Pagos y facturación

- Pagos de pensiones: `RN-PP-NNN`.
- Facturación y recibos: `RN-FR-NNN`.
- Pasarelas de pago: `RN-PA-NNN`.
- Descuentos y becas: `RN-DB-NNN`.
- Políticas de cobro y mora: `RN-CM-NNN`.
- Paz y salvo: `RN-PZ-NNN`.

## Plataforma y operación

- Log de auditoría: `RN-LA-NNN`.
- Backups y restauración: `RN-BR-NNN`.
- Almacenamiento y cuotas: `RN-AC-NNN`.
- Histórico y años cerrados: `RN-HA-NNN`.
- Gestión documental: `RN-GD-NNN`.

## Notas y pendientes

- **[Operativo]** Mantener este índice actualizado al agregar nuevas reglas en cualquier proceso. **Mantenimiento manual**.
- **[Decisión tomada]** **Sin generación automática del índice de reglas en MVP.** El índice se mantiene **manualmente**; la generación automática extrayendo `RN-XX-NNN` de cada archivo se evalúa como mejora de tooling de documentación posteriormente.
