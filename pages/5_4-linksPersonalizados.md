---
title: Links personalizados
description: Muestra enlaces en la barra de navegación.
layout: libdoc_page.liquid
permalink: /pages/5-navegacion/5_4-linksPersonalizados/index.html
eleventyNavigation:
    key: Links personalizados
    parent: Navegación
    order: 4
tags:
    - navegación
    - links personalizados
date: 2026-03-26
---

Los links personalizados permiten mostrar enlaces en la barra de navegación. En general los voy a utilizar para enlazar con lo que puede estar relacionado con el proyecto:
* **Trello** - tablero de gestión del proyecto.
* **OneNote** - borradores y preparación del proyecto.
* **Nube** - carpeta con los archivos del proyecto.
* **Fusion** - enlace a la página de fusión del proyecto.
* **GitHub** - repositorio del proyecto o enlace a mi GitHub.

*En este proyecto he eliminado alguno de los enlaces personalizados.*

# Crear link personalizado
* Se crean en el archivo de configuración ```settings.json```
* Para crear un link personalizado, añade a la propiedad ```customLinks```:

<br>

```json
{
    "url": "https://ejemplo.com",
    "text": "Texto del enlace" 
}
```
