# Crear imagenes propias

- Primero necesitamos crear una archivo Dockerfile, este archivo es donde
se indica la configuracion de la imagen que se desea generar

- Crear el archivo Dockerfile (receta)
- El dockerfile siempre debe empezar con el FROM le indicamos cual va a ser nuestra imagen base para empezar
3- RUN para correr un comando
- Creamos un archivo touch /usr/src/hola-mundo
- Construimos el dockerfile

- Construir la imagen      

        docker build -t <imagen>:<tag de la imagen> <path de donde vamos a obtener el contexto build, para este caso .>

si el contexto , es decir con lo que se construye la imagen esta en otra ruta , tendria que indicarse toda la ruta

## Ejemplo
```dockerfile
FROM ubuntu
RUN touch /usr/src/hola-mundo
```

- Luego se corre el comando

        $ docker build -t ubuntu:Test .

## Hacer push de la imagen

- hacer login del dockerHub
        
        $ docker login

- Retagear la imagen creada ya que sino intentara hacer push al repositorio origen de la imagen base , en este caso de ubuntu

        $ docker tag <tag contenedor> <nuevo tag contenedor>

        ejemplo:
        docker tag ubuntu:Test <user>/ubuntu:Test

- Hacer push

        $ docker push <user>/ubuntu:Test

        
