---
title: HTML en línea
description: Ejemplo de las etiquetas HTML disponibles.
layout: libdoc_page.liquid
permalink: /pages/4-crear-contenido/4_2-html/index.html
eleventyNavigation:
    key: HTML en línea
    parent: Crear contenido
    order: 2
tags:
    - html
    - abreviatura
    - cita en línea
    - entrada de teclado
    - salto de línea
    - enlaces internos
    - énfasis en texto
    - variables
date: 2026-03-27
---

Además del formato [Markdown](4_1-markdown.md) habitual , es posible utilizar algunas etiquetas HTML sin formato.

# Abreviatura

Con <abbr title="Eleventy">11ty</abbr> puedes usar <abbr title="Cascading Style Sheets">CSS</abbr> para dar estilo a tu <abbr title="HyperText Markup Language">HTML</abbr>. El atributo `title` es opcional pero si se establece, las etiquetas `<abbr>` son clicables y se expanden una vez hacen clic.

<aside>
    <p class="alert alert-success">
        En Eleventy LibDoc, los elementos de abreviatura con atributo de título son clicables como este: <abbr title="Exempli Gratia">E.G.</abbr>
    </p>
</aside>

``` markdown
<abbr title="Eleventy">11ty</abbr>
```

# Cita en línea (para citar fuentes)

Y entonces Albus dijo a Harry <q cite="https://www.harrypotter.com/fr/features/pearls-of-wisdom-from-professor-dumbledore"> 
    Son nuestras decisiones, Harry, las que muestran quiénes somos realmente, mucho más que nuestras habilidades.
</q>.

``` html
Y entonces Albus dijo a Harry <q cite="https://www.harrypotter.com/fr/features/pearls-of-wisdom-from-professor-dumbledore"> 
    Son nuestras decisiones, Harry, las que muestran quiénes somos realmente, mucho más que nuestras habilidades.
</q>.
```
Este tipo de citas se utiliza para marcar una referencia, título de una obra (libro, película, web...) y no la cita en sí misma. Se muestra el contenido de la cita entre comillas y en cursiva. El atributo `cite` se utiliza para proporcionar la URL de la fuente de la cita (aunque no se puede acceder a ella ni es un enlace).

Este tipo de cita es diferente a la cita en bloque, sobre todo en el tamaño del texto, que es más pequeño. La cita en bloque se utiliza para citas más largas y se muestra en un bloque grande separado del texto principal.

Lo puedo utilizar sin incluir una url en el atributo `cite` <q cite=""> y que me sirva como una cita en línea normal</q>.

``` markdown
Lo puedo utilizar sin incluir una url en el atributo `cite` <q cite="">
y que me sirva como una cita en línea normal</q>.
```

# Entrada de teclado

Puedes usar <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>R</kbd> para actualizar la página y vaciar la caché.

``` html
Puedes usar <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>R</kbd> para actualizar la página y vaciar la caché.
```

# Salto de línea

* Soy un punto importante.<br>
    A veces necesitamos romper la línea dentro del markdown.
* Soy otro punto importante.
Aquí no se ha roto la línea.

``` markdown
* Soy un punto importante.<br>
    A veces necesitamos romper la línea dentro del markdown.
* Soy otro punto importante.
Aquí no se ha roto la línea aunque lo he escrito en otra línea.
```

# Enlaces internos
Al igual que los [enlaces internos de Markdown](/pages/4_1_3-enlaces.md), también puedes usar enlaces internos con HTML.
* **ESTÁTICOS** - Son los que apuntan a una página interna en el **_site**, referencian a la página index.html (*se puede omitir index.html*).<br>
*Vamos a la página* <a href="/pages/4-crear-contenido/4_1-markdown/index.html">Markdown</a> *con un enlace estático.*
``` html
Vamos a la página <a href="/pages/4-crear-contenido/4_1-markdown/index.html">Markdown</a> con un enlace estático.
```
* **DINÁMICOS** - Son los que apuntan a un ***permalink*** y referencian siempre a una plantilla ```*.md```.<br> 
Si el permalink cambia, los enlaces internos se actualizan automáticamente.<br>
*Vamos a la página* <a href="/pages/4_1-markdown.md">Markdown</a> *con un enlace dinámico.*
``` html
Vamos a la página <a href="/pages/4_1-markdown.md">Markdown</a> con un enlace dinámico.
```
# Énfasis en texto

Hay cosas que Markdown no puede hacer, como el <mark>resaltado</mark> de texto en amarillo, <samp>simular texto de salida</samp>, <small>texto de tamaño reducido</small>, <s>tachado</s>, subíndices (**H**<sub>2</sub>**O**) y superíndices (**E**=**mc**<sup>2</sup>), para eso tenemos el HTML.

[Énfasis en texto](./4_2_1-enfasisTextoHtml.md)

# Variables

Se utilizan para marcar texto que se refiere a una variable, se muestra con una fuente monoespaciada.<br>
El volumen de una caja **(Vol)** donde <var>l</var> es la longitud, <var>w</var> es el ancho y <var>h</var> es la altura es: **Vol**=<var>l</var> × <var>w</var> × <var>h</var>

``` html
El volumen de una caja **(Vol)** donde <var>l</var> es la longitud, <var>w</var> es el ancho y <var>h</var> es la altura es: **Vol**=<var>l</var> × <var>w</var> × <var>h</var>
```