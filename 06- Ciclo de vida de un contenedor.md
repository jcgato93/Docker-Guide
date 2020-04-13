# Ciclo de vida de un contenedor

Un contenedor solo estara corriendo mientras tenga un proceso
o comando que se este ejecutando.

- Para correr un contenedor que se quede esperando un output infinitamente 
podemos escirbir el siguiente comando :
    - docker run [imagen o contenedor] tail -f /dev/null

- tail = es un comando de linux que lo que hace es pasar cualquier contenido
al standar output.

- -f = o follow es que mueste la informacion que ya existe y se quede esperando 
mas informacion.

- /dev/null = es basicamente un barril sin fondo en linux , todo lo que se le pase
va a desaparecer

## Ejecutar comando dentro de un contenedor que esta corriendo

- El contenedor debe esta Up

- ejetucar el siguiente comando
    
    - docker exec  -it [contenedor] [comando]

- Ejemplo 
    - docker exec -it container_ubuntu bash

- docker kill nombre_contenedor = mata el proceso completo

- docker pause = suspende todos los comandos de un contenedor especifico.

- docker stop [command] = detiene el proceso  principal de un contenedor
