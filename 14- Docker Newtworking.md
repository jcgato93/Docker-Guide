# Docker Newtworking

Debemos tener en cuenta que los contenedores se comportan en parte 
como maquinas virtuales, por lo que si queremos conectar con recursos de 
otro contenedor debemos crear primero una red para dicha comunicacion.

## Visualizar redes existentes

Corriendo el comando 

        $ docker network ls

este muestra las redes por defecto

- bridge : En desuso

- host: es la forma de docker de representar la red de la computadora

- none: si se ancla un contedor a esta red basicamente se le esta deshabilitando el network


## Crear una red

Corriendo el comando

        $ docker network create --attachable [nombre red]

el flat <strong>--attachable</strong> permite que otros contenedores se puedan unir a esta red.


## Conectar un contenedor a la red

- crear un contenedor de mongo 

        $ docker run -d  --name db mongo

- Añadir a la red

        $ docker network connect [nombre red] [contenedor]

ejemplo

        $ docker network connect mired db

## Conectar aplicaciones por medio del nombre del contenedor 

Teniendo la aplicacion de ejemplo docker-project creada con nodejs , esta usando una variable de entorno para la conexion a la base de datos de mongo

- Crear contenedor de la aplicacion

        $docker run -d --name app -p 3000:3000 --env MONGO_URL=mongodb://db:27017/[nombre db] [imagen]

MONGO_URL : es la variable de entorno que utiliza la aplicacion y donde <strong>db</strong> hace referencia al contenedor de mongo junto con el puerto

- Por ultimo debemos conectar el contenedor creado de la aplicacion a la misma red del contenedor de mongo

        $docker network connect [red] [contenedor]