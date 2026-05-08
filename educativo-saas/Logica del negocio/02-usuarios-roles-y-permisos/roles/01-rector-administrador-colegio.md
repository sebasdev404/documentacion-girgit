---
titulo: "Rol: Rector / Administrador del Colegio"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, rector, administrador, tenant]
---

# Rol: Rector / Administrador del Colegio

## Identificación

- **Nombre del rol:** Administrador del Colegio (típicamente el Rector, aunque puede ser otra figura directiva que asuma ese rol)
- **Tipo de usuario asociado:** Personal directivo del colegio
- **Ámbito:** Tenant (colegio)
- **Configurable por el colegio:** parcial — el colegio puede renombrar el rol, pero los permisos estructurales no se pueden quitar
- **Tipo:** principal

## Descripción

Es el actor con **mayor nivel de acceso dentro del tenant**. Puede hacer todo lo que hacen los demás roles internos del colegio. Es el responsable directo de la configuración inicial del colegio, de la creación de usuarios para los demás actores y del control de las reglas de negocio que el sistema permite ajustar.

## Responsabilidades

### Configuración institucional
- Definir nombre, logo, NIT, resolución del Ministerio de Educación Nacional y datos de contacto del colegio.
- Definir el calendario académico (Calendario A o B — la elección dentro de los habilitados por el Superadmin) y las fechas exactas de cada periodo lectivo.
- Configurar las jornadas escolares y los bloques horarios (ej. Jornada Mañana 6:30am–12:30pm, bloques de 55 minutos).
- Definir el modelo pedagógico por nivel educativo (docente único por salón vs. rotación, estudiantes desplazándose o no, existencia de directores de grupo).
- Configurar la escala valorativa (numérica con rango configurable, p. ej. 1.0–5.0; o por imágenes/caritas para preescolar, donde el colegio sube las imágenes y define cuántos niveles tiene la escala).
- Configurar el método de aprobación de materias (promedio, porcentajes ponderados o sumatoria dividida).
- Definir la nota mínima de aprobación.

### Gestión de usuarios y roles
- Gestionar los roles del colegio y sus permisos (dentro de los límites que el sistema permite).
- Crear usuarios para todos los actores internos (coordinadores, docentes, secretaría, estudiantes).
- Asignar y cambiar roles a los usuarios.

### Operación
- Acceso total a reportes, consolidados, boletines y configuraciones.
- Capacidad de hacer todo lo que cualquier otro rol del colegio hace, en caso de necesidad.

## Scope / alcance de visibilidad

- Ve **todos los datos del tenant**: estudiantes, docentes, notas, asistencia, observador, reportes, configuración.
- No tiene visibilidad de otros tenants (aislamiento total).

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Configurar identidad institucional | Nombre, logo, NIT, resolución MEN, contactos |
| Definir calendario académico y períodos | Dentro de los calendarios habilitados por el Superadmin |
| Configurar jornadas y bloques horarios | |
| Configurar escala valorativa | Numérica o por imágenes |
| Configurar método de aprobación y nota mínima | |
| Gestionar roles del tenant | Activar/desactivar permisos configurables, renombrar |
| Crear, editar y desactivar usuarios | De todos los roles del tenant |
| Acceso total a reportes y consolidados | |
| Acceso a logs de auditoría del tenant | |

## Permisos configurables por el colegio

Aunque el rector tiene poder total, el colegio puede decidir delegar algunas configuraciones a otros roles (típicamente al Coordinador Académico). Esa delegación se expresa quitando o agregando permisos al otro rol, no quitándoselos al Rector.

| Permiso delegable | A quién típicamente |
| --- | --- |
| Edición directa de notas | Coordinador Académico |
| Cierre de período académico | Coordinador Académico |
| Generación de constancias | Secretaría Académica |

## Permisos explícitamente NO otorgados

- No puede crear ni eliminar tenants (eso es del Superadmin).
- No puede cambiar el calendario A ↔ B si el Superadmin no lo habilita en el plan.
- No puede acceder a datos de otros colegios.

## Reglas de asignación

- Lo asigna el Superadministrador de la Plataforma cuando crea el tenant: el primer Rector es el contacto del colegio que recibe el acceso inicial.
- Posteriores cambios (ej. relevo de rector) los hace el rector saliente, o el Superadmin si el saliente no está disponible.
- **Mínimo 1, máximo configurable** por tenant. Default sugerido: 1 rector activo, opcional un segundo como respaldo.

## Compatibilidad con otros roles

- Un usuario con rol de Rector no necesita roles adicionales: ya cubre todo.
- No es típico, pero un Rector también podría dictar clase. En ese caso se sugiere crear una segunda cuenta con rol Docente para mantener la separación de auditoría.

## Variantes según configuración del colegio

- El colegio puede renombrar el rol (ej. "Director General", "Administrador Académico") sin que cambien los permisos.
- El colegio puede activar/desactivar permisos configurables a otros roles, pero los del Rector son fijos.

## Notas y pendientes

- Definir flujo formal para el relevo de Rector (handover de credenciales y trazabilidad).
- Definir si el Rector puede impersonar a otros roles del colegio para diagnóstico.
