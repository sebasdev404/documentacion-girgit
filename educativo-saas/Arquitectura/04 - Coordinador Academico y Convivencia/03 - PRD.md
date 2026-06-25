---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - rol/coord-combinado
  - prd
aliases:
  - PRD-06
  - PRD Coord. Combinado
---

# PRD — Coordinador Academico y Convivencia

| Campo | Valor |
|---|---|
| ID PRD | PRD-06 |
| HU | Como coordinador combinado quiero gestionar la estructura academica y el seguimiento de convivencia de mi colegio desde un solo perfil |
| Funcionalidad | Coordinacion academica operativa + convivencia escolar (Ley 1620) dentro de un tenant |
| Actor | ROL-05 Coordinador Academico y de Convivencia (combinado) |
| Dispositivo | Desktop (portal del colegio por subdominio) |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Permitir que un unico rol cubra tanto la gestion academica operativa (plan de estudios, grupos, asignacion docente, horarios, consolidados, cierre y nivelaciones) como el seguimiento de convivencia (observador, tipologias, casos Ley 1620, citaciones y reportes), en colegios que no tienen el equipo para separar las dos coordinaciones, sin acceder a la configuracion base del sistema ni a los documentos oficiales.

## Flujo General

```
Inicio de ano -> Plan de estudios -> Grupos + asignacion docente -> Horarios
   -> Operacion del periodo (consolidados) -> Cierre de periodo -> Nivelaciones (auto)
   -> Aprobacion de boletines (si configurado)
   |
   +--> Seguimiento de convivencia: observador -> reporte de caso -> clasificar I/II/III
        -> activar RAI -> citar acudientes -> Comite -> acuerdos -> seguimiento -> cierre
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-11 | Gestionar plan de estudios | Alta |
| RF-12 | Crear y gestionar grupos | Alta |
| RF-13 | Asignar docentes a materias y grupos | Alta |
| RF-14 | Designar director de grupo | Alta |
| RF-15 | Construir horarios de clase | Alta |
| RF-18 | Ver consolidados de notas por grupo | Alta |
| RF-19 | Ver consolidado de todos los grupos | Media |
| RF-20 | Cierre de periodo academico | Alta |
| RF-21 | Gestion de nivelaciones y habilitaciones | Media |
| RF-17 | Editar notas despues del cierre (si configurado) | Media |
| RF-39 | Aprobar / firmar boletines (si configurado) | Alta |
| RF-26 | Registrar anotacion en observador de cualquier estudiante | Alta |
| RF-27 | Definir tipologias de anotacion | Media |
| RF-28 | Citar formalmente a acudientes | Media |
| RF-29 | Generar reportes de convivencia | Media |

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| RR-01 | Aislamiento total entre tenants | Solo ve datos de su propio colegio | Alta |
| RR-03 | Auditoria de acciones sensibles | Notas, cierre, observador, clasificacion y citaciones quedan en el log | Alta |
| RR-04 | Asignacion de roles por el Rector | El Rector le otorga el rol combinado | Alta |
| RR-05 | Configurabilidad acotada de permisos | Hereda los configurables de ROL-03 y ROL-04; no crea permisos nuevos | Media |
| RR-06 | Acceso por subdominio | Entra por el subdominio del colegio, no por URL de plataforma | Alta |
| RR-07 | Notas dentro del periodo abierto | Editar tras el cierre exige permiso configurable + justificacion | Alta |
| RR-09 | Director de Grupo solo opera sobre su grupo | El coordinador designa al director; sus permisos extra aplican solo a ese grupo | Media |
| RR-10 | Docente ve solo lo asignado | El docente solo ve los grupos y materias que el coordinador le asigna | Media |
| RR-12 | Combinado excluye separados | Si el tenant activa ROL-05 no usa ROL-03 + ROL-04 a la vez | Alta |
| RN-OB-081 | Visibilidad por anotacion | Cada anotacion del observador se marca publica / docentes / interna | Media |
| RN-CVE-002 | Clasificacion obligatoria y auditada | Todo caso se clasifica I/II/III antes de avanzar; reclasificable con justificacion | Alta |
| RN-CVE-004 | Tipo III escala al Rector | El caso tipo III escala automaticamente y no cierra sin reporte a la autoridad | Alta |
| RN-NH-002 | Solo el docente titular registra la nivelacion | El coordinador supervisa, no registra la nota de recuperacion | Media |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Modificar la configuracion base (escala valorativa, jornadas, calendario, modelo pedagogico) | Es configuracion estructural del tenant | Rector (ROL-02) |
| 2 | Emitir documentos oficiales (constancias, certificados, paz y salvos) | Responsabilidad de matricula / secretaria | Secretaria (ROL-06) |
| 3 | Reportar a SIMAT | Tramite oficial de matricula | Secretaria (ROL-06) |
| 4 | Registrar la nota de una nivelacion / habilitacion | La registra el docente titular de la materia x grupo | Docente (ROL-07) |
| 5 | Cerrar un caso de convivencia tipo III sin reporte | Exige constancia de reporte a la autoridad (RN-CVE-004) | El Rector preside y reporta |
| 6 | Enviar comunicados a todo el colegio | Comunicacion institucional masiva | Rector (ROL-02) |
| 7 | Acceder al expediente clinico de bienestar | Informacion sensible de orientacion | Personal de Apoyo / Orientador (ROL-09) |
| 8 | Acceder a datos de otro tenant | Aislamiento total (RR-01) | Nadie (salvo Superadmin auditado) |

## Dependencias

- Configuracion base del tenant ya definida por el Rector (escala, calendario, jornadas, periodos).
- Catalogo de areas del conocimiento y de tipologias de anotacion.
- Modulo de log de auditoria del tenant (RR-03).
- Modulo de convivencia Ley 1620 y observador del estudiante.
- Ver [[../_Globales/09 - Dependencias|Dependencias]].
