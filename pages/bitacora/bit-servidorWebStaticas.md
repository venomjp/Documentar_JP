---
title: Servidor de páginas web estáticas
description: Cómo instalar y configurar un servidor de páginas web estáticas con Caddy.
layout: libdoc_page.liquid
permalink: "{{ libdocConfig.blogSlug }}/{{title | slugify}}/index.html"
tags:
    - post
    - caddy
    - web server
    - páginas estáticas
date: 2026-08-12
---

# Usuario y permisos

* **USUARIO webadmin**

  Creamos un usuario específico `webadmin` para administrar las páginas web:

  ```bash
    sudo adduser webadmin
  ```

  No utilizamos `root` para trabajar con las páginas.

  `id webadmin` - para comprobar que el usuario se ha creado correctamente.
  ```
  uid=1001(webadmin)
  gid=1001(webadmin)
  groups=1001(webadmin),100(users)
  ```
  La finalidad es que `webadmin`sea el propietario de: `/opt/static-sites` y de todo su contenido.

* **DIRECTORIO /opt/static-sites**
  
  Creamos el directorio `/opt/static-sites` y le asignamos la propiedad al usuario `webadmin`:

  ```bash
    sudo mkdir -p /opt/static-sites
    sudo chown -R webadmin:webadmin /opt/static-sites
  ```

* **PERMISOS de los sitios**
Queremos que:

  * `webadmin`pueda modificar las páginas
  * Caddy pueda leerlas
  * Los directorios puedan ser atravesados por Caddy
  * Los archivos puedan ser leídos por Caddy
  * Por eso usamos como permisos normales:
  ```
  Directorios -> 755
  Archivos    -> 644
  ```

  Para cambiar los permisos de un sitio existente:
  ```bash
    sudo chown -R webadmin:webadmin /opt/static-sites/mi-sitio

    sudo find /opt/static-sites/mi-sitio -type d -exec chmod 755 {} \;
    sudo find /opt/static-sites/mi-sitio -type f -exec chmod 644 {} \;
  ```

* **ACL para Caddy**
  
  Caddy necesita poder leer los archivos y atravesar los directorios. Para ello, añadimos una ACL al directorio `/opt/static-sites` para que el usuario `caddy` pueda acceder a él:

  ```bash
    sudo setfacl -R -m u:caddy:rx /opt/static-sites
  ```
  Pero esto por sí solo no es suficiente para futuros sitios.
  Necesitamos ACL por defecto en `/opt/static-sites` para que todos los nuevos sitios tengan la ACL correcta:

  ```bash
    sudo setfacl -m d:u::rwx,d:u:caddy:rx,d:u:webadmin:rwx,d:g::r-x,d:m::rwx,d:o::r-x /opt/static-sites
  ```
  La consecuencia es que cuando `webadmin` crea o copia un nuevo sitio, los nuevos archivos y directorios heredan automáticamente una ACL que permite a Caddy acceder a ellos. 


# Caddy
* **INSTALACIÓN de Caddy**
  
  ```bash
    sudo apt install caddy
  ```
  * El binario de Caddy se encuentra en `/usr/bin/caddy`.
  * El servicio oficial systemd está en `/usr/lib/systemd/system/caddy.service`.
  * Es recomendable usar la instalación oficial de Caddy:
    * Comprobar versión: `caddy version`
    * Comprobar estado del servicio: `systemctl status caddy`

* **USUARIO utilizado por Caddy**

  La instalación oficial de Caddy crea su propio usuario `caddy`. No hacemos que Caddy sea propietario de las páginas. Esto es importante, mantener una separación de responsabilidades y permisos:
  ```
    webadmin  -> propietario / administrador
    caddy     -> servidor web / lectura
  ```

* **CONFIGURACIÓN de Caddy /etc/caddy/Caddyfile**
  
  La configuración de Caddy se encuentra en `/etc/caddy/Caddyfile`. 
  
  El siguiente código es el que he utilizado, de manera que Caddy sirve una página principal localizada en el directorio `/usr/share/caddy` y la carpeta donde cargaremos nuestros sitios web estáticos, cada uno en un directorio `/opt/static-sites/`:

  ```
  # El archivo Caddyfile es la forma más sencilla de configurar
  # tu Caddy como servidor de páginas web.
  #
  # La primera línea sin comentar será siempre la dirección de
  # tu sitio web.
  :80 {

    # ============================================================
    # PÁGINA PRINCIPAL
    # ============================================================
    # Utilizo la misma ubicación que la página de ejemplo de Caddy.
    # Nuestra página principal se actualiza cada vez que se crea o
    # se borra una carpeta de /opt/static-sites.
    # Se reescribe la página index.html con los enlaces a cada
    # web estática que subamos.

    route {
        @principal path /
        handle @principal {
            root * /usr/share/caddy
            file_server
        }

    # ============================================================
    # SITIOS
    # ============================================================
    # Permite presentar cada sitio web estático sin tener que
    # reescribir este archivo Caddyfile
        handle {
             root * /opt/static-sites
             file_server
        }
    }
  }

  ```

  Esto indica que Caddy servirá:
  * La página principal en: `http://pluton/` 
  * Los sitios web estáticos en: `http://pluton/mi-sitio` donde `mi-sitio` es el nombre de la carpeta que contiene los archivos de la página.

# Generador auromático del index.html principal

  La página principal se encuentra en `/usr/share/caddy/index.html`. 
  Esta página se reescribe automáticamente cada vez que se crea o borra un sitio web estático en `/opt/static-sites`. 
  Contiene enlaces a cada uno de los sitios web estáticos disponibles.

* **PERMISOS**
  
  Aquí hay una cuestión importante de permisos. El destino es `/usr/share/caddy/index.html`, que pertenece al sistema/Caddy, no a `webadmin`. Por lo tanto, el script que genera la página principal debe ejecutarse con los permisos necesarios para modificar ese archivo.

* **AUTOMATIZACIÓN**

  Para evitar tener que ejecutar manualmente el script cada vez que se crea o borra un sitio web estático, podemos usar un servicio systemd que observe el directorio `/opt/static-sites` y ejecute automáticamente el script cuando haya cambios.

  La solución está formada por dos unidades:

    * `/etc/systemd/system/generate-static-sites-index.service` - el servicio que ejecuta el script para generar la página principal, define qué hacer.
      `sudo nano /etc/systemd/system/generate-static-sites-index.service`
      ```
      [Unit]
      Description=Generar índice de sitios web estáticos

      [Service]
      Type=oneshot
      ExecStart=/usr/local/bin/generate-static-sites-index.sh
      ```

  * `/etc/systemd/system/generate-static-sites-index.path` - la unidad que observa el directorio `/opt/static-sites` y activa el servicio cuando hay cambios, define cuándo hacerlo.
      `sudo nano /etc/systemd/system/generate-static-sites-index.path`
      ```
      [Unit]
      Description=Detectar cambios en los sitios web estáticos

      [Path]
      PathChanged=/opt/static-sites
      Unit=generate-static-sites-index.service

      [Install]
      WantedBy=multi-user.target
    ```
* **SCRIPT para generar la página principal**
  
  El script `/usr/local/bin/generate-static-sites-index.sh` es el que genera la página principal `index.html` con los enlaces a cada sitio web estático. 
  Este script debe tener permisos de ejecución y ser propiedad de root, ya que modifica un archivo del sistema.

  `sudo nano /usr/local/bin/generate-static-sites-index.sh`

  ```
      #!/bin/bash

      set -e

      SITES_DIR="/opt/static-sites"
      INDEX="/usr/share/caddy/index.html"

      {
          cat <<'EOF'
      <!DOCTYPE html>
      <html lang="es">
      <head>
          <meta charset="UTF-8">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>Servidor web</title>
          <style>
              body {
                  font-family: Arial, sans-serif;
                  max-width: 900px;
                  margin: 40px auto;
                  padding: 0 20px;
                  background: #f5f5f5;
                  color: #222;
              }

              .container {
                  background: white;
                  padding: 30px;
                  border-radius: 10px;
                  box-shadow: 0 2px 10px rgba(0,0,0,.1);
              }

              h1 {
                  margin-top: 0;
              }

              ul {
                  padding-left: 20px;
              }

              li {
                  margin: 12px 0;
              }

              a {
                  color: #1769aa;
                  text-decoration: none;
              }

              a:hover {
                  text-decoration: underline;
              }
          </style>
      </head>

      <body>
      <div class="container">

      <h1>Servidor web</h1>

      <p>
          Caddy está funcionando correctamente.
      </p>

      <h2>Sitios disponibles</h2>

      <ul>
      EOF

          find "$SITES_DIR" -mindepth 1 -maxdepth 1 -type d -printf '%f\n' \
              | sort -f \
              | while IFS= read -r site; do
                  printf '    <li><a href="/%s/">%s</a></li>\n' \
                      "$site" "$site"
              done

          cat <<'EOF'
      </ul>

      </div>
      </body>
      </html>
      EOF

      } > "$INDEX"

      chown root:caddy "$INDEX"
      chmod 644 "$INDEX"
  ```
  Guardamos el script y le damos permisos de ejecución:

  ```bash
    sudo chmod 755 /usr/local/bin/generate-static-sites-index.sh
  ```

# Activación del servicio y la unidad de observación

  Para que el servicio y la unidad de observación funcionen correctamente, debemos habilitarlos y arrancarlos:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now  generate-static-sites-index.path
sudo systemctl start generate-static-sites-index.service
sudo systemctl status generate-static-sites-index.service
```

  * Esto asegura que cada vez que se cree o borre un sitio web estático en `/opt/static-sites`, el script se ejecutará automáticamente para actualizar la página principal `index.html`.

  * No hay que cambiar permisos siempre que `webadmin` sea el propietario de `/opt/static-sites`, y que Caddy tenga la ACL adecuada para leer los archivos.

  * Al copiar mediante `scp -r`los archivos de un sitio web estático al directorio `/opt/static-sites`, se heredan automáticamente los permisos y ACL correctos, gracias a la configuración que hemos hecho.
  
  * Con este sistema no debemos añadir nada al `Caddyfile`. La nueva web estará automáticamente disponible en `http://pluton/nombre-del-sitio/` y la página principal se actualizará con el enlace correspondiente.
  * No hace falta reiniciar ni recargar Caddy, ya que el servicio de observación y el script se encargan de actualizar la página principal automáticamente. En caso de necesitarlo la instrucción es: `sudo systemctl reload caddy`.