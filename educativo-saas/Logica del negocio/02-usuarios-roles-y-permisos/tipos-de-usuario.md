---
titulo: Tipos de usuario
modulo: usuarios-roles-y-permisos
tipo: referencia
estado: borrador
tags: [usuarios, tipos]
---

# Tipos de usuario

Catálogo de tipos de usuario que existen en el sistema. Cada tipo representa una clase de actor con distintas necesidades, scope y permisos.

> **Tipo vs rol:** un *tipo de usuario* describe quién es la persona en términos de su relación con el colegio (docente, estudiante, etc.). Un *rol* describe el conjunto de permisos asignados. En este sistema tipos y roles coinciden 1 a 1.

> **Aclaración estructural (`RN-TU-410`):** el **acudiente / padre de familia NO es un tipo de usuario** y no figura en este catálogo. El menor tiene una única cuenta —la del **estudiante**— y el acudiente la opera de hecho. Los datos del acudiente se registran como información de contacto del estudiante, sin credenciales ni perfil propios.

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
| Estudiante | Tenant | [[roles/08-estudiante-y-acudiente\|Estudiante]] | Matrícula |

## Distinciones clave

### Estudiante y acudiente operativo
- Existe **un único tipo de usuario para el menor: Estudiante** (`RN-TU-410`).
- El acudiente **no es usuario**: opera la cuenta del estudiante de hecho. Sus datos viven dentro de la ficha del estudiante.
- Detalle del rol y de su alcance en [[roles/08-estudiante-y-acudiente|Rol Estudiante]].

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

- **[Decisión estructural confirmada]** **El "acudiente" / "padre de familia" NO es un tipo de usuario.** El estudiante posee la cuenta y, en la práctica, el acudiente la usa para gestionar pagos, recibir comunicados y consultar información del menor. **Toda referencia a "acudiente como rol" en el resto del vault debe interpretarse como "usuario del estudiante"** y revisarse durante el repaso final del vault. Regla: **RN-TU-410 — Sin rol "acudiente" como usuario; el estudiante posee la única cuenta del menor**.
- **[Decisión tomada]** **Rol "Personal de apoyo"**: incorporado como tipo de usuario para psicólogo, enfermera, bibliotecario u otros perfiles no docentes con interacción académica. Permisos **limitados y configurables**: consulta acotada del expediente y aporte al **observador** del estudiante con visibilidad según `RN-OB-081`. Regla: **RN-TU-411 — Rol "Personal de apoyo" con permisos mínimos de consulta + aporte al observador**.
- **[Caso resuelto por la decisión estructural]** Docente cuyo hijo estudia en el mismo colegio: como **no existe el rol acudiente**, el hijo tiene su propia **cuenta de estudiante** y el docente la administra **de facto** fuera del sistema. No hay "doble rol" que modelar.
