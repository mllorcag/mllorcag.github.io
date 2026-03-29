# Guía de migración: WordPress → GitHub Pages (Jekyll)

Esta guía explica paso a paso cómo exportar tus posts de WordPress e importarlos a este blog Jekyll.

---

## Paso 1: Exportar el contenido de WordPress

1. En tu panel de WordPress, ve a **Herramientas → Exportar**.
2. Selecciona **Todo el contenido** (o solo "Entradas" si solo quieres los posts).
3. Haz clic en **Descargar archivo de exportación**.  
   Obtendrás un fichero `.xml` (formato WXR — WordPress eXtended RSS).

---

## Paso 2: Convertir el XML de WordPress a posts de Jekyll

Usa el conversor oficial de Jekyll:

```bash
# Instala Ruby y Jekyll si no los tienes
gem install jekyll bundler

# Instala el importador de WordPress
gem install jekyll-import

# Convierte el fichero XML exportado
ruby -r rubygems -e 'require "jekyll-import";
  JekyllImport::Importers::WordpressDotCom.run({
    "source" => "wordpress-export.xml",
    "no_fetch_images" => false,
    "assets_folder" => "assets/images"
  })'
```

Esto genera automáticamente los ficheros `.md` en la carpeta `_posts/` y descarga las imágenes a `assets/images/`.

> **Alternativa online:** Puedes usar [wordpress-to-jekyll-exporter](https://github.com/benbalter/wordpress-to-jekyll-exporter), un plugin de WordPress que exporta directamente en formato Jekyll con un solo clic.

---

## Paso 3: Revisar los posts generados

Cada post generado tendrá un **front matter** similar a este:

```yaml
---
layout: post
title: "Título del post"
date: 2023-05-15 10:30:00 +0200
categories: [categoria1, categoria2]
tags: [tag1, tag2]
---
```

Revisa los posts para asegurarte de que:
- El formato de las fechas es correcto (`YYYY-MM-DD HH:MM:SS +ZONA`)
- Los nombres de fichero siguen el patrón `YYYY-MM-DD-slug-del-post.md`
- Las imágenes se referencian con rutas relativas correctas
- El HTML del contenido se ha convertido a Markdown limpio

---

## Paso 4: Imágenes y media

Las imágenes de WordPress se guardan en `/wp-content/uploads/`. Tienes dos opciones:

**Opción A – Descargar las imágenes al repo:**
```bash
# El importador ya las descarga si no usas --no_fetch_images
# Muévelas a assets/images/ y actualiza las rutas en los posts
```

**Opción B – Mantener las URLs de WordPress:**  
Si tu sitio WordPress sigue activo durante la transición, puedes dejar las URLs de imágenes tal cual en los posts. Migra las imágenes más adelante.

---

## Paso 5: Publicar en GitHub Pages

1. Añade los ficheros generados a este repositorio:
   ```bash
   git add _posts/ assets/images/
   git commit -m "Migrar posts desde WordPress"
   git push origin main
   ```

2. GitHub Pages reconstruirá el sitio automáticamente en pocos segundos.

3. Tu blog estará disponible en: `https://mllorcag.github.io`

---

## Paso 6 (Opcional): Redireccionamientos

Si quieres mantener las URLs antiguas de WordPress funcionando, usa el plugin `jekyll-redirect-from`:

1. Añade al `_config.yml`:
   ```yaml
   plugins:
     - jekyll-redirect-from
   ```

2. En cada post, añade al front matter:
   ```yaml
   redirect_from:
     - /2023/05/15/titulo-del-post/    # URL antigua de WordPress
   ```

---

## Paso 7 (Opcional): Dominio personalizado

Si tienes un dominio propio (p.ej. `www.miblog.es`):

1. Crea el fichero `CNAME` en la raíz del repositorio con tu dominio:
   ```
   www.miblog.es
   ```

2. En tu proveedor de DNS, añade un registro CNAME:
   ```
   www  →  mllorcag.github.io
   ```

3. En GitHub: **Settings → Pages → Custom domain**, introduce tu dominio.

---

## Recursos útiles

- [Documentación oficial de Jekyll](https://jekyllrb.com/docs/)
- [GitHub Pages + Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll)
- [jekyll-import (importador WordPress)](https://import.jekyllrb.com/docs/wordpressdotcom/)
- [wordpress-to-jekyll-exporter (plugin WP)](https://github.com/benbalter/wordpress-to-jekyll-exporter)
- [Tema Minima (usado en este blog)](https://github.com/jekyll/minima)
