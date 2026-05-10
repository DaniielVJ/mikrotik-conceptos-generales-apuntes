## ¿Para que sirve?
Permite proporcionar direcciones ip automaticamente en una network o interface a los hosts que se conecten a estas.


## Consideraciones Tecnicas
- la interface donde trabajara el DHCP server debe tener dirección ip asignada, ya que es un servicio de capa de aplicación que escucha peticiones en el puerto 67, por ende requiere de comunicación IP para poder funcionar y la comunicación IP se habilita en una interface asignando una dirección IP y ya no sea solo a nivel de capa 2. ya que los paquetes DHCP se envian sobre la capa 3.

- En mikrotik podemos crear multiples procesos de DHCP Server, para proveer de direccionamiento IPv4 automatico a equipos en multiples subredes que ejecuten un proceo DHCP Client, como computadoras, Proyectos, SmartPhones, etc.

- Pool: es el elemento que posee la lista de direcciones ip que alquilara (lease) el servidor. (DHCP)

- Lease: El lease dice cuanto tiempo se alquilara una ip a un host, la cosa es que si luego del tiempo determinado se sigue detectando trafico que el host la sigue usando se le vuelve alquilar la misma por el mismo tiempo, ahora si en el tiempo determinado transcurre y se detecta que ya no esta activo se liberara la ip para que la use otro.

## Winbox
1. Eliminar correctamente un servidor DHCP.
    - **IP -> DHCP Server**
        - **[Tab]DHCP -> [Seleccionamos proceso o servidor dhcp a eliminar] -> [-]** (Eliminar el proceso del servidor)
        - **[Tab]Networks -> [Seleccionamos la red o network en la que estaba proporcionando ip el server] -> [-]** (Eliminar la red en la que estaba trabajando el proceso del servidor)
    - **IP -> Pool -> [Tab]Pools**
        - [Seleccionamos el pool de direcciones a eliminar] -> [-]
    - Si queremos deshabilitar completamente la comunicacion a nivel de capa 3 en la interface podemos eliminar la direccion ip
        - **IP -> Addresses -> [Seleccionamos ip a eliminar] -> [-]**
    
2. Configurar un nuevo proceso de servidor DHCP.
    - **IP -> Addresses -> [+]**
        - Address: 192.168.2.1/24 | (Asignamos la dirección ip que utilizara la interface para su comunicacion de capa 3)
        - Network: (Se asigna automaticamente la dirección de red a la que pertenece la ip asignada)
        - Interface: bridge 🔽 | (Seleccionamos la interface que le asignaremos la ip y habilitaremos la comunicacion de capa 3)
    
    - **IP -> DHCP Server -> [Tab]DHCP -> [DHCP Setup]** | (Esto abre un wizard con diferentes paginas para ir estableciendo la configuración del servidor DHCP).
        1. 
            - DHCP Server interface: bridge | (Seleccionamos la interface donde se ejecutara el servidor dhcp)
            - [Next]
        2. 
            - DHCP Address Space: 192.168.2.0/24 | (La red ip de la cual proporcionara direcciones el servidor)
            - [Next]
        3. 
            - Gateway for DHCP Network: 192.168.2.1 | (Indicamos el gateway que asignara el servidor dhcp a los clientes)
                - Aqui usaran al bridge como gateway para comunicarse con otras redes, pero podria ser la dirección ip de otro router que este en el dominio de broadcast, es la ip del dispositivo que interconectara a los equipos de la network del dhcp con otras redes.
            - [Next]
        4. 
            - Addresses to Give Out: 192.168.2.10-192.168.2.254 | (Configuramos el pool[rango] de direcciones ipv4 que alquilara el servidor de la network) 
            - [Next]
        5. 
            - DNS Servers: 192.168.2.1 (🔽) | (Aqui podemos ir agregando los servidores DNS que entregara el sv dhcp a los client que solicit)       8.8.8.8
                           1.1.1.1
            - [Next]
        6.  
            - Lease Time: 00:30:00 | (Es el tiempo por el cual alquilara la dirección ip entregada al cliente, para que este proceso cliente la libere.)
            - [Next]

3. Ver los equipos y direcciones ip alquiladas a esos equipos.
    - **IP -> DHCP Server -> [Tab]Leases** | (Aparecera el listado de direcciones ip alquiladas y la MAC de la NIC a la que se le alquilo esa dirección ip por parte del server.)

4. Configurar un Static Leases
    - **IP -> DHCP Server -> [Tab]Leases -> [+]**
        - Address: 192.168.2.5 | (dirección ip que siempre se alquilara)
        - MAC Address: 40:EC:99:50:D2:22 | (MAC de la NIC o equipo que siempre resivira esa dirección ip por el servidor)
        - Server: dhcp1 | (El proceso o servidor dhcp que alquilara esa ip ya que podemos tener varios server dhcp)
        - [OK]
5. Pasar un lease dinamico a estatico
    - **IP -> DHCP Server -> [Tab]Leases -> [Click sobre el lease dinamico] -> [Make Static]** | (Esto automaticamente indica que al equipo que se le asigno esa ip  dinamicamente por el servidor DHCP sera estatica y siempre se le debe otorgar esa)

6. Hacer que el servidor DHCP solo alquile direcciones ip estaticamente y no utilice el pool.
    - **IP -> DHCP Server -> [Tab]DHCP -> [Click sobre el servidor dhcp]**
        - Address Pool: static only | (Esto hace que el servidor solo alquilara direcciones ip a los dispositivos que se encuentren en la tabla leases con static lease)
        - [OK]



## Notas
- La interface bridge se compone de multiples puertos fisicos (tambien pueden ser virtuales), por ende cualquier conexion a uno de esos puertos significa que estamos conectandonos a la interface bridge. Y si esta interface bridge tiene un servidor dhcp asignado entonces todos los equipos conectados a la interface bridge a traves de un port o puerto recibira direccionamiento ip automatico por ese servidor dhcp y si la interface bridge tiene una direccion ip, cualquier equipo conectado a un puerto fisico que es parte de la interface bridge puede comunicarse con ping a esta interface en su ip y usarlo como gateway.

- Los puertos pasan a ser un puente para poder conectarnos a la interface bridge, todos son partes de esta.

- la network se le pasa al servidor dhcp para que no se le pueda pasar cualquier pool, si no que tiene que ser un pool que contenga ip dentro del rango de direcciones de la red ip o network asignada


- EJ QUE SE ME OCURRIO CON LA CAPA 3 Y PQ ES IMPORTANTE TENER IP:
    - Si requerimos que por ejemplo un puerto bonding que formamos entre 2 mikrotik no solamente sirva para que pase sobre ellos trafico de capa 3 como ping, http, etc. Si no que queremos que esos mismos puertos bonding puedan generar trafico que requiere la capa 3 como OSPF que trabaja sobre IP, DHCP, DNS, SSH.
    Es decir que no solo sirva como un puerto de capa 2 como transporte si no que el pueda generar trafico OSPF y enviarlo requiere que le asignemos una dirección ip para habilitar la capa 3.

    - Si queremos que una interface solo sirva para reenviar trafico de otros dispositivos que son o requieren capa 3 como htto o ospf a traves de ellos y que ellos solo generen trafico de capa 2. Simplemente no debemos habilitarle la capa 3 dandole una IP. Pero si quiero el puerto virtual bonding o de un switch puede generar su propio trafico de capa 3 con su propia ip como ip de origen como podria ser un server dhcp en un puerto bonding y enviar trafico dhcp, este puerto para generarlo necesita dirección ip para habilitar la capa 3 y asi sobre el poder generar el paquete dhcp correspondiente. 

- Comandos DHCP en windows:
    - ipconfig /release: Libera la ip alquilada al servidor.
    - ipconfig /renew: Para solicitar una nueva ip al servidor hace el proceso DORA.