---
title: Funcionamiento general
description: Descripción de las distintas formas de crear y publicar las páginas.
layout: libdoc_page.liquid
permalink: /pages/2-funcionamiento/index.html
eleventyNavigation:
    key: Funcionamiento general
    order: 2
tags:
    - modo desarrollo
    - modo web pública en GitHub Pages
    - modo web privada en servidor propio
date: 2026-08-12
---
<img src="/assets/funcionamiento.png" 
  alt="Funcionamiento general" 
  style="width: 128px; height: 128px; display: block; margin: 0 auto;">

Hay tres modos de funcionamiento para generar la documentación de un proyecto y publicarla:

# Modo desarrollo

Es el modo **normal de funcionamiento para generar la documentación**, creando los archivos de la documentación y visualizándolos en localhost. 

**Pasos para generar el proyecto en modo local, los cambios se visualizan instantáneamente:**
   * `npm run clean` - script para limpiar (borra la carpeta de salida y la caché) antes de generar la documentación.
   * `npm run start` - script para iniciar el servidor local y comprobar que se visualiza la documentación en [localhost](http://localhost:8080/)

---

# Modo web pública en GitHub Pages

Si queremos tener una web pública de la documentación, se puede utilizar **GitHub Pages** para alojar la documentación de forma gratuita, el *proyecto debe ser público y accesible por cualquier persona*.


   * `npm run clean` - script para limpiar la carpeta de salida y la caché
   * `npm run build-ghpages` - script para generar la carpeta de salida con el pathPrefix correcto para GitHub Pages.
   * Realizar un commit y subir los cambios al repositorio de GitHub utilizando GitHub Desktop o la terminal integrada de Visual Studio Code.

Cada vez que se suben los cambios al repositorio de GitHub, gracias a GitHub Actions se genera automáticamente la página web. Los cambios en la página web de GitHub Pages no se generan al instante, según lo extensa y complicada que sea la documentación, tardará un tiempo en actualizarse *(generalmente unos pocos minutos)*.

---

# Modo web privada en servidor propio

En el caso de que no queramos que la documentación sea pública y accesible por cualquier persona, se puede alojar en un servidor propio, de esta forma la documentación será privada y solo se podrá acceder a ella desde el servidor donde esté alojada, en mi caso utilizo Tailscale para acceder a mi servidor desde cualquier lugar y dispositivo.

He intentado generar un procedimiento que permita alojar la documentación en un servidor propio usando Caddy para acceder a las páginas estáticas. En cuanto a la generación de la documentación, el procedimiento es el mismo que para GitHub Pages, pero en este caso se debe subir la carpeta de salida (_site) al servidor propio.

* **INSTALACIONES Y CONFIGURACIÓN DEL SERVIDOR**

    El procedimiento de instalación está documentado en: 

    [Servidor de páginas estáticas con Caddy](./bitacora/bit-servidorWebStaticas.md)


* **CARACTERÍSTICAS DEL SERVIDOR DE PÁGINAS ESTÁTICAS CON CADDY**
  
  * `webadmin` - Usuario específico para administrar los sitios.
  * Caddy solamente necesita leer los sitios y se utiliza el usuario `caddy` sin necesidad de crear usuarios adicionales.
  * Cada carpeta dentro de `/opt/static-sites` representa un sitio web independiente.
  * Se automatiza la detección de cambios en la carpeta de los sitios web y se reescribe la página principal que contiene una lista con accesos a cada sitio web.
  * Se crea un `Caddyfile` que genera automáticamente los accesos a cada sitio web cada vez que se sube un sitio, sin necesidad de cambiarlo manualmente.
  * Al copiar un nuevo sitio web mediante `scp`, los permisos se heredan automáticamente.
  * No es necesario reiniciar Caddy para que se apliquen los cambios, ya que se detectan automáticamente.


* **COPIAR SITIO AL SERVIDOR**

    Desde Windows y utilizando un terminal de PowerShell:
     1. Crear una carpeta local para el sitio. Debe tener el mismo nombre que el PathPrefix definido en el archivo `settings.json` del proyecto. Por ejemplo, si el PathPrefix es `/mi-proyecto`, la carpeta local debe llamarse `mi-proyecto`:
    
    ```ssh webadmin@pluton "mkdir -p /opt/static-sites/mi-proyecto"```
    
     2. Instrucción para copiar el contenido de la carpeta `_site`: 
    
    ```scp -r .\_site\* webadmin@pluton:/opt/static-sites/mi-proyecto/```


De manera automática se actualiza la página principal que contiene los accesos a cada sitio web `http://pluton.tailf0dd91.ts.net/`, y se debería poder acceder al sitio web desde la URL: `http://pluton.tailf0dd91.ts.net/mi-proyecto/` siempre que tengamos acceso a la red de Tailscale.