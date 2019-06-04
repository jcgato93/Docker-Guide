# Docker in Docker 

- Una las areas donde mas se utiliza docker es en entornos de integracion continua por que es mucho mas facil de mantener.

- Un problema al correr docker desde el host es que los scripts que se ejecuten en como por ejemplo los que dejamos en el docker file corren de manera nativa al host , por lo que no es lo mismo el listar los archivos y directorios en windows con el comando "dir" que en linux que es con el comando "ls". Entonces una forma de resolver esto es utilizar Docker in Docker

- Docker in Docker es basicamente tener un contenedor con la imagen de docker donde podemos ejecutar los build de nuestras imagenes, haciendo que la reproduccion de un entorno de produccion real sea transparente.

## Ejecutar contedor de docker image

- La forma en la que interactua el cliente de docker con el demon de docker es atraves de un archivo de socket de linux , por lo que si montamos ese archivos al volumen de un contenedor de docker deberi ser la misma comunicacion como cliente del demon atraves de un contenedor 

        $docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock docker:[Version estable] 

Ejemplo        

    $docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock docker:latest