---
title: Tablas
description: Creación y formato de tablas.
layout: libdoc_page.liquid
permalink: /pages/n1-crear-contenido/n2-markdown/n3-tablas/index.html
eleventyNavigation:
    key: Tablas
    parent: Markdown
    order: 6
tags:
    - contenido
    - markdown
    - tablas
date: 2026-03-27
---

Las tablas en Markdown fueron creadas por [Github Flavoured Markdown](https://github.github.com/gfm/#tables-extension-) como una extensión de las [especificaciones de Markdown](https://daringfireball.net/projects/markdown/syntax).

Las tablas son responsivas y tienen desplazamiento horizontal habilitado si su contenido es más ancho que el ancho máximo del contenedor principal.

| Primera columna       | Segunda               | Tercera |
| -------------         |:-------------:        | -------:|
| La columna 3 está     | alineada a la derecha |    1600 |
| La columna 2 está     | centrada              |      12 |
| Líneas alternativas   | están ordenadas       |       1 |

| Año | Película                                          | Director       | Compositor          |
|------|-----------------------------------------------|----------------|-------------------|
| 2001 | Harry Potter and the Philosopher's Stone      | Chris Columbus | John Williams     |
| 2002 | Harry Potter and the Chamber of Secrets       | Chris Columbus | John Williams     |
| 2004 | Harry Potter and the Prisoner of Azkaban      | Alfonso Cuarón | John Williams     |
| 2005 | Harry Potter and the Goblet of Fire           | Mike Newell    | Patrick Doyle     |
| 2007 | Harry Potter and the Order of the Phoenix     | David Yates    | Nicholas Hooper   |
| 2009 | Harry Potter and the Half-Blood Prince        | David Yates    | Nicholas Hooper   |
| 2010 | Harry Potter and the Deathly Hallows – Part 1 | David Yates    | Alexandre Desplat |
| 2011 | Harry Potter and the Deathly Hallows – Part 2 | David Yates    | Alexandre Desplat |


**Debe de haber al menos 3 guiones separando cada celda de encabezado.**
Las barras verticales (|) son opcionales, y no necesitas hacer que la línea de Markdown raw se vea bonita. También puedes usar Markdown en línea dentro de las celdas de la tabla.

Markdown | Es menos | bonito
--- | --- | ---
*Aún* | `renderiza` | **bien**
1 | 2 | 3

```markdown
| Primera columna       | Segunda               | Tercera |
| -------------         |:-------------:        | -------:|
| La columna 3 está     | alineada a la derecha |    1600 |
| La columna 2 está     | centrada              |      12 |
| Líneas alternativas   | están ordenadas       |       1 |

| Año  | Película                                      | Director       | Compositor          |
|------|-----------------------------------------------|----------------|-------------------|
| 2001 | Harry Potter and the Philosopher's Stone      | Chris Columbus | John Williams     |
| 2002 | Harry Potter and the Chamber of Secrets       | Chris Columbus | John Williams     |
| 2004 | Harry Potter and the Prisoner of Azkaban      | Alfonso Cuarón | John Williams     |
| 2005 | Harry Potter and the Goblet of Fire           | Mike Newell    | Patrick Doyle     |
| 2007 | Harry Potter and the Order of the Phoenix     | David Yates    | Nicholas Hooper   |
| 2009 | Harry Potter and the Half-Blood Prince        | David Yates    | Nicholas Hooper   |
| 2010 | Harry Potter and the Deathly Hallows – Part 1 | David Yates    | Alexandre Desplat |
| 2011 | Harry Potter and the Deathly Hallows – Part 2 | David Yates    | Alexandre Desplat |

Markdown | Es menos | bonito
--- | --- | ---
*Aún* | `renderiza` | **bien**
1 | 2 | 3
```
