---
title: Definición
description: Código para crear términos y definiciones.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_3-widgets/4_3_3-definicion/index.html
eleventyNavigation:
    key: Definición
    parent: Widgets
    order: 3
tags:
    - contenido
    - widgets
    - definición
date: 2026-03-30
---

Las definiciones son elementos que permiten explicar términos o conceptos específicos dentro de la documentación. 

Se pueden crear utilizando la etiqueta `<dl>` (definición de lista) junto con `<dt>` (término de definición) y `<dd>` (descripción de definición).

``` html
<dl class="definition">
    <dt>TERMINO</dt>
    <dd>Definición del término.</dd>
</dl>
```
Visualmente, las definiciones se presentan como un bloque con el término destacado en azul y la descripción debajo.

<dl class="definition">
    <dt>Markdown</dt>
    <dd>Markdown es un lenguaje de marcado ligero para crear texto formateado utilizando un editor de texto plano. John Gruber creó Markdown en 2004 como un lenguaje de marcado fácil de leer.</dd>
    <dt>Término</dt>
    <dd>Se pueden enlazar definiciones ya que es una lista.</dd>
    <dt>HTML</dt>
    <dd>El lenguaje de marcado de hipertexto (HTML) es el lenguaje de marcado estándar para documentos diseñados para ser visualizados en un navegador web.
    </dd>
</dl>

``` html
<dl class="definition">
    <dt>Markdown</dt>
    <dd>Markdown es un lenguaje de marcado ligero para crear texto formateado
        utilizando un editor de texto plano. John Gruber creó Markdown en 2004 
        como un lenguaje de marcado fácil de leer.</dd>
        <dt>Término</dt>
    <dd>Se pueden enlazar definiciones ya que es una lista.</dd>
    <dt>HTML</dt>
    <dd>El lenguaje de marcado de hipertexto (HTML) es el lenguaje de marcado 
        estándar para documentos diseñados para ser visualizados en un navegador 
        web.</dd>
</dl>
```

