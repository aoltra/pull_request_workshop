#  Taller Pull Request (PR)

Repo para hacer pruebas de PR en **GitHub**. 

Y de paso obtener un lista de canciones para programar y de películas para ver 😉

Uso únicamente académico.

# Flujo de trabajo

## Solicitud de PR

1. Loguearse en **GitHub**

2. Ir a la [url del repo](https://github.com/0492-0616-0379-PI-DAM-DAW-ASIR/pull_request_workshop) y hacer un fork del repositorio 

3. Clonar __fork__ en local

4. Crear una rama en el local para la nueva _feature_

    ```bash
    git checkout -b nueva_cancion
    ```

5. Añadir una (o más) nueva(s) canción(es) en el fichero _song4programming.md_

6. Hacer un _commit_ de la modificación

    ```bash
    git add song4programming.md
    git commit -m "feat: añadida nueva canción"
    ```
7. Subimos el _commit_ a nuestro repo 

    ```bash
    git push --set-upstream origin nueva_cancion
    ```

    > El uso de --set-upstream es debido a que la rama _nueva_cancion_ existe solo en local, y todavía no tiene ninguna relación con una rama en el servidor. _--set-upstream_ permite crearla en el remoto y vincularla. A partir de ese momento ya podremos usar simplemente _git push_.

    la salida del comando, entre otra información, nos indicará algo similar :
    
    ```bash
    remote: Create a pull request for 'nueva_cancion' on GitHub by visiting:
    remote:      https://github.com/GITHUB_USER/pull_request_workshop/pull/new/nueva_cancion
    ```

    Es decir, se nos indica que nos conectemos a nuestro _fork_ para poder solicitar un _PR_.

  8. Acceder a nuestro repo en GitHub y pulsar sobre _Compare & PR_

  9. Crear el PR

     * Indicar sobre quién y desde dónde se quiere hacer el PR. A la izquierda se indica el repo original y la derecha la rama de nuestro repo (el _fork_). En general viene configurado correctamente por defecto.

     * Indicar un título al PR. Por defecto viene asignado el mensaje del commit

     * Añadir una descripción. Es muy importante explicar con detalle que se ha hecho, que mejoras se añaden, qué errores se corrigen... 

     * Pulsamos en _Create Pull Request_

## Revisión

1. El revisor se loguea en **GitHub**

2. Una vez se accede al repo, en la barra superior aparecerán los PR pendientes.

3. El PR puede haber sido asignado a un revisor determinado o que alguien del equipo tenga una solictud para aceptar ser el revisor de ese PR. En este caso el revisor puede asignarse a si mismo u optar por solictar a otro(s) revisor(es) que se encarguen de ese PR.

4. Una vez está asignado, desde dentro del PR se puede acceder a la revisión.

5. Aprobar el PR, hacer un comentario o solicitar cambios para que pueda ser aprobada en un futuro.

6. Hacer la fusión con la rama principal. Para ello hay que elegir la estrategia de fusionado.

## Actualización del repo local

Si el PR ha sido aprobado y fusionado lo más adecuado es actualizar nuestro repo local, eliminando la rama de la feature y actualizando el código desde el repo original.

1. Añadir, si no lo está, el repositorio original como remoto. 
 
   **Git** por defecto sólo crea como remoto aquel repositorio desde el cual se ha clonado. En nuestro caso como la clonación se ha hecho a partir del _fork_ realizado del repositorio original, es este él digo que está configurado (generalmente con el alias _origin_). 

   ```bash
   $ git remote -v                                                                
   origin  git@github.com:GITHUB_USER/pull_request_workshop.git (fetch)
   origin  git@github.com:GITHUB_USER/pull_request_workshop.git (push)
   ```

   Es decir, nuestra repo local no sabe de al existencia del repo original, de aquel que hemos "forkeado".

   Para poder tener acceso a su código y actualizar debemos añadir otro remoto, en nuestro caso:

   ```bash
   $ git remote add upstream git@github.com:0492-0616-0379-PI-DAM-DAW-ASIR/pull_request_workshop.git
   $ git remote -v                                                                                  
   origin  git@github.com:GITHUB_USER/pull_request_workshop.git (fetch)
   origin  git@github.com:GITHUB_USER/pull_request_workshop.git (push)
   upstream  git@github.com:0492-0616-0379-PI-DAM-DAW-ASIR/pull_request_workshop.git (fetch)
   upstream  git@github.com:0492-0616-0379-PI-DAM-DAW-ASIR/pull_request_workshop.git (push)
   ```

2. En el repo local, cambiar a la rama _main/master_

   ```bash
   $ git checkout main
   ```

3. Borrar la rama local

   ```bash
   $ git branch -d nueva_cancion
   ```

4. Borrar la rama remota del _fork_ (_origin_)

   ```bash
   $ git push origin --delete nueva_cancion
   ```

5. Traer los cambios desde el repo original (_upstream_)

   ```bash
   $ git fetch upstream
   remote: Enumerating objects: 16, done.
   remote: Counting objects: 100% (16/16), done.
   remote: Compressing objects: 100% (8/8), done.
   remote: Total 13 (delta 5), reused 11 (delta 4), pack-reused 0 (from 0)
   Desempaquetando objetos: 100% (13/13), 3.81 KiB | 354.00 KiB/s, listo.
   Desde github.com:0492-0616-0379-PI-DAM-DAW-ASIR/pull_request_workshop
    * [nueva rama]      main       -> upstream/main
   ```

6. Fusionamos los cambios descagados a la rama local, eligiendo la opción de fusionado que queramos. Por ejemplo:

   ```bash
   $ git merge upstream/main
   ```

   o

   ```bash
   git rebase upstream/main
   ```

7. Ya tenemos actualizado el repo local, pero no nuestro fork de GitHub (_origin_). Simplemente subimos los cambios

   ```bash
   $ git push origin main
   ```

