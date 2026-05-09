## ¿Para que sirve?
Para restablecer la configuracion del dispositivo a las de fabrica, en blanco, o cargar configuraciones desde cero a partir de un script.


## Consideraciones Tecnicas
- Podemos mantener los usuarios actuales del sistema si queremos resetearlo.
- Cada vez que reseteamos el equipo este genera un backup de las configuraciones previas antes de hacerlo si no lo deshabilitamos. (Puede llenar el almacenamiento)


## Winbox
1. Resetear la configuración.
    - **System -> Reset Configuration** (Se abrira una ventana emergente con las opciones de reseteo que podemos marcar)
        - Keep User Configuration | ([✅-> Mantendra los usuarios y contraseñas despues del reset])
        - CAPS Mode | ([✅] -> Delega la configuracion a un controlador centralizado, se usa en AP Light)
        - No Default Configuration | ([✅] -> Permite que el dispositivo quede sin configuraciones [blank])
        - Do Not Backup | ([✅] -> Indica al mikrotik que no guarde un respaldo de las configuraciones en un .backup)
        - Run After Reset: 🔽 | (Permite definir que se ejecute un script .rsc que seleccionemos del sistema **Files**)


## Notas
[✅]: Significa que si marcamos esa opcion ocurrira eso, ya que vienen desmarcadas
configuraciones blank: Significa que el router queda totalmente vacio sin las configuraciones por defecto de fabrica, no tendra ip absolutamente nada, solo los servicios con los que viene habiltiados y permitira conexion MAC por winbox nada mas.
[🔽]: Significa que hay un conjunto de opciones que podemos seleccionar y pueden ser variables o fijas ya por el sistema.



