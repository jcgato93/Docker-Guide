# Qué es Docker: containarization vs virtualization

## Qué es Docker?
Docker Permite resolver problemas de construir, distribuir y ejecutar software en diferentes plataformas.

## Containarization: 
un estándar para llevar algo dentro. Agrupadores de procesos.

- Versátiles:	
En el orden de los MB
Tienen todas las dependencias que necesitan para funcionar correctamente.
Funcionan igual en todos lados.

- Eficientes:
Comparten archivos simultáneos con otros contenedores.
Solo se ejecutan procesos, no un SS.OO completo.

- Aislados:
Lo que pasa en el container queda en el container.
No pueden alterar su entorno de ejecución (a menos que explícitamente se indique lo contrario)

## Virtualization: 
es una imagen o archivo que contiene información dentro. Por lo general son pesadas de administración costosa y son lentas.

- Pesadas:	
En el orden de los GB
Muchas VMs en el mismo host suelen repetirse en lo que contienen
Administración costosa:
Una VM tiene que ser administrada como cualquier otra computadora: patching, update, etc
Hay que administrar la seguridad interna entre apps

- Lentas:
Correr nuestro código en una VM implica no solo arrancar aplicaciones, sino también esperar el boot de la VM en sí.

