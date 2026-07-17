---
title: Botones
description: Código para crear botones y crear llamadas a la acción.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_3-widgets/4_3_2-botones/index.html
eleventyNavigation:
    key: Botones
    parent: Widgets
    order: 2
tags:
    - contenido
    - widgets
    - botones
date: 2026-03-30
---

Los botones son elementos interactivos que permiten a los usuarios realizar acciones específicas, como enviar un formulario o navegar a otra página. 

Se pueden crear botones como un **enlace** <code>&lt;a href="#"&gt;</code> de una de las *clases de botones* o como un **botón** <code>&lt;button&gt;</code>.

# Clases de botones

Al igual que las alertas hay botones temáticos:
* `btn`: Botón estándar <button type="button" class="btn">blanco y negro</button>
* `btn-primary`: Botón de información <button type="button" class="btn btn-primary">fondo azul</button>
* `btn-primary-light`: Botón de información <button type="button" class="btn btn-primary-light">borde azul</button>
* `btn-success`: Botón de acción exitosa <button type="button" class="btn btn-success">fondo verde</button>
* `btn-success-light`: Botón de acción exitosa <button type="button" class="btn btn-success-light">borde verde</button>
* `btn-warning`: Botón de acción de advertencia <button type="button" class="btn btn-warning">fondo amarillo</button>
* `btn-warning-light`: Botón de acción de advertencia <button type="button" class="btn btn-warning-light">borde amarillo</button>
* `btn-danger`: Botón de acción de peligro <button type="button" class="btn btn-danger">fondo rojo</button>
* `btn-danger-light`: Botón de acción de peligro <button type="button" class="btn btn-danger-light">borde rojo</button>

1. **DEFINIDOS COMO ENLACES**

    Botón de información definido como 
    <a href="#" class="btn btn-primary">
        Enlace
    </a>

    ``` html
    Botón de información definido como 
    <a href="#" class="btn btn-primary">
        Enlace
    </a>
    ```

2. **DEFINIDOS COMO BOTONES**

    Botón de advertencia definido como 
    <button type="button" class="btn btn-warning">
    Botón
    </button>

    ``` html
    Botón de advertencia definido como 
    <button type="button" class="btn btn-warning">
        Botón
    </button>
    ```

# Botones con iconos

1. **DEFINIDOS COMO ENLACES**

    Soy un 
    <a href="#" class="btn btn-danger">
         <span class="icon-play"></span>
        Enlace
    </a>

    ``` html
    Soy un
    <a href="#" class="btn btn-danger">
         <span class="icon-play"></span>
        Enlace
    </a>
    ```

2. **DEFINIDOS COMO BOTONES**
    
    Soy un 
    <button type="button" class="btn btn-success">
        <span class="icon-faders"></span>
        Botón
    </button>

    ``` html
    Soy un
    <button type="button" class="btn btn-success">
        <span class="icon-faders"></span>
        Botón
    </button>
    ```