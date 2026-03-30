---
title: Detalle y Acordeón
description: Código para crear contenido colapsable.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_3-widgets/4_3_4-acordeon/index.html
eleventyNavigation:
    key: Detalle y Acordeón
    parent: Widgets
    order: 4
tags:
    - contenido
    - widgets
    - detalle
    - acordeón
date: 2026-03-30
---

# Detalle
Los **detalles** presentan un símbolo sobre el que se puede pulsar para expandir o colapsar el contenido.

<details>
    <summary>DETALLE</summary>
    <p> El contenido del detalle se muestra al pulsar sobre el símbolo, y se oculta al volver a pulsar. Es una forma sencilla de mostrar información adicional sin saturar la página.</p>
    </p>
</details>

``` html
<details>
    <summary>DETALLE</summary>
    <p> El contenido del detalle se muestra al pulsar sobre el símbolo, 
        y se oculta al volver a pulsar. Es una forma sencilla de mostrar 
        información adicional sin saturar la página.</p>
    </p>
</details>
```

# Acordeón
El **acordeón** se forma con variois detalles contiguos que tengan el mismo valor de su atributo `name`, de esta forma se asegura que solo un detalle esté abierto a la vez.

<details name="acordeon">
    <summary>UNO</summary>
    <p> Solo se muestra el contenido del <b>primer</b> detalle.</p>
    </p>
</details>
<details name="acordeon">
    <summary>DOS</summary>
    <p> Solo se muestra el contenido del <b>segundo</b> detalle.</p>
    </p>
</details>
<details name="acordeon">
    <summary>TRES</summary>
    <p> Solo se muestra el contenido del <b>tercer</b> detalle.</p>
    </p>
</details>

``` html
<details name="acordeon">
    <summary>Uno</summary>
    <p> Solo se muestra el contenido del **primer** detalle.</p>
    </p>
</details>
<details name="acordeon">
    <summary>Dos</summary>
    <p> Solo se muestra el contenido del **segundo** detalle.</p>
    </p>
</details>
<details name="acordeon">
    <summary>Tres</summary>
    <p> Solo se muestra el contenido del **tercer** detalle.</p>
    </p>
</details>
```