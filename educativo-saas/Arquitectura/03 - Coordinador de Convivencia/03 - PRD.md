---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
  - prd
aliases:
  - PRD-05
  - PRD Coord. Convivencia
---

# PRD — Coordinador de Convivencia

| Campo | Valor |
|---|---|
| ID PRD | PRD-05 |
| HU | Como Coordinador de Convivencia quiero registrar y dar seguimiento al comportamiento y a los casos de convivencia de cualquier estudiante para mantener un historial trazable y cumplir la Ley 1620 |
| Funcionalidad | Gestion de la convivencia escolar dentro del tenant |
| Actor | ROL-04 Coordinador de Convivencia |
| Dispositivo | Desktop (principal); mobile para anotaciones rapidas |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Permitir que el Coordinador de Convivencia mantenga un registro completo y oportuno del comportamiento de los estudiantes del colegio, gestione el observador del estudiante, clasifique y opere los casos del Sistema Nacional de Convivencia Escolar (Ley 1620) respetando plazos y protocolos, y produzca reportes consolidados con trazabilidad total, sin participar en la operacion academica de notas.

## Flujo General

```
Situacion reportada (docente / director de grupo / coordinador)
   -> Registrar anotacion en observador (tipo + visibilidad)
   -> Si aplica Ley 1620: clasificar caso (tipo I/II/III) -> instanciar protocolo
   -> Ejecutar actuaciones (escuchar partes, atencion en salud, citacion a acudiente)
   -> Tipo II/III: convocar Comite Escolar -> generar acta
   -> Tipo III: escalar al Rector -> registrar reporte a autoridad
   -> Registrar acuerdos/compromisos (alimentan el observador)
   -> Seguimiento -> Cierre del caso -> Reporte consolidado de convivencia
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-26 | Registrar anotacion en observador de cualquier estudiante | Alta |
| RF-27 | Definir tipologias de anotacion | Media |
| RF-28 | Citar formalmente a acudientes (configurable) | Media |
| RF-29 | Generar reportes de convivencia | Media |
| CU-1620 | Clasificar y operar un caso de convivencia (ver `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md`) | Alta |

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| RR-01 | Aislamiento total entre tenants | Solo ve el observador y los casos de su colegio | Alta |
| RR-03 | Auditoria de acciones sensibles | Anotaciones, clasificaciones, reclasificaciones, actas y reportes quedan en log inmutable | Alta |
| RR-04 | Asignacion de roles por el Rector | El rol lo asigna ROL-02; un usuario tiene un solo rol principal | Alta |
| RR-05 | Configurabilidad acotada de permisos | Citaciones, sanciones, comunicados y acceso a notas son configurables; lo estructural no se desactiva | Media |
| RR-06 | Acceso por subdominio del colegio | Entra por el subdominio de su tenant, no por URL de plataforma | Alta |
| RR-12 | Coord. combinado excluye los separados | ROL-04 no coexiste con ROL-05 en el mismo tenant | Alta |
| RN-OB-081 | Visibilidad por anotacion (3 niveles) | Cada anotacion se crea como publica / docentes / interna | Alta |
| RN-OE-003 | Anulacion preserva historial | Anular no borra; conserva la anotacion como anulada con justificacion | Alta |
| RN-CVE-002 | Clasificacion obligatoria y auditada | Todo caso se clasifica en tipo I/II/III antes de avanzar | Alta |
| RN-CVE-004 | Tipo III escala al Rector y exige reporte | No se cierra sin constancia de reporte a la autoridad competente | Alta |
| RN-CVE-005 | Atencion en salud prioritaria | Dano al cuerpo: remision a EPS/urgencias bloquea el cierre | Alta |
| RN-CVE-006 | Acta firmada para tipo II y III | El acta es inmutable una vez firmada por el Rector | Media |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Registrar / editar notas academicas | No es su ambito (salvo configuracion que unifique coordinaciones) | Docente (ROL-07) |
| 2 | Gestionar plan de estudios u horarios | Es del Coordinador Academico | Coord. Academico (ROL-03) |
| 3 | Emitir documentos oficiales (constancias, certificados, paz y salvos) | Responsabilidad de Secretaria | Secretaria Academica (ROL-06) |
| 4 | Firmar actas del Comite Escolar de Convivencia | El Comite lo preside y firma el Rector | Rector (ROL-02) |
| 5 | Reportar un caso tipo III a la autoridad competente | El reporte legal lo activa el Rector | Rector (ROL-02) |
| 6 | Acceder al expediente clinico completo de bienestar | Informacion sensible reservada a orientacion | Personal de Apoyo (ROL-09) |
| 7 | Acceder a datos de otros tenants | Aislamiento (RR-01) | Solo soporte via impersonacion auditada (ROL-01) |

## Dependencias

- Modulo de Observador del estudiante (`Logica del negocio/04-procesos-academicos/observador-del-estudiante.md`).
- Modulo de Convivencia Ley 1620 (`Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md`).
- Modulo de Comunicaciones / notificaciones para citaciones.
- Gestion documental para actas y acuerdos firmados (sujeto a cuota del tenant).
- Articulacion con Bienestar / Orientacion (ROL-09) para remisiones.
- Ver [[../_Globales/09 - Dependencias|Dependencias]].
