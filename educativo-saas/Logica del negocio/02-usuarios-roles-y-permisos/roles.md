---
titulo: Roles
modulo: usuarios-roles-y-permisos
tipo: referencia
estado: borrador
tags: [roles, autorizacion, moc]
---

# Roles

Un rol es un **conjunto de permisos** asignable a un usuario. Cada rol está documentado en su propio archivo dentro de la subcarpeta [[roles/|`roles/`]], siguiendo la plantilla [[../_plantillas/plantilla-rol|`plantilla-rol.md`]].

## Roles definidos (orden jerárquico)

| # | Rol | Ámbito | Tipo | Archivo |
| --- | --- | --- | --- | --- |
| 00 | Superadministrador de la Plataforma | Global | Principal | [[roles/00-superadministrador-plataforma\|00-superadministrador-plataforma.md]] |
| 01 | Rector / Administrador del Colegio | Tenant | Principal | [[roles/01-rector-administrador-colegio\|01-rector-administrador-colegio.md]] |
| 02 | Coordinador Académico | Tenant | Principal | [[roles/02-coordinador-academico\|02-coordinador-academico.md]] |
| 03 | Coordinador de Convivencia | Tenant | Principal | [[roles/03-coordinador-convivencia\|03-coordinador-convivencia.md]] |
| 04 | Coordinador combinado (académico + convivencia) | Tenant | Principal | [[roles/04-coordinador-academico-y-convivencia\|04-coordinador-academico-y-convivencia.md]] |
| 05 | Secretaría Académica | Tenant | Principal | [[roles/05-secretaria-academica\|05-secretaria-academica.md]] |
| 06 | Docente | Tenant | Principal | [[roles/06-docente\|06-docente.md]] |
| 07 | Director de Grupo | Tenant | Complemento | [[roles/07-director-de-grupo\|07-director-de-grupo.md]] |
| 08 | Estudiante | Tenant | Principal | [[roles/08-estudiante-y-acudiente\|08-estudiante-y-acudiente.md]] |

## Reglas de asignación

Las reglas que aplican a todos los roles están consolidadas en [[reglas-transversales-de-roles|Reglas transversales de roles]]. En resumen:

- Un usuario tiene **un solo rol principal** dentro del tenant.
- Se permiten **complementos** sobre el rol principal sin cambiar el rol base. El complemento estandarizado es `Director de Grupo` sobre un Docente.
- Los roles se asignan dentro del tenant por el Rector. El rol del Rector lo entrega el Superadmin al crear el tenant.
- El Superadministrador es el único rol global y se asigna fuera del flujo del tenant.

## Roles compuestos / heredados

| Rol | Composición |
| --- | --- |
| Coordinador combinado | Permisos del Coord. Académico + Coord. de Convivencia |
| Docente + Director de Grupo | Permisos del Docente + permisos extra sobre un grupo dirigido |

## Permisos: matriz general

La matriz cruzada rol × acción se mantiene en [[matriz-de-permisos|matriz-de-permisos.md]].

## Ámbitos

```
Plataforma (global, fuera de cualquier tenant)
└── Superadministrador de la Plataforma

Tenant (dentro del colegio)
├── Rector / Administrador del Colegio
├── Coordinador Académico    ┐
├── Coordinador de Convivencia ┤── (mutuamente excluyentes con el combinado)
├── Coordinador combinado    ┘
├── Secretaría Académica
├── Docente
│   └── + Director de Grupo (complemento)
└── Estudiante (solo consulta; cuenta operada por el acudiente según `RN-TU-410`)
```

## Notas y pendientes

- Documentar qué pasa cuando se elimina un rol con usuarios activos asignados.
- Definir si es posible tener "roles personalizados" que el colegio cree desde cero, o solo se permiten los del catálogo.
