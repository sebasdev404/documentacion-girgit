---
titulo: "Rol: Estudiante"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, estudiante, tenant]
---

# Rol: Estudiante

> **Aclaración estructural (`RN-TU-410`):** el "acudiente" / "padre de familia" **NO es un tipo de usuario** en la plataforma. La única cuenta del menor es la del **estudiante**, y el acudiente la **opera de hecho** (consulta de notas, recepción de comunicados, pago de pensiones, cargue de documentos). El acudiente no tiene credenciales propias, perfil propio ni permisos propios en el sistema. Sus datos se registran como **información de contacto del estudiante**, no como un usuario aparte.

## Identificación

- **Nombre del rol:** Estudiante
- **Tipo de usuario asociado:** Estudiante matriculado en el colegio
- **Ámbito:** Tenant (colegio)
- **Configurable por el colegio:** sí — el portal puede estar activado, desactivado o restringido a ciertos módulos
- **Tipo:** principal (solo consulta)

## Descripción

Rol de **solo consulta**. El estudiante (o, en la práctica, su acudiente operando la cuenta) accede al portal para ver la información académica, financiera y disciplinaria propia del estudiante. Ningún usuario con este rol modifica datos del sistema.

## Responsabilidades

- Consultar **notas** por materia y por período.
- Consultar **horario** de clases.
- Recibir y leer **comunicados** y notificaciones.
- Consultar **boletines** emitidos.
- Consultar **observaciones académicas** registradas por los docentes.
- Consultar **anotaciones del observador** según la configuración del colegio (`RN-OB-080`, `RN-OB-081`).
- Consultar **estado de cuenta**, generar pagos y descargar comprobantes (`RN-PP-120`).
- Cargar **documentos requeridos** y recibir notificación de aprobación o rechazo (`RN-GD-270`).

## Scope / alcance de visibilidad

- Únicamente los **datos propios** del estudiante.
- En ningún caso ve datos de otros estudiantes del mismo colegio ni de otros tenants.
- No accede a información administrativa o de configuración del colegio.

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Consultar notas propias | Por materia y por período |
| Consultar horario | Del grupo correspondiente |
| Consultar boletines emitidos | |
| Recibir comunicados | Del colegio y de los docentes según configuración |
| Consultar observaciones académicas | Registradas por los docentes |
| Consultar estado de cuenta y pagar | Según pasarelas habilitadas en el tenant |
| Cargar documentos requeridos | Sujeto a flujo de revisión administrativa (`RN-GD-270`) |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
| --- | --- | --- |
| Acceso al portal | activado | El colegio puede desactivarlo completamente |
| Ver el observador disciplinario | configurable | Algunos colegios prefieren que sea solo interno (`RN-OB-081`) |
| Descargar boletines en PDF | configurable | |
| Recibir notificaciones por correo | configurable | |
| Comunicarse con docentes vía portal | configurable | Por defecto restringido a canales formales (`RN-MI-180`) |

## Permisos explícitamente NO otorgados

- No modifica ningún dato del sistema (rol exclusivamente de consulta).
- No accede a notas o información de otros estudiantes.
- No accede a configuración del colegio.
- No accede a datos de otros tenants.

## Reglas de asignación

- La cuenta de estudiante se crea durante la **matrícula** por la Secretaría Académica.
- **Un estudiante = una cuenta.** No se crean cuentas adicionales para los acudientes.
- Los datos de **acudiente(s)** del estudiante (nombre, identificación, parentesco, contacto, autorización de salida, etc.) se registran como **información de contacto del estudiante** dentro de su ficha de matrícula. Esos datos **no constituyen un usuario** y no generan credenciales.
- Si el colegio desactiva el portal para este rol, las cuentas existen pero no pueden iniciar sesión.
- El primer ingreso usa contraseña temporal con cambio obligatorio (`RN-AU-360`).

## Compatibilidad con otros roles

- No es compatible con roles internos del colegio (Docente, Coordinador, Secretaría, Rector). Una persona del colegio cuyo hijo estudia ahí mismo conserva su cuenta laboral y, **por separado**, el hijo tiene su propia cuenta de estudiante; el docente la opera de facto fuera del sistema, sin "doble rol" modelado.

## Variantes según configuración del colegio

- En algunos colegios este acceso está **completamente desactivado**. La información se entrega presencialmente o por canales paralelos.
- En otros colegios se restringe a ciertos módulos (ej. solo notas y boletines, sin observador).
- La intensidad de uso del portal por parte del menor o del acudiente es decisión de cada familia; el sistema no la modela.

## Egresados

- Al graduarse, el estudiante pasa al rol de [[14-egresado|Egresado]] y conserva acceso a su histórico (boletines, certificados, paz y salvo) según `RN-HC-281`.

## Notas y pendientes

- Definir la política de **acceso post mayoría de edad** del estudiante: hoy la cuenta sigue siendo única y no cambia de titular; pendiente formalizar si el colegio puede cerrar canales de notificación al acudiente operativo.
- Definir si el portal ofrece **vista consolidada multi-hijo** para acudientes con varios estudiantes en el mismo colegio (login cruzado entre cuentas de los hijos). **Funcionalidad futura.**
