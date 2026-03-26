---
title: Instalaciones necesarias
description: Pasos previos para que funcione cualquier proyecto.
layout: libdoc_page.liquid
permalink: /pages/n1-instalaciones/index.html
eleventyNavigation:
    key: Instalaciones necesarias
    order: 1
tags:
    - instalación
    - nodejs
    - github pages
    - git
    - github desktop
    - visual studio code
date: 2026-03-24
---

Partimos de la base de que el ordenador que se utilice deberá tener instalado previamente:
* [Git](https://git-scm.com/)
* [GitHub Desktop](https://desktop.github.com/)
* [Visual Studio Code](https://code.visualstudio.com/). Extensiones:
  * Markdown All in One
  * GitHub Actions
  * GitHub Copilot Chat
  * Git History
  * Liquid
* [NodeJS](https://nodejs.org/)

---
 Además, para que funcione cualquier proyecto basado en la plantilla de proyectos con documentación en formato web alojada en GitHub Pages, se necesitan los siguientes **pasos iniciales**:


1. Clonar el repositorio de la [plantilla para proyectos](https://github.com/venomjp/Plantilla_Proyecto) y cambiarle el nombre.
   * Borrar la carpte oculta .git para desvincularlo del repositorio original.
2. Instalar **Eleventy** en el repositorio clonado: 
   * `npm install @11ty/eleventy` - instalar Eleventy
   * `npm audit fix` - corregir vulnerabilidades de seguridad
3. Comprobar que el proyecto funciona en modo local: 
   * `npm run clean` - script para limpiar la carpeta de salida
   * `npm run start` - script para iniciar el servidor local y comprobar que se visualiza la documentación en [localhost](http://localhost:8080/)
4. Subir el proyecto a un repositorio nuevo en **GitHub**: 
    * Crear un nuevo repositorio en GitHub con el mismo nombre que el proyecto.
    * Subir el proyecto al nuevo repositorio utilizando GitHub Desktop.
    * Modificar el pathPrefix (.eleventy.js) con el nombre del repositorio nuevo.
    * `npm run clean` - script para limpiar la carpeta de salida antes de subir los cambios.
    * `npm run build-ghpages` - script para generar la carpeta de salida con el pathPrefix correcto para GitHub Pages.
5. Activar **GitHub Pages** en el repositorio nuevo y comprobar que se visualiza la documentación.
    * Settings > Pages > Build & Deploy: GitHub Actions > Save - genera la página web automáticamente cada vez que se suben cambios al repositorio.
    * Hacer algún cambio, generar un **commit** y subirlo con **push** para comprobar que se actualiza la página web.
    * Recuerda que el repositorio tiene que ser público para que se visualice la página web.