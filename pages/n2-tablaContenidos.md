---
title: Tabla de contenidos
description: Puedes navegar por la tabla de contenido principal y la flotante.
layout: libdoc_page.liquid
permalink: /pages/n1-navegacion/n2-tablaContenidos/index.html
eleventyNavigation:
    key: Tabla de contenidos
    parent: Navegación
    order: 6
tags:
    - navegación
    - tabla de contenidos
    - encabezados
date: 2026-03-26
---

Basándose en la estructura del contenido de las etiquetas de nivel de encabezado ( **\<h1>** a **\<h6>** ) de cada plantilla, se generan automáticamente dos tablas de contenido: una **principal** y otra **flotante**.

En la página web resultado, los distintos niveles de encabezados se muestran con distinto tamaño de fuente, pero no generan una jerarquía en la tabla de contenido, todos los encabezados tienen el mismo nivel de importancia.

Los enlaces resultantespermiten desplazarse rápidamente a las diferentes secciones del contenido. 

# Tabla de contenido principal
* Localizado en el encabezado de cada página.
* Se genera a partir del proceso de compilación de cada plantilla.
* Es plegable.
<br>![TablaContenidoPrincipal](/assets/tocPrincipal.png)

# Tabla de contenido flotante
* Localizado en el lateral derecho de cada página, fuera del área de contenido principal y visible solo en pantallas grandes.
* Tiene función ScrollSpy, lo que significa que resalta automáticamente la sección actual a medida que el usuario se desplaza por la página.
* Es plegable.
* Generado desde el lado del cliente, requiere que JavaScript esté habilitado en el navegador del usuario para funcionar correctamente. Si JavaScript está deshabilitado, la tabla de contenido flotante no se mostrará ni funcionará, pero la tabla de contenido principal seguirá siendo accesible y funcional.
<br>![TablaContenidoFlotante](/assets/tocFlotante.png)
