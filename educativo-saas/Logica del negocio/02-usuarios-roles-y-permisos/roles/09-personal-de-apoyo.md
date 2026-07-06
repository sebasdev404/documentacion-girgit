---
titulo: "Rol: Personal de apoyo"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, personal-de-apoyo, psicologo, enfermera, bibliotecario, tenant]
---

# Rol: Personal de apoyo

> **Origen (`D-04`, `RN-TU-411`):** rol formalizado para perfiles **no docentes** que sí interactúan con el estudiante —psicólogo / orientador, enfermería, bibliotecario y otros perfiles de servicio—. Es un rol de **permisos mínimos y configurables**: consulta acotada del expediente del estudiante y **aporte al observador** con la visibilidad de `RN-OB-081`. En `Arquitectura/` corresponde a **ROL-12 / PRD-11**.

## Identificación

- **Nombre del rol:** Personal de apoyo
- **Tipo de usuario asociado:** Funcionario no docente con interacción directa con el estudiante (orientador / psicólogo, enfermería, bibliotecario, otros perfiles de servicio)
- **Ámbito:** Tenant (colegio)
- **Configurable por el colegio:** sí — el colegio define el **perfil concreto** y qué módulo de servicio habilita; los permisos base de consulta son fijos
- **Tipo:** principal (no es complemento; no se combina con Docente ni Coordinador)

## Descripción

Rol **transversal de bajo privilegio** para funcionarios que acompañan al estudiante desde un servicio específico, sin dictar clase ni administrar el colegio. Su comportamiento se **especializa por perfil**: el orientador trabaja sobre [[../../12-bienestar-y-servicios/bienestar-y-orientacion|Bienestar y orientación]], la enfermera sobre [[../../12-bienestar-y-servicios/salud-y-enfermeria|Salud y enfermería]] y el bibliotecario sobre [[../../12-bienestar-y-servicios/biblioteca|Biblioteca]]. En todos los casos comparte un mismo **núcleo de permisos**: ve una ficha acotada del estudiante y puede **aportar anotaciones al observador**. **No accede a notas ni a la configuración del colegio.**

## Perfiles concretos

| Perfil | Módulo de servicio | Prefijo RN |
| --- | --- | --- |
| Orientador / Psicólogo | [[../../12-bienestar-y-servicios/bienestar-y-orientacion\|Bienestar y orientación]] | `RN-BW` |
| Enfermería | [[../../12-bienestar-y-servicios/salud-y-enfermeria\|Salud y enfermería]] | `RN-SA` |
| Bibliotecario | [[../../12-bienestar-y-servicios/biblioteca\|Biblioteca]] | `RN-BI` |
| Otros perfiles de servicio | Sin módulo dedicado; solo núcleo de consulta + aporte al observador | — |

El colegio asocia cada cuenta a **un perfil**, que determina qué módulo de servicio se le habilita además del núcleo común.

## Responsabilidades

- Consultar la **ficha acotada** del estudiante (identificación, grupo, contacto del acudiente, alertas básicas) para prestar el servicio.
- **Aportar anotaciones al observador** del estudiante con la visibilidad de `RN-OB-081`.
- Operar el **módulo de servicio** propio de su perfil (registrar atenciones de salud, notas de bienestar o préstamos de biblioteca, según corresponda).
- Reportar al **Rector** o a la **coordinación** que el colegio defina como su línea de supervisión.

## Scope / alcance de visibilidad

- Ve **únicamente** la ficha acotada del estudiante necesaria para su servicio: identificación, grupo, datos de contacto del acudiente y alertas básicas.
- **No** ve notas, boletines ni promedios; **no** ve consolidados académicos del grupo.
- En el observador ve sólo las anotaciones cuyo nivel de visibilidad `RN-OB-081` lo permita; **no** ve necesariamente todo el observador.
- El **expediente completo** de su módulo de servicio (bienestar, salud) sólo es accesible al perfil correspondiente, no a todos los perfiles de apoyo.
- No ve datos de otros tenants.

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Consultar ficha acotada del estudiante | Identificación, grupo, contacto del acudiente, alertas básicas |
| Aportar anotaciones al observador | Con selección de visibilidad según `RN-OB-081` |
| Operar su módulo de servicio | Sólo el del perfil asignado (salud / bienestar / biblioteca) |
| Consultar su propia bandeja / agenda del servicio | Atenciones, citas o préstamos a su cargo |

## Permisos configurables por el colegio

| Permiso | Default | Quién lo puede ajustar |
| --- | --- | --- |
| Perfil concreto y módulo de servicio habilitado | según contratación | Rector |
| Nivel de visibilidad por defecto de sus anotaciones | interna (`RN-OB-081`) | Rector / coordinación |
| Notificarse de remisiones internas dirigidas a su servicio | activado | Rector / coordinación |
| Comunicarse con el acudiente vía portal | desactivado | Rector |

## Permisos explícitamente NO otorgados

- **No accede a notas, calificaciones ni boletines** del estudiante (rol no académico).
- **No accede a la configuración del colegio** ni a parámetros del tenant.
- No emite documentos académicos oficiales (certificados, paz y salvo, boletines).
- No asigna ni modifica roles, grupos, materias ni horarios.
- No accede al módulo de **pagos y cartera** ni a información financiera del estudiante.
- No accede al expediente de servicio de un perfil distinto al suyo (la enfermera no ve el expediente de bienestar y viceversa).
- No accede a datos de otros tenants.

## Flujo típico de uso

1. El **Rector** crea la cuenta, asigna el rol **Personal de apoyo** y selecciona el **perfil** (orientador / enfermería / bibliotecario / otro).
2. El sistema habilita el **módulo de servicio** correspondiente y aplica el núcleo común de consulta.
3. Ante una situación con un estudiante, el funcionario ubica su **ficha acotada** por nombre, documento o grupo.
4. Presta el servicio en su módulo (registra la atención de salud, la nota de bienestar o el préstamo de biblioteca).
5. Si el hecho debe quedar en el seguimiento del estudiante, **aporta una anotación al observador** y elige su nivel de visibilidad (`RN-OB-081`), por defecto **interna**.
6. Si el caso excede su servicio, genera una **remisión interna** a la coordinación o al perfil que corresponda; el funcionario nunca decide sanciones ni promoción.
7. Toda consulta y aporte queda registrado en el **log de auditoría** del tenant.

## Estados y transiciones

La cuenta de Personal de apoyo sigue el ciclo de vida estándar de usuario del tenant:

```
Invitado → Activo → Inactivo
                  → Suspendido → Activo
```

- El paso `Activo → Inactivo` es **manual** por un rol con permiso (`D-02`), típicamente al terminar el vínculo laboral.
- El cambio de **perfil** (p. ej. de enfermería a otro servicio) lo realiza el Rector y reconfigura el módulo habilitado sin borrar el historial de aportes.

## Reglas de asignación

- Lo asigna el **Rector** (o quien el colegio configure con permiso de gestión de usuarios).
- Requisito previo: definir el **perfil concreto** antes de activar la cuenta, para habilitar el módulo correcto.
- Cantidad: la que el colegio necesite; suele ser un grupo pequeño de funcionarios.
- Reporta al **Rector** o a la **coordinación** que el colegio designe como línea de supervisión.

## Compatibilidad con otros roles

- Un usuario tiene un único rol principal. **Personal de apoyo es incompatible** con Docente, Director de Grupo, Coordinador, Secretaría y Rector, para mantener la separación entre lo académico/administrativo y lo de servicio.
- No admite el complemento [[07-director-de-grupo\|Director de Grupo]].
- En un colegio pequeño, una misma persona física podría ejercer dos funciones; aun así se modela como **cuentas separadas** por trazabilidad, no como doble rol.

## Configurabilidad por colegio

- El catálogo de **perfiles** habilitados (orientador, enfermería, biblioteca, otros) depende de los servicios que el colegio contrate.
- El **nivel de visibilidad por defecto** de los aportes al observador es configurable (recomendado **interna**).
- Qué **módulo de servicio** se habilita por perfil.
- La **línea de reporte** (Rector o coordinación específica) la define el colegio.
- Si el colegio no usa el módulo de biblioteca/salud/bienestar, el perfil correspondiente opera sólo con el **núcleo de consulta + aporte al observador**.

## Integraciones con otros módulos

- **Observador del estudiante:** los aportes se rigen por la visibilidad de `RN-OB-081` (ver [[../../04-procesos-academicos/observador-del-estudiante\|Observador del estudiante]]).
- **Bienestar / Salud / Biblioteca:** el perfil concreto opera su módulo de servicio (`RN-BW`, `RN-SA`, `RN-BI`).
- **Matriz de permisos:** este rol tiene columna propia (`D-04`) en [[../matriz-de-permisos\|Matriz de permisos]].
- **Espacios físicos:** consultorios y salas de atención reutilizan el modelo de [[../../04-procesos-academicos/espacios-fisicos\|Espacios físicos]].
- **Comunicación:** las remisiones y citas se notifican por los canales habilitados sin exponer el motivo sensible (ver [[../../05-comunicacion/notificaciones\|Notificaciones]]).

## Reglas de negocio

- **RN-TU-001 — Rol de permisos mínimos:** el Personal de apoyo opera con el conjunto de permisos más acotado entre los roles internos: consulta de ficha acotada del estudiante y aporte al observador, sin acceso académico ni administrativo.
- **RN-TU-002 — Sin acceso a notas ni configuración:** el rol nunca accede a calificaciones, boletines, promoción ni a la configuración del tenant, independientemente del perfil asignado.
- **RN-TU-003 — Perfil obligatorio antes de activar:** toda cuenta de Personal de apoyo debe tener un perfil concreto (orientador / enfermería / biblioteca / otro) definido por el Rector antes de quedar activa, ya que determina el módulo de servicio habilitado.
- **RN-TU-004 — Módulo de servicio según perfil:** cada perfil sólo accede a su propio módulo de servicio (`RN-BW`, `RN-SA` o `RN-BI`); ningún perfil ve el expediente de un módulo ajeno.
- **RN-TU-005 — Aporte al observador con visibilidad RN-OB-081:** las anotaciones que el Personal de apoyo lleva al observador se crean con los tres niveles de visibilidad de `RN-OB-081` y por defecto en nivel **interna**, dado el carácter sensible del dato.
- **RN-TU-006 — Ficha acotada, no expediente completo:** la consulta del estudiante se limita a identificación, grupo, contacto del acudiente y alertas básicas; el rol no obtiene la vista académica ni financiera completa.
- **RN-TU-007 — Rol incompatible con roles académicos y administrativos:** Personal de apoyo no se combina con Docente, Director de Grupo, Coordinador, Secretaría ni Rector; una persona con dos funciones se modela con cuentas separadas.
- **RN-TU-008 — Línea de reporte configurable:** el rol reporta al Rector o a la coordinación que el colegio designe; esa relación de supervisión es un parámetro del tenant.
- **RN-TU-009 — Auditoría de consultas y aportes:** toda consulta de la ficha del estudiante y todo aporte al observador quedan registrados en el log de auditoría con usuario, fecha, hora e IP.
- **RN-TU-010 — Remisión, no decisión:** ante un caso que excede su servicio, el rol genera una remisión interna; nunca decide sanciones disciplinarias, promoción ni medidas académicas.

## Notas y pendientes

- **[Decisión tomada]** El rol se **formaliza** como tipo de usuario y rol con permisos mínimos: consulta acotada + aporte al observador (`D-04`, `RN-TU-411`). Tiene columna propia en la matriz de permisos y corresponde a **ROL-12 / PRD-11** en `Arquitectura/`.
- **[Decisión tomada]** Los aportes al observador usan la visibilidad de `RN-OB-081` y se crean por defecto en nivel **interna** (`RN-TU-005`), coherente con `RN-BW-004` y `RN-SA-008`.
- **[Pendiente — producto]** Definir el **catálogo cerrado de perfiles** soportados de fábrica (orientador, enfermería, biblioteca) frente a perfiles "otros" sin módulo dedicado, y si "otros" admite micro-permisos adicionales.
- **[Pendiente — producto]** Validar con jurídico el alcance de la **ficha acotada** frente a Habeas Data (Ley 1581) para perfiles que tratan datos sensibles de salud del menor.

## Documentos relacionados

- [[../tipos-de-usuario|Tipos de usuario]]
- [[../matriz-de-permisos|Matriz de permisos]]
- [[01-rector-administrador-colegio|Rol: Rector]]
- [[03-coordinador-convivencia|Rol: Coordinador de Convivencia]]
- [[08-estudiante-y-acudiente|Rol: Estudiante]]
- [[../../04-procesos-academicos/observador-del-estudiante|Observador del estudiante]]
- [[../../12-bienestar-y-servicios/bienestar-y-orientacion|Bienestar y orientación]]
- [[../../12-bienestar-y-servicios/salud-y-enfermeria|Salud y enfermería]]
- [[../../12-bienestar-y-servicios/biblioteca|Biblioteca]]
- [[../../04-procesos-academicos/espacios-fisicos|Espacios físicos]]
- [[../../05-comunicacion/notificaciones|Notificaciones]]
