si tengo 2 equipos conectados directamente por un cable o a traves de un switch sin direccion ip existe comunicacion pero a nivel de capa 2 , pero si quiero mandar un ping fallara obviamente pq este es un programa trabaja sobre la capa 3 (ya que requiere direccionamiento ip para funcionar) y para habilitar la capa 3 en una interface requiere direccionamiento ip por eso cuando usamos ping para probar conectividad en realidad es para probar que exista comunicacion de capa 3 entre dispositivos lo cual es importante ya que todas las app trabajan sobre esta capa 3 y si no esta funcionando la capa 3 no existira comunicacion http,etc. pero no quiere decir que ya no exista comunicacion en otras capas, ping es solo un programa que trabaja en capa 3.5 digamos y para que funcione requiere capa 3 ip, existe algun programa para provar comunicacion de capa 2.

Efectivamente, si no hay IP, la Capa 3 (Red) está "apagada", pero los electrones siguen viajando y las tarjetas de red siguen hablando en Capa 2 (Enlace de Datos) mediante tramas Ethernet y direcciones MAC.

Aquí tienes las herramientas para probar esa comunicación "invisible" de Capa 2:

1. MikroTik MAC Ping (Tu mejor amigo en el laboratorio)
Como estás dándole duro a MikroTik, debes saber que ellos tienen su propia implementación para romper la limitación de la IP. El MAC Ping envía un paquete especial envuelto directamente en una trama Ethernet.

¿Cómo se usa? En Winbox, ve a Tools -> Ping. En el campo Ping To, en lugar de una IP, pones la Dirección MAC del otro equipo.

¿Por qué funciona? MikroTik usa un protocolo propio (basado en ICMP pero sin cabecera IP) que viaja directamente sobre la capa 2. Si el otro equipo es MikroTik, te responderá aunque no tenga IP asignada.


2. MNDP / CDP / LLDP (Protocolos de Vecinos)
Si conectas dos equipos y quieres saber si hay "vida" en el cable sin configurar nada:

En MikroTik ve a IP -> Neighbors.

Si ves al otro equipo en la lista, ¡felicidades! Tienes comunicación de Capa 2 funcional.

Estos protocolos funcionan enviando mensajes de broadcast o multicast a nivel de MAC. Si el switch o el cable estuvieran malos, el vecino no aparecería.