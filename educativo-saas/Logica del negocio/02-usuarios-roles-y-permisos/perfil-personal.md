---
titulo: Perfil personal y menú de usuario
tipo: regla
estado: vigente
tags: [identidad, perfil, seguridad]
---

# Perfil personal y menú de usuario

El perfil siempre pertenece al usuario autenticado. Ajustes institucionales conserva sus rutas y permisos separados. La vista no utiliza nombres, fotografías, suscripciones ni estadísticas de demostración.

| Dato o acción | Personal del colegio / Plataforma | Estudiante | Validación |
|---|---|---|---|
| Nombre | Edita su propio nombre | Consulta; el colegio administra su identidad académica | Obligatorio, máximo 160 caracteres; rechazo en API si intenta cambiarlo siendo estudiante |
| Teléfono personal | Edita | Edita | Máximo 32 caracteres; no sustituye contactos oficiales del expediente |
| Correo de acceso | Cambia con contraseña actual | Consulta; solicita cambio al colegio | Formato, unicidad en la base correspondiente; cambio deja el correo sin verificar |
| Contraseña | Cambia con contraseña actual | Igual | 8–128 caracteres, mayúscula, minúscula, número y símbolo; confirmación; revoca otras sesiones |
| Roles, permisos, estado, sede | Consulta cuando corresponde | Consulta cuando corresponde | Nunca se reasignan desde el perfil propio |
| Plan del colegio | Consulta nombre real del catálogo central | Consulta | No editable desde perfil; una sede muestra el plan del colegio padre |
| Datos institucionales | Ruta independiente y permiso correspondiente | Sin edición institucional | No forman parte del formulario personal |
| MFA | Opcional para todos los perfiles | Opcional | Solo se exige código al iniciar sesión después de que el usuario lo active |

En el menú se muestran nombre, correo, iniciales y plan actual. En Plataforma sin colegio activo aparece «Plataforma». Al suplantar se mantiene nombre/correo del superadministrador y se consulta el plan del colegio activo sin reutilizar el de otro contexto. Un plan inexistente muestra «Plan no disponible», nunca un plan inventado.

No existe inscripción obligatoria ni sesión limitada por falta de MFA. Las sesiones limitadas emitidas por la política anterior recuperan el acceso. La activación opcional desde Ajustes de la cuenta requiere contraseña, muestra QR y clave manual para una aplicación autenticadora y se confirma con un código de seis dígitos. Al confirmarlo, las otras sesiones se revocan. TOTP y códigos de recuperación no se envían por Reverb. Los ocho códigos de recuperación se muestran una vez y cada uno se consume una sola vez. Se almacenan hashes, no los códigos originales.

El cambio de correo no demuestra que el buzón exista: falta completar el flujo de verificación del nuevo correo. No se presenta como correo verificado. La recuperación asistida por pérdida de todos los factores y la renovación del autenticador quedan pendientes; desactivar MFA activo exige contraseña y código válido.

El menú de usuario conserva Mis proyectos, Mi suscripción con sus opciones, y Mis estados de cuenta para su futura implementación. No muestran cifras inventadas ni ejecutan operaciones aún inexistentes. La administración del estado del usuario permanece en gestión de usuarios. Google vinculado puede mostrarse cuando ya exista; la interfaz de vinculación solo se ofrece si la integración está configurada y la cuenta puede modificarla. No es un método de inicio de sesión SSO.

Referencias: [[autenticacion]], [[tipos-de-usuario]], [[../../Arquitectura/_Globales/11 - Matriz de Verificacion|Matriz de verificación]].
