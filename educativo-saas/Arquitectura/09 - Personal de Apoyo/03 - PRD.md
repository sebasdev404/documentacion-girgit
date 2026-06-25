---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - prd
aliases:
  - PRD-11
  - PRD Personal de Apoyo
---

# PRD — Personal de Apoyo

| Campo | Valor |
|---|---|
| ID PRD | PRD-11 |
| HU | Como personal de apoyo quiero prestar el servicio de mi perfil y dejar constancia en el observador, consultando solo lo necesario del estudiante |
| Funcionalidad | Servicio no docente especializado por perfil (bienestar / salud / biblioteca) + aporte al observador |
| Actor | ROL-12 Personal de Apoyo |
| Dispositivo | Desktop / tablet (mostrador, enfermeria, consultorio) |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Habilitar a los funcionarios no docentes (orientador/psicologo, enfermeria, bibliotecario) para que presten su servicio con trazabilidad y dejen constancia en el observador del estudiante cuando corresponda, accediendo unicamente a una **ficha acotada** del estudiante y **sin** intervenir en lo academico, financiero ni en la configuracion del colegio. El rol opera con el conjunto de permisos mas acotado entre los roles internos (`RN-TU-001`).

## Flujo General

```
Rector crea cuenta + asigna PERFIL (RN-TU-003)
   -> Sistema habilita el modulo de servicio del perfil (RN-TU-004)
   -> Funcionario ubica la FICHA ACOTADA del estudiante (RN-TU-006)
   -> Presta el servicio en su modulo (atencion / cita / prestamo)
   -> Aporta al observador con visibilidad RN-OB-081 (default interna)
   -> Si excede su servicio: REMISION interna (no decide, RN-TU-010)
   -> Toda consulta y aporte queda en el log de auditoria (RN-TU-009)
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-48 | Consultar / aportar al observador (visibilidad `RN-OB-081`) | Alta |
| RF-43 | Comunicarse con el acudiente via portal (si el colegio lo habilita) | Media |
| RF-44 | Recibir notificaciones de remisiones, citas y vencimientos | Alta |
| CU-Apoyo-A | Registrar atencion en enfermeria y notificar al acudiente (perfil Salud, `RN-SA`) | Alta |
| CU-Apoyo-B | Abrir caso de bienestar y agendar cita (perfil Orientador, `RN-BW`) | Alta |
| CU-Apoyo-C | Registrar prestamo y devolucion en biblioteca (perfil Bibliotecario, `RN-BI`) | Alta |
| CU-011 | Registrar anotacion en el observador (ver `Logica del negocio/08-casos-de-uso/CU-011`) | Alta |

> Los modulos de servicio (Bienestar/Salud/Biblioteca) operan sobre las reglas `RN-BW`, `RN-SA` y `RN-BI` de Logica. Los RF formales de estos modulos se asignan de forma central en [[../_Globales/03 - Tabla de Requerimientos|Tabla de Requerimientos]]; aqui se referencian las reglas de negocio que los gobiernan.

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| `RN-TU-001` | Rol de permisos minimos | Conjunto de permisos mas acotado: ficha acotada + aporte al observador | Alta |
| `RN-TU-002` | Sin acceso a notas ni configuracion | Nunca accede a calificaciones, boletines, promocion ni a la config del tenant | Alta |
| `RN-TU-003` | Perfil obligatorio antes de activar | La cuenta requiere un perfil concreto definido por el Rector antes de quedar activa | Alta |
| `RN-TU-004` | Modulo de servicio segun perfil | Cada perfil solo accede a su propio modulo; ninguno ve el de otro | Alta |
| `RN-TU-005` | Aporte al observador con visibilidad `RN-OB-081` | Anotaciones con tres niveles; por defecto **interna** | Alta |
| `RN-TU-006` | Ficha acotada, no expediente completo | Identificacion, grupo, contacto del acudiente y alertas basicas | Alta |
| `RN-TU-007` | Incompatible con roles academicos/administrativos | No se combina con Docente, Director, Coordinador, Secretaria ni Rector | Media |
| `RN-TU-009` | Auditoria de consultas y aportes | Toda consulta de ficha y todo aporte quedan en el log | Alta |
| `RN-TU-010` | Remision, no decision | Ante casos que exceden su servicio remite; nunca decide sanciones ni promocion | Alta |
| `RN-OB-081` | Visibilidad por anotacion (publica/docentes/interna) | Define que ve cada audiencia del observador | Alta |
| RR-03 | Auditoria de acciones sensibles | Quien, que, cuando, IP; logs inmutables | Alta |
| RR-05 | Configurabilidad acotada de permisos | El colegio activa/desactiva permisos configurables; no crea nuevos | Media |
| RR-06 | Acceso solo por subdominio del colegio | Entra por el subdominio de su tenant | Alta |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Registrar / editar notas o boletines | Rol no academico (`RN-TU-002`) | Docente (ROL-07) / Coordinador |
| 2 | Acceder al expediente academico o consolidados | Solo ve ficha acotada (`RN-TU-006`) | Coordinador / Director de Grupo |
| 3 | Acceder a pagos / cartera del estudiante | Rol no financiero | Secretaria / Rector |
| 4 | Configurar el colegio (parametros del tenant) | Fuera de su alcance (`RN-TU-002`) | Rector (ROL-02) |
| 5 | Operar el modulo de un perfil ajeno | Aislamiento entre perfiles (`RN-TU-004`) | El perfil correspondiente |
| 6 | Decidir sanciones disciplinarias o promocion | Solo remite (`RN-TU-010`) | Coordinador de Convivencia / Consejo |
| 7 | Suministrar medicamento sin autorizacion vigente | Proteccion del menor (`RN-SA-003`) | — (requiere autorizacion del acudiente) |
| 8 | Compartir datos en remision externa sin consentimiento | Habeas Data (`RN-BW-005`) | — (requiere consentimiento del acudiente) |

## Dependencias

- Modulo de **Observador del estudiante** y su esquema de visibilidad `RN-OB-081`.
- Modulos de servicio segun perfil: Bienestar (`RN-BW`), Salud (`RN-SA`), Biblioteca (`RN-BI`).
- Modulo de **Notificaciones** para citas, remisiones y vencimientos sin exponer motivo sensible.
- Modulo de **Espacios fisicos** (consultorio, enfermeria, biblioteca como espacios del colegio).
- Log de auditoria del tenant.
- Ver [[../_Globales/09 - Dependencias|Dependencias]].
