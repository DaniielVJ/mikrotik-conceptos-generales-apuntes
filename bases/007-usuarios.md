## ¿Para que sirve?
Para conectarse al dispositivo e identificar quienes estan conectados al dispositivo.
Proporciona una capa de autenticacion al solicitar un usuario y contraseña.

## Configuraciones
1. Ver usuarios del sistema
    - **System -> Users**
2. Crear un nuevo usuario
    - **System -> Users -> [Tab]Users -> [+]**
        - Name: daniel | (nombre que se usara para ingresar con el usuario)
        - Group: full | (grupo con permisos que tendra el usuario)
        - Allowed Address: 192.168.88.10 | (Permite proporcionar todas las direcciones IP que debe tener la maquina de donde se esta conectando el usuario)
        - Last Logged In | (fecha y hora de la ultima vez que ingreso el usuario)
        - Password: churrasco | (contraseña que usara el usuario para ingresar)
        - Confirm Password: churrasco | (confirmamos la contraseña)
3. Ver Usuarios que estan conectados actualmente al equipo.
    - **System -> Users -> [Tab]Active Users**
4. Asignar grupo read al usuario admin
    - **System -> Users -> [Tab]Users -> [Click en usuario admin]**
        - Group: read | (Este grupo solo le dara permisos al usuario admin para ver las configuraciones del dispositivo, no crear nuevas ni modificar las actuales.)

## Consideraciones Tecnicas



## Notas
- Podemos crear grupos personalizados y asignarles permisos en especifico. para luego asignarlos a usuarios que queremos heredar esos permisos.

