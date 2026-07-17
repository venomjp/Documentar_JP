---
title: Tarjeta con icono
description: Resalta facilmente la información con un icono, un texto principal y una descripción.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_3-widgets/4_3_8-tarjetaIcono/index.html
eleventyNavigation:
    key: Tarjeta con icono
    parent: Widgets
    order: 6
tags:
    - contenido
    - widgets
    - tarjeta con icono
    - icono
date: 2026-03-31
---
# Formato

Utiliza el siguiente formato: 

`{% raw %}{% iconCard '<TÍTULO>', '<CONTENIDO>', '<NOMBRE_ICONO>' %}{% endraw %}`.


* `<TÍTULO>` - *OBLIGATORIO*. Es una cadena de texto con el título de la tarjeta.
* `<CONTENIDO>` *OBLIGATORIO*. Es una cadena de texto con el contenido que deseas mostrar dentro, puede ser markdown o HTML.
* `<NOMBRE_ICONO>` es el nombre del icono que quieres usar, puede ser:
    * Un icono de la [lista](./4_3_5-iconos.md#lista-de-iconos-del-sistema) del sistema.
    * {% iconCard 'Tarjeta con icono', 'Facilmente resalta algo importante de manera simple con un icono, un texto principal y su descripción.', 'code' %}
    * Un icono personalizado (SVG, PNG o AVIF). 
    * {% iconCard 'Icono personalizado', 'Agrega tu propio icono, SVG o raster de transparencia (PNG y AVIF).', '/assets/logo-11ty.svg' %}
    * Si no se indica se le asigna el icono por defecto (tick dentro de un círculo).
    * {% iconCard 'Icono por defecto', 'Si no se establece un nombre de icono válido, se aplica el icono por defecto, que es este.' %}

```markdown
{% raw %}{% iconCard 'Tarjeta con icono', 'Facilmente resalta algo importante de manera simple con un icono, un texto principal y su descripción.', 'code' %}
{% iconCard 'Icono por defecto', 'Si no se establece un nombre de icono válido, se aplica el icono por defecto, que es este.' %}
{% iconCard 'Icono personalizado', 'Agrega tu propio icono, SVG o raster de transparencia (PNG y AVIF).', '/assets/logo-11ty.svg' %}{% endraw %}
```

# Uso
{% iconCard 'Formas de uso', 'Las tarjetas de iconos pueden usarse en listas (ordenada y NO ordenada) como la anterior o se pueden usar de manera independiente, como esta.', 'user' %}
