---
tags:
  - arquitectura
  - reglas-de-negocio
aliases:
  - Reglas de Negocio
---

# Reglas de Negocio

Reglas RR-NN consolidadas. Cada regla viene de la fuente de verdad en `Logica del negocio/`.

---

## Reglas transversales

| ID | Regla | Descripcion |
|---|---|---|
| RR-01 | Aislamiento total entre tenants | Ningun rol puede acceder a datos de otro tenant. Aislamiento a nivel BD (base separada por tenant) y autenticacion (subdominio). Unica excepcion: ROL-01 (Superadmin) con acceso auditado |
| RR-02 | Verificacion de permisos en frontend y backend | Cada accion se valida tanto en UI (oculta/deshabilita) como en backend (rechaza llamadas). No es posible saltarse un permiso por interfaz |
| RR-03 | Auditoria de acciones sensibles | Toda accion sensible (notas, documentos, configuracion, cambios de roles, accesos del Superadmin) registra: quien, que, cuando, IP, registro afectado. Los logs son inmutables |
| RR-04 | Asignacion de roles por el Administrador del Colegio | Los roles del tenant solo los asigna ROL-02 (Rector). El rol del Rector lo entrega el Superadmin al crear el tenant. Un usuario tiene un solo rol principal |
| RR-05 | Configurabilidad acotada de permisos | El colegio no puede crear permisos nuevos. Solo puede activar/desactivar permisos configurables existentes. Los permisos estructurales no se pueden desactivar |
| RR-06 | Acceso al sistema solo por subdominio del colegio | Un usuario de un tenant no puede autenticarse en el portal de otro tenant, aunque use las mismas credenciales. El tenant_id se infiere del subdominio antes de validar credenciales |

---

## Reglas operativas

| ID | Regla | Descripcion |
|---|---|---|
| RR-07 | Notas se editan dentro del periodo abierto | Una vez cerrado el periodo, no se escriben notas. El Rector con permiso de transicion, o la suplantacion valida, debe reabrirlo. La ventana de solicitudes futura no permite escribir en estado cerrado |
| RR-08 | Bloqueo de documentos por pendientes | La secretaria puede ser configurada para bloquear emision de constancias/certificados/paz y salvos cuando hay documentos de matricula o pagos pendientes |
| RR-09 | Director de Grupo solo opera sobre su grupo | Los permisos extra del complemento Director de Grupo aplican solo sobre el grupo dirigido. En otros grupos sigue siendo solo Docente sobre sus materias |
| RR-10 | Docente ve solo grupos y materias asignados | Un docente nunca ve datos de grupos o materias que no le han sido asignados explicitamente por el Coordinador Academico |
| RR-11 | El menor tiene una unica cuenta (Estudiante) | No existe rol "Acudiente" como usuario (`RN-TU-410`). El menor posee una unica cuenta -la del Estudiante- y el acudiente la opera de hecho. El estudiante ve sus propios datos; el acudiente actua sobre esa misma cuenta |
| RR-12 | Coordinador combinado excluye los separados | Un tenant elige: o usa Coord. Academico + Coord. de Convivencia separados, o usa el Coordinador combinado. No ambos esquemas simultaneamente |
| RR-13 | Cambio de calendario A/B es del Superadmin | El Rector elige el calendario dentro de los habilitados por el plan, pero solo el Superadmin puede cambiar el calendario habilitado para un tenant |
| RR-14 | Cuenta individual del estudiante y ampliacion multihijo | En el lanzamiento rige RN-TU-410: el correo compartido no concede acceso entre cuentas. El selector multihijo queda futuro hasta definir vinculos autorizados y verificados; no fusiona expedientes ni deudas |
| RR-15 | Reporte SIMAT obligatorio | Los colegios estan obligados a reportar matricula al SIMAT (Ministerio de Educacion Nacional). El sistema debe generar el formato requerido |
| RR-16 | Visibilidad triple del observador para Personal de Apoyo | Las anotaciones que el Personal de Apoyo (ROL-12) aporta al observador se crean con los tres niveles de visibilidad de `RN-OB-081` y por defecto en nivel **interna**, dado el caracter sensible del dato. El rol solo ve en el observador las anotaciones cuya visibilidad lo permita (origen: `RN-OB-081`, `RN-TU-005`) |
| RR-17 | Otros cobros entran a la cartera unica del estudiante sin split | Todo cobro fuera de pension (tienda, transporte, comedor, biblioteca, eventos, certificados) se carga a la **cartera unica del estudiante**; no existe canal de cobro paralelo ni split entre hermanos ni entre acudientes: una sola deuda integral por estudiante (origen: `RN-PP-120`, `RN-TI-001`) |
| RR-19 | Tratamiento de datos del menor exige consentimiento | El consentimiento de tratamiento de datos de un estudiante menor lo otorga el **acudiente con patria potestad**; el sistema no acepta la autorizacion del propio menor. Las autorizaciones son granulares, no premarcadas, y se atan a la version de politica vigente (Ley 1581) (origen: `RN-HD-001`, `RN-HD-002`) |
| RR-20 | Convivencia sigue la Ruta de Atencion Integral Ley 1620 | Los casos de convivencia se atienden por la **Ruta de Atencion Integral (RAI)** de la Ley 1620: el protocolo se instancia segun el tipo (I/II/III) y no permite saltarse actuaciones obligatorias; los casos tipo III escalan automaticamente al Rector con constancia de reporte a la autoridad (origen: `RN-CVE-003`, `RN-CVE-004`) |

---

## Referencias cruzadas

- Fuente de verdad de las reglas transversales: `Logica del negocio/02-usuarios-roles-y-permisos/reglas-transversales-de-roles.md`.
- Las reglas operativas RR-07 a RR-15 provienen de los archivos individuales de rol en `Logica del negocio/02-usuarios-roles-y-permisos/roles/`.
- Las reglas operativas RR-16, RR-17, RR-19 y RR-20 provienen de los modulos nuevos de `Logica del negocio/` (`12-bienestar-y-servicios/`, `13-cumplimiento-colombia/`); ver su origen `RN` en [[10 - Mapeo RN-RR]].
- Cuando una regla aplique solo a un modulo especifico, ver el archivo de ese modulo en `Logica del negocio/`.

---

## Documentos relacionados

- [[03 - Tabla de Requerimientos|Tabla de Requerimientos]] — referencias RR-XX en la columna Notas.
- [[06 - Matriz de Permisos|Matriz de Permisos]] — los permisos configurables vienen de RR-05.
- [[08 - Criterios de Aceptacion|Criterios de Aceptacion]] — cada AC referencia la RR que cubre.
