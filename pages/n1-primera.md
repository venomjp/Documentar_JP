---
title: Nivel 1
description: Nivel 1 de navegación entre páginas
layout: libdoc_page.liquid
permalink: /pages/n1-primera/index.html
eleventyNavigation:
    key: Nivel 1. Primera
tags:
    - nivel 1
    - etiqueta 2
date: 2026-03-20
---
Hola soy una página de nivel 1. 

Vamos a una página hijo con referencia a la plantilla de origen [Nivel 2]( ./n2-primera.md "Hacia adelante = hija").
Este otro enlace se hace con referencia a la ruta relativa (que ya lleva pathPrefix) [Nivel 2](./n2-primera/ "Hacia adelante=hija").

```markdown
Para bajar un nivel, se puede hacer referenciando la plantilla de origen
[página nivel 2](n2-segunda.md "También cambia a nivel inferior").
```