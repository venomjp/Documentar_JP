---
title: Estructura de ficheros
description: Como es la estructura de ficheros y dónde se guarda cada cosa.
layout: libdoc_page.liquid
permalink: /pages/n1-estructura-ficheros/index.html
eleventyNavigation:
    key: Estructura de ficheros
    order: 5
tags:
    - estructura
    - ficheros
    - file tree
date: 2026-03-24
---

En esta sección se muestra la estructura de ficheros y archivos más significativos de la plantilla de proyecto, con una breve descripción.

* He modificado la estructura original de LibDoc
  * Las plantillas que serán transformadas en páginas web se han movido a la carpeta **pages**.
  * El blog (bitácora) lo he incluido dentro de la carpeta **pages/bitacora**.
  * Hay una nueva carpeta **.github** para almacenar los archivos de configuración de GitHub Actions.

* Los proyectos disponen de unas carpetas para organizar los archivos
  * **3dDesign**: para diseños 3D
  * **fieles**: para archivos del proyecto
  * **sourceCode**: para el código fuente del proyecto

```
RAIZ DEL PROYECTO
¦   .eleventy.js      -> Configuración de Eleventy
¦   .eleventyignore   -> Indica a Eleventy qué ignorar
¦   .gitattributes    -> Configurar atributos específicos para Git
¦   .gitignore        -> Indica a Git qué archivos o carpetas ignorar
¦   LICENSE           -> Licencia del proyecto
¦   package-lock.json -> Versiones de las dependencias instaladas
¦   package.json      -> Configuración de NodeJS
¦   README.md         -> Resumen del proyecto
¦   settings.json     -> Configuración general del proyecto
¦   
+---.github
¦   +---workflows
¦           build.yml -> GHAction automatiza la construcción de la web
¦           
+---3dDesign          -> Carpeta para almacenar diseños 3D
¦   ¦   readme.md
¦   ¦   
¦   +---3mf
¦   +---gcode
¦   +---stl
+---assets            -> Recursos estáticos como imágenes, íconos...
¦       logo-11ty.png
¦       myfavicon.png -> Favicon del proyecto
¦       
+---core              -> Archivos del núcleo del proyecto
¦   ¦   feed.njk
¦   ¦   libdoc_blog.liquid
¦   ¦   libdoc_fuzzy_index.liquid
¦   ¦   libdoc_search.html
¦   ¦   libdoc_search_index.liquid
¦   ¦   libdoc_tag.liquid
¦   ¦   libdoc_tags.liquid
¦   ¦   
¦   +---assets        -> Recursos específicos del núcleo
¦       +---css
¦       ¦      
¦       +---fonts
¦       ¦       
¦       +---icons
¦       ¦       
¦       +---js
¦                       
+---files             -> Carpeta para archivos del proyecto
¦   ¦   readme.md
¦   ¦   
¦   +---audio
¦   +---images
¦   +---text
¦   +---video
¦  
+---node_modules      -> Dependencias del proyecto
¦               
+---pages             -> Páginas web del proyecto
¦   ¦   home.md
¦   ¦   n1-primera.md
¦   ¦   n2-primera.md
¦   ¦   n2-segunda.md
¦   ¦   n3-primera.md
¦   ¦   
¦   +---bitacora     -> Páginas del Blog = bitácora del proyecto
¦           bit-bitacora1.md
¦           bit-ejemplo.md
¦           
+---sandboxes        -> (No usado) Proyectos experimentales
¦           
+---sourceCode       -> Carpeta para almacener el Código fuente
¦   ¦   readme.md
¦   ¦   
¦   +---proyectoX1
¦   +---proyectoX2
+---_data            -> Datos globales para el proyecto
¦       libdocConfig.js
¦       libdocFunctions.js
¦       libdocMessages.json
¦       libdocSystem.json
¦       libdocUtils.js
¦       
+---_includes        -> Estructura de las páginas
        libdoc_before_html.liquid
        libdoc_breadcrumb.liquid
        libdoc_page.liquid
        sandbox.liquid
```
