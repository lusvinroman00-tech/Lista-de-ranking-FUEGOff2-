# FUEGOff2 – Seguidores Fieles (sitio online)

Este paquete contiene el sitio estático listo para publicar en Netlify y el esquema inicial para Supabase.

## Archivos
- `index.html`: sitio público de rankings y acceso privado de administrador.
- `supabase/schema.sql`: tablas, índices y políticas de seguridad (RLS).

## 1. Crear el proyecto Supabase
1. Crea un proyecto nuevo en Supabase.
2. Abre SQL Editor y ejecuta todo el contenido de `supabase/schema.sql`.
3. En Authentication > Users, crea tu usuario administrador con tu correo y contraseña.
4. Copia el UUID de ese usuario.
5. En SQL Editor ejecuta:
   ```sql
   insert into public.admins (user_id) values ('PEGA-AQUI-EL-UUID');
   ```
   Sustituye el texto por el UUID real.

## 2. Configurar el sitio
1. Abre `index.html` con un editor de texto.
2. Busca `PEGA_AQUI_TU_SUPABASE_URL` y reemplázalo por la URL del proyecto.
3. Busca `PEGA_AQUI_TU_CLAVE_PUBLICA` y reemplázalo por la clave pública (publishable key o anon key).
4. Nunca uses la clave `service_role` ni una clave secreta en el navegador.

## 3. Publicar en Netlify
1. En Netlify crea un sitio nuevo mediante deploy manual.
2. Sube `index.html` (puedes subir la carpeta del proyecto descomprimida).
3. Netlify publicará el sitio y te dará una dirección `*.netlify.app`.

## Cómo funciona
- Los visitantes pueden ver rankings y actividad, pero no modificar datos.
- Solo el usuario autenticado cuyo UUID esté en `public.admins` puede registrar, editar o borrar interacciones.
- YouTube cuenta comentarios; Facebook, Instagram y TikTok cuentan comentarios, compartidos y likes.
- Cada acción suma 1 punto.
- Se rechaza repetir la misma acción de una persona en la misma publicación.
- Los períodos diario, semanal, mensual, anual y permanente se calculan con la fecha registrada.

## Límites de esta primera versión
- El registro de interacciones es manual.
- Los rankings se actualizan al cargar la página; para refrescar los datos, recarga el sitio.
- No incluye todavía edición/borrado desde el panel visual, solo políticas seguras en la base de datos.
- La clave pública de Supabase está diseñada para usarse en el navegador con RLS correctamente activado.
