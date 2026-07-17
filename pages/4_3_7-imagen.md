---
title: Imágenes
description: Código para insertar imágenes.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_3-widgets/4_3_7-imagen/index.html
eleventyNavigation:
    key: Imágenes
    parent: Widgets
    order: 8
tags:
    - contenido
    - widgets
    - imagen
date: 2026-03-31
---

Las [imágenes en Markdown](/pages/4_1_4-imagenes.md) son útiles para el uso diario, pero a veces es necesario destacar tus imágenes usando HTML.

# Fondo claro

Si en la clase `<img>` le ponemos la etiqueta `light` y es una **imagen con transparencia**, se le aplica un fondo blanco en lugar del fondo transparente. 

*Si estamos en modo oscuro se le aplica un fondo negro.*

<img class="light"
    src="/assets/gypaetus-barbatus-peisey.png"
    alt="Gypaetus barbatus">

``` html
<img class="light"
    src="/assets/gypaetus-barbatus-peisey.png"
    alt="Gypaetus barbatus">
```
# Fondo oscuro

Si en la clase `<img>` le ponemos la etiqueta `dark` y es una **imagen con transparencia**, se le aplica un fondo negro en lugar del fondo transparente.

*Si estamos en modo oscuro se le aplica un fondo blanco.*

<img class="dark"
    src="/assets/gypaetus-barbatus-peisey.png"
    alt="Gypaetus barbatus">

```html
<img class="dark"
    src="/assets/gypaetus-barbatus-peisey.png"
    alt="Gypaetus barbatus">
```

# Fondo de damier

Fondo damier se le denomina al típico fondo de cuadrícula que se aplica a las imágenes con transparencia.

Si en la clase `<img>` le ponemos la etiqueta `damier` y es una **imagen con transparencia**, se le aplica un fondo de cuadrícula (damier) en lugar del fondo transparente.

*Si estamos en modo oscuro se le aplica un damier también.*

<img class="damier"
    src="/assets/gypaetus-barbatus-peisey.png"
    alt="Gypaetus barbatus">

```html
<img class="damier"
    src="/assets/gypaetus-barbatus-peisey.png"
    alt="Gypaetus barbatus">
```
# Sombreado

Si en la clase `<img>` le ponemos la etiqueta `long-shadow` se le aplica un cajeado redondeado con un sombreado.

<img class="long-shadow"
    src="/assets/pierra-menta.jpg"
    alt="Pierra Menta">

```html
<img class="long-shadow"
    src="/assets/pierra-menta.jpg"
    alt="Pierra Menta">
```
# Marco

Las imágenes enmarcadas requieren una estructura específica `figure` como se muestra a continuación. Debajo de la imagen aparece una descripción y tanto la imagen como la descripción quedan enmarcadas con un marco redondeado.

<figure>
    <img src="/assets/pierra-menta.jpg" alt="Pierra Menta">
    <figcaption>Esta es una imagen con marco y descripción en una línea.</figcaption>
</figure>

```html
<figure>
    <img src="/assets/pierra-menta.jpg" alt="Pierra Menta">
    <figcaption>Esta es una imagen con marco y descripción en una línea.</figcaption>
</figure>
```
# Marco ancho

Genera una imagen más grande que el contenido principal (se nota en pantallas grandes). Permite ademas tener una descripción más larga, en varias líneas, en la que podamos escribir en HTML, a la estructura `figure` le agregamos la clase `wide`.

<figure class="wide">
    <img src="/assets/pierra-menta.jpg"
        alt="Pierra Menta">
    <figcaption>
        Esta es una imagen enmarcada ancha. <br>
        Permite escribir una descripición más larga en varias líneas.<br>
        Poniendo en <mark>figure</mark> la clase: <code>wide</code>.
    </figcaption>
</figure>

```html
<figure class="wide">
    <img src="/assets/pierra-menta.jpg"
        alt="Pierra Menta">
    <figcaption>
        Esta es una imagen enmarcada ancha. <br>
        Permite escribir una descripición más larga en varias líneas.<br>
        Poniendo en <mark>figure</mark> la clase: <code>wide</code>.
    </figcaption>
</figure>
```
# Combinar sombreado y marco ancho
<figure class="long-shadow wide">
    <img src="/assets/pierra-menta.jpg"
        alt="Pierra Menta">
    <figcaption>
        Esta es una imagen enmarcada ancha con sombreado. <br><br>
        Poniendo en <mark>figure</mark> las clases: <code>long-shadow</code> y <code>wide</code>.
        <br><br>
        Genera una imagen con <b>sombreado y marco, con descripción en varias líneas.</b>.
    </figcaption>
</figure>

```html
<figure class="long-shadow wide">
    <img src="/assets/pierra-menta.jpg"
        alt="Pierra Menta">
    <figcaption>
        Esta es una imagen enmarcada ancha con sombreado. <br><br>
        Poniendo en <mark>figure</mark> las clases: <code>long-shadow</code> y <code>wide</code>.
        <br><br>
        Genera una imagen con <b>sombreado y marco, con descripción en varias líneas.</b>.
    </figcaption>
</figure>
```