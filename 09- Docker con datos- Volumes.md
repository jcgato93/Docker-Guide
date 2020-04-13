# Persistencia de datos en Docker con Volumes

https://docs.docker.com/storage/

Docker nos permite persistir los datos que se generan en un contenedor
la mas comun es <strong>Bind mount</strong> en la cual se da una ruta en
el host para guardar los datos pero suele tener inplicaciones de seguridad
e integridad ya que interacutua con el file System del host.

Docker evoluciono y creo otra forma de persistir los datos 
los <strong>Volumes</strong>.

## Volumes

Forma de persistir los datos que funciona de forma muy parecida a 
<strong>Bind mount</strong> , pero que en los procesos del host nunca acceden 
a esa ubicacion


## Interactuar con Volumes

- Listar los volumes existentes
    - docker volume ls

- Borrar volumes que no estan siendo usados por un contenedor
    - docker volume prune

- Crear Volume
    - docker volume create [nombre Volume]

- Utilizar un Volume
    - docker run -d --name [nombre container] --mount src=[nombre volume] , dst=[Ruta en  el contenedor que enlaza los datos que se guardan] [imagen a utilizar]

    - Ejemplo : $ docker run -d --name db --mount src=dbdata,dst=/data/db mongo


## Ventajas de utilizar Volumes

- Mayor seguridad
- Docker brinda herramientas para mover Volumnes de una computadora a otra
- Tiene herramientas para conectar contenedores de forma remota.
- Permite tener Volumes en la nube.
