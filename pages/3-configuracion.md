---
title: Configuraciones
description: Pasos previos para que funcione cualquier proyecto.
layout: libdoc_page.liquid
permalink: /pages/3-configuracion/index.html
eleventyNavigation:
    key: Configuraciones
    order: 3
tags:
    - configuración
    - package.json
    - settings.json
    - README.md
    - favicon
    - niveles de páginas
    - bitácora
date: 2026-03-24
---
<img src="/assets/configuraciones.png" 
  alt="Configuraciones" 
  style="width: 128px; height: 128px; display: block; margin: 0 auto;">

# Qué cambiar al iniciar un nuevo proyecto

Una vez que hemos realizado las instalaciones necesarias, nuestro proyecto ya funciona en modo local y su website funciona en GitHub, hemos de realizar algunos cambios en los archivos de configuración para adaptarlos al nuevo proyecto:
* Nombre del proyecto y descripción.
* Icono del sitio web (myfavicon.png).
* Custom links de la barra de navegación.
* PathPrefix para GitHub Pages (repositorio).
* Resaltado de sintaxis para los lenguajes de programación relevantes para el proyecto.


# Archivos de configuración
Estos son los principales archivos de configuración que hay que modificar para adaptar el proyecto a nuestras necesidades:

* `package.json` - archivo de **configuración de NodeJS** con los scripts para generar la documentación.
  * **Nombre del proyecto** - debe coincidir con el nombre del repositorio en GitHub.
  * **Versión** -  para indicar la versión inicial del proyecto.
  * **Descripción** - para proporcionar una breve descripción del proyecto, es como un subtítulo.
  * **main**: ***"index.js"*** aunque no se utiliza un archivo index.js en este proyecto, es necesario mantener esta propiedad para que NodeJS no genere errores al ejecutar los scripts.
  * **Licencia** - **CC BY-NC-SA 4.0** para que coincida con la licencia del proyecto.
  * **Scripts**: Ya están definidos, no es necesario cambiarlos, pero es importante conocer su función:
    * `start` para iniciar el servidor local y comprobar que se visualiza la documentación en localhost. **("npx @11ty/eleventy --serve")**
    * `build-ghpages` para generar la carpeta de salida con el pathPrefix correcto para GitHub Pages. **("npx @11ty/eleventy --pathprefix")**
    * `clean` para limpiar la carpeta de salida antes de generar la documentación. **("rimraf _site .cache")**
* `settings.json` - este archivo contiene la configuración general del sitio web y del home, sobreescribe los valores por defecto de LibDoc.
  * **Título del sitio web** - para darle un título personalizado al sitio web.
  * **Descripción del sitio web** - para proporcionar una breve descripción del sitio web, es como un subtítulo.
  * **Autor** - para mostrar el nombre del autor en las entradas del blog (bitácora).
  * **Ubicación del favicon** - para mostrar un favicon personalizado en la pestaña del navegador.
  * **Título del blog** - para darle un título personalizado a la sección del blog, que en este caso es el cuaderno de bitácora donde se registran los cambios realizados en el proyecto.
  * **Descripción del blog** - para proporcionar una breve descripción de la sección del blog (bitácora).
  * **customLinks** para agregar enlaces personalizados en la barra de navegación, como el enlace a mi perfil de GitHub.
  * **Lenguaje** - para establecer el idioma del sitio web, en este caso español ("es").
  * **htmlBasePathPrefix** para que los enlaces a los archivos y recursos funcionen correctamente en GitHub Pages, ya que el sitio web se alojará en una subcarpeta con el nombre del repositorio.
  * **hljsLanguages** para incluir lenguajes de programación relevantes para el tipo de documentación que estoy creando, como arduino, python, c y gcode.
  * **tocEnabled** para mostrar una tabla de contenidos en todas las páginas de la documentación (en el blog no aparecía antes).
* `README.md` - archivo de presentación del proyecto con información general y enlaces a la documentación. ***Recuerda cambiarlo en cada proyecto.***
* `myfavicon.png` - archivo de imagen para el favicon del sitio web. Recomendado usar una imagen PNG de 512x512 pixeles. [./assets/myfavicon.png]

# Niveles de Plantillas
En Eleventy las plantillas son los archivos con el contenido de las páginas. He decidido organizar las plantillas en 3 niveles.

* `home.md` - Esta es la plantilla para la página de inicio del sitio web (nivel 0).
* `x-<pagina_nivel_1>.md` - Este es el formato de las páginas de nivel 1, sección principal (x).
* `x_y-<pagina_nivel_2>.md` - Este es el formato de las páginas de nivel 2, subsección (y) dentro de la sección principal (x).
* `x_y_z-<pagina_nivel_3>.md` - Este es el formato de las páginas de nivel 3, sub-subsección (z) dentro de la subsección (y) y sección (x).

# Cuaderno de Bitácora
* `bit-nombreEntrada.md` - Este es el formato de las entradas del cuaderno de bitácora (blog), con información sobre los cambios realizados en el proyecto, problemas encontrados, soluciones implementadas, etc. 