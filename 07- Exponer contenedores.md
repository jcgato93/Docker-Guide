# Exponer contenedores

para dar un ejemplo de como exponer un contenedor al exterior

- docker run -d --name server nginx
    - El modo separado, que se muestra con la opción --detacho -d, significa que un contenedor Docker se ejecuta en el fondo de su terminal. No recibe entrada ni muestra salida. Si ejecuta contenedores en segundo plano, encontrará sus detalles y luego volverá a conectar su terminal a su entrada y salida.

    - --name nombra el contenedor

- Cada contenedor esta aislado incluso a nivel de networking, tienes sus propios puertos
diferentes y aislados a los de la maquina.

- para comunicarse a traves de red con un contenedor se tiene configurar explicitamente.
Es decir que se tiene que configurar un puerto en el host y otro en el contenedor para 
que se comuniquen.

    - primero removamos el contenedor recien creado 
        - docker rm -f server

    - Crear nuevamente el contenedor pero especificando el puerto
        - docker run -d --name server -p 8080:80 nginx

-p 8080:80 , la -p indica la configuracion del puerto , el 8080 es el puerto del host
y el 80 en este caso es el puerto del contenedor, por lo que si vamos al navegador
y colocamos localhost:8080 se tendria acceso al contenedor
