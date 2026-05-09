## ¿Para que sirve?
El DNS sirve para resolver o referenciar un nombre a una direccion ip. permitiendo que podamos conectar a una direccion ip usando un nombre.


## Consideraciones Tecnicas
- A mikrotik le podemos agregar manualmente servidores DNS que puede utilizar para resolver un nombre a una dirección IP.
- Si el mikrotik tiene configurado dhcp clients, este puede utilizar los SV DNS que obtengan estos client.
- Mikrotik permite que podamos agregar entradas DNS estaticas, permitiendo agregar nuestros propios nombres y ips a las que debe resolverse si se quiere comunicar a esos nombres.
- La configuracion por defecto trae una entrada estatica de router o router.lan a la dirección ip 192.168.88.1 y configura a los dispositivos que se conectan al mikrotik como servidor DNS al mikrotik, haciendo que si nos conectamos a router.lan resuelva a la ip del mikrotik 192.168.88.1 y nos podamos comunicar a el usando un nombre.

- Los servidores DNS escuchan peticiones en el puerto 53 UDP. 
- Podemos configurar al mikrotik para que procese peticiones DNS al puerto 53 si van con destino a el mismo, y el se encargue de resolver el nombre enviado en la peticion a una dirección ip. Los pasos del proceso son:
    1. Recibe la petición, revisa en su cache si se encuentra el nombre para resolver. Si esta le envia la ip.
    2. Si no esta consulta sus entradas estaticas. Si esta devuelve la ip de la entrada estatica.
    3. Si no esta consultara a un servidor DNS que tenga agregado ya sea manualmente o por un dhcp client.
    4. Si este servidor le responde con la ip del nombre la agrega al cache y se la envia al cliente para que pueda conectarse.
- Ahora si no queremos configurar al mikrotik para que resuelva los nombres a ip de los dispositivos en la LAN en el DHCP server local debemos indicar que el servidor DNS no sera el equipo mikrotik si no otro.

## Winbox
1. Ver y agregar servidores DNS al Mikrotik.
    - **IP -> DNS** 
        - Servers: 🔽 | (flechita hacia abajo permite ir agregando servidores manualmente)
            - 8.8.8.8
        - [Apply]
        - Dynamic Servers | (Son los servidores DNS que recibio automaticamente por dhcp client el mikrotik y los usara para resolver nombres.)
2. Agregar entradas DNS Estaticas
    - **IP -> DNS -> [Static]**
        - [+]
            - Name: router-bkn | (nombre que queremos que se utilize para comunicarse a un equipo)
            - Type: A | (type A permite resolver el nombre a una IP)
            - Address: 192.168.88.1 | (Es a la ip que se comunicara cuando se use el nombre)
            - [OK]
3. Permitir que el router mikrotik resuelva los nombres a ip que soliciten otros equipos
    - **IP -> DNS**
        - [✅] Allow Remote Request | (Marcar esta opción le dice al mikrotik que si recibe un paquete DNS con ip destino la de el, el resolvera el nombre a una ip para ese cliente que consulta)
## Notas
- Los DNS que tiene el mikrotik o le agregamos en primer lugar son usados por el para resolver nombres a ip en sus comunicaciones a otros equipos, pero podemos configurar que los utilice para resolver nombres si otro equipo le preguntan a el por una peticion DNS.
- Allow Remote Request: Es importante saber que si configuramos al mikrotik como servidor DNS para los dispositivos de nuestra red habilitar esto para que resuelva los nombres y obviamente tener servidores configurados en el mikrotik que lo auxilien si no tiene la ip de ese nombre. 
    - Si lo tenemos deshabilitado, y configuramos para los equipos al mikrotik como DNS entonces ocurrira, que no podran resolver los nombres pq las peticiones DNS 53 que reciba el mikrotik las rechazara. Por ende si lo deshabilitaremos debemos configurar en a los hosts de nuestra red que usen como servidor DNS otro equipo que no sea nuestro mikrotik, y este solo enrutara esos paquetes DNS al servidor DNS que consulten los clientes.

- Comandos DNS en windows importantes: 
    - ipconfig /all -> Muestra el servidor DNS usado por la maquina.
    - ipconfig /displaydns -> Muestra el cache DNS de la maquina.
    - ipconfig /flushdns -> Limpia o borra todas las entradas del cache de la maquina.


Tip de Ingeniero: Si quieres bloquear un sitio (ej. facebook.com), puedes crear una entrada estática para ese nombre que apunte a 127.0.0.1. El router la encontrará primero y el cliente nunca llegará al servidor real.

