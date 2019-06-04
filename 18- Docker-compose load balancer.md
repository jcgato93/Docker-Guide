# Load balancer con Docker-compose

En aplicaciones de alta demanda requiren balanceadores de carga para 
que la aplicacion pueda escalar, esto tambien es posible utilizando docker-compose

La idea general de generar una imagen de una aplicacion es poder 
crear multiples contenedores de la misma imagen.

## Configurar docker-compose para escalar 

- Se debe definir el rango de puertos del host disponibles para el escalado 
con la sintaxis de [desde]-[hasta]

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
    #definir rando de puertos del host
      - "3000-3010:3000"
  db:
    image: mongo
```

## Ejecutar comando de escalado

    $docker-compose scale [service]=[num containers]

Ejemplo:

    $docker-compose scale app=4

## Crear load balancer

- Teniendo los diferentes contenedores ejecutandose necesitamos un balanceador que distribuya las peticiones, para esto necesitamos crear otro servicio que se encarde de ello

- En este caso la manera mas facil es utilizar haproxy , un software open source para balanceo de carga. Este esta como imagen de docker , por lo que solo es crear un servicio con dicha imagen

Ejemplo

```yml
services:
  app:    
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000-3010:3000"
  db:
    image: mongo
  lb:
    image: dockercloud/haproxy
    links:
     - app
    ports:
     - '3000:80'
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

- Otra opcion es utilizar el load balancer de traefik. Este cuenta incluso con una interfaz grafica de monitoreo

```yml
services:
  app:    
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000-3010:3000"
    labels:
      #- "traefik.backend=machine-echo"
      - "traefik.frontend.rule=Host:app.localhost" 
  db:
    image: mongo
  lb:
    image: traefik
    # Enables the web UI and tells Traefik to listen to docker
    command: --web --docker  --docker.domain=docker.localhost --logLevel=DEBUG
    ports:
      - "2900:80" # The HTTP port
      - "8080:8080" 
      - "443:443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /dev/null:/traefik.toml   
```