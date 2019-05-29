# Docker para desarrollo de aplicaciones

Tomando como ejemplo una aplicacion creada en node.js

- Crear docker file
```dockerfile
# Imagen base
FROM node:8

# [<ubicacion de los archivos a copiar>, <destino donde van a quedar los archivos copiados>]
COPY ['.' , "/usr/src/"]

# es similar al comando cd, WORKDIR <entrar en la siguiente ruta> 
WORKDIR /usr/src

# RUN ejecuta el comando npm install 
RUN npm install --production

# [<ubicacion de los archivos a copiar>, <destino donde van a quedar los archivos copiados>]
COPY [".", "/usr/src/"]

# le indica al contenedor el puerto por el cual va a salir o exponer el contenedor, es el mismo puerto por donde esta escuchando node
EXPOSE 3000

# ejecuta el comando node index.js el cual levanta el servidor de express
CMD ["node", "index.js"]

```

- Hacer build de la imagen

        $ docker build -t testApp .


- Verificar la construccion de la imagen

        $ docker image ls

- Correr un contenedor con la imagen creada

        $ docker run -d -p [port]:[port] testApp