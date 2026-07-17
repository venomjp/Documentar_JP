---
title: Instalaciones necesarias
description: Pasos previos para que funcione cualquier proyecto.
layout: libdoc_page.liquid
permalink: /pages/2-instalaciones/index.html
eleventyNavigation:
    key: Instalaciones necesarias
    order: 2
tags:
    - instalación
    - nodejs
    - github pages
    - git
    - github desktop
    - visual studio code
date: 2026-03-24
---
<img src="/assets/instalaciones.png" 
  alt="Instalaciones necesarias" 
  style="width: 128px; height: 128px; display: block; margin: 0 auto;">

# Instalaciones previas
Partimos de la base de que el ordenador que se utilice deberá tener instalado previamente:
* [Git](https://git-scm.com/)
* [GitHub Desktop](https://desktop.github.com/)
* [Visual Studio Code](https://code.visualstudio.com/). Algunas Extensiones interesantes:
  * Markdown All in One
  * GitHub Actions
  * GitHub Copilot Chat
  * Git History
  * Liquid
* [NodeJS](https://nodejs.org/)

---

# Pasos iniciales
 Para que funcione cualquier proyecto basado en la plantilla de proyectos con documentación integrada en formato web y alojada en GitHub Pages, se deben seguir los siguientes **pasos iniciales**:


1. Crear un **nuevo repositorio en GitHub** con el nombre que le queramos dar.
   * **Visibilidad:** ***pública*** para que se visualice la página web en GitHub Pages.
   * **Add README:** ***no***, personalizamos el README.md de la plantilla con la información del nuevo proyecto.
   * **Add .gitignore:** ***no***, la plantilla ya incluye un archivo .gitignore personalizado.
   * **Add license:** ***no***, la plantilla ya incluye una licencia personalizada (CC BY-NC-SA 4.0) que se puede mantener para todos los proyectos.
2. **Clonar el repositorio nuevo utilizando GitHub Desktop**, para que descargue el proyecto vacío en el ordenador.
3. **Descargar la** [plantilla para proyectos](https://github.com/venomjp/Plantilla_Proyecto) de mi cuenta de GitHub.
   * Borrar la carpeta oculta .git para desvincularlo del repositorio original.
   * Mover el contenido de la plantilla en la carpeta del nuevo proyecto que se ha clonado, para que tenga la estructura y archivos necesarios para generar la documentación (borrar la carpeta de la plantilla).
   * Modificar el pathPrefix en el archivo `settings.json` con el nombre del repositorio nuevo.
4. **Abrir el proyecto con Visual Studio Code**.
5. **Instalar Eleventy en el proyecto**, abrir una terminal integrada (PowerShell 7 preferiblemente) y escribir los siguientes comandos en la terminal: 
   * `npm install @11ty/eleventy` - instala Eleventy en la carpeta del proyecto
   * `npm audit fix` - correge vulnerabilidades de seguridad
   * `npm i - D rimraf` - instala una herramienta de Node.js para borrar archivos y carpetas de forma recursiva, sin tener que preocuparte por el sistema operativo ni el shell que utilices.
6. **Comprobar que el proyecto funciona en modo local**
   * `npm run clean` - script para limpiar (borra la carpeta de salida y la caché) antes de generar la documentación.
   * `npm run start` - script para iniciar el servidor local y comprobar que se visualiza la documentación en [localhost](http://localhost:8080/)
7. **Configurar GitHub Pages para el proyecto**
    * **Settings > Pages > Build & Deploy: GitHub Actions > Save** - permite generar la página web automáticamente cada vez que se suben cambios al repositorio.
8. **Subir el proyecto a GitHub** 
    1. `npm run clean` - script para limpiar la carpeta de salida y la caché antes de subir los cambios.
    2. `npm run build-ghpages` - script para generar la carpeta de salida con el pathPrefix correcto para GitHub Pages.
    3. Subir el proyecto al nuevo repositorio utilizando GitHub Desktop que permite subir muchos archivos a la vez. También se puede hacer con la terminal integrada de Visual Studio Code utilizando los comandos de Git.
    4. Comprobar que se visualiza la documentación en la URL del repositorio ```https://<nombreUsuario>.github.io/<nombreRepositorio>/```

# Funcionamiento general
El control de versiones con GitHub se puede utilizar tanto para gestionar el código fuente de un proyecto de software como para generar la documentación del propio proyecto. Estas son las indicaciones para generar la documentación. 

Una vez que se ha creado el proyecto y realizado los pasos iniciales, el proceso para generar la documentación puede tener dos modos de funcionamiento:

* **MODO LOCAL**

    Es el modo **normal de funcionamiento para generar la documentación**, creando los archivos de la documentación y visualizándolos en localhost.

   1. Realizar cambios en los archivos de la documentación.
   2. `npm run clean` - script para limpiar la carpeta de salida y la caché
   3. `npm run start` - script para iniciar el servidor local y comprobar que se visualiza la documentación en localhost.

* **MODO WEB**

    Es el modo para **publicar la documentación en GitHub Pages**. También se debe utilizar **al final de cada sesión de trabajo para actualizar los cambios realizados** a la documentación y que se actualice la página web.

    1. Realizar cambios en los archivos de la documentación.
    2. `npm run clean` - script para limpiar la carpeta de salida y la caché
    3. `npm run build-ghpages` - script para generar la carpeta de salida con el pathPrefix correcto para GitHub Pages.
    4. Realizar un commit y subir los cambios al repositorio de GitHub utilizando GitHub Desktop o la terminal integrada de Visual Studio Code.

Cada vez que se suben los cambios al repositorio de GitHub, gracias a GitHub Actions se genera automáticamente la página web. Los cambios en la página web de GitHub Pages no se generan al instante, según lo extensa y complicada que sea la documentación, tardará un tiempo en actualizarse *(generalmente unos pocos minutos)*.

# Actualización de Eleventy
Para actualizar Eleventy a la última versión, se pueden seguir los siguientes pasos:

1. `npm install @11ty/eleventy@latest` - actualiza Eleventy a la última versión.
2. `npm audit fix` - corrige vulnerabilidades de seguridad.
3. `npx @11ty/eleventy` - para iniciar Eleventy.