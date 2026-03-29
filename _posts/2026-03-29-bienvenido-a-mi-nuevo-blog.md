---
layout: post
title: "Bienvenido a mi nuevo blog"
date: 2026-03-29 12:00:00 +0100
categories: general
tags: [bienvenida, blog, github-pages]
excerpt: "Estreno de mi blog migrado de WordPress a GitHub Pages con Jekyll."
---

¡Bienvenidos a la nueva versión de mi blog!

He migrado este blog de **WordPress** a **GitHub Pages** usando [Jekyll](https://jekyllrb.com/). Este cambio me permite:

- Escribir posts en **Markdown** de forma sencilla
- Tener el blog completamente **gratuito** en GitHub
- **Control total** sobre el código y el contenido
- **Versionado** de todos los cambios con Git
- Carga muy rápida al ser un sitio estático

## ¿Por qué GitHub Pages?

GitHub Pages genera páginas estáticas a partir de ficheros Markdown. Sin bases de datos, sin plugins pesados, sin mantenimiento de servidor.

## ¿Cómo escribir un nuevo post?

Basta con crear un fichero en la carpeta `_posts/` con el formato:

```
YYYY-MM-DD-titulo-del-post.md
```

Y añadir al principio del fichero el **front matter** en YAML:

```yaml
---
layout: post
title: "Título del post"
date: 2026-03-29 12:00:00 +0100
categories: general
tags: [tag1, tag2]
---
```

A continuación, escribe el contenido en Markdown. ¡Así de sencillo!
