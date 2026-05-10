## ¿Para que sirve?
DHCP: Usado para la distribuccion automatica de direcciones ip en una red local.
DHCP Client: Usado para que nuestro dispositivo mikrotik adquiera una dirección ip, subnet mask, gateway, servidores dns y otras configuraciones IP desde un servidor DHCP, sin la necesidad que nosotros se lo configuremos estaticamente.


## Consideraciones Tecnicas
- DHCP trabaja dentro de un dominio de broadcast. Por cosas tecnicas, deberiamos tener un servidor DHCP por dominio de broadcast.
- Proceso DORA (Intercambio de paquetes entre un sv dhcp y un cliente dhcp para obtener configuracion ip):
    - Discovery: La interface con dhcp client envia un frame broadcast al puerto 67 UDP buscando un servidor dhcp en la network.
    - Offer: Si hay un servidor, este escucha el paquete DHCP y se comunica al cliente diciendolo que el existe y tiene esa config ip para ofrecerle y alquilarle.
    - Request: El dhcp client acepta la config ip (se la asigna) y envia un mensaje unicast al sv dhcp diciendole que acepta la config.
    - ACK: Servidor DHCP le indica que reservo la direccion ip para el y le entrega por cuanto tiempo puede usarla o se la alquila para posteriormente sea liberada (release). 
- Puertos:
    - 67 UDP -> Servidor
    - 68 UDP -> Cliente
- Solo se puede tener un proceso dhcp client por interface fisica o virtual de nuestro dispositivo mikrotik, ya que por estandar cada interface solo se puede ejecutar 65535 puertos virtuales, pero no puede repetirse ninguno por interface, y el proceso dhcp client usa el puerto 68 UDP, no podemos tener en la misma interface ejecutando el 68 mas de una vez.


## Winbox
1. Agregar un proceso cliente DHCP a una interface para obtener configuracion IP Automatica.
    - **IP -> DHCP Client -> [+]**
        - Interface: wlan1 | (Especificamos la interfaz que tomara configuracion ip automatica de un sv dhcp)
        - Use Peer DNS: ✅ | (Indicamos que utilice los servidores DNS que proporciona el sv dhcp)
        - Use Peer NTP: ✅ | (Indicamos que use el servidor NTP que el sv dhcp nos entregue)
        - Add Default Route: 🔽
            - yes: Agregara una ruta que permite llegar a todos los destinos 0.0.0.0/0 a traves del gateway que entregue el sv dhcp
            - no: Indicamos que no utilice el gateway que entrega el dhcp server para llegar a todos los destinos.
        - [OK] (status debe decir bound para indicar que recibimos configuracion ip del sv dhcp correctamente)
2. Ver la información IP que nos entrega un sv dhcp.
    - **IP -> DHCP Client -> [click sobre un dhcp client agregado]**
        - [Tab]Status | (Ahi aparece la dirección ip que le dio a la interface, la mascara, el gateway, el dns, el ntp, etc.)
3. Liberar la dirección ip otorgada por el servidor dhcp para que la use alguien mas
    - **IP -> DHCP Client -> [click sobre un dhcp client agregado] -> [Tab][Release]**
4. Obtener una nueva direccion ip del sv dhcp una vez liberada
    - **IP -> DHCP Client -> [click sobre un dhcp client agregado] -> [Tab][Renew]** | (Hace que la interface vuelva hacer el proceso DORA)



## Notas
- Asegurarnos de configurar un dhcp client en una interface que se conecte a un dominio de broadcast o red ptp que exista un servidor dhcp.
- Asegurarnos que la red multi acceso o ptp que conecte la interface con dhcp client no tenga un equipo intermedio que bloquee los paquetes DHCP o paquetes al puerto 67 UDP que es donde escucha un servidor dhcp y es el puerto donde consume el servicio un dhcp client por defecto.

