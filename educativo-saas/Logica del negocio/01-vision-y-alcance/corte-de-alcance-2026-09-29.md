---
titulo: Corte de alcance y decisiones de implementación
tipo: decision
estado: vigente
tags: [alcance, decisiones, verificacion]
---

# Corte de alcance — 29 de septiembre de 2026

Este corte separa el producto comprometido, la implementación comprobada y la hoja de ruta. Una pantalla, permiso, semilla o documento existente no constituye por sí solo una funcionalidad terminada. La evidencia y la brecha de **cada AC vigente** están en [[../../Arquitectura/_Globales/11 - Matriz de Verificacion|Matriz de verificación]].

## Orden de interpretación

Las decisiones del producto de esta sesión, incorporadas aquí y en las reglas de negocio citadas, prevalecen sobre diseños anteriores incompatibles. `Logica del negocio` sigue siendo la fuente de verdad; `Arquitectura` describe su aplicación. Los documentos de `archivo-contexto` son históricos. El plan maestro es una hoja de ruta documental, no un acta de aceptación del software.

## Entregas y límites

| Entrega | Incluye | Puerta de salida |
|---|---|---|
| Base del lanzamiento | Aislamiento, identidad, permisos, perfil, MFA opcional, auditoría, respaldo/restauración, configuración institucional y académica | Evidencia positiva y negativa de acceso; restauración real en entorno aislado; cierre de brechas P0 |
| Operación escolar del lanzamiento | Matrícula, evaluación, asistencia, convivencia, boletines oficiales, comunicación, cartera y exportación oficial | Completar los AC correspondientes; las rutas «Próximamente» no cuentan como implementadas |
| Ampliaciones | Servicios de bienestar, biblioteca, transporte, cafetería, inventario, talento humano y portal multihijo | Nueva entrega explícita con sus dependencias; no bloquean por sí solas la base académica |
| Integraciones futuras | SSO Google/Microsoft, WhatsApp, conexión directa a sistemas oficiales y aplicación nativa | Integración, autorización y pruebas propias; vincular una cuenta Google no equivale a SSO |

Las exclusiones del [[alcance-y-no-alcance]] se aplican al lanzamiento. Las secciones de ampliación del plan maestro no las incorporan automáticamente al lanzamiento. Exportar archivos oficiales para carga manual sí está contemplado; conectarse directamente a los sistemas oficiales continúa siendo futuro.

## Contradicciones resueltas

| Tema | Decisión vigente | Consecuencia verificable |
|---|---|---|
| Schema o base por colegio | Una **base de datos PostgreSQL por tenant**; base central separada | AC-01 y PRD corregidos; una prueba con SQLite no demuestra provisionamiento PostgreSQL productivo |
| Configurar calendario | El Rector gestiona fechas del año y períodos; el tipo A/B del colegio lo gestiona Plataforma con las restricciones del histórico | AC-04 no concede el cambio A/B; se conserva AC-22 |
| Período cerrado | Ningún permiso permite escribir notas manteniendo el período cerrado. Rector con `academico.periodos.transicionar`, o suplantación válida, lo reabre explícitamente | AC-08 y RR-07 corregidos. La ventana de solicitudes de corrección queda futura; el permiso heredado `notas.editar_despues_cierre` no evita el bloqueo |
| Año cerrado | Las transiciones visibles requieren rol autorizado y permiso. El flujo completo de promoción, justificación y ventanas del histórico aún no está demostrado | No confundir la reapertura del período con el proceso de cierre anual ni dar este último por completo |
| Acudiente y varios hijos | RN-TU-410 mantiene una cuenta por estudiante, sin rol independiente de acudiente | AC-15 pasa a ampliación futura: un correo compartido no autoriza acceso a otro estudiante |
| Restauraciones semestrales/trimestrales | **Trimestrales**, con evidencia y reporte bajo solicitud (RN-BR-260) | AC-20 corregido; simulacro técnico local no sustituye restauración completa de un tenant |
| Región de respaldo | Destino secundario obligatorio por definir en infraestructura; otra región/proveedor es objetivo de resiliencia | No afirmar que existe replicación externa, retención o DR sin comprobación operativa |
| «Todo listo» o «todo mock» | Ambos extremos son incorrectos: existe API y persistencia; quedan módulos y controles pendientes | La matriz fechada sustituye afirmaciones de estado de documentos históricos |
| Perfil y colegio | El perfil modifica la cuenta autenticada; institución y plan son contexto de lectura | [[../02-usuarios-roles-y-permisos/perfil-personal|Perfil personal]]; suplantar conserva la identidad de Plataforma |
| MFA obligatorio u opcional | **Opcional para todos los perfiles**, por decisión posterior del usuario | El acceso no se bloquea por no activar MFA; quien lo activa debe introducir un código al iniciar sesión |

## Prioridad de avance

1. **P0 Seguridad de acceso:** comprobar acceso sin MFA, activación voluntaria, código exigido después de activarlo, recuperación de un solo uso, revocación de sesiones, aislamiento y ausencia de secretos en respuestas generales. Quedan recuperación asistida y renovación del autenticador.
2. **P0 Respaldo/restauración operativo:** implementar y desplegar el trabajo diario, almacenamiento cifrado externo, custodia separada de claves, retención, alertas y restauración completa de un tenant con archivos. Medir RPO/RTO con volumen representativo. Ver [[../11-plataforma-y-operacion/procedimiento-respaldo-restauracion|Procedimiento y evidencias]].
3. **P0 Datos y auditoría:** consentimiento granular, consultas de auditoría del Rector, eliminación/retención verificadas y flujos oficiales de boletines. Una matriz de permisos no sustituye estas implementaciones.
4. **P1 Operación académica:** completar cierre/promoción, escalas por imagen, director de grupo y cobertura de consulta móvil.
5. **P1 Flujos restantes del lanzamiento:** admisiones, pagos, certificados, convivencia y exportaciones con validación oficial.
6. **P2/P3 Ampliaciones:** activarlas en una entrega definida, después de sus dependencias de identidad, consentimiento y cartera.

No se declaran cumplidos disponibilidad, protección de datos, RPO/RTO ni formato oficial por haber escrito esta documentación. Cada uno requiere su evidencia específica. El catálogo conserva algunos permisos de funciones futuras; deben rotularse y limitarse cuando se implemente cada módulo.
