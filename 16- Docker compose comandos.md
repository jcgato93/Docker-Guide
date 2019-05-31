# Comandos de docker compose

- Arrancar el docker compose 

        $docker-compose up

Este sube todos los servicios y arroja los logs

- Arrancar docker compose detached

        $dcoker-compose up -d

este sube los servicio en modo deteach por lo que no arroja los logs

- Listar servicios 

        $docker-compose ps


- Ver logs de un servicio 

        $docker-compose logs [nombre servicio]

- Entrar a la terminal de un servicio

        $docker-compose exec [servicio] bash

- Bajar todos los servicios junto con la red

        $docker-compose down