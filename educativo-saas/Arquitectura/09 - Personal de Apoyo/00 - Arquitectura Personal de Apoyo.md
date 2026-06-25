---
tags:
  - arquitectura
  - rol/personal-de-apoyo
aliases:
  - Arquitectura ROL-12
  - Wireframe Personal de Apoyo
---

# Arquitectura — Personal de Apoyo

Wireframe principal del rol. Es el documento mas visual y referenciado del rol ROL-12 (Personal de Apoyo).

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo.md` y los modulos de servicio en `Logica del negocio/12-bienestar-y-servicios/` (bienestar, salud, biblioteca).

> Rol transversal de **bajo privilegio** (`RN-TU-001`). Su nucleo comun es: consultar la **ficha acotada** del estudiante y **aportar al observador** con la visibilidad de `RN-OB-081`. El sidebar **se especializa por perfil**: orientador, enfermeria o bibliotecario. **No accede a notas, boletines, cartera ni a la configuracion del colegio** (`RN-TU-002`).

---

## N0 — Inicio (login del tenant)

El Personal de Apoyo entra por el **subdominio del colegio** (RR-06), igual que el resto de usuarios del tenant. No tiene acceso de plataforma.

```
[ micolegio.plataforma.com ]
        |
        v
  Login (correo + contrasena + MFA si el colegio lo exige)
        |
        +--- credenciales invalidas --> mensaje generico + registro en log
        |
        +--- cuenta sin perfil asignado --> acceso bloqueado (RN-TU-003)
        |
        v
  Home del servicio (segun perfil: bienestar / salud / biblioteca)
```

- El tenant_id se infiere del subdominio antes de validar credenciales (RR-06).
- Una cuenta de Personal de Apoyo **debe tener un perfil concreto** definido por el Rector antes de quedar activa (`RN-TU-003`); sin perfil no se habilita ningun modulo de servicio.
- Todo intento de login (exito/fallo) queda en el log de auditoria del tenant.

---

## HEADER (presente en toda la app)

```
[ Logo Colegio ]   [ Buscar estudiante (ficha acotada) ]      [ Mi agenda ]  [ Perfil ]  [ Notificaciones ]
```

- **Perfil del usuario:** datos del funcionario, perfil asignado (orientador / enfermeria / bibliotecario), cerrar sesion.
- **Buscador:** localiza al estudiante por nombre, documento o grupo y abre **solo su ficha acotada** (identificacion, grupo, contacto del acudiente, alertas basicas — `RN-TU-006`). No expone notas ni cartera.
- **Mi agenda:** bandeja propia del servicio (citas, atenciones o prestamos a cargo).
- **Notificaciones:** remisiones internas dirigidas a su servicio, recordatorios de cita, vencimientos de prestamo, confirmaciones de lectura del acudiente. Nunca exponen el motivo sensible (`RN-BW-006`).

---

## N1 — SIDEBAR (modulos del rol)

El sidebar **depende del perfil** que el Rector asigno a la cuenta. Todos los perfiles comparten el **nucleo comun**; cada uno suma su **modulo de servicio**.

```
+-------------------------------+      Nucleo comun (todos los perfiles)
|  Inicio del servicio          |
|  Buscar estudiante (ficha)    |
|  Aportes al observador        |
|  Mi agenda / bandeja          |
+-------------------------------+
        +  (solo el modulo del perfil asignado, RN-TU-004)
+-------------------------------+      Perfil ORIENTADOR / PSICOLOGO
|  Bienestar y orientacion      |        RN-BW
+-------------------------------+
+-------------------------------+      Perfil ENFERMERIA
|  Salud y enfermeria           |        RN-SA
+-------------------------------+
+-------------------------------+      Perfil BIBLIOTECARIO
|  Biblioteca                   |        RN-BI
+-------------------------------+
```

El Personal de Apoyo **NO** tiene en su sidebar: Notas/Consolidados, Asistencia, Documentos oficiales, Boletines, Configuracion del colegio, Pagos/Cartera. Esos modulos no aparecen para este rol (`RN-TU-002`).

> Callout importante: un perfil **solo ve su propio modulo de servicio**. La enfermera no ve el expediente de bienestar y viceversa (`RN-TU-004`).

---

## Detalle por modulo

### Inicio del servicio (nucleo comun)

Vista de entrada. Tarjetas resumen acotadas al servicio del funcionario:
- Citas / atenciones / prestamos del dia.
- Remisiones internas pendientes dirigidas a su servicio.
- Alertas basicas de los estudiantes que atendio recientemente.

> Callout informativo: el inicio es de solo lectura; las acciones se ejecutan en cada modulo. No muestra indicadores academicos ni financieros.

### Buscar estudiante — Ficha acotada (nucleo comun)

- **Sub-vistas:** resultado de busqueda / ficha acotada del estudiante.
- **Filtros:** por nombre, documento o grupo.
- **Detalle (ficha acotada, `RN-TU-006`):** identificacion, foto, grupo, datos de contacto del acudiente, alertas basicas (y alertas tempranas `RN-VA-101` solo si el colegio activo esa visibilidad para el rol).
- **Acciones:** Abrir ficha · Ver aportes propios al observador · Iniciar atencion/cita/prestamo en su modulo · Generar remision interna.
- Callout warning: la ficha **no** incluye notas, boletines, promedios ni estado de cartera. Toda apertura de ficha queda auditada (`RN-TU-009`).

**Como se usa este modulo:** ante una situacion con un estudiante, el funcionario lo ubica por nombre, documento o grupo, abre su ficha acotada para confirmar identidad, grupo y contacto del acudiente, y desde ahi inicia la atencion en su modulo de servicio. Si el caso excede su servicio, genera una **remision interna** (a coordinacion o a otro perfil).

### Aportes al observador (nucleo comun)

- **Sub-vistas:** lista de mis aportes / nuevo aporte.
- **Detalle:** anotacion con tipo, descripcion y **nivel de visibilidad** (`RN-OB-081`): publica / docentes / interna. Por defecto **interna** (`RN-TU-005`).
- **Acciones:** Crear aporte · Editar aporte propio (por anotacion, sin borrar el original) · Elegir visibilidad.
- Callout importante: el rol **aporta**, no decide. Nunca define sanciones, promocion ni medidas academicas (`RN-TU-010`). En el observador ve solo las anotaciones cuyo nivel `RN-OB-081` se lo permita.

**Como se usa este modulo:** cuando un hecho debe quedar en el seguimiento del estudiante, el funcionario crea una anotacion en el observador y elige su nivel de visibilidad; por la sensibilidad del dato, el sistema preselecciona **interna**. (Ver [[Casos de Uso/RF-48 Consultar y aportar al observador|CU RF-48]] y CU-011 de Logica del negocio.)

### Mi agenda / bandeja (nucleo comun)

- Citas, atenciones o prestamos a cargo del funcionario.
- Estados del servicio (solicitada/confirmada/realizada; abierta/remitida/cerrada; activo/vencido/devuelto, segun el perfil).
- Recordatorios y confirmaciones de lectura del acudiente.

### Bienestar y orientacion (perfil Orientador / Psicologo — `RN-BW`)

- **Sub-vistas:** mis casos / expediente de bienestar del estudiante / agenda de citas.
- **Filtros:** estado del caso (abierto / en seguimiento / remitido / cerrado), tipo de atencion, fecha.
- **Detalle:** expediente unico por estudiante, transversal al ano (`RN-BW-001`): citas, notas de seguimiento, planes de acompanamiento, remisiones.
- **Acciones:** Abrir/ubicar expediente · Agendar cita · Registrar nota de seguimiento · Definir plan de acompanamiento (parte visible + parte interna, `RN-BW-008`) · Generar remision interna o externa · Cerrar caso con resumen.
- Callout warning: la informacion sensible **no alimenta el boletin** (`RN-BW-003`). Las remisiones externas exigen **consentimiento del acudiente** registrado (`RN-BW-005`). La notificacion de cita nunca revela el motivo clinico (`RN-BW-006`).

**Como se usa este modulo:** un caso se abre por solicitud del estudiante/acudiente, por remision interna o por una alerta de riesgo (`RN-VA-101`). El orientador ubica el expediente, agenda la cita, registra la atencion en nivel **interna**, y si procede arma un plan o remite. El cierre exige resumen y preserva el historial (`RN-BW-009`).

### Salud y enfermeria (perfil Enfermeria — `RN-SA`)

- **Sub-vistas:** atenciones del dia / ficha medica del estudiante / control de vacunas.
- **Filtros:** estado de atencion (abierta / en observacion / remitida / cerrada), severidad.
- **Detalle:** ficha medica (EPS, tipo de sangre, alergias, condiciones cronicas, medicamentos autorizados, contactos de emergencia, restricciones). La diligencia el acudiente (`RN-SA-001`); el rol la **consulta y registra atenciones**.
- **Acciones:** Identificar estudiante · Registrar atencion (motivo, signos, disposicion) · Suministrar medicamento **solo con autorizacion vigente** (`RN-SA-003`) · Generar remision a centro medico · Actualizar estado de vacunacion.
- Callout warning: todo evento de salud **notifica al acudiente** (`RN-SA-005`); los graves notifican de inmediato y escalan al segundo contacto. La remision a centro medico notifica tambien al Coordinador de Convivencia (`RN-SA-006`) y no se cierra sin desenlace.

**Como se usa este modulo:** el estudiante llega a enfermeria; el sistema carga su ficha con alertas activas; la enfermera registra la atencion, suministra medicamento solo si hay autorizacion vigente, define la disposicion (regreso a clase, reposo, llamado al acudiente o remision) y, si es relevante, aporta al observador en nivel interna (`RN-SA-008`).

### Biblioteca (perfil Bibliotecario — `RN-BI`)

- **Sub-vistas:** mostrador (prestamo/devolucion) / catalogo y ejemplares / reservas / multas / inventario.
- **Filtros:** estado del ejemplar (disponible / prestado / reservado / en reparacion / baja / extraviado), usuario, vencimiento.
- **Detalle:** material (titulo, autor, ISBN, CDU, ubicacion) y ejemplar (codigo de barras, estado).
- **Acciones:** Catalogar material · Registrar prestamo sobre **ejemplar concreto** (`RN-BI-001`) · Registrar devolucion · Generar multa por mora/dano/extravio · Gestionar cola de reservas · Conciliar inventario.
- Callout importante: el vencimiento se calcula por configuracion del colegio (`RN-BI-002`), no a mano. Si el colegio activo la integracion a cartera, una multa pendiente puede afectar el **paz y salvo** (`RN-BI-007`). El bloqueo por morosidad es configurable (`RN-BI-004`).

**Como se usa este modulo:** el usuario solicita un material; el sistema valida cupo, morosidad y disponibilidad; el bibliotecario registra el prestamo sobre un ejemplar y el sistema calcula el vencimiento. En la devolucion, si hay retraso o dano genera la multa segun politica y libera el ejemplar para la siguiente reserva en cola (`RN-BI-008`).

### Remisiones internas (transversal a los perfiles)

- Derivacion a coordinacion (academica o de convivencia) o a otro perfil de servicio.
- El rol **remite, no decide** (`RN-TU-010`): nunca aplica sanciones, promocion ni medidas academicas.
- La notificacion de la remision no expone el motivo sensible.

---

## Diferencias clave vs otros roles

| Aspecto | Personal de Apoyo (ROL-12) | Docente (ROL-07) | Coordinador de Convivencia (ROL-04) |
| --- | --- | --- | --- |
| Naturaleza | Servicio no docente, bajo privilegio | Academico | Academico/administrativo |
| Vista del estudiante | Ficha **acotada** (`RN-TU-006`) | Sus grupos y materias | Expediente y observador completos |
| Notas / boletines | Sin acceso (`RN-TU-002`) | Registra notas de su materia | Aprueba/edita segun permiso |
| Observador | **Aporta** con visibilidad `RN-OB-081` | Observacion academica de su materia | Registra y decide; tipologias |
| Modulo propio | Bienestar / Salud / Biblioteca (segun perfil) | Clase y notas | Convivencia (Ley 1620) |
| Decisiones disciplinarias / academicas | No (solo remite) | No | Si |
| Configuracion del colegio | Sin acceso | Sin acceso | Sin acceso |
| Combinable con otro rol | No (`RN-TU-007`) | Si (Director de Grupo) | Segun esquema del tenant |

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo |  Buscar estudiante (ficha) | Mi agenda | Perfil | Notif    |
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                               |
|        |                                                          |
| Inicio |  [ Inicio del servicio: citas/atenciones/prestamos hoy ] |
| Buscar |  [ Ficha acotada del estudiante + alertas basicas ]      |
| Observ.|  [ Mis aportes al observador (visibilidad RN-OB-081) ]   |
| Agenda |  [ Mi bandeja del servicio ]                             |
|  - - - |                                                          |
| Modulo |  [ Solo el del perfil asignado: ]                        |
|  perfil|     Bienestar  |  Salud y enfermeria  |  Biblioteca      |
+--------+---------------------------------------------------------+
   (Sin Notas, Asistencia, Documentos, Boletines, Config, Cartera)
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
- [[09 - Campos del Formulario]]
- [[10 - Validaciones]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo.md`
- Modulos de servicio: `Logica del negocio/12-bienestar-y-servicios/bienestar-y-orientacion.md`, `.../salud-y-enfermeria.md`, `.../biblioteca.md`
