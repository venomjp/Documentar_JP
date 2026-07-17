---
title: Iconos
description: Código para crear iconos y mejorar la visualización del contenido.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_3-widgets/4_3_5-iconos/index.html
eleventyNavigation:
    key: Iconos
    parent: Widgets
    order: 5
tags:
    - contenido
    - widgets
    - iconos
date: 2026-03-30
---

# Lista de iconos del sistema

Estos son los iconos SVG incluidos, pero también puedes usar tus propios iconos.

{% icons %}

# Cómo usarlos

Utiliza el siguiente formato: 

`{% raw %}{% icon '<NOMBRE_ICONO>', <TAMAÑO_ICONO> %}{% endraw %}`.

*El tamaño del icono se basa en la propiedad CSS font-size.*

* `<NOMBRE_ICONO>` es el nombre del icono que quieres usar, puede ser:
    * Un icono de la lista del sistema.
    * Un [icono personalizado](#icono-personalizado) a través de una ruta local o una URL remota a un SVG, PNG o AVIF.
* `<TAMAÑO_ICONO>` es opcional, debe ser un entero de 1 a 10.

# Tamaño de icono

* **HEREDADO** 

    El tamaño predeterminado de icono es `1em`

    {% icon 'rocket' %}

    ``` liquid
    {% raw %}
    {% icon 'rocket' %}
    {% endraw %}
    ```
* **TAMAÑO FIJO** 
    
    {% icon 'rocket', 1 %}
    {% icon 'rocket', 2 %}
    {% icon 'rocket', 3 %}
    {% icon 'rocket', 4 %}
    {% icon 'rocket', 5 %}
    {% icon 'rocket', 6 %}
    {% icon 'rocket', 7 %}
    {% icon 'rocket', 8 %}
    {% icon 'rocket', 9 %}
    {% icon 'rocket', 10 %}

    ``` liquid
    {% raw %}
    {% icon 'rocket', 1 %}
    {% icon 'rocket', 2 %}
    {% icon 'rocket', 3 %}
    {% icon 'rocket', 4 %}
    {% icon 'rocket', 5 %}
    {% icon 'rocket', 6 %}
    {% icon 'rocket', 7 %}
    {% icon 'rocket', 8 %}
    {% icon 'rocket', 9 %}
    {% icon 'rocket', 10 %}
    {% endraw %}
    ```

* **PERSONALIZADO** 

    Puedes establecer tu propio tamaño a través de la propiedad `font-size` del elemento padre, por ejemplo:

    <div style="font-size: 100px">
        {% icon 'rocket' %}
    </div>

    ``` html
    <div style="font-size: 100px">
        {% raw %}{% icon 'rocket' %}{% endraw %}
    </div>
    ```
# Icono personalizado

Puedes usar tu propio icono. El widget soporta tanto imágenes SVG, PNG y AVIF con transparencia. Puedes acceder a la imagen local o remota a través de una URL.

<table>
    <tr>
        <td>SVG Local</td>
        <td>
            {% icon '/assets/logo-11ty.svg', 10 %}
        </td>
        <td><code>{% raw %}{% icon '/assets/logo-11ty.svg', 10 %}{% endraw %}</code></td>
    </tr>
    <tr>
        <td>SVG Remoto</td>
        <td>
            {% icon 'https://cdn.jsdelivr.net/gh/ita-design-system/ita-medias@main/logo-11ty.svg', 10 %}
        </td>
        <td><code>{% raw %}{% icon 'https://cdn.jsdelivr.net/gh/ita-design-system/ita-medias@main/logo-11ty.svg', 10 %}{% endraw %}</code></td>
    </tr>
    <tr>
        <td>PNG Local</td>
        <td>
            {% icon '/assets/logo-11ty.png', 10 %}
        </td>
        <td><code>{% raw %}{% icon '/assets/logo-11ty.png', 10 %}{% endraw %}</code></td>
    </tr>
    <tr>
        <td>PNG Remoto</td>
        <td>
            {% icon 'https://cdn.jsdelivr.net/gh/ita-design-system/ita-medias@main/logo-11ty.png', 10 %}
        </td>
        <td><code>{% raw %}{% icon 'https://cdn.jsdelivr.net/gh/ita-design-system/ita-medias@main/logo-11ty.png', 10 %}{% endraw %}</code></td>
    </tr>
    <tr>
        <td>AVIF Local</td>
        <td>
            {% icon '/assets/logo-11ty.avif', 10 %}
        </td>
        <td><code>{% raw %}{% icon '/assets/logo-11ty.avif', 10 %}{% endraw %}</code></td>
    </tr>
    <tr>
        <td>AVIF Remoto</td>
        <td>
            {% icon 'https://cdn.jsdelivr.net/gh/ita-design-system/ita-medias@main/logo-11ty.avif', 10 %}
        </td>
        <td><code>{% raw %}{% icon 'https://cdn.jsdelivr.net/gh/ita-design-system/ita-medias@main/logo-11ty.avif', 10 %}{% endraw %}</code></td>
    </tr>
</table>

*Como se aprecia en la tabla, las imagenes remotas aunque si existen y están disponibles, se muestran en VS-Code al editar el código, pero no se muestran al generar la página ni en local ni en GitHub Pages. Desconozco el motivo y no lo he podido corregir.*

# Color personalizado

El color del icono también se hereda y se puede personalizar de la siguiente manera:

{% alert 'Asignar un color personalizado puede provocar un mal contraste con el cambio de color entre modo claro y oscuro', 'warning', 'Problema de contraste de color' %}

<div style="color: fuchsia">
    {% icon '/assets/logo-11ty.avif', 10 %}
</div>


``` liquid
<div style="color: fuchsia">
    {% raw %}{% icon '/assets/logo-11ty.avif', 10 %}{% endraw %}
</div>
```