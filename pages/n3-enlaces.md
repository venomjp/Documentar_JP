---
title: Enlaces
description: Tipos de enlaces.
layout: libdoc_page.liquid
permalink: /pages/n1-crear-contenido/n2-markdown/n3-enlaces/index.html
eleventyNavigation:
    key: Enlaces
    parent: Markdown
    order: 3
tags:
    - contenido
    - markdown
    - enlaces
date: 2026-03-27
---
<dl>
    <dt>Permalink</dt>
    <dd>En el encabezado (front matter) de las plantillas que luego se convertirán en páginas web podemos utilizar la funcionalidad de <b>permalink</b> que define la ruta URL final de salida del archivo generado, sobreescribiendo la estructura de directorios predeterminada. </dd>
</dl>


* **Enlace EXTERNO** es aquel que apunta a una URL fuera del sitio web.
* **Enlace INTERNO** es aquel que apunta a otra página dentro del mismo sitio web.  
  * Pueden ser estáticos (permalink).
  * O dinámicos (usando el nombre de la plantilla `*.md`).

* Se crean con corchetes [] para el texto del enlace y paréntesis () para la URL o el permalink de la página interna.

    ``` markdown
    [Enlace a Google](https://www.google.com)
    [Enlace a página interna](./n2-html.md).
    ```
