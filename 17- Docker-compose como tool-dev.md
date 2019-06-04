# Docker compose como herramienta de desarrollo

- Cuando se esta trabaja en un entorno de desarrollo normalmente lo que se hace
es estar haciendo el build de la imagen y no utilizando una preconstruida.

- Para dar la instruccion de build desde docker-compose, se remplaza por el 
uso de image el cual indica que imagen se debe utilizar.

Ejemplo
```yml
services:
  app:
    # Indica que utilizara todo el contexto donde se encuentra o si encuentra un dockerfile lo ecutara
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
  db:
    image: mongo
```

Para hacer el build

        $docker-compose build


## Establecer el volum del contenedor 

```yml
services:
  app:
    # Indica que utilizara todo el contexto donde se encuentra o si encuentra un dockerfile lo ecutara
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
    volumes:
        # Bind mound , copia todo el contexto donde esta a la ruta de /usr/src
      - .:/usr/src
      #Esta segunda instruccion indica que archivos no debe sobre escribir
      - /usr/src/node_modules
  db:
    image: mongo
```