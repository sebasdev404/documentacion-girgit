---
titulo: "CU-003: Solicitud de matrícula desde portal público"
modulo: 04-procesos-academicos
tipo: caso-de-uso
estado: implementado-local
tags: [caso-de-uso, pre-matricula, portal, pin]
---

# CU-003: Solicitud de matrícula desde portal público

Versión del 7 de octubre de 2026. Sin usuario de acudiente, cuenta estudiantil previa, pagos o firma de contrato. Referencia: [[../04-procesos-academicos/matriculas|Matrículas por enlace]].

## Precondiciones

Convocatoria habilitada dentro de fechas, año planificado/en curso, grados/requisitos configurados; dominio del colegio, correo saliente y almacenamiento operativo.

## Flujo

1. Abrir enlace, indicar correo y grado.
2. Recibir PIN y acceder con correo + PIN.
3. Completar nombres/apellidos, nacimiento, identificación y campos adicionales. Guardar borrador.
4. Adjuntar documentos; validar MIME, tamaño, cuota y escáner; conservar nombre/versiones.
5. Aceptar texto institucional de tratamiento y enviar.
6. Registrar envío, notificar al correo y mostrar en bandeja interna.
7. Seguimiento desde `/ingreso`, convocatoria, correo + PIN.
8. Corregir datos/documentos observados y reenviar.

## Alternativas y aceptación

- Recuperación de PIN vencido/olvidado no duplica solicitud ni revela existencia del email.
- Sesión terminada: recuperar lo guardado; sin credenciales/PII persistidas en navegador.
- Archivo no válido: rechazo claro; no omitir escáner ni reemplazar aprobados.
- Durante revisión: formulario bloqueado hasta solicitud de correcciones.
- Convocatoria cerrada: seguimiento sí; iniciar/editar/subir no. Colegio puede reabrir para recibir correcciones.
- Documentos solo del propio expediente; selectores ajenos/numéricos no dan acceso.
- Al aprobar: correo con acceso, contraseña 72 h y cambio obligatorio; grupo pendiente hasta CU-002.
- Un borrador no crea cuenta ni matrícula académica.

Pruebas: `EnrollmentIntakeTest` y `npm run test:ui:ingreso` con navegador aislado y datos simulados. Verificar proveedor de correo antes de operar públicamente.
