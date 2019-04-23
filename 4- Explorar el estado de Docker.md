# Explorar el estado de Docker

- docker ps = lista los contenedores
- docker ps -a = lista contenedores a detalles
- docker ps -aq = lista solo los ID de los contenedores (la q significa quiet, tranquilo o silencioso)

- docker inspect id_contenedor = detalles internos del contenedor
- docker inspect nombre_contenedor = lo mismo que el anterior
- docker inspect -f {{}} nombre_contenedor = filtra una variable especifico del contenedor
    - Ejemplo : docker inspect -f {{ json .Config.Env}}

- docker rm nombre_contenedor = elimina un contenedor
- docker rm $(ps -aq) = borra TODOS los contenedores que no esten corriendo
- docker rm -f $(docker ps -aq)  = borra TODOS los contenedores incluso si estan corriendo.

- docker rename current_name new_name = renombra un contenedor

- docker logs contenedor = muestra el log de un contenedor

