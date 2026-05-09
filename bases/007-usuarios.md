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
5. Deshabilitar el usuario admin
    - **System -> Users -> [Tab]Users -> [Click en usuario admin] -> [-]**


## Consideraciones Tecnicas
- ⚠️ Regla de Oro del "Admin": Nunca dejes el usuario admin por defecto con la contraseña en blanco. Lo primero al configurar un router nuevo es crear tu usuario personal (ej. daniel) como full, probar que entras bien, y luego desactivar o cambiar la clave del admin original.
- ⚠️ Riesgo del "Allowed Address": Si pones una IP fija (ej. 192.168.88.10) y mañana tu PC cambia de IP por DHCP, te vas a quedar fuera del router.
    Tip: Es mejor poner un rango (ej. 192.168.88.0/24) o dejarlo en blanco mientras estás en etapa de pruebas.

- ⚠️ Orden de Permisos: Si un usuario pertenece a un grupo que no tiene el permiso winbox o ssh, no podrá entrar aunque la contraseña sea correcta. Siempre verifica las Policies del grupo antes de asignar.

- ⚠️ Active Users: Si ves un usuario conectado que no eres tú en Active Users, es señal de que el router está comprometido. Es tu panel de monitoreo en tiempo real.



## Notas
- Podemos crear grupos personalizados y asignarles permisos en especifico. para luego asignarlos a usuarios que queremos heredar esos permisos.

