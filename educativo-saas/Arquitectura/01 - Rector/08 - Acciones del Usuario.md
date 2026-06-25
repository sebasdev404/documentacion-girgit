---
tags:
  - arquitectura
  - rol/rector
  - acciones
aliases:
  - Acciones ROL-02
  - Rector Acciones
---

# Acciones del Usuario — Rector / Administrador del Colegio

Tabla accion -> resultado. Cada accion sensible (configuracion, usuarios, roles, notas, firmas) genera entrada en el log de auditoria del tenant (RR-03, RNF-03).

## Configuracion institucional

| Accion | Resultado |
|---|---|
| Completa el asistente de identidad institucional (RF-04) | Sistema valida NIT y resolucion MEN · guarda datos · habilita emision de documentos oficiales · registra en log |
| Elige calendario (A o B) y define periodos (RF-05) | Sistema verifica que el calendario este habilitado por el plan · crea la estructura de periodos y fechas de cierre · registra en log |
| Crea jornadas y bloques horarios (RF-06) | Sistema valida solapamientos · guarda la malla horaria base · la deja disponible para construir horarios · registra en log |
| Define la escala valorativa numerica o por imagenes (RF-07) | Sistema guarda la escala · si ya hay notas cargadas, advierte impacto antes de aplicar · registra en log |
| Configura el metodo de aprobacion y la nota minima (RF-08) | Sistema guarda la formula y la nota minima · advierte si afecta consolidados ya calculados · registra en log |

## Usuarios y roles

| Accion | Resultado |
|---|---|
| Crea un usuario y le asigna rol (RF-10, RR-04) | Sistema valida correo unico en el tenant · crea la cuenta · envia acceso · asigna el rol · registra en log |
| Carga masiva de usuarios | Sistema valida el archivo fila por fila · crea los validos · lista los rechazados con su motivo · registra el lote en log |
| Desactiva / reactiva un usuario | Sistema cambia el estado · conserva el historial · invalida (o restablece) las sesiones activas · registra en log |
| Restablece la contrasena de un usuario | Sistema genera enlace de restablecimiento · lo envia al correo del usuario · registra en log |
| Activa / desactiva un permiso configurable de un rol (RR-05) | Sistema aplica el cambio a todos los usuarios de ese rol · no toca los permisos estructurales · registra en log |
| Renombra un rol | Sistema actualiza la etiqueta visible · conserva los permisos asociados · registra en log |
| Elige el esquema de coordinacion (separados vs combinado, RR-12) | Sistema habilita un esquema y deshabilita el otro · impide tener ambos simultaneamente · registra en log |

## Operacion academica y actos del Rector

| Accion | Resultado |
|---|---|
| Coordina el cierre de un periodo (RF-20) | Sistema valida que las notas esten completas · bloquea la edicion ordinaria · habilita generacion de boletines · registra en log |
| Edita una nota despues del cierre (RF-17, RR-07) | Sistema exige justificacion · aplica el cambio · conserva el valor anterior en el historial · registra en log |
| Aprueba / firma un boletin (RF-39) | Sistema marca el boletin como aprobado · habilita su entrega oficial a las familias · registra la firma con autor y fecha en log |
| Agrega una observacion general a un boletin | Sistema adjunta la observacion al boletin del estudiante · registra en log |
| Consulta el consolidado de un grupo o de todos los grupos (RF-18, RF-19) | Sistema muestra el consolidado calculado segun el metodo de aprobacion vigente · permite exportar |

## Convivencia (Ley 1620)

| Accion | Resultado |
|---|---|
| Registra una anotacion en el observador de cualquier estudiante (RF-26) | Sistema guarda la anotacion con tipologia · notifica al director de grupo y al acudiente segun configuracion · registra en log |
| Cita formalmente a un acudiente (RF-28) | Sistema genera la citacion · la envia por el portal/correo · la agenda · registra en log |
| Genera un reporte de convivencia (RF-29) | Sistema consolida casos por periodo/tipologia · permite exportar |

## Secretaria y documentos

| Accion | Resultado |
|---|---|
| Genera o respalda una constancia / certificado / paz y salvo (RF-34 a RF-36) | Sistema verifica pendientes si el bloqueo esta activo (RR-08) · genera el PDF con la identidad institucional · registra emision en log |
| Reporta matricula al SIMAT (RF-37, RR-15) | Sistema genera el formato requerido por el MEN · marca el reporte como enviado · registra en log |

## Comunicaciones y reportes

| Accion | Resultado |
|---|---|
| Envia un comunicado al colegio entero (RF-42) | Sistema selecciona la audiencia · programa o envia · entrega por portal/correo · registra el envio en log |
| Genera un reporte o KPI | Sistema calcula la metrica con datos del tenant · muestra el dashboard · permite exportar PDF/CSV |
| Consulta el log de auditoria del tenant (RF-49) | Sistema muestra resultados filtrados (solo de su tenant, RR-01) · permite exportar · la exportacion queda registrada |

## Sesion

| Accion | Resultado |
|---|---|
| Inicia sesion por el subdominio del colegio (RR-06) | Sistema infiere el tenant del subdominio · valida credenciales · registra el ingreso en log |
| Cierra sesion | Sistema invalida el token · registra el logout en log |

## Relacionado

- [[10 - Validaciones]] — que bloquea el sistema en cada accion
- [[11 - Respuestas del Sistema]] — eventos y respuestas
- [[09 - Campos del Formulario]] — campos de cada formulario
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
