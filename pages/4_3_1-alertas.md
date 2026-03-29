---
title: Alertas
description: Código para crear alertas y resaltar información importante.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_3-widgets/4_3_1-alertas/index.html
eleventyNavigation:
    key: Alertas
    parent: Widgets
    order: 1
tags:
    - contenido
    - widgets
    - alertas
date: 2026-03-29
---
Las alertas permiten resaltar información importante o advertencias en tu sitio web.

# PARTES DE LAS ALERTAS

* ```<CONTENIDO>``` - OBLIGATORIO. Es una cadena de texto con el contenido que deseas mostrar dentro, puede ser markdown o HTML.
* ```<TIPO>``` - *Opcional*. Es una cadena de texto que define el tipo de alerta:  
  * ```info``` - Color *azul* de información, valor por defecto si no se especifica el tipo.
  * ```success``` - Color *verde* de éxito.
  * ```warning``` - Color *amarillo* de advertencia.
  * ```danger``` - Color *rojo* de error.
* ```<TITULO>``` - *Opcional*. Es una cadena de texto que se muestra resaltado y del color del tipo de alerta, luego se muestra una línea horizontal y luego el texto de la alerta.

# ALERTAS EN UNA LÍNEA

Se pueden escribir alertas cortas en una sola línea, con el formato: 

``` markdown
{% raw %}{% alert "<CONTENIDO>', "<TIPO>", "<TITULO>" } {% endraw %}
```

{% alert "Esta es una alerta de **información**, de color AZUL", "info", "Alerta de información" %}
{% alert "Esta es una alerta de **éxito**, de color VERDE", "success", "Alerta de éxito" %}
{% alert "Esta es una alerta de **advertencia**, de color AMARILLO", "warning", "Alerta de advertencia" %}
{% alert "Esta es una alerta de **error**, de color ROJO", "danger", "Alerta de error" %}

``` markdown
{% raw %}{% alert "Esta es una alerta de **información**, de color AZUL", "info", "Alerta de información" %}
{% alert "Esta es una alerta de **éxito**, de color VERDE", "success", "Alerta de éxito" %}
{% alert "Esta es una alerta de **advertencia**, de color AMARILLO", "warning", "Alerta de advertencia" %}
{% alert "Esta es una alerta de **error**, de color ROJO", "danger", "Alerta de error" %} {% endraw %}
```

# ALERTAS DE VARIAS LÍNEAS

También se pueden escribir alertas más largas que ocupen varias líneas, con el formato:

``` markdown
{% raw %}{% alertAlt "<TIPO>", "<TITULO>" %} 
CONTENIDO
EN 
VARIAS LÍNEAS
Y CON FORMATO
{% endalertAlt %}{% endraw %}
```

Este es un ejemplo de alerta de varias líneas:

{% alertAlt "success", "Alerta de éxito" %}
Esta es una alerta de **éxito**, de color VERDE.
* Puede ocupar varias líneas
* Contener formato como **negritas** o *cursivas*
* Listas como esta
* O incluso [enlaces](#)
{% endalertAlt %}

# ALERTAS EN HTML PLANO

También puedes escribir alertas utilizando HTML plano, los "\<TIPOS>" son parecidos:
* ```alert``` predeterminado sin color (gris)
* ```alert-info``` para información (azul)
* ```alert-success``` para éxito (verde)
* ```alert-warning``` para advertencia (amarillo)
* ```alert-danger``` para error (rojo)

``` html
<aside class="widget widget-alert">
    <div class="TIPO"
        data-title="Título de la alerta">
        Esta es una alerta con título.
        Si la quieres sin título, solo hay que eliminar el título "data-title="Título de la alerta".
        Puedes escribir aquí cualquier CONTENIDO en formato HTML.
    </div>
</aside>
```

<aside class="widget widget-alert">
    <div class="alert alert-danger"
        data-title="Alerta de PELIGRO (rojo) con Título">
        Alerta con titulo y tema de peligro.
        Aquí puedes escribir cualquier contenido en formato HTML, como este párrafo.
    </div>
</aside>

<aside class="widget widget-alert">
    <div class="alert alert-success">
        Alerta SIN titulo y tema de éxito (verde).
        Aquí puedes escribir cualquier contenido en formato HTML, como este párrafo.
    </div>
</aside>