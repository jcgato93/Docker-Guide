# Docker compose

Es una herramienta que nos permite describir de forma declarativa
la arquitectura de nuestra aplicacion

Docker compose utiliza el <strong>dockercompose file</strong> que es un archivo
con el nombre de docker-compose.yml

## Estructura de un docker-compose.yml

```yml
version: "3" # Version del docker compose

# Servicios de la aplicacion, y no se refiere a los contenedores
services:
  app:
    # imagen que debe utilizar 
    image: platziapp 
    # Variables de entorno
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    # Especifica que depende que un servicio arranque primero
    depends_on:
      - db
    # Puerto host : puerto contenedor
    ports:
      - "3000:3000"

  # Otro servicio
  db:
    image: mongo
```

## Ejecutar el docker compose

    $ docker-compose up