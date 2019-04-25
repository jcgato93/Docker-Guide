# Docker con datos

Supongamos que se requiere el manejo de datos desde un contenedor,
como por ejemplo una base de datos 

- docker run -d --name db mongo
- Verificar el estado 
    - docker ps
- Verificar el log 
    - docker logs db

## Ejecutar comandos dentro del contenedor

Para interactuar con la base de datos , en este caso con
mongo se utiliza el siguiente comando.

- docker exec -it db bash 

Desde el contenedor de mongo vamos a crear una base de datos
de prueba, en mongo es tan simple como ejecutar el siguiente
comando.

- Estando en el bash del contenedor se crea la base de datos
    - mongo
    - use dbtest

- insertar un registro en una coleccion llamado users
    - db.users.insert({"name":"camilo"})

- para buscar el registro 
    - db.users.find()

pero que pasa si se mata o se borra el contenedor , en ese
caso la data tambien se perderia , entonces como hacer para
que los datos sobrevivan incluso despues de su ejecucion.


## Establecer almacenamiento del contenedor

- primero creamos un directorio donde queramos que el
contenedor haga uso de datos que persistan incluso despues
de su ciclo de vida 
    
    - D:\mongodata

- montar explicitamente al contenedor un sistema de archivos

    - docker run --name db  -v D:\mongodata : /data/db mongo

-v indica la creacion de un volumen de datos.
luego el directorio del host donde se guardan los datos , luego el lugar en el contenedor desde donde se van a enviar esos datos que en este caso de mongodb los datos se guardan
en /data/db  y por ultimo el nombre de la imagen


Ahora si se crea otro contenedor apuntando a los mismos 
directorios, podra tener acceso a dicha información, que 
aunque es bantante util , no es muy seguro ya que otros
procesos de la maquina host podrian alterar el funcionamiento de un contenedor y seria dificil de detectar.

