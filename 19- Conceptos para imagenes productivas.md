# Conceptos para imagenes productivas

Cuando pasamos a construir imagenes y contenedores para hacer deploy es bueno 
tener ciertas cosas en cuenta 

## Ignorar contenido del contexto de build

- Puede que no queramos que cuando se haga build de una imagen copie todo el contexto
es decir todos los archivo , para esto podemos crear un archivo <strong>.dockerignore</strong>, en el cual podemos indicar que archivos o carpetas se deben excluir del contexto como por ejemplo los modulos de node.

ejemplo del contenido de un .dockerignore

```
*.log
.dockerignore
.git
.gitignore
build/*
Dockerfile
node_modules
npm-debug.log*
README.md
```

## Docker multi stage build

- Tambien nombrado build de muiltiples pasos. Esto se utiliza cuando queremos ejecutar una serie de pasos en las cuales se debe hacer build de la imagen pero en la cual solo se quedara con el ultimo paso que se ejecute , como por ejemplo cuando queremos hacer los test antes de generar la imagen final para produccion

- Docker permite reutilizar los resultados de cada paso utilizando la notacion de "as [variable]"

Ejemplo

```dockerfile
FROM node:10 as builder

COPY ["package.json", "package-lock.json", "/usr/src/"]

WORKDIR /usr/src
# instala solo dependencias de produccion
RUN npm install --only=production

COPY [".", "/usr/src/"]
# instala dependencias de desarrollo
RUN npm install --only=development
# Ejecuta los test
RUN npm run test


# Productive image
FROM node:10

COPY ["package.json", "package-lock.json", "/usr/src/"]

WORKDIR /usr/src

RUN npm install --only=production
# Toma como referencia del contexto anterior , en este caso solo me intereza el index js y se omiten el resto de archivos
COPY --from=builder ["/usr/src/index.js", "/usr/src/"]

EXPOSE 3000

CMD ["node", "index.js"]
```

- Para cada configuracion podemos crear un archivo con la extencion .Dockerfile y especificar que archivo debe ser utilizado cuando se ejecuta el build de docker con el flag de -f (file)

        $docker build -t [nameImage] -f [path/any.Dockerfile]

ejemplo:

        $docker build -t testImage -f build/production.Dockerfile
