# Imagenes de Docker

Las imágenes son un componente fundamental de Docker y sin ellas los contenedores no tendrían sentido. Estas imágenes son fundamentalmente plantillas o templates.
Algo que debemos tener en cuenta es que las imágenes no van a cambiar, es decir, una vez este realizada no la podremos cambiar.


Una imagen es un conjunto de capas , una sobre otra. Las 
capas son muy parecidas aun commit de git, por lo que si
se tiene la ultima version de la imagen no es necesario descargarla nuevamente , simplemente se debe especificar con que version se desea crear el contenedor.

## Trabajar con imagenes 

la foma mas sencilla de utilizar una imagen es descargandola 
des de dockerhub que es el repositorio de imagenes publicas que tiene
docker.

### Descargar una imagen

        docker pull [imagen]

ejemplo
    
        docker pull mongo


### Descargar una version especifica

        docker pull [imagen] : [version]

ejemplo 

        docker pull ubuntu:18.04


## Comandos 

- Listar imagenes
    
        docker image ls

- Eliminar una sola imagen

        docker rmi [image_name:version | image-id]

- Eliminar todas las imágenes

        docker rmi $(docker images -qf "dangling=true")

- Mata contenedores y quítalos:

        docker rm $(docker kill $(docker ps -aq))

Nota: Reemplazar kill con stop para un apagado correcto


- Eliminar todas las imágenes excepto "my-image"
Use grep para eliminar todo, excepto my-image y ubuntu

`docker rmi $(docker images | grep -v ‘ubuntu|my-image’ | awk {‘print $3’})
O (sin awk)

docker rmi $(docker images --quiet | grep -v $(docker images --quiet ubuntu:my-image))`   