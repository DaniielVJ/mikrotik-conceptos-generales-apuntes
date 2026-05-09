## ¿Para que sirve?
Proporciona diferentes formas que podemos utilizar para conectarnos al dispositivo mikrotik a nivel aplicativo o capa 7.



## Winbox
1. Visualizar los servicios activos
    - **IP -> Services**
2. Deshabilitar un servicio
    - **IP -> Services -> [-]** (Esto hace que ningun cliente puede acceder o consumir dicho servicio)
3. Habilitar un servicio deshabilitado
    - **IP -> Services -> [✅]**
4. Modificar el puerto de un servicio
    - **IP -> Services -> [Doble click sobre el servicio a modificar su puerto]**
        - Port: 9000 | (Esto modifica el puerto en se podra conectar al mikrotik usando winbox por direccion ip, como este por defecto usa el 8291 tendremos que en winbox especificar el nuevo puerto + la direccion ip del equipo: 192.168.88.1:9000)
5. Limitar quien puede acceder a un servicio
    - **IP -> Services -> [Doble click sobre el servicio]**
        - Available From: 192.168.1.200 | (Esto indica que solo se puede acceder al servicio seleccionado de una maquina con esa dirección IP, si no no se puede acceder.)



## Consideraciones Tecnicas
- El servicio winbox es el que controla toda la conexión por direccion IP, este no afecta al ingreso por MAC, asi que si lo deshabilitamos la conexion por winbox por MAC seguira funcionando, en cambio por dirección IP no.
- Deshabilitar los servicios que no se utilicen.
- Cambiar el puerto por defecto en que vienen ejecutandose los servicios.
- Definir el available from para acotar el numero de dispositivos que pueden acceder a ellos.


## Notas
Los servicios son aplicaciones que estan ejecutandose en segundo plano en un dispositivo 24/7 sin parar, a las cuales podemos conectarnos utilizando una aplicacion cliente y consumir esos servicios.

ssh: ofrece el servicio de acceso remoto a traves de CLI o terminal para configurar el dispositivo via comandos usando un cliente ssh como putty o ssh client en linux.
winbox: Es un servicio de mikrotik que permite conectarse con winbox utilizando direccion ip con TCP, permitiendo una conexion mas estable debido a la naturaleza de TCP.
ftp: Servicio que permite transferir archivos desde un cliente al router.
