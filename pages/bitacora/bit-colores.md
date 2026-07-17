---
title: Cambiar colores
description: Dónde se definen los colores y cómo cambiarlos.
layout: libdoc_page.liquid
permalink: "{{ libdocConfig.blogSlug }}/{{title | slugify}}/index.html"
tags:
    - post
    - colores LibDoc
date: 2026-03-31
---
# Idea pendiente
Una de las cosas que me gustaría cambiar del proyecto base es el esquema de colores:
* El modo claro tiene un fondo demasiado claro
* El modo oscuro tiene un fondo demasiado oscuro
* También me gustaría hacer un par de esquemas de colores completos
  * Azul --> Proyectos completos
  * Verde --> Proyectos solo de software
  * Naranja --> Proyectos solo de diseño 3D 

En el directorio `/core/assets/css` se encuentra la gestión de colores.

# ds.css 
Contiene los colores en modo claro por defecto que se aplican a las plantillas y la definición de las variables CSS para los colores.

# ds__colors.css
Contiene la asignación de colores a los distintos elementos que forman la plantilla, como el fondo, el texto, los enlaces, etc.

# ds__dark_mode.css
Contiene la definición y asignación de los colores para el modo oscuro.

* Body: Contiene el color para el fondo de la página y para los puntitos (radiangradient) que se muestran en el fondo.
* Nav primary: Contiene el color para el fondo del menú de navegación.
* Main Content: Contiene el color para el texto del contenido principal.