## ¿Para que sirve?
Es un bootloader encargado de ejecutar el RouterOS en la placa base o en el routerboard.


## Configuracion
Podemos actualizar el routerboot (firmware)

1. 
    - **System -> RouterBOARD**
        - [Upgrade] -> [Yes]
2. 
    - **System -> Reboot** | Se termine de instalar durante el reinicio


## Consideraciones tecnicas

- El firmware que actualizamos se conoce como MAIN. pero si este falla o se corrompe el routerboard contiene un firmware bootloader de BACKUP, que podemos ejecutar presionando el boton de reset con el equipo unos segundos y encenderlo.


## Nota
- firmware: es codigo que corre directamente sobre el hardware.
- software: es codigo que corre sobre otro codigo, no directamente en el hardware, requiere del firmware o un kernel para comunicarse con el hardware.

