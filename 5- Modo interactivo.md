# Modo interactivo o bash de un contenedor

- Como ejemplo , que tal si se corre un contenedor de ubunty
    - docker run ubuntu

Al usar este comando se corre el contenedor pero inmediatamente se cierra al no tener
ningun dato de entrada es su terminal

- Ahora si quisiera utilizar la terminal de dicho ubuntu
    - docker run -it ubuntu

El significado de las flags -it:

- -t: Asignar un pseudo-tty (Terminal).
- -i: mantén STDIN abierto incluso si no está conectado.
