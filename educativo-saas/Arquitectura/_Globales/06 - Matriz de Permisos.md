---
tags:
  - arquitectura
  - matriz-permisos
aliases:
  - Matriz de Permisos
---

# Matriz de Permisos

Quien puede hacer que, modulo por modulo, accion por accion.

Para el detalle granular de cada rol ver `Arquitectura/[NN - Rol]/04 - Permisos Detallados.md`.

Para los simbolos ver [[05 - Leyenda]].

Convenciones cortas usadas en esta matriz:
- `Crear` / `Ver` / `Editar` / `CRUD` / `Aprobar` / `Configurable` / `Auto` / `C` / `—` / `En pausa`
- `Auto*` significa que el sistema lo ejecuta automaticamente para este rol.
- `C` = comentar / aportar anotacion (ver [[05 - Leyenda]]).

> **Columnas de la matriz (D-07).** La matriz opera con ROL-01..ROL-09 + **ROL-12 (Personal de Apoyo)**. **ROL-10 (Sistema)** y **ROL-11 (Administrador Tecnico)** no llevan columna por diseno: ROL-10 no es persona (sus acciones se marcan `Auto`) y ROL-11 esta en pausa. **ROL-12** es un rol de servicio de bajo privilegio: en general `—`; tiene `Ver`/`C`/`Configurable` acotado solo en su modulo de servicio (segun perfil: orientador, enfermeria, bibliotecario) y `C` en el aporte al observador (`RN-TU-005`, visibilidad `RN-OB-081`).

---

## Plataforma (cross-tenant)

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Plataforma** | Crear / eliminar tenant | CRUD | — | — | — | — | — | — | — | — | — |
| | Asignar plan de licencia | Editar | — | — | — | — | — | — | — | — | — |
| | Cambiar calendario A/B del tenant | Editar | — | — | — | — | — | — | — | — | — |
| | Definir subdominio del tenant | Editar | — | — | — | — | — | — | — | — | — |
| | Gestionar almacenamiento del tenant | Editar | — | — | — | — | — | — | — | — | — |
| | Acceso cross-tenant para soporte | Ver | — | — | — | — | — | — | — | — | — |
| | Acceder a logs globales de plataforma | Ver | — | — | — | — | — | — | — | — | — |

---

## Configuracion del Colegio

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Identidad** | Configurar logo, NIT, MEN | — | Editar | — | — | — | — | — | — | — | — |
| **Calendario** | Definir periodos lectivos | — | Editar | — | — | — | — | — | — | — | — |
| | Cambiar calendario A/B | — | Ver | — | — | — | — | — | — | — | — |
| **Jornadas** | Configurar jornadas y bloques | — | Editar | — | — | — | — | — | — | — | — |
| **Modelo pedagogico** | Configurar por nivel | — | Editar | — | — | — | — | — | — | — | — |
| **Escala valorativa** | Configurar escala (numerica / imagenes) | — | Editar | — | — | — | — | — | — | — | — |
| **Aprobacion** | Configurar metodo y nota minima | — | Editar | — | — | — | — | — | — | — | — |

---

## Usuarios y Roles

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Usuarios** | Crear / editar / desactivar usuarios | — | CRUD | — | — | — | — | — | — | — | — |
| | Asignar roles | — | Editar | — | — | — | — | — | — | — | — |
| | Ajustar permisos configurables | — | Editar | — | — | — | — | — | — | — | — |

---

## Plan Academico y Horarios

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Plan de estudios** | Gestionar materias por grado | — | CRUD | CRUD | — | CRUD | — | — | — | — | — |
| **Grupos** | Crear / gestionar grupos | — | CRUD | CRUD | — | CRUD | — | — | — | — | — |
| **Asignacion** | Asignar docentes a materias/grupos | — | Editar | Editar | — | Editar | — | — | — | — | — |
| | Designar director de grupo | — | Editar | Editar | — | Editar | — | — | — | — | — |
| **Horarios** | Construir / editar horarios | — | CRUD | CRUD | — | CRUD | — | — | — | — | — |
| | Consultar horario propio | — | Ver | Ver | Ver | Ver | Ver | Ver | Ver | Ver | — |

---

## Notas y Consolidados

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Notas** | Registrar/editar notas en materia asignada | — | Editar | Configurable | — | Configurable | — | Editar | Editar | — | — |
| | Editar notas que no dicta | — | Editar | Configurable | — | Configurable | — | — | Configurable | — | — |
| | Editar notas despues del cierre | — | Editar | Configurable | — | Configurable | — | Configurable | Configurable | — | — |
| **Consolidados** | Ver consolidado del grupo dirigido | — | Ver | Ver | — | Ver | — | — | Ver | — | — |
| | Ver consolidado de todos los grupos | — | Ver | Ver | — | Ver | — | — | — | — | — |
| | Ver notas propias / del estudiante asociado | — | Ver | Ver | — | Ver | Configurable | — | — | Ver | — |
| **Periodo** | Coordinar cierre de periodo | — | Editar | Editar | — | Editar | — | — | — | — | — |
| | Gestionar nivelaciones / habilitaciones | — | Editar | Editar | — | Editar | — | — | — | — | — |

---

## Asistencia

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Asistencia** | Registrar en sus clases | — | Editar | — | — | — | — | Editar | Editar | — | — |
| | Consultar del grupo dirigido | — | Ver | Ver | — | Ver | — | — | Ver | — | — |
| | Consultar propia / del estudiante asociado | — | Ver | Ver | Ver | Ver | Ver | — | — | Ver | — |

---

## Convivencia y Observador

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Observador academico** | Registrar observacion en su materia | — | Editar | — | — | — | — | Editar | Editar | — | — |
| **Observador disciplinario** | Anotacion en grupo dirigido | — | Editar | — | Editar | Editar | — | — | Editar | — | — |
| | Anotacion en cualquier estudiante | — | Editar | — | Editar | Editar | — | — | — | — | — |
| **Observador (aporte de servicio)** | Aportar anotacion al observador con visibilidad RN-OB-081 | — | Editar | — | Editar | Editar | — | — | — | — | C |
| **Configuracion** | Definir tipologias de anotacion | — | Editar | — | Editar | Editar | — | — | — | — | — |
| **Citaciones** | Citar formalmente a acudientes | — | Editar | Configurable | Configurable | Configurable | — | — | Configurable | — | — |
| | Definir sanciones formales | — | Editar | — | Configurable | Configurable | — | — | — | — | — |
| **Reportes** | Generar reportes de convivencia | — | Ver | — | Reportar | Reportar | — | — | — | — | — |
| **Consulta** | Ver observador propio / del estudiante | — | Ver | — | Ver | Ver | — | — | Ver | Configurable | Ver |

---

## Matricula y Secretaria

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Estudiantes** | Registrar / editar estudiantes y acudientes | — | CRUD | — | — | — | CRUD | — | — | — | — |
| | Asignar a grupo (matricula) | — | Editar | Configurable | — | Configurable | Editar | — | — | — | — |
| | Cambiar grupo post-matricula | — | Editar | Configurable | — | Configurable | Configurable | — | — | — | — |
| | Consultar ficha acotada del estudiante (id, grupo, contacto, alertas) | — | Ver | Ver | Ver | Ver | Ver | — | — | — | Ver |
| **Documentos matricula** | Cargar y validar | — | Ver | — | — | — | Editar | — | — | — | — |

---

## Documentos Oficiales

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Constancias** | Generar constancias de estudio | — | Reportar | — | — | — | Reportar | — | — | — | — |
| **Certificados** | Generar certificados de notas | — | Reportar | — | — | — | Reportar | — | — | — | — |
| **Paz y salvos** | Emitir paz y salvos | — | Reportar | — | — | — | Reportar | — | — | — | — |
| **SIMAT** | Reportar a SIMAT | — | Reportar | — | — | — | Reportar | — | — | — | — |
| **Bloqueos** | Bloquear emision por pendientes | — | Configurable | — | — | — | Configurable | — | — | — | — |

---

## Boletines

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Boletines** | Generar boletin del grupo dirigido | — | Reportar | Reportar | — | Reportar | — | — | Reportar | — | — |
| | Aprobar / firmar boletines | — | Aprobar | Configurable | — | Configurable | — | — | Configurable | — | — |
| | Agregar observacion general | — | Editar | — | — | — | — | — | Editar | — | — |
| | Consultar propio / del estudiante | — | Ver | Ver | — | Ver | Ver | — | — | Ver | — |
| | Descargar PDF | — | Ver | Ver | — | Ver | Ver | — | Ver | Configurable | — |

---

## Comunicaciones y Portal

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Comunicados** | Enviar al colegio entero | — | Editar | Configurable | Configurable | Configurable | Configurable | — | — | — | — |
| **Mensajes** | Comunicarse con acudientes via portal | — | Editar | Configurable | Configurable | Configurable | Configurable | Configurable | Configurable | — | Configurable |
| **Notificaciones** | Recibir por correo | — | Auto | Auto | Auto | Auto | Auto | Auto | Auto | Configurable | Auto |
| **Portal** | Acceder al portal | — | Ver | Ver | Ver | Ver | Ver | Ver | Ver | Configurable | Ver |

---

## Auditoria

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Auditoria** | Acceder a logs del tenant | — | Ver | — | — | — | — | — | — | — | — |
| | Ver historial de cambios de un registro | — | Ver | Configurable | Configurable | Configurable | Configurable | — | — | — | — |

---

## Salud y Enfermeria (Bienestar y Servicios)

ROL-12 con perfil **enfermeria**. Modulo configurable (no todos los colegios lo activan).

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Ficha medica** | Consultar ficha medica (dato sensible) | — | Ver | — | Ver | Ver | — | — | — | — | Ver |
| | Diligenciar / actualizar ficha medica | — | — | — | — | — | — | — | — | Editar | Editar |
| | Ver alerta de salud (alergias, condicion critica) | — | Ver | — | Ver | Ver | — | Configurable | Configurable | — | Ver |
| **Atenciones** | Registrar atencion en enfermeria | — | Ver | — | — | — | — | — | — | — | Editar |
| | Suministrar medicamento (solo autorizado vigente) | — | — | — | — | — | — | — | — | — | Editar |
| **Remision** | Generar remision a centro medico | — | Ver | — | Ver | Ver | — | — | — | — | Editar |
| **Vacunas** | Registrar / hacer seguimiento de esquema | — | Ver | — | — | — | Editar | — | — | Editar | Editar |

---

## Bienestar y Orientacion (Bienestar y Servicios)

ROL-12 con perfil **orientador / psicologo**. Expediente sensible, visibilidad RN-OB-081.

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Expediente de bienestar** | Crear / gestionar expediente del estudiante | — | — | — | — | — | — | — | — | — | CRUD |
| | Consultar expediente completo de bienestar | — | Ver | — | — | — | — | — | — | — | Ver |
| **Citas** | Agendar cita psicosocial (sin motivo sensible) | — | — | — | — | — | — | — | — | — | Editar |
| **Atenciones** | Registrar atencion / nota de orientacion | — | — | — | — | — | — | — | — | — | Editar |
| **Remisiones** | Remision interna (a coordinacion) | — | Ver | — | Ver | Ver | — | — | — | — | Editar |
| | Remision externa (con consentimiento RN-HD) | — | — | — | — | — | — | — | — | — | Configurable |
| **Plan de apoyo** | Definir plan con doble visibilidad | — | — | — | — | — | — | — | — | Ver | Editar |

---

## Biblioteca (Bienestar y Servicios)

ROL-12 con perfil **bibliotecario**. Modulo configurable.

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Catalogo** | Catalogar material / ejemplares | — | Configurable | — | — | — | — | — | — | — | CRUD |
| **Prestamos** | Registrar prestamo / devolucion por ejemplar | — | Ver | — | — | — | — | — | — | — | Editar |
| **Reservas** | Gestionar cola de reservas | — | Ver | — | — | — | — | — | — | — | Editar |
| **Multas** | Liquidar multa por mora / reposicion | — | Configurable | — | — | — | — | — | — | — | Editar |
| **Consulta** | Consultar disponibilidad y solicitar prestamo | — | Ver | Ver | — | Ver | Ver | Ver | Ver | Ver | Ver |

---

## Transporte Escolar (Bienestar y Servicios)

Operado por Secretaria (rutas y cobro) y monitor de ruta (registro de abordajes). ROL-12 no opera este modulo.

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Rutas** | Definir rutas, paradas y cupos | — | Aprobar | — | — | — | CRUD | — | — | — | — |
| **Asignacion** | Asignar estudiante a ruta / parada | — | Ver | — | — | — | Editar | — | — | — | — |
| **Abordajes** | Registrar abordaje / descenso (notifica) | — | Ver | — | — | — | Editar | — | — | — | — |
| **Cobro** | Generar cobro recurrente de transporte | — | Aprobar | — | — | — | Editar | — | — | — | — |
| **Consulta** | Ver ruta / notificaciones del estudiante | — | Ver | — | — | — | Ver | — | — | Ver | — |

---

## Convivencia Ley 1620 (Cumplimiento Colombia)

Ruta de Atencion Integral (RAI) y Comite Escolar de Convivencia (CEC).

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Comite (CEC)** | Configurar y presidir el CEC | — | CRUD | — | Configurable | Configurable | — | — | — | — | — |
| **Casos** | Reportar situacion (incidente) | — | Editar | — | Editar | Editar | — | Editar | Editar | Configurable | C |
| | Clasificar / reclasificar caso (tipo I/II/III) | — | Ver | — | Editar | Editar | — | — | — | — | — |
| **Protocolo** | Ejecutar actuaciones de la ruta (RAI) | — | Ver | — | Editar | Editar | — | — | — | — | — |
| | Escalar tipo III al Rector (Auto) | Auto | Auto | — | Auto | Auto | — | — | — | — | — |
| **Actas** | Firmar acta del comite | — | Aprobar | — | Ver | Ver | — | — | — | — | — |
| **Consulta** | Ver lo que le corresponde del caso | — | Ver | — | Ver | Ver | — | Configurable | Configurable | Configurable | Configurable |

---

## Admisiones (Procesos academicos)

El aspirante no es usuario del sistema. Operado por Secretaria, Coordinacion y Rector.

| Modulo | Accion | ROL-01 | ROL-02 | ROL-03 | ROL-04 | ROL-05 | ROL-06 | ROL-07 | ROL-08 | ROL-09 | ROL-12 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Proceso** | Configurar etapas y derecho de inscripcion | — | CRUD | Configurable | — | Configurable | Ver | — | — | — | — |
| **Inscripcion** | Registrar aspirantes y documentos | — | Ver | — | — | — | CRUD | — | — | — | — |
| **Pruebas** | Agendar y registrar pruebas / entrevistas | — | Ver | Editar | Editar | Editar | Editar | — | — | — | — |
| **Decision** | Decidir admision (justificada y auditada) | — | Aprobar | Editar | — | Editar | Ver | — | — | — | — |
| **Lista de espera** | Gestionar lista de espera ordenada | — | Ver | Editar | — | Editar | Editar | — | — | — | — |
| **Conversion** | Emitir PIN de matricula al admitido (Auto) | Auto | Ver | — | — | — | Editar | — | — | — | — |

---

## Notas clave

> **Permisos estructurales vs configurables.** Las marcas "Configurable" indican que el colegio puede activar o desactivar el permiso desde la pantalla de configuracion del rol. Las marcas firmes (CRUD/Editar/Ver/Reportar/Aprobar/Auto/—) son **estructurales**, no se pueden modificar.

> **Director de Grupo (ROL-08) es complemento, no rol principal.** Solo se asigna sobre un usuario que ya tenga ROL-07 (Docente). Los permisos de ROL-08 listados aqui son ADICIONALES sobre el grupo dirigido; conserva todos los permisos de ROL-07 sobre sus materias asignadas.

> **Coordinador combinado (ROL-05) es excluyente con ROL-03 + ROL-04.** El colegio elige el esquema. No se asignan ambos esquemas simultaneamente.

> **Personal de Apoyo (ROL-12) opera solo el modulo de su perfil.** En general no tiene permiso (`—`). Solo accede al modulo de servicio que su perfil habilite (enfermeria -> Salud, orientador -> Bienestar, bibliotecario -> Biblioteca) mas el nucleo comun: consultar la ficha acotada del estudiante (`Ver`) y aportar al observador (`C`) con visibilidad RN-OB-081 (por defecto interna). En el observador solo `Ver` las anotaciones cuya visibilidad RN-OB-081 lo permita; no ve todo el observador. No accede a notas, boletines, documentos oficiales, configuracion del colegio ni cartera/pagos (`RN-TU-002`).

> **ROL-10 (Sistema) y ROL-11 (Administrador Tecnico) no llevan columna (D-07).** ROL-10 no es persona: las acciones automaticas se marcan `Auto` en la columna del rol que las dispara. ROL-11 esta en pausa.

> **Aislamiento por tenant (RR-01) aplica a todos los roles del tenant.** Nadie ve datos de otro colegio.

> **Auditoria (RR-03) aplica a todas las acciones sensibles** sin importar el rol.

> **Fuente de verdad del detalle:** `Logica del negocio/02-usuarios-roles-y-permisos/matriz-de-permisos.md`. Esta matriz es la **interpretacion UX** de esa.
