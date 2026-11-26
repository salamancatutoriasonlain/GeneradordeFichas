# Generador de fichas · SALAMANCA Tutorías Online

Web estática (sin compilación): portada, generador en línea y página de descargas.

```
wrangler.jsonc        configuración de Cloudflare (apunta a la carpeta public)
public/               la web completa:
  index.html            portada
  generador/index.html  el generador (un solo archivo, funciona sin conexión)
  descargas/            página de descargas + paquete del Mac G5
  assets/               logotipo, estilos, imágenes
  _headers              cabeceras de seguridad y caché
  404.html  robots.txt
```

## Publicar en GitHub

1. En GitHub: **New repository** → nombre p. ej. `generador-fichas` → *Create repository* (sin README).
2. En una terminal, dentro de esta carpeta:
   ```
   git init
   git add .
   git commit -m "Web del generador de fichas"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/generador-fichas.git
   git push -u origin main
   ```
   (O arrastra los archivos desde el navegador con **Add file → Upload files**.)

## Publicar en Cloudflare

1. Cloudflare → **Workers & Pages → Create → Import a repository (Connect to Git)** y elige el repositorio.
2. Si te pide configuración:
   - **Build command:** *(vacío)*
   - **Deploy command:** `npx wrangler deploy` (ya viene así por defecto; usa `wrangler.jsonc`)
   - **Si es un proyecto de *Pages* clásico:** Framework *None*, Build output directory **`public`**.
3. **Save and Deploy**. Cada `git push` la actualiza. Quedará en una dirección `*.workers.dev` o `*.pages.dev`.
4. Dominio propio (opcional): *Settings → Domains & Routes → Add*.

**Si ves «Could not detect a directory containing static files»:** los archivos `index.html` deben estar dentro de la carpeta `public/` en la raíz del repositorio (no una carpeta más abajo). Comprueba en GitHub que ves `public/index.html` y `wrangler.jsonc` en la raíz.

## Las descargas de Windows y Linux (archivos de ~100–150 MB)

Cloudflare Pages admite archivos de hasta 25 MB y GitHub de 100 MB, así que los instaladores **no van en el repositorio**:

1. En GitHub: **Releases → Draft a new release** (etiqueta `v1.1`), arrastra `Generador_Fichas_SALAMANCA_Windows.zip`, `..._Linux.deb` y `..._Linux.AppImage`, y **Publish release**.
2. En `public/descargas/index.html` sustituye `TU_USUARIO/TU_REPOSITORIO` por los tuyos (hay 2 enlaces). Haz `git commit` y `git push`.

## Imagen al compartir en redes

Para que `og:image` funcione al compartir enlaces, cambia en los `<head>` la ruta relativa
`/assets/og.png` (en `public/`) por la absoluta, p. ej. `https://TU-DOMINIO/assets/og.png`.
