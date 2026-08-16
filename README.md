# ATPL Planner — despliegue independiente

App estática (un solo `index.html`, sin build, sin backend propio). Habla
directo con Supabase desde el navegador. Vercel solo sirve el archivo.

## 1. Supabase (cuenta/proyecto nuevo)

1. Ve a supabase.com y crea una cuenta nueva (o un proyecto nuevo si ya
   tienes cuenta, pero **no uses el mismo proyecto que Docentium**).
2. Crea el proyecto, espera a que arranque.
3. `SQL Editor` → `New query` → pega el contenido de `supabase-schema.sql`
   → `Run`.
4. `Project Settings` → `API` → copia:
   - `Project URL`
   - `anon public` key

## 2. GitHub (cuenta/repo nuevo)

1. Crea una cuenta de GitHub nueva si quieres separarlo del todo, o un
   repo nuevo en tu cuenta actual — **no lo metas en el repo de Docentium**.
2. Repo nuevo, por ejemplo `atpl-planner`.
3. Sube estos 3 archivos tal cual (`index.html`, `supabase-schema.sql`,
   `README.md`) a la raíz del repo. Puedes arrastrarlos directamente desde
   la web de GitHub ("Add file → Upload files"), no hace falta terminal.

## 3. Vercel (cuenta/proyecto nuevo)

1. Ve a vercel.com y entra con una cuenta nueva, o con tu cuenta actual
   pero creando un **proyecto nuevo** separado del de Docentium.
2. `Add New → Project` → conecta tu GitHub → selecciona el repo
   `atpl-planner`.
3. Vercel detecta que es estático — no toques ninguna configuración,
   dale directamente a `Deploy`.
4. En un minuto tienes una URL tipo `atpl-planner.vercel.app`.

## 4. Conectar la app con Supabase

1. Abre tu URL de Vercel.
2. Pulsa `⚙ Supabase` arriba a la derecha.
3. Pega la `Project URL` y la `anon public key` del paso 1.
4. "Guardar y sincronizar".

A partir de aquí, cada dispositivo/navegador desde el que entres a esa
URL necesita pegar esa misma URL + clave una vez (se queda guardada en
ese navegador). Si prefieres que ya venga conectado sin tener que
configurarlo cada vez, dile a Claude que las meta directamente en el
`index.html` antes de subirlo — así todo el mundo que abra la URL se
conecta solo, sin tocar el panel de ajustes.

## Nota de seguridad

La clave `anon public` es pública por diseño (así funciona Supabase
desde el navegador), pero la tabla `atpl_planner_logs` queda abierta a
quien tenga esa clave (política RLS permisiva, ver el `.sql`). Vale para
uso personal; no compartas la URL de Vercel si no quieres que nadie más
pueda leer o escribir tu progreso.
