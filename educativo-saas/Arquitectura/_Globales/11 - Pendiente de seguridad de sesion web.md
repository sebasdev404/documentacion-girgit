# Estado de seguridad de sesión web y selectores públicos

**Corte:** 30 de septiembre de 2026. Esta nota actualiza el estado del 29 de septiembre: la migración del navegador a cookies y los selectores opacos ya se implementaron localmente en `pedro-dev`.

## Implementado y comprobado localmente

- La sesión de navegador utiliza cookie HttpOnly, CSRF y comprobación de origen. El cliente limpia credenciales y datos de suplantación heredados de `localStorage`; solo persisten preferencias no sensibles.
- La suplantación mantiene su estado en el servidor y los canales privados de Reverb comprueban identidad y colegio.
- La API académica pública rechaza rutas numéricas y claves `id`/`*_id` en consultas y cuerpos. Usa selectores opacos estables de 24 caracteres ligados al colegio y tipo de recurso. El modo numérico heredado solo funciona en `testing` con cabecera explícita para pruebas antiguas.
- La plataforma usa `slug`, `key` o token público para colegios, planes, roles, sedes, usuarios y archivos. Las respuestas de auditoría eliminan claves internas.
- La autorización se verifica por sesión, permiso, colegio y recurso; conocer un token no concede acceso. Las pruebas incluyen rechazos entre colegios, permisos y rutas numéricas.
- Las cargas aplican permiso, tamaño, cuota y escáner. En producción se rechazan cuando ClamAV no está disponible.

La evidencia técnica está en `colegio-saas-backend/docs/SEGURIDAD_API.md` y en pruebas como `BrowserCookieAuthTest`, `RequireOpaqueAcademicContractTest`, `ColegioPublicSelectorTest` y `StoredFilePublicTokenTest`. En el corte se ejecutaron 206 pruebas backend (1443 aserciones), 20 frontend, compilación y recorridos de navegador; `composer audit` y `npm audit` no reportaron avisos.

## Pendientes por momento

| Momento | Tarea | Motivo |
|---|---|---|
| Antes de producción | HTTPS, cookies y orígenes seguros, secretos y rotación, ClamAV real, copias externas y restauración ensayada, Reverb/colas/scheduler supervisados. | La configuración local no acredita la operación segura. Sin escáner, la carga falla cerrada. |
| Antes de grandes catálogos | Indexar la resolución de algunos tokens y medir latencia. | La búsqueda actual recorre registros de una consulta limitada al colegio. |
| Tras migrar clientes externos | Retirar la compatibilidad Bearer heredada. | El navegador ya usa cookies, pero podrían existir otros clientes. |
| Continuo | Revisar autorización por objeto, rol y colegio en cada ruta nueva, con pruebas negativas. | Los tokens no reemplazan permisos. |

El selector opaco reduce la exposición y enumeración trivial de claves internas. No oculta el servidor, no es una credencial ni permite declarar seguridad absoluta o disponibilidad productiva.
