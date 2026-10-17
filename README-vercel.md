# IONES — Desplegar el sitio en Vercel (gratis)

Esta carpeta contiene lo mínimo para subir la página a Vercel: `index.html`
(tu página IONES) y `vercel.json` (configuración básica). No necesitas build,
es HTML puro.

## Antes de subir

Abre `index.html` y confirma que ya pusiste:
- Tu **Client ID** real de PayPal en la línea del `<script src="...paypal.com/sdk/js?client-id=...">`
- Los **Plan ID** reales en cada `data-planid="..."` de los 4 planes

(Si aún no los tienes, sigue el README del backend que ya te di — paso 2.)

## Opción A — Sin usar terminal (más fácil, recomendada)

1. Crea cuenta gratis en **https://vercel.com** (puedes entrar con GitHub, GitLab o email).
2. Sube tu carpeta a un repositorio de GitHub:
   - Ve a **https://github.com/new**, crea un repo llamado por ejemplo `iones-web`.
   - Sube ahí los archivos `index.html` y `vercel.json` (botón "Add file" → "Upload files" en GitHub, arrastras los 2 archivos, y "Commit changes").
3. En Vercel, da clic en **Add New... → Project**.
4. Selecciona **Import Git Repository** y elige el repo `iones-web` que acabas de crear.
5. Vercel detecta que es un sitio estático — deja todo por defecto y da clic en **Deploy**.
6. En menos de un minuto te da una URL tipo `https://iones-web.vercel.app` — esa ya es tu página en vivo.

## Opción B — Con la terminal (más rápida si te sientes cómodo)

```bash
npm install -g vercel
cd iones-site
vercel login
vercel --prod
```
Te va a preguntar el nombre del proyecto y confirmar la carpeta — acepta los valores por defecto. Al terminar te da la URL de producción directo.

## Conectar tu propio dominio (iones.mx, o el que tengas)

1. En el panel de Vercel, entra a tu proyecto → **Settings → Domains**.
2. Escribe tu dominio (ej. `iones.mx` o `www.iones.mx`) y da **Add**.
3. Vercel te muestra un registro DNS (tipo **A** o **CNAME**) que debes agregar
   donde tengas comprado el dominio (Hostinger, GoDaddy, Namecheap, etc.).
   - Si el dominio está en Hostinger: entra a **hPanel → Dominios → DNS / Nameservers**
     y agrega el registro exactamente como te lo indica Vercel.
4. Espera unos minutos a que propague — Vercel activa HTTPS automático.

## Actualizar la página después

Cada vez que cambies `index.html` (por ejemplo si subes nuevos precios),
solo tienes que:
- **Opción A:** subir el archivo actualizado a GitHub (Vercel redeploya solo).
- **Opción B:** correr `vercel --prod` otra vez desde la carpeta.

## Y el backend de cobros (PayPal)

Este despliegue en Vercel es solo la página (`index.html`). El backend que
recibe los webhooks de PayPal (`iones-backend`) va aparte — te recomendé
**Render.com** para eso porque necesita correr un proceso Node de forma
continua, cosa que el plan gratis de Vercel no está pensado para hacer bien
en este caso (guardado de archivo, procesos largos). Si en algún momento
quieres intentar meter también el backend en Vercel como funciones
serverless, dime y te lo adapto — pero implica cambiar el guardado del
archivo JSON por una base de datos externa gratuita (por ejemplo Supabase),
porque el sistema de archivos de Vercel no es persistente entre llamadas.
