---
title: Embebido
description: Código para embeber contenido externo.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_3-widgets/4_3_6-embebido/index.html
eleventyNavigation:
    key: Embebido
    parent: Widgets
    order: 7
tags:
    - contenido
    - widgets
    - embebido
date: 2026-03-30
---

# Filtro embebido simple
Convierte automáticamente URLs (youtube, mapa, documentos) en contenido embebido y visualizable directamente en nuestra página web.

Formato: 

`{% raw %}{{ '<Dirección_URL_con_comillaInglesa>' | embed }}{% endraw %}`

Es importante que la URL esté entre comillas inglesas simples, de lo contrario el filtro no funcionará, también son importantes los espacios antes y después de la tubería `|` y el filtro `embed`, si no se respetan el filtro no funcionará y las llaves son dobles.

He tenido problemas para incrustar un vídeo de Youtube directamente con su dirección URL. He encontrado 2 formas de hacerlo:
1. Usando el código de embebido proporcionado por Youtube, selecciona **compartir** en el vídeo y aparece el código completo para embeberlo. <br>
    ``` html
    <iframe width="560" height="315" 
    src="https://www.youtube.com/embed/tCk_4b6nM2o?si=4kmp_JS0IY4vSP57" 
    title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; 
    clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
    referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
    </iframe>
    ```
2. Añadiendo la palabra "embed" despues de ```www.youtube.com/``` y antes del código del vídeo. También puedes añadir ```?controls=0``` al final de la URL para ocultar los controles del vídeo.<br>

<br>{{ 'https://www.youtube.com/embed/tCk_4b6nM2o' | embed }}

```liquid
{% raw %}{{ 'https://www.youtube.com/embed/tCk_4b6nM2o' | embed }}{% endraw %}
```

# Shortcode embebido

También se puede usar shortcode para embeber contenido, en principio la diferencia con el filtro anterior es que el shortcode genera HTML completo, mientras que el filtro solo transforma los datos de la URL en un formato que el navegador pueda interpretar como contenido embebido.

Formato:

`{% raw %}{% embed "Dirección_URL_entreComillas" %}{% endraw %}`

Como en el caso anterior, hay que añadir ```/embed``` después de la URL para que funcione correctamente. 

Se puede moficar la altura añadiendo un valor al final de la instrucción, en este caso el valor es ```500```.

{% embed "https://sketchfab.com/3d-models/batman-v-superman-batmobile-abea4cdb296f4fafab03a404e515c109/embed", 500 %}

``` liquid
{% raw %}{% embed "https://sketchfab.com/3d-models/
batman-v-superman-batmobile-abea4cdb296f4fafab03a404e515c109/embed", 500 %}{% endraw %}
```
{% embed "https://sketchfab.com/3d-models/the-batman-begin-tumbler-83b64fe11adc43dba84a3f27aa0e7ec1/embed", 500 %}