---
tags:
  - arquitectura
  - indice
aliases:
  - Indice Arquitectura
  - MOC Arquitectura
---

# Indice — Arquitectura

Mapa de contenido (MOC) de la carpeta `Arquitectura/`. Para la fuente de verdad del negocio ver `Logica del negocio/`.

> Metodologia oficial documentada en [[../_GUIA - Metodologia de Arquitectura|Guia de Metodologia]]. Convenciones del proyecto en [[../CLAUDE|CLAUDE.md]].

---

## Globales

Documentos compartidos por todo el proyecto.

- [[_Globales/01 - Portada|01 - Portada]] — indice de roles y datos del proyecto
- [[_Globales/02 - PRD - Plataforma|02 - PRD - Plataforma]] — Product Requirements Document general
- [[_Globales/03 - Tabla de Requerimientos|03 - Tabla de Requerimientos]] — todos los RF/RNF/RR/RI
- [[_Globales/04 - Por Modulo|04 - Por Modulo]] — RFs agrupados por modulo del sidebar
- [[_Globales/05 - Leyenda|05 - Leyenda]] — simbolos de la matriz y convenciones
- [[_Globales/06 - Matriz de Permisos|06 - Matriz de Permisos]] — rol x accion
- [[_Globales/07 - Reglas de Negocio|07 - Reglas de Negocio]] — RR-NN consolidadas
- [[_Globales/08 - Criterios de Aceptacion|08 - Criterios de Aceptacion]] — AC-NN verificables
- [[_Globales/09 - Dependencias|09 - Dependencias]] — internas, externas, catalogos, semaforos

---

## Roles (orden jerarquico)

Cada rol tiene 12 archivos numerados (00 a 11) + subcarpeta `Casos de Uso/`. Los archivos prellenados con contenido derivado de Logica del negocio son: 01 (Ficha), 04 (Permisos), 05 (Requerimientos), 06 (Resumen). Los demas estan como esqueleto.

### ROL-01 Superadministrador de la Plataforma

- [[00 - Superadministrador de la Plataforma/01 - Ficha de Rol|Ficha de Rol]]
- [[00 - Superadministrador de la Plataforma/04 - Permisos Detallados|Permisos Detallados]]
- [[00 - Superadministrador de la Plataforma/05 - Requerimientos|Requerimientos]]
- [[00 - Superadministrador de la Plataforma/06 - Resumen Rapido|Resumen Rapido]]

### ROL-02 Rector

- [[01 - Rector/01 - Ficha de Rol|Ficha de Rol]]
- [[01 - Rector/04 - Permisos Detallados|Permisos Detallados]]
- [[01 - Rector/05 - Requerimientos|Requerimientos]]
- [[01 - Rector/06 - Resumen Rapido|Resumen Rapido]]

### ROL-03 Coordinador Academico

- [[02 - Coordinador Academico/01 - Ficha de Rol|Ficha de Rol]]
- [[02 - Coordinador Academico/04 - Permisos Detallados|Permisos Detallados]]
- [[02 - Coordinador Academico/05 - Requerimientos|Requerimientos]]
- [[02 - Coordinador Academico/06 - Resumen Rapido|Resumen Rapido]]

### ROL-04 Coordinador de Convivencia

- [[03 - Coordinador de Convivencia/01 - Ficha de Rol|Ficha de Rol]]
- [[03 - Coordinador de Convivencia/04 - Permisos Detallados|Permisos Detallados]]
- [[03 - Coordinador de Convivencia/05 - Requerimientos|Requerimientos]]
- [[03 - Coordinador de Convivencia/06 - Resumen Rapido|Resumen Rapido]]

### ROL-05 Coordinador Academico y Convivencia (combinado)

- [[04 - Coordinador Academico y Convivencia/01 - Ficha de Rol|Ficha de Rol]]
- [[04 - Coordinador Academico y Convivencia/04 - Permisos Detallados|Permisos Detallados]]
- [[04 - Coordinador Academico y Convivencia/05 - Requerimientos|Requerimientos]]
- [[04 - Coordinador Academico y Convivencia/06 - Resumen Rapido|Resumen Rapido]]

### ROL-06 Secretaria Academica

- [[05 - Secretaria Academica/01 - Ficha de Rol|Ficha de Rol]]
- [[05 - Secretaria Academica/04 - Permisos Detallados|Permisos Detallados]]
- [[05 - Secretaria Academica/05 - Requerimientos|Requerimientos]]
- [[05 - Secretaria Academica/06 - Resumen Rapido|Resumen Rapido]]

### ROL-07 Docente

- [[06 - Docente/01 - Ficha de Rol|Ficha de Rol]]
- [[06 - Docente/04 - Permisos Detallados|Permisos Detallados]]
- [[06 - Docente/05 - Requerimientos|Requerimientos]]
- [[06 - Docente/06 - Resumen Rapido|Resumen Rapido]]

### ROL-08 Director de Grupo (complemento)

- [[07 - Director de Grupo/01 - Ficha de Rol|Ficha de Rol]]
- [[07 - Director de Grupo/04 - Permisos Detallados|Permisos Detallados]]
- [[07 - Director de Grupo/05 - Requerimientos|Requerimientos]]
- [[07 - Director de Grupo/06 - Resumen Rapido|Resumen Rapido]]

### ROL-09 Estudiante / Acudiente

- [[08 - Estudiante y Acudiente/01 - Ficha de Rol|Ficha de Rol]]
- [[08 - Estudiante y Acudiente/04 - Permisos Detallados|Permisos Detallados]]
- [[08 - Estudiante y Acudiente/05 - Requerimientos|Requerimientos]]
- [[08 - Estudiante y Acudiente/06 - Resumen Rapido|Resumen Rapido]]

---

## Archivos por rol pendientes de llenar (esqueleto)

Cada carpeta de rol tiene tambien estos archivos como esqueleto (frontmatter + heading). Requieren decisiones de UX antes de prellenar:

- `00 - Arquitectura [Rol].md` — **wireframe principal** del rol
- `02 - Ficha Detallada.md` — ficha extendida tipo Sheet
- `03 - PRD.md` — PRD por rol
- `07 - Feature Map.md` — mapa de features
- `08 - Acciones del Usuario.md` — tabla accion -> resultado
- `09 - Campos del Formulario.md` — campos de los formularios del rol
- `10 - Validaciones.md` — validaciones por campo / flujo
- `11 - Respuestas del Sistema.md` — eventos y respuesta del sistema
- `Casos de Uso/` — subcarpeta para casos de uso narrativos por RF
