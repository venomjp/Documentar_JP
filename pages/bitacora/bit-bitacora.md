---
title: Cuaderno de bitácora
description: Cómo lo voy a utilizar, qué tipo de contenido voy a incluir, cómo lo voy a organizar, etc.
layout: libdoc_page.liquid
permalink: "{{ libdocConfig.blogSlug }}/{{title | slugify}}/index.html"
tags:
    - post
    - bitácora
    - cuaderno
date: 2026-03-24
---
# Imagen principal del post
![Cuaderno de Bitácora](/assets/cuadernoBitacora.jpg)
Esto es un cuaderno de bitácora. Me gusta insertar una imagen principal en cada post, justo debajo se puede incluir una descripción más detallada del contenido del post o una introducción.

# Cómo lo voy a utilizar
> *Voy a utilizar el BLOG como un cuaderno de BITÁCORA, un blog técnico o un diario de trabajo.* 

Cada entrada del blog será un post de cualquier cosa que me parezca relevante para el proyecto y que me gustaría tener documentada.

# Qué tipo de Contenido incluir
* Avances en el proyecto
* Cambios importantes que surgen durante el desarrollo
* Problemas encontrados en el proceso
* Soluciones aplicadas a esos problemas
* Distintas Versiones de firmware o software
* Notas técnicas
* Decisiones de diseño
* Aclaraciones sobre el proyecto
* Cosas aprendidas
* Recordatorios de aciertos y errores que me gustaría no olvidar

# Cómo organizarlo
En principio, todos los posts se organizan cronológicamente con el post más reciente en la parte superior. 
<br>Para facilitar la organización y búsqueda de los posts, es recomendable utilizar tags relacionados con el contenido del post. 

# Ubicación de las plantillas
Las plantillas de los posts se encuentran en la subcarpeta **pages/bitacora**.

# Formato de los nombres los posts
* El formato de los nombres de plantilla de los posts es: 
<br>```bit-``` + ```<nombre del post>.md```

* Sin embargo el formato de salida de los posts es:
<br>```{{ libdocConfig.blogSlug }}/``` + ```<nombre del post>/```+```index.html```

# Cabecera de los posts
Lo más importante es que cada post contenga el tag **post** que sirve para identificarlo como una entrada del (blog) cuaderno de bitácora. Además, es recomendable incluir otros tags relacionados con el contenido del post para facilitar su organización y búsqueda.

```yml
---
title: Título del post
description: Subtítulo del post o brevedescripción del post
layout: libdoc_page.liquid
permalink: "{{ libdocConfig.blogSlug }}/{{title | slugify}}/index.html"
tags:
    - post
    - tag relacionado con el contenido del post
date: 2026-03-26
---
![Imagen del post](/assets/cuadernoBitacora.jpg)

Contenido del post...

```
