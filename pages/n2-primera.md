---
title: Primera página de nivel 2
description: Soy una página de nivel 2
layout: libdoc_page.liquid
permalink: /pages/n1-primera/n2-primera/index.html
eleventyNavigation:
    key: Nivel 2. Primera
    parent: Nivel 1. Primera
tags:
    - nivel 2
    - blockquote
---
A continuación una cita:

> Hola! soy una página de nivel 2, hija de una de nivel 1
> 
> ― **Child**

Vamos hacia atrás [página de nivel 1](../n1-primera/ "Hacia atrás") o hacia adelante [página de nivel 3](./n3-primera/ "Vamos hacia adelante = hija").

A continuación un texto en Markdown:

```markdown
> Así se escriben las citas en Markdown.
> 
> ― **Cita**

Ir hacia atrás con rutas relativas (..):
[página de nivel 1](../n1-primera/ "Hacia atrás")
Ir hacia atrás con rutas absolutas y pathPrefix:
[página de nivel 1]({{ 'pages/n1-primera/' | url }} "Hacia atrás")
Sin poner / delante y usará pathPrefix 2 veces

Ir hacia adelante con ruta relativa:
./pagina-siguiente/
```