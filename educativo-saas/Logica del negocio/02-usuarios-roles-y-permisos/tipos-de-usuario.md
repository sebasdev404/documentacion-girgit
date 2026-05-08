---
titulo: Tipos de usuario
modulo: usuarios-roles-y-permisos
tipo: referencia
estado: borrador
tags: [usuarios, tipos]
---

# Tipos de usuario

Catálogo de tipos de usuario que existen en el sistema. Cada tipo representa una clase de actor con distintas necesidades, scope y permisos.

> **Tipo vs rol:** un *tipo de usuario* describe quién es la persona en términos de su relación con el colegio (docente, estudiante, etc.). Un *rol* describe el conjunto de permisos asignados. En este sistema casi siempre coinciden 1 a 1 — la única excepción importante es que **estudiante y acudiente son tipos distintos pero comparten el mismo rol** (`Estudiante / Acudiente`), con scope diferente.

## Catálogo

| Tipo | Ámbito | Rol asignado | Origen del usuario |
| --- | --- | --- | --- |
| Superadministrador de la Plataforma | Global | [[roles/00-superadministrador-plataforma\|Superadmin]] | Equipo interno del SaaS |
| Rector / Administrador del Colegio | Tenant | [[roles/01-rector-administrador-colegio\|Rector]] | Personal directivo del colegio |
| Coordinador Académico | Tenant | [[roles/02-coordinador-academico\|Coord. Académico]] | Personal directivo del colegio |
| Coordinador de Convivencia | Tenant | [[roles/03-coordinador-convivencia\|Coord. de Convivencia]] | Personal directivo del colegio |
| Coordinador combinado (académico + convivencia) | Tenant | [[roles/04-coordinador-academico-y-convivencia\|Coord. combinado]] | Personal directivo del colegio |
| Secretaria Académica | Tenant | [[roles/05-secretaria-academica\|Secretaría]] | Personal administrativo del colegio |
| Docente | Tenant | [[roles/06-docente\|Docente]] (+ opcional [[roles/07-director-de-grupo\|Director de Grupo]]) | Profesores del colegio |
| Estudiante | Tenant | [[roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] (scope: sus propios datos) | Matrícula |
| Acudiente / Padre | Tenant | [[roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] (scope: datos del estudiante asociado) | Vinculación en matrícula |

## Distinciones clave

### Estudiante vs Acudiente
- Son tipos de usuario distintos.
- **Comparten el mismo rol** (`Estudiante / Acudiente`).
- El **scope** los diferencia: el estudiante ve sus propios datos; el acudiente ve los datos del / los estudiantes a los que está vinculado.
- Detalle en [[roles/08-estudiante-y-acudiente|Rol Estudiante / Acudiente]].

### Docente vs Director de Grupo
- Director de Grupo **no** es un tipo de usuario, ni un rol principal: es un **complemento** que se asigna a un docente sobre un grupo concreto.
- Una persona con tipo Docente puede o no tener este complemento, dependiendo de la decisión del Coordinador Académico.

### Coordinador combinado vs separado
- En colegios pequeños puede existir un único Coordinador que asume las dos funciones (académica y de convivencia).
- En ese caso, el tipo de usuario es "Coordinador combinado" y se le asigna el rol `Coord. combinado`.
- El sistema recomienda no mezclar ambos esquemas en el mismo tenant simultáneamente.

## Detalles por tipo

Cada tipo tiene su archivo de rol asociado con el detalle de permisos. Ver la subcarpeta [[roles/|`roles/`]].

## Notas y pendientes

- Definir si en algún colegio puede existir un tipo "Personal de apoyo" (psicólogo, enfermera, bibliotecario) y qué rol heredaría.
- Definir si un usuario puede tener simultáneamente cuentas como Docente del colegio y como Acudiente (caso real: profesor del colegio cuyo hijo estudia ahí).
