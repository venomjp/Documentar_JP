---
title: Estructura de las páginas de la documentación
description: Formato de las páginas de la documentación y del cuaderno de bitácora.
layout: libdoc_page.liquid
permalink: /pages/1-estructuraDoc/index.html
eleventyNavigation:
    key: Estructura de las páginas de la Documentación
    order: 1
tags:
    - estructura
date: 2026-03-24
---

Esta documentación tiene un formato común en todas las páginas, con distintas secciones y elementos que permiten una navegación fácil y una presentación clara de la información.
En Eleventy, las plantillas son los archivos ```*.md``` con el contenido que se mostrará en las páginas que se generan. He decidido organizar las plantillas en 3 niveles.

# Zona de Navegación

Situada a la **izquierda** de la página y ocupa un 30% del ancho de la página.

<div style="display: flex; align-items: center; gap: 20px;">
  
  <!-- Columna 1: Imagen -->
  <div style="flex: 1;">
    <img src="/assets/zonaNavegacion.png" alt="Zona de Navegación" style="width: 100%; max-width: 200px;">
  </div>

  <!-- Columna 2: Texto -->
  <div style="flex: 2;">
    
    <ol>
        <li><b>Título del Proyecto</b> - Es el nombre del archivo home.md y la página de inicio del sitio web</li>
        <li><b>Barra de búsqueda</b> - Permite buscar contenido dentro del sitio web. Su atajo de teclado es ```S```</li>
        <li><b>Links personalizados</b> - Enlaces a sitios web externos, como mi perfil de GitHub</li>
        <li><b>Bitácora</b> - Es un blog que utilizaré como cuaderno de bitácora</li>
        <li><b>Lista de tags</b> - Muestra las etiquetas utilizadas en el sitio web para organizar el contenido</li>
    </ol>
  </div>
</div>

# Zona de Contenido

Es la zona principal y ocupa un 70% del ancho de la página.

<div style="display: flex; align-items: center; gap: 20px;">
  
  <!-- Columna 1: Imagen -->
  <div style="flex: 50%;">
    <img src="/assets/zonaContenido.png" alt="Zona de Contenido" style="width: 100%; max-width: 340px;">
  </div>

  <!-- Columna 2: Texto -->
  <div style="flex: 50%;">
    <ol>
        <li><b>Miga de Pan</b> - Muestra la ruta actual dentro del sitio web y es navegable</li>
        <li><b>Selector de esquema de color</b> - Situado arriba a la derecha, permite cambiar el esquema de colores del sitio web</li>
        <li><b>Título de la página</b> - es el título de cada plantilla y su descripción (subtitulo)</li>
        <li><b>Lista de tags de la página</b> - Muestra las etiquetas asociadas a cada página para organizar el contenido</li>
        <li><b>Tabla de Contenido</b> - Proporciona un índice de los temas tratados en la página. Se puede contraer y es navegable</li>
        <li><b>Contenido Principal</b> - Es la sección donde se presenta el contenido principal de la página</li>
        <li><b>Botón de Ir Atrás</b> - Situado al final del contenido, permite regresar a la página anterior en la navegación. Se desactiva en el Home y la lista de Tags</li>
    </ol>
  </div>
</div>

# Elementos automáticos

Estos elementos aparecen automáticamente en el lado **derecho** de la página.

<div style="display: flex; align-items: center; gap: 20px;">
  
  <!-- Columna 1: Imagen -->
  <div style="flex: 1;">
    <img src="/assets/elementosAutomaticos.png" alt="Elementos Automáticos" style="width: 100%; max-width: 200px;">
  </div>

  <!-- Columna 2: Texto -->
  <div style="flex: 2;">
    <ol>
        <li><b>Contenido Flotante</b> - Es un botón desplegable que muestra los encabezados (h1 a h6) de cada plantilla, tiene función ScrollSpy que resalta automáticamente la sección actual a medida que el usuario se desplaza por la página</li>
        <li><b>Ir al Principio</b> - Es un botón que aparece al desplazarse hacia abajo en la página, permite regresar rápidamente al principio de la página</li>
    </ol>
  </div>
</div>