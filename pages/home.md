---
title: Documentar un Proyecto
description: Página HOME del proyecto
layout: libdoc_page.liquid
permalink: /index.html
tags:
    - home
---

<img src="/assets/myfavicon.png" 
     alt="Documentar un Proyecto" 
     style="width: 128px; height: 128px; display: block; margin: 0 auto;">


# Introducción

La **documentación** de un proyecto es una parte fundamental, permite entender el proyecto, su estructura, su funcionamiento, las decisiones tomadas y como reutilizarlo en otros proyectos.

Este proyecto es una guía de uso de mi plantilla de documentación para proyectos que está basada en el generador de sitios estáticos [Eleventy](https://www.11ty.dev/) y en el starter project [LibDoc](https://eleventy-libdoc.netlify.app/), adaptado para satisfacer mis necesidades y gustos. 

Mi idea es **integrar el proyecto y la documentación en un mismo repositorio**, de esta forma se puede versionar tanto la documentación como el código del proyecto y se puede integrar también más documentación, diseños 3D, electrónicos, etc.

* Una documentación con formato web me permite más flexibilidad que la documentación tradicional. 
* Las funcionalidades de búsqueda y navegación me permiten acceder fácilmente a la información que necesito. 
* He creado una estructura de ficheros propia que quiero estandarizar en todos mis proyectos. 
* Esta integración permite desarrollar el proyecto y generar una documentación elegante y adaptable, también incluye un cuaderno de bitácora en formato blog para poder registrar progresos, problemas, decisiones...
* Puedo acceder a la documentación desde cualquier dispositivo, lo que facilita su consulta en cualquier momento y lugar.
* Al estar alojada en GitHub Pages, las páginas tienen que ser públicas y estáticas, es fácil de actualizar, mantener y no necesito un servidor propio.

# Estructura de las páginas

{% iconCard 'Estructura de las páginas', 'Formato de las páginas y los distintos elementos que las componen.<br>[Estructura de las páginas de la Documentación](./1-estructuraDoc.md/).', 'copy-simple' %}

# Instalaciones necesarias

{% iconCard 'Instalaciones Previas y Pasos Iniciales', 'Lo que se necesita para que funcione.<br>[Instalaciones necesarias](./2-instalaciones.md/).', 'plus-circle' %}

# Configuraciones
{% iconCard 'Haciendo que funcione', '¿Qué hay que cambiar y en qué archivos se cambia?<br>[Configuración](./3-configuracion.md/).', 'faders' %}

# Crear contenido
{% iconCard 'Escribe como quieras', 'Cómo escribir mi documentación con <abbr title="Hyper Text Markup Language"> Markdown y HTML </abbr> y añadirle widgets. <br>[Crear Contenido](./4-crear-contenido.md/).', 'pen' %}

# Navegación
{% iconCard 'Recorre el proyecto', 'Tabla de contenidos, navegación inteligente, búsqueda difusa y estándar. Además aprende a cómo crear items en el menú.<br>[Navegación](./5-navegacion.md/).', 'list' %}

# Estructura de ficheros
{% iconCard 'FileTree', 'Como es la estructura de ficheros y dónde se guarda cada cosa.<br>[Estructura de Ficheros](./6-estructura-ficheros.md/).', 'list-dashes' %}

# Cuaderno de bitácora
{% iconCard 'Blog', 'Es un diario de trabajo y un blog técnico.<br>[Cuaderno de Bitácora](./posts/).', 'sidebar' %}


# Créditos y referencias

Este proyecto no sería posible sin el trabajo de otras personas, aquí dejo una lista de las herramientas y recursos que he utilizado:

* [Node.js](https://nodejs.org/) <br>Es un entorno de ejecución de JavaScript, necesario para ejecutar Eleventy.
* [Eleventy](https://www.11ty.dev/) <br>Es un generador de sitios estáticos, es decir, la herramienta que permite generar el sitio web a partir de plantillas fuente.
* [LibDoc](https://eleventy-libdoc.netlify.app) <br>Es un starter project de 11ty (Eleventy) que me permite crear documentación elegante y adaptable.


# Licencia

Aquí encontrarás información sobre la licencia del proyecto y de la documentación: [Licencia](./n1-licencia.md)

<br><a href="https://venomjp.github.io/Documentar_Proyecto/">Documentar un Proyecto</a> © 2026 by <a href="https://github.com/venomjp/venomjp">Juan Pedro Perianes</a> is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International</a><img src="https://mirrors.creativecommons.org/presskit/icons/cc.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/by.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/nc.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/sa.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;">

