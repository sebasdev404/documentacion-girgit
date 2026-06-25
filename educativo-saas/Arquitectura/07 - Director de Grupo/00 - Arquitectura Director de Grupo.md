---
tags:
  - arquitectura
  - rol/director-de-grupo
aliases:
  - Arquitectura ROL-08
  - Wireframe Director de Grupo
---

# Arquitectura — Director de Grupo

Wireframe principal del rol. Es el documento mas visual y referenciado del complemento ROL-08.

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/07-director-de-grupo.md`.
> El Director de Grupo es un **complemento** del Docente (ROL-07), no un rol principal. Toda la interfaz del Docente sigue presente; este wireframe describe lo que se **suma** sobre el grupo dirigido.

---

## N0 — Inicio (login del colegio)

El Director de Grupo entra por el subdominio de SU colegio (RR-06), igual que cualquier usuario del tenant. No tiene URL ni login distinto al de Docente: el complemento se detecta tras autenticar.

```
[ colegio.plataforma.com ]
        |
        v
  Login (correo + contrasena) + MFA si el colegio lo exige
        |
        +--- credenciales invalidas --> mensaje generico + registro en log
        |
        v
  El sistema detecta: ROL-07 (Docente) + complemento ROL-08 (Director de Grupo)
        |
        v
  Dashboard del docente con bloque destacado "Mi grupo dirigido"
```

- El tenant_id se infiere del subdominio antes de validar credenciales (RR-06).
- Si la persona es directora de mas de un grupo, el dashboard muestra un selector de grupo dirigido.
- Toda accion sensible sobre el grupo (observador, boletin, citacion) queda en el log del tenant (RR-03).

---

## HEADER (presente en toda la app)

```
[ Logo Colegio ]   [ Buscador (estudiantes de mi grupo / mis materias) ]      [ Mi grupo: 5B v ]  [ Perfil ]  [ Notificaciones ]
```

- **Perfil del usuario:** datos del docente-director, materias asignadas, grupo(s) dirigido(s), cerrar sesion, configurar MFA.
- **Buscador:** acotado a estudiantes del grupo dirigido y a estudiantes de sus materias asignadas (RR-10). No busca fuera de su scope.
- **Selector de grupo dirigido:** visible solo si dirige mas de un grupo; conmuta el contexto de toda la pantalla.
- **Notificaciones:** boletines por cerrar, anotaciones que requieren confirmacion, citaciones respondidas por acudientes, casos de convivencia de su grupo, alertas tempranas (inasistencia / bajo rendimiento).

---

## N1 — SIDEBAR (modulos del rol)

```
+---------------------------------+
|  Inicio (Mi grupo dirigido)     |
|  Mi horario                     |
|  Notas (mis materias)           |
|  Asistencia                     |
|  Consolidado del grupo          |   <- adicional del complemento
|  Boletines del grupo            |   <- adicional del complemento
|  Observador del grupo           |   <- adicional del complemento
|  Convivencia (Ley 1620)         |   <- adicional del complemento
|  Citaciones y acudientes        |   <- configurable
|  Comunicacion con acudientes    |   <- configurable
|  Bienestar y alertas            |
+---------------------------------+
```

Los modulos **Notas (mis materias)**, **Asistencia (mis clases)**, **Observador academico** y **Mi horario** son los del rol Docente (ROL-07). Los modulos marcados como adicionales solo aparecen porque la persona es Directora de este grupo (RR-09): en cualquier otro grupo no los ve.

El Director de Grupo NO ve modulos de Configuracion del Colegio, Usuarios y Roles, Documentos Oficiales ni Matricula: esos pertenecen al Rector y a la Secretaria.

---

## Detalle por modulo

### Inicio — Mi grupo dirigido

Vista de entrada del director. Tarjetas resumen del grupo dirigido:
- Estudiantes del grupo (total, activos, retirados del periodo).
- Estado del periodo academico (abierto / en cierre / cerrado).
- Boletines pendientes de generar o de observacion general.
- Alertas del grupo: inasistencia acumulada, materias en rojo, casos de convivencia abiertos.

> Callout informativo: el dashboard es de solo lectura; las acciones se hacen en cada modulo. Si dirige varios grupos, el bloque cambia con el selector del header.

### Mi horario

- Horario propio como Docente (RR-10): solo materias y grupos asignados.
- Resaltado del bloque que corresponde al grupo dirigido cuando aplica.
- Solo lectura. No construye horarios (eso es del Coordinador Academico).

### Notas (mis materias)

Identico al Docente (ROL-07). El complemento NO cambia este modulo.
- Registrar / editar notas dentro del periodo abierto (RR-07), solo en materias asignadas.
- Editar despues del cierre: configurable (RF-17, RR-07).
- **Como se usa:** el director sigue calificando sus propias materias aqui, igual que cualquier docente. Para ver notas de las materias que NO dicta usa el modulo Consolidado del grupo.

### Asistencia

Identico al Docente sobre sus clases. Como complemento se agrega:
- **Consultar asistencia del grupo dirigido** completa (todas las materias), no solo sus clases (RF-23).
- Vista de inasistencia acumulada por estudiante con semaforo de alerta.

### Consolidado del grupo (adicional del complemento)

- **Sub-vistas:** consolidado por periodo / consolidado acumulado del ano.
- **Filtros:** periodo, materia, estado de aprobacion, estudiante.
- **Detalle:** todas las materias del grupo dirigido con sus notas, no solo las que el director dicta (RF-18).
- **Acciones:** ver, descargar consolidado en PDF, ordenar por promedio.
- Callout importante: el director **ve** todas las notas del grupo, pero solo **edita** las de sus propias materias. Editar notas que no dicta es configurable y por defecto esta desactivado (RR-09, ver Matriz).

**Como se usa este modulo:** antes del cierre de periodo el director revisa el consolidado completo para detectar estudiantes en riesgo, preparar la entrega de boletines y conversar con docentes de las materias en rojo. (Ver RF-18.)

### Boletines del grupo (adicional del complemento)

- **Sub-vistas:** lista de estudiantes del grupo / boletin individual.
- **Acciones:** Generar boletin del grupo (RF-38) · Agregar observacion general por estudiante (RF-40) · Descargar PDF · (Aprobar/firmar: configurable, RF-39).
- Callout warning: el boletin se genera sobre las notas cerradas del periodo. Si hay notas sin registrar, el sistema lo advierte y lista los faltantes.

**Como se usa este modulo:** al cerrar el periodo el director genera los boletines del grupo, redacta una observacion general por estudiante (fortalezas, compromisos) y los entrega. La firma final puede quedar en el director, en el Coordinador Academico o en el Rector segun la politica del colegio (RF-39, ver Matriz). (Ver [[Casos de Uso/RF-38 Generar boletin del grupo dirigido|CU RF-38]].)

### Observador del grupo (adicional del complemento)

- **Sub-vistas:** observador disciplinario del grupo / por estudiante.
- **Filtros:** estudiante, tipo de anotacion, periodo, estado (abierta / confirmada por acudiente).
- **Acciones:** Registrar anotacion en el observador del grupo dirigido (RF-25) · Adjuntar evidencia · Solicitar confirmacion del acudiente.
- Callout importante: las anotaciones del observador respetan la visibilidad configurada por anotacion (`RN-OB-081`). El director anota sobre estudiantes de SU grupo; sobre otros estudiantes no puede (RR-09).

**Como se usa este modulo:** cuando ocurre una situacion con un estudiante del grupo, el director registra la anotacion, la clasifica segun la tipologia del colegio y, si corresponde, la articula con un caso de convivencia. (Ver [[Casos de Uso/RF-25 Anotacion en observador del grupo|CU RF-25]].)

### Convivencia (Ley 1620) (adicional del complemento)

- **Sub-vistas:** situaciones reportadas de mi grupo / seguimiento de acuerdos.
- **Acciones del director (segun la ley):**
  - **Reportar** una situacion de convivencia de su grupo (cualquier tipo I/II/III).
  - **Aplicar medidas pedagogicas inmediatas** en situaciones **tipo I**, en el aula (`RN-CVE-003`).
  - **Acompanar** al estudiante y **ejecutar acuerdos de seguimiento** definidos por el comite.
- Callout warning: el director NO clasifica el tipo (eso es del Coordinador de Convivencia) ni decide tipo III (eso es del Rector). Si detecta un presunto delito, marca "presunto delito" y el sistema escala de inmediato al Rector y restringe la visibilidad del caso (`RN-CVE-004`).
- Fuente: `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md`.

**Como se usa este modulo:** ante un conflicto en el aula el director lo resuelve como tipo I (medida pedagogica) y lo deja registrado; si la situacion es mas grave la reporta para que el Coordinador de Convivencia la clasifique y active la Ruta de Atencion Integral. Luego hace el seguimiento de los acuerdos firmados.

### Citaciones y acudientes (configurable)

- **Acciones:** Citar formalmente a un acudiente del grupo (configurable por colegio) · Ver respuesta del acudiente · Registrar asistencia a la citacion.
- Callout importante: citar formalmente puede ser potestad exclusiva del Coordinador de Convivencia. Si el colegio no le activa este permiso, el director solo puede **solicitar** la citacion al coordinador, no emitirla (ver Matriz, fila Citaciones).

### Comunicacion con acudientes (configurable)

- Mensajeria con los acudientes de los estudiantes del grupo via portal (configurable).
- Plantillas de comunicado (recordatorio de entrega de boletines, citacion, felicitacion).
- Callout informativo: la comunicacion queda registrada; el acudiente opera la cuenta del Estudiante (RR-11), no existe cuenta de acudiente independiente.

### Bienestar y alertas

- **Alertas tempranas** del grupo: cruce de asistencia + notas + observador que marca estudiantes en riesgo (`RN-VA-101`).
- Visibilidad de **remisiones a orientacion escolar** de estudiantes de su grupo (solo lo que le corresponde como acompanante, sin el detalle psicosocial reservado).
- Enlace de consulta a servicios de bienestar (salud/enfermeria, restaurante) solo a nivel de alerta del grupo, sin gestion.
- Fuente: `Logica del negocio/12-bienestar-y-servicios/bienestar-y-orientacion.md`.

---

## Diferencias clave vs otros roles

| Aspecto | Docente (ROL-07) | Director de Grupo (ROL-08) | Coord. Convivencia (ROL-04) |
| --- | --- | --- | --- |
| Notas que ve | Solo sus materias | Sus materias + consolidado completo del grupo dirigido | Las que configure el colegio |
| Notas que edita | Sus materias | Sus materias (las que no dicta: configurable) | Configurable |
| Observador disciplinario | No anota | Anota sobre estudiantes del grupo dirigido | Anota sobre cualquier estudiante |
| Boletines | No genera | Genera y observa el grupo dirigido | No (los del coordinador academico) |
| Convivencia Ley 1620 | Reporta tipo I del aula | Reporta + medidas tipo I + seguimiento del grupo | Clasifica I/II/III y activa la RAI |
| Citaciones formales | No | Configurable (solo su grupo) | Si, sobre cualquier estudiante |
| Ambito | Sus materias/grupos | + Su grupo dirigido (RR-09) | Todo el colegio (convivencia) |

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo |  Buscador grupo/materias   | Mi grupo:5B v | Perfil | Notif|
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                               |
|        |                                                          |
| Inicio |  [ Mi grupo dirigido: tarjetas resumen + alertas ]       |
| Horario|                                                          |
| Notas  |  [ Notas de mis materias (igual que Docente) ]           |
| Asist. |  [ Asistencia: mis clases + consulta del grupo ]         |
| Consol.|  [ Consolidado completo del grupo dirigido (solo ver) ]  |
| Boletin|  [ Generar boletin + observacion general por estud. ]    |
| Observ.|  [ Observador disciplinario del grupo dirigido ]         |
| Conviv.|  [ Reportar situacion + medidas tipo I + seguimiento ]   |
| Citac. |  [ Citaciones (configurable) ]                           |
| Comunic|  [ Mensajes a acudientes del grupo (configurable) ]      |
| Bienest|  [ Alertas tempranas del grupo ]                         |
+--------+---------------------------------------------------------+
```

---

## Relacionado

- [[01 - Ficha de Rol]]
- [[02 - Ficha Detallada]]
- [[03 - PRD]]
- [[04 - Permisos Detallados]]
- [[05 - Requerimientos]]
- [[06 - Resumen Rapido]]
- [[07 - Feature Map]]
- [[08 - Acciones del Usuario]]
- Rol base: [[../06 - Docente/00 - Arquitectura Docente|Arquitectura Docente (ROL-07)]]
- [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/07-director-de-grupo.md`
- Convivencia: `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md`
