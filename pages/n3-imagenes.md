---
title: Imágenes
description: Locales y externas, con o sin enlace, pequeñas o grandes.
layout: libdoc_page.liquid
permalink: /pages/n1-crear-contenido/n2-markdown/n3-imagenes/index.html
eleventyNavigation:
    key: Imágenes
    parent: Markdown
    order: 4
tags:
    - contenido
    - markdown
    - imagen
date: 2026-03-27
---
Para optimizar el rendimiento de la página y el ancho de banda, las imágenes rasterizadas como PNG, JPEG y GIF se transcodifican a los formatos [AVIF](https://en.wikipedia.org/wiki/AVIF) y [WEBP](https://en.wikipedia.org/wiki/WebP) mediante el [plugin de imágenes de Eleventy](https://www.11ty.dev/docs/plugins/image/) . Además, para garantizar la adaptabilidad, cada imagen rasterizada se transcodifica en varios archivos con diferentes anchos para ajustarse a los dispositivos de destino.

Las imágenes vectoriales SVG se utilizan tal cual.

El formato para la imágenes locales o externas es el mismo, pero las imágenes locales se optimizan automáticamente, mientras que las externas no se optimizan y se muestran tal cual.

---

# Imagen

![Imagen](/assets/imagen.png)

Para insertar una imagen se utiliza la admiración (!) seguida de corchetes [] para el texto alternativo y paréntesis () para la URL o el permalink de la página interna.
``` markdown
![Texto imagen](/assets/imagen.png)
```
---
# Imagen con enlace

[![Imagen con enlace](/assets/imagenConEnlace.png)](/n2-home.md "Enlace para ir a Navegación -> HOME")

Para insertar una imagen que también funcione como enlace, se coloca el código de la imagen dentro de los paréntesis de un enlace. 

``` markdown
[![TextImagenConEnlace](/assets/imagenConEnlace.png)]
    (enlace o permalink "Texto del enlace")
```
---
# Imagen pequeña o grande

![Imagen pequeña](/assets/imagenPequena.png)
    
*Las imágenes rasterizadas más pequeñas que el ancho del contenido principal no se visualizan correctametne en pantallas de alta densidad como Retina.*
<br><br> Se puede solucionar usando HTML: aplicando **style** con **width** y **height** en pixeles. 

<img src="/assets/imagenPequena.png" alt="Imagen pequeña" style="width: 64px; height: 64px;">

La imagen anterior tiene 256x256 pixeles y vamos a hacer que se vea como si tuviera 64x64 pixeles. También se puede hacer al contrario y que una imagen pequeña se vea más grande.

``` html
    <img src="/assets/imagenPequena.png" alt="Imagen pequeña" style="width: 64px; height: 64px;">
```
