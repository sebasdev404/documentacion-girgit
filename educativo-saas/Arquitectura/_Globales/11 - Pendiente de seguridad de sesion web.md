# Pendiente de seguridad: sesión web y suplantación

Estado revisado el 29 de septiembre de 2026. Esta nota distingue lo implementado de lo que falta; no declara la autenticación actual como cifrada en el navegador.

## Estado actual

- El selector de año lectivo de las vistas académicas usa en la URL un valor opaco derivado mediante HMAC y vinculado al tenant. Evita mostrar el ID numérico en `?ano=`, pero no sustituye la autorización del backend ni cifra el resto de las peticiones.
- El frontend aún guarda el token de autenticación en `localStorage`. Durante la suplantación guarda allí también el token temporal y el ID del colegio activo. Varias rutas internas de la API usan IDs numéricos; estos no son contraseñas y ocultarlos por sí solo no protege los datos.
- El acceso sigue dependiendo de la autenticación, los permisos y el aislamiento por tenant en el servidor. No se debe interpretar el selector opaco como una barrera de acceso.

## Por qué no se «cifra» simplemente `localStorage`

Una clave incorporada en JavaScript quedaría disponible para el mismo código del navegador que lee `localStorage`. Ante una inyección de scripts, el atacante podría recuperar la clave o usar directamente la sesión. Ese cambio solo daría una falsa sensación de seguridad y podría romper la apertura en nuevas pestañas o la suplantación.

## Trabajo pendiente para una solución real

1. Diseñar sesiones de autenticación y suplantación administradas por el servidor, entregadas mediante cookies `HttpOnly`, `Secure` y `SameSite` apropiado para los dominios del colegio y las sedes. Definir caducidad, rotación y revocación.
2. Incorporar protección CSRF para operaciones que cambian datos y revisar CORS, dominios y el cierre de sesión en todas las pestañas.
3. Migrar el cliente y los flujos de inicio de sesión, MFA, cambio de colegio y apertura de nuevas pestañas; retirar tokens y el ID del colegio de `localStorage` sin invalidar sesiones de forma inesperada.
4. Mantener y probar autorización por rol, alcance de tenant y auditoría en cada endpoint. Un ID o un token opaco en una URL nunca debe conceder acceso por sí mismo.
5. Verificar los flujos anteriores en PostgreSQL de staging con varios colegios y sedes antes de desplegar a producción.

Este trabajo se deja para una fase de autenticación coordinada entre frontend, backend y despliegue. No está implementado por el cambio del selector de año lectivo.
