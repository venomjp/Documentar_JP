---
title: Código
description: En línea, bloque con resaltado de sintaxis y variables.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_1-markdown/4_1_5-codigo/index.html
eleventyNavigation:
    key: Código
    parent: Markdown
    order: 5
tags:
    - contenido
    - markdown
    - resaltado de sintaxis
date: 2026-03-27
---

# Código en línea
Se crea con una sola comilla invertida ( \` )  al inicio y al final del texto que se desea formatear como código.
<br>Para ver trozos de `código pequeños` en la misma línea código en línea.

``` markdown
Para ver trozos de `código pequeños` en la misma línea código en línea.
```

# Bloque con resaltado de sintaxis
Puedes utilizar el resaltado de sintaxis, que permitirá que muestre el resaltado en los lenguajes de programación que hayas incorporado en `settings.json`.
1. Introduce tres comillas invertidas (```) seguido del [alias](https://highlightjs.readthedocs.io/en/latest/supported-languages.html) del lenguaje de programación
2. Escribe el código que quieres resaltar.
3. Finaliza con otras tres comillas invertidas (```) en una nueva línea.

Por ejemplo, para resaltar código HTML:

``` html
<h1>Hello World!</h1>
<p>This is a <a href="/link/">link</a>.</p>
```
