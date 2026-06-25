---
tags:
  - arquitectura
  - rol/rector
aliases:
  - Arquitectura ROL-02
  - Wireframe Rector
---

# Arquitectura — Rector / Administrador del Colegio

Wireframe principal del rol. Es el documento mas visual y referenciado del rol ROL-02.

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio.md`. El Rector es el actor con mayor nivel de acceso DENTRO del tenant: ve y puede operar todo lo que hacen los demas roles internos del colegio.

---

## N0 — Inicio (login por subdominio del colegio)

El Rector entra por el subdominio de SU colegio (RR-06), no por una URL global de plataforma como el Superadmin. El `tenant_id` se infiere del subdominio antes de validar credenciales.

```
[ micolegio.plataforma.com ]
        |
        v
  Login (correo + contrasena)
        |
        +--- credenciales invalidas --> mensaje generico + registro en log del tenant
        |
        +--- tenant suspendido --------> pantalla "colegio suspendido" (RR-01 / accion del Superadmin)
        |
        v
  Dashboard del colegio
```

- Si el colegio activo SSO (RI-07) o MFA, el flujo agrega ese paso. MFA no es obligatorio para este rol como si lo es para el Superadmin.
- Todo intento de login (exito/fallo) queda en el log de auditoria del tenant (RR-03, RF-49).
- En el primer ingreso (tenant recien creado por el Superadmin) el sistema lleva al Rector al asistente de configuracion institucional.

---

## HEADER (presente en toda la app)

```
[ Logo del colegio ]   [ Buscador interno ]   [ Selector de ano lectivo ]   [ Perfil ]   [ Notificaciones ]
```

- **Perfil del usuario:** datos del Rector, cambiar contrasena, cerrar sesion, preferencias.
- **Buscador interno:** busca estudiantes, docentes, grupos, usuarios y documentos DENTRO del tenant (nunca cross-tenant — RR-01).
- **Selector de ano lectivo:** cambia el contexto entre ano vigente y anos anteriores (consulta historica).
- **Notificaciones:** cierres de periodo pendientes, boletines por aprobar, casos de convivencia abiertos (Ley 1620), alertas de cartera/mora, documentos por vencer, acciones del Superadmin sobre el tenant (RN-LA-002).

---

## N1 — SIDEBAR (modulos del rol)

El Rector ve TODOS los modulos operativos del colegio. A diferencia de los demas roles, no se le ocultan secciones: su sidebar es el superset del tenant.

```
+-------------------------------+
|  Dashboard del colegio        |
|                               |
|  CONFIGURACION                |
|   Identidad institucional     |
|   Calendario y periodos       |
|   Jornadas y bloques          |
|   Modelo pedagogico           |
|   Escala valorativa           |
|   Metodo de aprobacion        |
|                               |
|  GOBIERNO                     |
|   Usuarios                    |
|   Roles y permisos            |
|   Auditoria del tenant        |
|                               |
|  ACADEMICO                    |
|   Plan de estudios            |
|   Grupos y asignacion         |
|   Horarios                    |
|   Notas y consolidados        |
|   Asistencia                  |
|   Boletines                   |
|                               |
|  CONVIVENCIA                  |
|   Observador del estudiante   |
|   Convivencia (Ley 1620)      |
|                               |
|  SECRETARIA                   |
|   Matricula y admisiones      |
|   Documentos oficiales        |
|                               |
|  BIENESTAR Y SERVICIOS        |
|   Salud / enfermeria          |
|   Bienestar / orientacion     |
|   Biblioteca                  |
|   Transporte                  |
|   Restaurante / comedor       |
|                               |
|  FINANCIERO                   |
|   Pensiones y cartera         |
|   Becas y descuentos          |
|   Paz y salvo                 |
|                               |
|  COMUNICACIONES               |
|   Comunicados y circulares    |
|                               |
|  REPORTES                     |
|   Reportes y KPIs             |
|   Reportes oficiales (MEN)    |
+-------------------------------+
```

> El Rector NO tiene acceso a modulos de plataforma (crear/eliminar tenants, planes, cambiar calendario A/B habilitado, logs globales, impersonacion). Esos son exclusivos del Superadmin (ROL-01). Solo elige su calendario dentro de los habilitados (RR-13).

---

## Detalle por modulo

### Dashboard del colegio

Vista de entrada. Tarjetas resumen del estado del colegio en el ano vigente:
- Estudiantes activos / matriculados / retirados; cupos por grado.
- Estado de cierre por periodo (abierto / en cierre / cerrado).
- Boletines pendientes de aprobacion.
- Casos de convivencia abiertos (Ley 1620) y citaciones programadas.
- Cartera: % al dia vs en mora.
- Alertas de configuracion incompleta (escala sin definir, periodos sin fechas, etc.).

> Callout informativo: el dashboard es de solo lectura; cada accion se ejecuta en su modulo. Las tarjetas enlazan al modulo correspondiente.

### Identidad institucional (RF-04)

- **Detalle:** nombre, nombre comercial, logo, NIT, resolucion del MEN, codigo DANE, direccion, telefonos, correo institucional, redes.
- **Acciones:** Editar identidad · Subir logo · Definir datos de contacto.
- Callout importante: el NIT y la resolucion MEN alimentan los documentos oficiales (constancias, certificados, reportes SIMAT); un dato errado se propaga a todo lo emitido.

**Como se usa este modulo:** apenas el Superadmin crea el tenant y entrega el acceso, el Rector entra al asistente y completa la identidad antes de cualquier otra cosa. Es prerequisito para emitir documentos.

### Calendario y periodos (RF-05)

- **Detalle:** calendario habilitado (A o B), lista de periodos lectivos con fecha de inicio/fin, fechas de cierre de notas, fechas de entrega de boletines.
- **Acciones:** Elegir calendario (dentro de los habilitados) · Crear / editar periodos · Definir fechas de cierre.
- Callout warning: el Rector elige A o B dentro de lo habilitado por el plan, pero NO puede cambiar el calendario habilitado del tenant; eso es del Superadmin (RR-13). Si necesita el otro calendario, solicita el cambio al Superadmin.

**Como se usa este modulo:** define la estructura temporal del ano. De estas fechas dependen los cierres de periodo (RF-20), la edicion de notas (RR-07) y la generacion de boletines.

### Jornadas y bloques (RF-06)

- **Detalle:** jornadas (Manana, Tarde, Unica, Nocturna), horas de inicio/fin, duracion de bloque, recreos.
- **Acciones:** Crear jornada · Definir bloques horarios · Asociar niveles a jornada.

### Modelo pedagogico

- **Detalle:** por nivel educativo, definir si hay docente unico por salon o rotacion, si los estudiantes se desplazan, si existen directores de grupo.
- **Acciones:** Configurar modelo por nivel.

### Escala valorativa (RF-07)

- **Sub-vistas:** escala numerica / escala por imagenes (preescolar).
- **Detalle:** rango (p. ej. 1.0–5.0), decimales, equivalencias por desempeno; o subir imagenes/caritas y definir cuantos niveles tiene la escala.
- **Acciones:** Definir escala · Subir imagenes · Mapear rangos a desempenos.

### Metodo de aprobacion (RF-08)

- **Detalle:** metodo de calculo (promedio simple / ponderado por porcentajes / sumatoria dividida) y nota minima de aprobacion.
- **Acciones:** Elegir metodo · Definir nota minima · Configurar redondeo.
- Callout importante: cambiar el metodo a mitad de ano afecta consolidados ya calculados; el sistema advierte.

### Usuarios (RF-10)

- **Sub-vistas:** lista de usuarios / detalle de usuario.
- **Filtros:** rol, estado (activo/inactivo), grupo, fecha de creacion.
- **Detalle:** datos del usuario, rol asignado, complementos (director de grupo), grupos y materias.
- **Acciones:** Crear usuario · Editar · Desactivar / reactivar · Reasignar rol · Restablecer contrasena · Carga masiva.
- Callout importante: desactivar un usuario no borra su historial (auditoria, observaciones, notas firmadas).

**Como se usa este modulo:** el Rector crea las cuentas de coordinadores, docentes, secretaria y estudiantes; les asigna rol (RR-04). Puede delegar la creacion ampliando permisos a otro rol, pero la responsabilidad estructural es suya.

### Roles y permisos (RF-09)

- **Detalle:** lista de roles del tenant con sus permisos estructurales (fijos) y configurables (activables).
- **Acciones:** Renombrar rol · Activar / desactivar permiso configurable · Elegir esquema de coordinacion (separados vs combinado — RR-12).
- Callout warning: no se pueden crear permisos nuevos ni quitar los estructurales (RR-05). La delegacion se hace ampliando permisos al otro rol, no quitandoselos al Rector.

### Auditoria del tenant (RF-49)

- **Detalle:** log inmutable de acciones sensibles del colegio (quien, que, cuando, IP, registro afectado).
- **Filtros:** actor, rol, accion, recurso, rango de fechas.
- **Acciones:** Consultar · Exportar (la exportacion queda registrada).
- Callout informativo: el Rector ve solo los logs de SU tenant (RR-01); los globales son del Superadmin. Las acciones del Superadmin sobre el tenant se le notifican (RN-LA-002).

### Plan de estudios / Grupos y asignacion / Horarios (RF-11 a RF-15)

- **Detalle:** materias por grado e intensidad horaria; grupos por grado y ano; asignacion de docentes a materias/grupos; designacion de director de grupo; horarios docente/materia/aula/bloque/dia.
- **Acciones:** CRUD academico completo.
- Callout informativo: aunque tipicamente lo opera el Coordinador Academico (ROL-03/ROL-05), el Rector tiene acceso total como supervision y respaldo.

### Notas y consolidados / Asistencia (RF-16 a RF-23)

- **Detalle:** consolidados por grupo y de todos los grupos; edicion de notas (incluso post-cierre con justificacion — RR-07); cierre de periodo; nivelaciones y habilitaciones; asistencia.
- **Acciones:** Ver consolidados · Editar nota (con justificacion) · Coordinar cierre de periodo · Gestionar nivelaciones.
- Callout warning: editar notas tras el cierre exige justificacion y queda auditado (RR-07, RR-03).

### Boletines (RF-38 a RF-41)

- **Detalle:** boletines por grupo; observaciones generales; descarga PDF.
- **Acciones:** Aprobar / firmar boletines (RF-39) · Agregar observacion · Descargar.
- Callout importante: la aprobacion/firma del boletin es un acto del Rector (o delegado configurable); habilita la entrega oficial a las familias.

### Observador del estudiante / Convivencia Ley 1620 (RF-24 a RF-29)

- **Detalle:** observaciones academicas y disciplinarias de cualquier estudiante; tipologias (leve/grave/gravisima); citaciones a acudientes; ruta de atencion integral (Ley 1620); reportes de convivencia.
- **Acciones:** Anotar en cualquier estudiante · Definir tipologias · Citar acudientes · Generar reportes.
- Callout warning: los casos de convivencia siguen la ruta de la Ley 1620 (`Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md`); los datos del menor son sensibles (Habeas Data, Ley 1581).

### Matricula y admisiones / Documentos oficiales (RF-30 a RF-37)

- **Detalle:** registro de estudiantes y acudientes; asignacion a grupo; documentos de matricula; constancias, certificados, paz y salvos; reporte SIMAT.
- **Acciones:** Ver/operar matricula · Generar documentos (respaldo de Secretaria) · Reportar SIMAT (RR-15).
- Callout importante: el reporte SIMAT al MEN es obligatorio (RR-15); el bloqueo de documentos por pendientes es configurable (RR-08).

### Bienestar y servicios (salud, orientacion, biblioteca, transporte, restaurante)

- **Detalle:** modulos transversales del colegio. El Rector tiene visibilidad de gestion (consulta y supervision) sobre enfermeria, orientacion escolar, prestamos de biblioteca, rutas de transporte y comedor.
- **Acciones:** Consultar reportes de cada servicio · Supervisar incidencias · Configurar responsables (ampliando permisos al personal de apoyo, ROL-09).
- Callout informativo: la operacion diaria de estos servicios la hace el Personal de Apoyo; el Rector consolida y supervisa. Datos de salud son sensibles (Habeas Data).

### Financiero (pensiones, becas, paz y salvo)

- **Detalle:** estado de cartera, pensiones, descuentos y becas, paz y salvo.
- **Acciones:** Consultar cartera y KPIs financieros · Aprobar becas/descuentos · Definir politica de mora.
- Callout informativo: la facturacion electronica (DIAN, RI-05) y las pasarelas (RI-01) son integraciones; el Rector ve resultados, no opera la integracion tecnica.

### Comunicaciones (RF-42, RF-43)

- **Detalle:** comunicados y circulares al colegio entero o a grupos; mensajeria con acudientes via portal.
- **Acciones:** Redactar comunicado · Seleccionar audiencia · Programar envio.

### Reportes y KPIs / Reportes oficiales MEN

- **Detalle:** dashboards academicos, de convivencia y financieros; reportes oficiales (SIMAT, MEN).
- **Acciones:** Generar reporte · Exportar · Programar reportes oficiales.

---

## Diferencias clave vs otros roles

| Aspecto | Rector (ROL-02) | Superadmin (ROL-01) | Coordinador Academico (ROL-03) |
| --- | --- | --- | --- |
| Ambito | Un solo tenant (todo el colegio) | Global, cross-tenant | Un tenant, foco academico |
| Entra por | Subdominio del colegio | URL de plataforma | Subdominio del colegio |
| Configuracion institucional | La define (identidad, escala, aprobacion) | No participa | No (la consume) |
| Usuarios y roles | Crea usuarios y asigna roles | No (eso es del tenant) | No |
| Calendario A/B | Elige dentro del habilitado | Cambia el habilitado (RR-13) | No |
| Operacion academica | Acceso total (respaldo/supervision) | No participa | Su area academica |
| Convivencia (Ley 1620) | Acceso total | No | Solo si es esquema combinado |
| Auditoria | Logs de su tenant | Logs globales | No |
| Impersonacion | No | Si (auditada) | No |

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo colegio | Buscador interno | Ano lectivo | Perfil | Notif    |
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                               |
|        |                                                          |
| Dashbrd|  [ Dashboard del colegio: tarjetas de estado ]           |
| Config |  [ Identidad / Calendario / Escala / Aprobacion ]        |
| Gobiern|  [ Usuarios / Roles / Auditoria ]                        |
| Academc|  [ Plan / Grupos / Horarios / Notas / Boletines ]        |
| Conviv |  [ Observador / Ley 1620 ]                               |
| Secret |  [ Matricula / Documentos / SIMAT ]                      |
| Bienest|  [ Salud / Orientacion / Biblioteca / Transporte ]       |
| Financ |  [ Pensiones / Becas / Paz y salvo ]                     |
| Comunic|  [ Comunicados ]                                         |
| Reportes [ KPIs / Reportes MEN ]                                  |
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
- [[09 - Campos del Formulario]]
- [[10 - Validaciones]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio.md`
