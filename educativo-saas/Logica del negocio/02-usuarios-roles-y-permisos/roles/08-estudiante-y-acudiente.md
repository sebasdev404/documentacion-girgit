---
titulo: "Rol: Estudiante / Acudiente"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, estudiante, acudiente, padres, tenant]
---

# Rol: Estudiante / Acudiente

## Identificación

- **Nombre del rol:** Estudiante / Acudiente (ambos comparten el mismo rol con scope distinto)
- **Tipo de usuario asociado:** Estudiante matriculado o padre/acudiente vinculado a un estudiante
- **Ámbito:** Tenant (colegio)
- **Configurable por el colegio:** sí — el portal puede estar activado, desactivado o restringido a ciertos módulos
- **Tipo:** principal (solo consulta)

## Descripción

Rol de **solo consulta**. El estudiante accede al portal para ver su propia información; el acudiente accede para ver la información de su(s) hijo(s). **Ambos comparten exactamente los mismos permisos**, pero el scope/alcance es distinto: el estudiante ve sus propios datos, el acudiente ve los de los estudiantes a los que está vinculado.

Ningún usuario con este rol puede modificar datos del sistema.

## Responsabilidades

- Consultar **notas** por materia y por período.
- Consultar **horario** de clases.
- Recibir y leer **comunicados** y notificaciones.
- Consultar **boletines** emitidos.
- Consultar **observaciones académicas** registradas por los docentes.
- Consultar **anotaciones del observador** (si el colegio lo habilita para este rol).

## Scope / alcance de visibilidad

El scope cambia según el tipo de usuario que tenga este rol asignado:

| Tipo de usuario | Qué ve |
| --- | --- |
| Estudiante | Únicamente sus propios datos |
| Acudiente | Datos de los estudiantes a los que está vinculado (uno o varios hijos) |

En ningún caso ve:
- Datos de otros estudiantes del mismo colegio.
- Datos de otros tenants.
- Información administrativa o de configuración del colegio.

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Consultar notas propias / del estudiante asociado | Por materia y por período |
| Consultar horario | Del grupo correspondiente |
| Consultar boletines emitidos | |
| Recibir comunicados | Del colegio y de los docentes (según configuración) |
| Consultar observaciones académicas | Registradas por los docentes |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
| --- | --- | --- |
| Acceso al portal | activado | El colegio puede desactivarlo completamente |
| Ver el observador disciplinario | configurable | Algunos colegios prefieren que el observador sea solo interno |
| Descargar boletines en PDF | configurable | |
| Recibir notificaciones por correo | configurable | |
| Comunicarse con docentes vía portal | configurable | Por defecto suele estar restringido a canales formales |

## Permisos explícitamente NO otorgados

- No modifica ningún dato del sistema (rol exclusivamente de consulta).
- No accede a notas o información de otros estudiantes.
- No accede a configuración del colegio.
- No accede a datos de otros tenants.

## Reglas de asignación

- El usuario tipo **Estudiante** se crea durante la matrícula por la Secretaría Académica.
- El usuario tipo **Acudiente** se crea por la Secretaría Académica al vincularlo al estudiante.
- Un estudiante = una cuenta. Un acudiente = una cuenta, posiblemente vinculada a varios estudiantes (varios hijos).
- Si el colegio desactiva el portal para este rol, las cuentas existen pero no pueden iniciar sesión.

## Compatibilidad con otros roles

- No es compatible con roles internos del colegio (Docente, Coordinador, Secretaría, Rector). Si una persona del colegio es además acudiente, tiene dos cuentas separadas.

## Variantes según configuración del colegio

- En algunos colegios este acceso está **completamente desactivado**. La información se entrega presencialmente o por canales paralelos.
- En otros colegios se restringe a ciertos módulos (ej. solo notas y boletines, sin observador).
- Algunos colegios habilitan el portal solo para el acudiente y no para el estudiante (común en grados de primaria).

## Notas y pendientes

- Definir flujo de **vinculación acudiente ↔ estudiante**: cómo se crea, cómo se cambia, cómo se rompe (ej. divorcio, custodia compartida).
- Definir si el acudiente puede ver simultáneamente los datos de varios hijos en una sola vista consolidada o si tiene que cambiar de perfil.
- Definir política cuando un estudiante cumple la mayoría de edad: ¿el acudiente sigue viendo sus datos?
