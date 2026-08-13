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
  
  Esta parte es informativa y no hace falta ejecutar ningún comando.
  Buscamos que:

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

* **CADDYFILE - CONFIGURACIÓN de Caddy**
  
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
      
      # No permitir dos ejecuciones simultáneas
      ExecStartPre=/usr/bin/test -d /opt/static-sites

      # Esperar como máximo 10 minutos
      TimeoutStartSec=10min
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

      set -euo pipefail

      SITES_DIR="/opt/static-sites"
      INDEX="/usr/share/caddy/index.html"

      echo "Esperando a que finalicen los cambios..."

      # ============================================================
      # ESPERAR A QUE EL ÁRBOL DE SITIOS SE ESTABILICE
      # ============================================================

      # Comprobamos varias veces que el número/tamaño de archivos
      # no esté cambiando.
      #
      # Esto evita procesar un sitio mientras todavía se está copiando.

      previous_state=""
      stable_count=0

      while [ "$stable_count" -lt 3 ]; do

          current_state=$(
              find "$SITES_DIR" \
                  -mindepth 1 \
                  -maxdepth 2 \
                  ! -name '.*' \
                  -printf '%p %s %T@\n' \
                  2>/dev/null |
              sort
          )

          if [ "$current_state" = "$previous_state" ]; then
              stable_count=$((stable_count + 1))
          else
              stable_count=0
              previous_state="$current_state"
          fi

          sleep 2
      done

      echo "Árbol de sitios estabilizado."


      # ============================================================
      # PROCESAR SITIOS
      # ============================================================

      find "$SITES_DIR" \
          -mindepth 1 \
          -maxdepth 1 \
          -type d \
          ! -name '.*' \
          -print0 |
      while IFS= read -r -d '' SITE; do

          echo "Procesando permisos: $SITE"

          # --------------------------------------------------------
          # Propietario
          # --------------------------------------------------------

          chown -R webadmin:webadmin "$SITE"

          # --------------------------------------------------------
          # Directorios
          #
          # 755 permite:
          #   webadmin -> rwx
          #   caddy    -> r-x
          #   pluton   -> r-x
          # --------------------------------------------------------

          find "$SITE" -type d -exec chmod 755 {} +

          # --------------------------------------------------------
          # Archivos
          #
          # 644 permite:
          #   webadmin -> rw-
          #   caddy    -> r--
          #   pluton   -> r--
          # --------------------------------------------------------

          find "$SITE" -type f -exec chmod 644 {} +

          # --------------------------------------------------------
          # ACL para Caddy
          #
          # Directorios necesitan r-x para poder atravesarlos.
          # Archivos necesitan r-- para poder leerlos.
          # --------------------------------------------------------

          find "$SITE" -type d \
              -exec setfacl -m u:caddy:r-x,m:r-x {} +

          find "$SITE" -type f \
              -exec setfacl -m u:caddy:r--,m:r-- {} +

          # --------------------------------------------------------
          # ACL POR DEFECTO
          #
          # Esto garantiza que cualquier archivo/directorio creado
          # posteriormente dentro del sitio herede permisos adecuados.
          # --------------------------------------------------------

          find "$SITE" -type d \
              -exec setfacl -m d:u::rwx,d:u:caddy:r-x,d:u:webadmin:rwx,d:g::r-x,d:m::rwx,d:o::r-x {} +

      done


      # ============================================================
      # GENERAR PÁGINA PRINCIPAL
      # ============================================================

      TMP_INDEX=$(mktemp)

      cat > "$TMP_INDEX" <<'EOF'
      <!DOCTYPE html>
      <html lang="es">
      <head>
          <meta charset="UTF-8">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">

          <title>Servidor Caddy - Sitios web</title>

          <style>
              body {
                  background: #f1f4f5;
                  font-family: Arial, sans-serif;
                  font-size: 18px;
                  margin: 0;
                  padding: 40px;
              }

              .container {
                  background: white;
                  max-width: 1000px;
                  margin: auto;
                  padding: 30px;
                  border-radius: 10px;
                  box-shadow: 0 2px 10px rgba(0,0,0,.1);
              }

              h1 {
                  margin-top: 0;
              }

              ul {
                  padding-left: 25px;
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

          <h1>Servidor Caddy - Sitios web</h1>

          <p>Listado de sitios web estáticos disponibles:</p>

          <ul>
      EOF

      # Generar automáticamente la lista de sitios.
      find "$SITES_DIR" \
          -mindepth 1 \
          -maxdepth 1 \
          -type d \
          ! -name '.*' \
          -printf '%f\n' |
      sort -f |
      while IFS= read -r site; do

          printf '        <li><a href="/%s/">%s</a></li>\n' \
              "$site" "$site"

      done >> "$TMP_INDEX"

      cat >> "$TMP_INDEX" <<'EOF'
          </ul>

      </div>

      </body>
      </html>
      EOF


      # ============================================================
      # INSTALAR ÍNDICE
      # ============================================================

      chown root:caddy "$TMP_INDEX"
      chmod 644 "$TMP_INDEX"

      mv "$TMP_INDEX" "$INDEX"

      echo "Índice generado correctamente."

  ```

# Activación del servicio y la unidad de observación

  Para que el servicio y la unidad de observación funcionen correctamente, debemos habilitarlos y arrancarlos:

  ```
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

# Script en Windows

* **IDEA Y FUNCIONAMIENTO**

  La idea es tener un script en Windows que haga todo el trabajo:
    1. Preparar un directorio temporal en el servidor para subir el sitio web estático. El nombre del directorio temporal será generado automáticamente con el nombre del directorio donde se ejecute el script, siempre que contenga una carpeta. Los directorios .tmp son excluidos en la detección de modificaciones en la carpeta `/opt/static-sites`, así la automatización no detecta cambios mientras se suben los archivos.
    2. Copiar la carpeta `_site` al directorio temporal anterior, ya que el proceso de carga puede tardar un tiempo y queremos que la automatización no detecte cambios mientras se suben los archivos.
    3. Mover el directorio temporal al directorio final en `/opt/static-sites/`, esto dispara la automatización que genera la página principal.
    4. Los permisos, tanto de propietario como de ACL, se heredan automáticamente, por lo que no es necesario hacer nada más.

* **UBICACIÓN DEL SCRIPT**

  El script de Windows se ubica en la carpeta `C:\Users\juanp\Scripts\`. Contiene:
  - <samp>subir-sitio.ps1</samp> - script de PowerShell que realiza la subida del sitio web estático al servidor y ejecuta el script para generar la página principal.
  - <samp>subir-sitio.cmd</samp> - lanzador que permite ejecutar el script unicamente con la instrucción `subir-sitio`.

* **CONTENIDO DEL SCRIPT**

  `edit subir-sitio.ps1` y pegar el siguiente contenido:

  ```
      # ============================================================
      # SUBIR SITIO WEB ESTÁTICO A PLUTON
      # ============================================================

      $ErrorActionPreference = "Stop"

      # ============================================================
      # CONFIGURACIÓN
      # ============================================================

      $RemoteUser = "webadmin"
      $RemoteHost = "pluton"
      $RemoteBase = "/opt/static-sites"

      # ============================================================
      # DIRECTORIO ACTUAL
      # ============================================================

      $ProjectPath = (Get-Location).Path
      $SiteName = Split-Path $ProjectPath -Leaf

      # ============================================================
      # RUTA _site
      # ============================================================

      $SitePath = Join-Path $ProjectPath "_site"

      # ============================================================
      # COMPROBACIONES
      # ============================================================

      if (-not (Test-Path $SitePath -PathType Container)) {

          Write-Host ""
          Write-Host "ERROR: No existe la carpeta _site." -ForegroundColor Red
          Write-Host ""
          Write-Host "Directorio actual:"
          Write-Host $ProjectPath
          Write-Host ""
          exit 1
      }

      if ([string]::IsNullOrWhiteSpace($SiteName)) {

          Write-Host ""
          Write-Host "ERROR: No se ha podido determinar el nombre del sitio." -ForegroundColor Red
          Write-Host ""
          exit 1
      }

      # ============================================================
      # INFORMACIÓN
      # ============================================================

      $TempName = ".uploading_$SiteName"

      $RemoteTemp = "$RemoteBase/$TempName"
      $RemoteFinal = "$RemoteBase/$SiteName"

      Write-Host ""
      Write-Host "============================================"
      Write-Host " SUBIDA DE SITIO WEB ESTÁTICO"
      Write-Host "============================================"
      Write-Host ""
      Write-Host "Proyecto : $SiteName"
      Write-Host "Origen   : $SitePath"
      Write-Host "Destino  : $RemoteFinal"
      Write-Host ""

      # ============================================================
      # CONFIRMACIÓN
      # ============================================================

      $Answer = Read-Host "¿Continuar con la subida? [S/N]"

      if ($Answer -notmatch "^[sS]$") {

          Write-Host ""
          Write-Host "Operación cancelada."
          Write-Host ""

          exit 0
      }

      # ============================================================
      # CREAR DIRECTORIO TEMPORAL
      # ============================================================

      Write-Host ""
      Write-Host "1. Preparando directorio temporal..."

      ssh "$RemoteUser@$RemoteHost" "rm -rf '$RemoteTemp' && mkdir -p '$RemoteTemp'"

      if ($LASTEXITCODE -ne 0) {

          Write-Host ""
          Write-Host "ERROR: No se pudo crear el directorio temporal." -ForegroundColor Red
          Write-Host ""

          exit 1
      }

      # ============================================================
      # COPIAR CONTENIDO DE _site
      # ============================================================

      Write-Host ""
      Write-Host "2. Copiando contenido de _site..."
      Write-Host ""

      # El punto después de _site significa:
      #
      #   copiar EL CONTENIDO de _site
      #
      # y no crear:
      #
      #   /opt/static-sites/Nombre/_site/
      #
      # De esta forma obtenemos directamente:
      #
      #   /opt/static-sites/Nombre/index.html
      #   /opt/static-sites/Nombre/assets/
      #   /opt/static-sites/Nombre/core/
      #   etc.
      #
      # También permite incluir archivos ocultos.

      scp -r "$SitePath\." "$RemoteUser@$RemoteHost`:$RemoteTemp/"

      if ($LASTEXITCODE -ne 0) {

          Write-Host ""
          Write-Host "ERROR: La copia ha fallado." -ForegroundColor Red
          Write-Host ""
          Write-Host "Eliminando directorio temporal..."

          ssh "$RemoteUser@$RemoteHost" "rm -rf '$RemoteTemp'"

          exit 1
      }

      # ============================================================
      # INSTALAR EL SITIO
      # ============================================================

      Write-Host ""
      Write-Host "3. Instalando sitio..."

      # El sitio definitivo solo aparece cuando la copia completa
      # ha terminado.
      #
      # Si ya existía una versión anterior, se sustituye ahora.

      $RemoteCommand = "rm -rf '$RemoteFinal' && mv '$RemoteTemp' '$RemoteFinal'"

      ssh "$RemoteUser@$RemoteHost" $RemoteCommand

      if ($LASTEXITCODE -ne 0) {

          Write-Host ""
          Write-Host "ERROR: No se pudo instalar el sitio." -ForegroundColor Red
          Write-Host ""

          ssh "$RemoteUser@$RemoteHost" "rm -rf '$RemoteTemp'"

          exit 1
      }

      # ============================================================
      # FINAL
      # ============================================================

      Write-Host ""
      Write-Host "============================================"
      Write-Host " SITIO COPIADO CORRECTAMENTE"
      Write-Host "============================================"
      Write-Host ""
      Write-Host "Sitio : $SiteName"
      Write-Host "URL   : http://$RemoteHost/$SiteName/"
      Write-Host ""
      Write-Host "Los permisos, ACL e índice se procesarán"
      Write-Host "automáticamente en Pluton."
      Write-Host ""
  ```

* **LANZADOR**

  `edit subir-sitio.cmd` y pegar el siguiente contenido:

  ```
    @echo off

    powershell.exe -ExecutionPolicy Bypass -File "%USERPROFILE%\Scripts\subir-sitio.ps1"

    if errorlevel 1 (
      echo.
      echo ERROR: La subida del sitio ha fallado.
      echo.
      pause
        exit /b 1
    )

    echo.
    echo Sitio subido correctamente.
    echo.
    pause
  ```

* **AÑADIR EL SCRIPT A LA VARIABLE DE ENTORNO PATH**

  No necesitamos modificar el PATH del sistema. Lo añadiremos solo para tu usuario.

  Ejecuta:
  ```
    [Environment]::SetEnvironmentVariable(
    "Path",
    [Environment]::GetEnvironmentVariable("Path", "User") + ";C:\Users\juanp\Scripts",
    "User"
    )
  ```

  * <mark>Importante</mark>

      * Cierra completamente PowerShell y abre una nueva ventana.

      * Esto es necesario para que la nueva sesión recoja el PATH actualizado.

  * <mark>Comprobar el PATH</mark>

    * En la nueva PowerShell: `$env:Path -split ";"`

    * Entre las entradas debería aparecer: `C:\Users\juanp\Scripts`

    * También puedes comprobar directamente: `$env:Path -like "*C:\Users\juanp\Scripts*"`

    * Debe devolver: `True`

* **USO DEL SCRIPT**

  El flujo queda reducido a situarse en la carpeta del proyecto y ejecutas `subir-sitio`. El script detectará automáticamente el nombre del proyecto y realizará la subida al servidor. Nos pedirá la contraseña del usuario `webadmin` en el servidor varias veces.

  ```
    cd C:\ruta\del\proyecto
    subir-sitio
  ```

  Aparecerá algo como lo siguiente en la terminal de PowerShell:
  ```
    ============================================
    SUBIDA DE SITIO WEB ESTÁTICO
    ============================================

    Proyecto : Documentar_Proyecto
    Origen   : C:\Users\juanp\Proyectos\Documentar_Proyecto\_site
    Destino  : /opt/static-sites/Documentar_Proyecto

    ¿Continuar con la subida? [S/N]: s

    1. Preparando directorio temporal...
    webadmin@pluton's password:

    2. Copiando contenido de _site...
    webadmin@pluton's password:
    busquedaDifusa.png            100%   24KB 123.0KB/s   00:00
    ...

    3. Instalando sitio...
    webadmin@pluton's password:

    ============================================
    SITIO COPIADO CORRECTAMENTE
    ============================================

    Sitio : Documentar_Proyecto
    URL   : http://pluton/Documentar_Proyecto/

    Los permisos, ACL e índice se procesarán
    automáticamente en Pluton.
  ```