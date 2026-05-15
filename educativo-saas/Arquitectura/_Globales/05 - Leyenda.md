---
tags:
  - arquitectura
  - leyenda
aliases:
  - Leyenda
---

# Leyenda

Convenciones de simbolos para la matriz de permisos y otros documentos de arquitectura.

---

## Simbolos de la Matriz de Permisos

| Simbolo | Significado | Aplica a |
|---|---|---|
| CRUD | Permiso completo (Crear, Ver, Editar, Eliminar) | Roles con dominio total sobre el modulo |
| Crear | Solo crear nuevos registros | Roles operativos limitados |
| Ver | Solo consulta, sin modificar | Lectura |
| C | Comentar / agregar observaciones | Anotaciones, observador |
| E | Editar | Modificar registros existentes |
| Aprobar | Aprobar / firmar | Boletines, documentos, sanciones |
| Rechazar | Rechazar / devolver | Documentos sometidos a revision |
| Investigar | Iniciar proceso de revision | Casos disciplinarios |
| Reportar | Generar reporte / exportar | Reportes academicos, convivencia, financieros |
| Auto | Sistema lo ejecuta automaticamente | Acciones disparadas por triggers |
| Configurable | El colegio decide si lo permite o no | Permisos no estructurales |
| — | Sin permiso | El rol no puede ejecutar la accion |
| En pausa | Permiso definido pero no activo en MVP | Roles o features que se entregan despues |

---

## Prioridad de Requerimientos

| Codigo | Significado |
|---|---|
| Alta | Bloqueante. Sin esto el MVP no arranca |
| Media | Necesario en MVP pero no critico de salida |
| Baja | Mejora, puede ir en una segunda release |

---

## Estado de Requerimientos

| Codigo | Significado |
|---|---|
| Pendiente | No iniciado |
| En curso | En desarrollo |
| Bloqueado | Esperando dependencia (regla, decision, integracion) |
| Listo | Implementado y aprobado |

---

## Tipos de Requerimiento

| Prefijo | Tipo | Define |
|---|---|---|
| RF | Funcional | QUE hace el sistema |
| RNF | No Funcional | COMO lo hace |
| RR | de Negocio | POR QUE existe |
| RI | de Integracion | CON QUE conecta |

---

## Roles definidos en el documento

| ID | Rol | Carpeta de detalle |
|---|---|---|
| ROL-01 | Superadministrador de la Plataforma | `Arquitectura/00 - Superadministrador de la Plataforma/` |
| ROL-02 | Rector / Administrador del Colegio | `Arquitectura/01 - Rector/` |
| ROL-03 | Coordinador Academico | `Arquitectura/02 - Coordinador Academico/` |
| ROL-04 | Coordinador de Convivencia | `Arquitectura/03 - Coordinador de Convivencia/` |
| ROL-05 | Coordinador Academico y Convivencia | `Arquitectura/04 - Coordinador Academico y Convivencia/` |
| ROL-06 | Secretaria Academica | `Arquitectura/05 - Secretaria Academica/` |
| ROL-07 | Docente | `Arquitectura/06 - Docente/` |
| ROL-08 | Director de Grupo | `Arquitectura/07 - Director de Grupo/` |
| ROL-09 | Estudiante / Acudiente | `Arquitectura/08 - Estudiante y Acudiente/` |
| ROL-10 | Sistema | No tiene carpeta (no es persona) |
| ROL-11 | Administrador Tecnico | En pausa |
