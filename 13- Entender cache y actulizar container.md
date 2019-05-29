# Entendiendo el Cache

Cuando hacemos build de una imagen ejecuta todos los comandos registrados
en cada layer , cuando se trabaja con dependencias si estas no han cambiado
estoy puede ser tardado por lo que existe una manera mucho mas optima para esto

- Ejemplo:

```dockerfile
FROM node:10

# Solo copia los archivos que cambia el listado de dependencias
COPY ['package.json','package-lock.json', '/usr/src/']

WORKDIR /usr/src

RUN npm install

# copia el contexto pero esta vez no vuelve a copiar los archivos de package.json ni package-lock.json
COPY ['.', '/usr/src/']

EXPOSE 3000

CMD ['node','index.js']
```

## Actulizar los archivos del contenedor sin detenerlo

Para no tener que estar haciendo el mismo proceso mientras se esta desarrollando , podemos hacer la siguiente configuracino en el dockerfile (esto solo aplica para nodejs, cada lenguje o framework tendra su propia configuracion de monitoreo de archivos para reiniciar el servicio con cada cambio)

```dockerfile
FROM node:10

# Solo copia los archivos que cambia el listado de dependencias
COPY ['package.json','package-lock.json', '/usr/src/']

WORKDIR /usr/src

RUN npm install

# copia el contexto pero esta vez no vuelve a copiar los archivos de package.json ni package-lock.json
COPY ['.', '/usr/src/']

EXPOSE 3000


# ejecuta el comando node index.js el cual levanta el servidor de express
# npx es una herramienta de cli que nos permite ejecutar paquetes de npm de forma mucho más sencilla
# nodemon es el paquete que nos va apermitir bajr y subir el server de manera automatica apenas exita un cambio en los archivos
# index.js es el archivo que levanta el servidor de express
CMD ["npx","nodemon", "index.js"]
```

- Crear el contenedor atachando el Volumen de la imagen para que cada que cambien los archivos tambien se actualice el contenedor

        $ docker run -p [port]:[port] -v [path]:/usr/src [image]

Ejemplo:

    $ docker run --rm -p 3000:3000 -v /Users/personal/Desktop/Docker-Guide/docker-project : /usr/src testapp