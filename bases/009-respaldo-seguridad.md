## ¿Para que sirve?
Permite crear una copia de las configuraciones actuales del dispositivo, permitiendo restaurarlo a estas si es que alguna nueva configuracion fallase, hubiese un error, se corrompiera, etc.



## Consideraciones Tecnicas
- Mikrotik posee 2 tipos de respaldos de seguridad
    - Backup (.backup): usado para restaurar la configuracion en el mismo router. (A pesar que tenga otro router del mismo modelo podria tener fallos para restaurarla, debe ser para el mismo este tipo de respaldo)
    - Export (.rsc): Permite mover la configuracion a otro router o aplicarla al mismo.

- En un respaldo tipo **backup** si no le damos nombre, este por defecto lo nombrara con el identity asignado al router + la fecha en que se hizo el respaldo.

- Estos son respaldos unicamente de las configuraciones que tiene asignadas del dispositivo, no es un respaldo de los archivos de los dispositivos de almacenamiento que este posea (Flash Memory, MicroSD, USB), para realizar copias de seguridad de un dispositivo de almacenamiento como un disco duro usando snapshot (AWS, GCP, ETC) debe usarse otros mecanismos.

- El tipo export, exporta las configuraciones como un script de los comandos que deben ejecutarse en el mikrotik para replicar las configuraciones actuales que tengo en el equipo en otro o en el mismo, y al ser un script significa que es texto plano donde puedo modificar esos comandos y manipular el resultado del export al momento de importarlo en un equipo.
- Importante saber que este tipo de respaldo solo almacena en el script las configuraciones diferentes a las que vienen de fabrica.

## Winbox

1. Crear una respaldo tipo backup normal sin indicar nombre y contraseña.
    - **Files -> [Tab]File -> [Backup] -> [Backup]** | (Genera un archivo .backup en el files con el identity mas la fecha)

2. Crear respaldo backup con nombre y contraseña
    - **Files -> [Tab]File -> [Backup]**
        - Name: backup1 | (nombre del archivo .backup)
        - Password: churrasco | (contraseña para poder cargar el backup)
        - Encryption: aes-sha256 | Cifrar el contenido binario del archivo para que no pueda ser interpretado.
        - [Backup]
3. Restaurar la configuracion a partir de un backup
     - **Files -> [Tab]File -> [Restore]**
        - Backup File: Seleccionamos el archivo del cual queremos restaurar el router.
        - Password: Aqui indicamos la password del backup si es que este la solicita.

4. Generar un respaldo de tipo export (.rsc)
    - **New Terminal**
        - export file=respaldo1 | (Compando que exporta las config totales del dispositivo en el archivo respaldo1)

## Notas
- Backup: Este es de tipo binario es decir el contenido no puede ser leeido por humanos y este hace un respaldo completo, es decir almacena igualmente los usuarios y contraseña que poseia el dispositivo.
- Importante saber que los backup solo almacenan o respaldan las configuraciones y credenciales del dispositivo, no realizan un seguimiento del estado de los archivos almacenados en el system files o files del dispositivo, por ende los archivos cargados al equipo despues de hacer el backup, al momento de restaurarlo a un backup antes que existan los nuevos archivos, estos no son eliminados.


