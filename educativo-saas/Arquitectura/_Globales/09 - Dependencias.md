---
tags:
  - arquitectura
  - dependencias
aliases:
  - Dependencias
---

# Dependencias

Mapeo de todo lo que el proyecto necesita para funcionar.

---

## 1. Dependencias internas

Modulos / componentes del sistema que se referencian entre si.

| Dependencia | Descripcion |
|---|---|
| Configuracion del tenant | Calendario, jornadas, escala valorativa, modelo pedagogico, metodo de aprobacion. La operacion academica depende totalmente de esta configuracion |
| Plan de estudios | Define materias por grado e intensidad horaria. Sin esto no se pueden registrar notas |
| Grupos y asignaciones | Determinan quien dicta que. Sin esto no hay horarios ni notas |
| Periodos lectivos abiertos | Determinan si se pueden registrar / editar notas y asistencia |
| Usuarios activos | Sin usuarios creados, no hay acceso. Sin roles asignados, no hay permisos |
| Reglas de negocio | Cada modulo respeta las RR-NN del documento [[07 - Reglas de Negocio]] |

---

## 2. Dependencias externas

Sistemas y servicios externos al SaaS.

| Dependencia | Descripcion |
|---|---|
| Pasarela de pago | Recaudo de pensiones y cobro de la suscripcion del SaaS al colegio |
| SIMAT (MEN Colombia) | Reporte oficial de matricula. Formato y especificacion definidos por el Ministerio de Educacion Nacional |
| Proveedor de correo | Envio de notificaciones por email (RI-03) |
| Proveedor de SMS | Envio de notificaciones criticas por SMS (RI-04) |
| DIAN — facturacion electronica | Emision de facturas y recibos electronicos (RI-05) |
| Almacenamiento en la nube | Documentos de matricula, evidencias, archivos cargados |
| Proveedor de SSO (opcional) | Login con Google / Microsoft, segun configuracion del tenant |
| Servicio de hosting / cloud | Infraestructura del SaaS |

---

## 3. Dependencias de catalogos

Configuraciones del sistema disponibles para todos los tenants.

| Catalogo | Descripcion |
|---|---|
| Calendarios oficiales | Calendario A y Calendario B, segun normativa MEN Colombia |
| Niveles educativos | Preescolar, Primaria, Secundaria, Media |
| Grados | Por nivel educativo (Pre-jardin a 11) |
| Areas del conocimiento | Catalogo MEN |
| Tipos de documento de identidad | TI, CC, CE, registro civil |
| Tipos de anotacion disciplinaria | Leve, grave, gravisima (configurable por colegio) |
| Tipos de evaluacion | Parcial, final, recuperacion, nivelacion |
| Estados de matricula | Pendiente, activa, retirada, graduada |
| Tipos de boletin | Parcial, final, consolidado |

---

## 4. Dependencias entre roles

Flujos donde varios roles intervienen secuencialmente.

| Flujo | Roles que intervienen |
|---|---|
| Provisioning de un colegio | ROL-01 crea tenant -> ROL-02 configura colegio |
| Matricula de un estudiante | ROL-06 inscribe -> ROL-03/ROL-05 asigna a grupo -> ROL-01 reporta SIMAT |
| Cierre de periodo | ROL-07 registra notas -> ROL-03/ROL-05 valida consolidado -> ROL-02 aprueba cierre |
| Boletin | ROL-07 registra notas -> ROL-08 genera boletin -> ROL-03/ROL-05 o ROL-02 aprueba -> distribucion a ROL-09 |
| Observador disciplinario | ROL-07/ROL-08 registra anotacion -> ROL-04/ROL-05 hace seguimiento -> notificacion a ROL-09 acudiente |
| Pago de pensiones | ROL-09 acudiente paga via pasarela -> sistema concilia -> ROL-06 registra recibo |

---

## 5. Dependencias semaforicas

Estados visuales del flujo que cambian segun condiciones.

| Estado | Color sugerido | Significado |
|---|---|---|
| Periodo abierto | Verde | Se pueden registrar/editar notas y asistencia |
| Periodo en cierre | Amarillo | Edicion limitada, en proceso de consolidacion |
| Periodo cerrado | Rojo | No se aceptan cambios sin configuracion especial |
| Matricula activa | Verde | Estudiante con documentos completos y pagos al dia |
| Matricula con pendientes | Amarillo | Faltan documentos o hay pagos vencidos |
| Matricula bloqueada | Rojo | No se pueden emitir documentos hasta resolver pendientes |
| Anotacion leve | Verde / sin marca especial | Observador comun |
| Anotacion grave | Amarillo | Requiere seguimiento del Coord. de Convivencia |
| Anotacion gravisima | Rojo | Requiere intervencion del Rector y/o citacion |
| Suscripcion del tenant activa | Verde | Colegio al dia |
| Suscripcion en mora | Amarillo | Pago vencido pero dentro de la gracia |
| Suscripcion suspendida | Rojo | Acceso restringido hasta regularizar |

---

## Documentos relacionados

- [[02 - PRD - Plataforma|PRD del proyecto]]
- [[07 - Reglas de Negocio|Reglas de Negocio]] — las dependencias semaforicas y entre roles se rigen por reglas
- [[06 - Matriz de Permisos|Matriz de Permisos]] — los flujos entre roles materializan los permisos
