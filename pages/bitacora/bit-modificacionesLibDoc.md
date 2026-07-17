---
title: Modificaciones respecto a "LibDoc Starter Project"
description: Cambios realizados en el proyecto base para adaptarlo a mis necesidades.
layout: libdoc_page.liquid
permalink: "{{ libdocConfig.blogSlug }}/{{title | slugify}}/index.html"
tags:
    - post
    - modificaciones respecto a LibDoc
date: 2026-03-25
---

# libdocMessages.js
Este archivo contiene los mensajes personalizados del proyecto.
* Incluí el lenguaje español **"es"** (LibDoc no tiene soporte para español), con las traducciones necesarias.

# libdocConfig.js
Este archivo contiene la configuración personalizada del **proyecto LibDoc** por defecto.
* Lenguaje- **lang**: ***"es"***
* Lenguajes de resaltado de código- **hljsLanguages**: incluyendo lenguajes como arduino, python, c y gcode que son relevantes para el tipo de documentación que estoy creando.

# libdoc_page.liquid
Este archivo contiene el layout para las páginas de documentación, es común para las páginas y los posts del blog. 
* Elimine la parte del pie de página (Footer) que mostraba la versión de libdoc en la que se basa el proyecto o el botón de editar está página. [Incorporo botón "ir atrás"](./bit-botonIrAtras.md) para mejorar la navegación entre páginas.

# libdocSystem.json
Este archivo contiene la configuración del sistema de navegación y diseño del proyecto.
* Cambié el ancho de la barra lateral a 250px y el ancho del contenido a 750px para darle un diseño más compacto y enfocado en el contenido.

# myfavicon.png
Este archivo es el favicon personalizado del proyecto, se muestra en la pestaña del navegador.
* Cambie el favicos por el tipico "under construction" para darle un toque divertido al proyecto, ya que es una documentación en construcción.

# build.yml
Este archivo contiene la configuración para el workflow de GitHub Actions que genera la documentación automáticamente al hacer push a la rama main.
* Tuve que crear la carpeta **.github/workflows** y el archivo **build.yml** para configurar el workflow de GitHub Actions, ya que el proyecto base no incluía esta configuración. El workflow se ejecuta cada vez que se hace push a la rama main, generando la documentación y publicándola en GitHub Pages automáticamente.
* Está basado en las instrucciones de **11ty** [Deploy an Eleventy project to GitHub pages ](https://www.11ty.dev/docs/deployment/)
* Modifiqué la versión de cada acción por las actuales a 25/03/2026.

# Carpetas para las plantillas
11ty utiliza las llamadas plantillas para generar las páginas web. LibDoc no tiene una estructura de carpetas para las plantillas y las almacenaba en la raíz del proyecto. Comprobé que daba igual que estuvieran en la raíz del proyecto o en una carpeta.
* Cree una carpeta llamada **pages** para almacenar las páginas de la documentación (home y niveles 1, 2 y 3).
  * Cree una subcarpeta dentro de **pages** llamada **bitacora** para almacenar las entradas del cuaderno de bitácora.
* La página HOME se llama **home.md**.
* Las páginas de nivel 1 se llaman **n1-nombreN1.md**.
* Las páginas de nivel 2 se llaman **n2-nombreN2.md**.
* Las páginas de nivel 3 se llaman **n3-nombreN3.md**.
* Las entradas del cuaderno de bitácora se llaman **bit-nombreEntrada.md**.

# Carpetas para los proyectos
La estructura de ficheros que he creado para almacenar los proyectos es la siguiente:
* **3dDesign** - para almacenar los proyectos relacionados con el diseño 3D.
* **files** - para almacenar los archivos relacionados con el proyecto, como imágenes, archivos varios, etc.
* **sourceCode** - para almacenar el código fuente de los proyectos.

# LICENSE
Cambie el archivo LICENSE original por uno nuevo con la licencia **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)** para proteger el contenido de la documentación y permitir su uso bajo ciertas condiciones, como atribución, uso no comercial y compartir bajo la misma licencia. Esta licencia es adecuada para proyectos de documentación que se quieren compartir pero no se quieren usar con fines comerciales sin permiso.

# README.md
Este archivo contiene la presentación del proyecto, con información general y enlaces a la documentación.

# .eleventyignore
Este archivo contiene la configuración de archivos y carpetas que Eleventy debe ignorar al generar el sitio web.
* **README.md** - para evitar que se genere una página web a partir del README, ya que es un archivo de presentación para el repositorio y no forma parte de la documentación en sí.
* **sandboxes/** - para evitar que se generen páginas web a partir de los proyectos de prueba.
* **3dDesign/** - para evitar que se generen páginas web a partir de los proyectos de diseño 3D.
* **archivos/** - para evitar que se generen páginas web a partir de los archivos relacionados con los proyectos.
* **sourceCode/** - para evitar que se generen páginas web a partir del código fuente de los proyectos.

# .gitignore
Este archivo contiene la configuración de archivos y carpetas que Git debe ignorar al hacer commits en el repositorio.
* Ignorar la carpeta **node_modules** necesaria para generar el sitio web local, ya que GitHub Actions instala automáticamente lo necesario para generar el sitio web en GitHub Pages.

# .eleventy.js
En principio cambié el directorio de salida a **docs** para que GitHub Pages lo detectara automáticamente, pero muchas de los elementos dejarón de funcionar pues no tiene en cuenta el pathPrefix. Dejé el directorio de salida por defeto **_site**, añadí el pathPrefix con el nombre del repositorio para que funcione correctamente en GitHub Pages y utilice GitHub Actions para la generación del sitio web en GitHub Pages. Así que este archivo es identico al original.

# package.json
Este archivo contiene la configuración de NodeJS, con los scripts para generar la documentación.
* Cambié la licencia a **CC BY-NC-SA 4.0** para que coincida con la licencia del proyecto.
* Eliminé el script de `test`, ya que no se han especificado tests para este proyecto y no es necesario tener un script de test que no se utiliza.
* Creé varios scripts:
  * `start` para iniciar el servidor local y comprobar que se visualiza la documentación en localhost.
  * `build-ghpages` para generar la carpeta de salida con el pathPrefix correcto para GitHub Pages.
  * `clean` para limpiar la carpeta de salida antes de subir los cambios a GitHub Pages, ya que GitHub Pages no borra los archivos antiguos automáticamente y pueden quedar archivos obsoletos si no se limpia la carpeta de salida antes de generar la nueva versión del sitio web.

# settings.json
Este archivo contiene la configuración del home y general del sitio web, sobreescribe los valores por defecto de LibDoc.
* Lenguaje - **lang:** ***"es"***
* Habilitar la tabla de contenidos - **tocEnabled:** ***true*** para mostrar una tabla de contenidos en cada página de la documentación (en el blog no aparecía).
* **hljsLanguages:** incluyendo lenguajes como arduino, python, c y gcode que son relevantes para el tipo de documentación que estoy creando.
* **htmlBasePathPrefix:** ***"/Documentar_Proyecto/"*** para que los enlaces a los archivos y recursos funcionen correctamente en GitHub Pages, ya que el sitio web se alojará en una subcarpeta con el nombre del repositorio.
* **blogTitle:** ***"Bitácora de Modificaciones"*** para darle un título personalizado a la sección del blog, que en este caso es el cuaderno de bitácora donde se registran los cambios realizados en el proyecto.
* Autor - **author:** ***"Juan Pedro Perianes"*** para mostrar el nombre del autor en las entradas del blog (bitácora).
* **faviconUrl:** ***"/myfavicon.png"*** para mostrar el favicon personalizado en la pestaña del navegador.
* **customLinks:** para agregar enlaces personalizados en la barra de navegación, como el enlace a mi perfil de GitHub.

# ds__defaults.css
Este archivo contiene los estilos por defecto de LibDoc, que se aplican a todas las páginas del sitio web.
* Cambié las rutas de los iconos de los detalles para que funcionen correctamente, ya que los iconos que indican que se puede expandir y colapsar no se mostraban.

``` Markdown
* Línea 572:
  mask-image: url('/core/assets/icons/plus-circle.svg');
Cambiada por:
  mask-image: url('../icons/plus-circle.svg');

* Línea 584:
  mask-image: url('/core/assets/icons/minus-circle.svg');
Cambiada por:
  mask-image: url('../icons/minus-circle.svg');
```

