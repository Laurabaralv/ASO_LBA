# PR0501: Carpetas Personales

Lo primero que debemos hacer es tener una máquina virtual con Windows Server que ya este promovido a dominio y con el rol de servivios de archivos y almacenamiento.

A continuacion nos vamos a la herramienta de 'Usuarios y equipos de Activity Directory'. Una vez dentro crearemos los dos usuarios y el grupo que nos indica el enunciado dentro de la carpeta de Users.

Con esto realizado nos vamos a la ventana de Administrador del servidor --> Servicios de archivos y almacenamiento --> Recursos compartidos.

Hacemos click derecho sober el rectangulo de servicios compartidos para crear un recurso nuevo  y nos aparecera una ventana donde iremos adaptando las opciones a lo que nosotros necesitemos. en este caso cuando lleguemos a la opcion de especificar nombre del recurso, lo llamaremos $carpetaPersonal . El simbolo $ es para que la carpeta permanezca oculta en la red. Tambien editamos los permisos para que solo los usuarios del grupo alumnos puedan acceder a ella y tambien editamos la opción de compartido.

Ahora volveremos a la herramienta de 'Usuarios y equipos de Activity Directory', seleccionamos a los dos usuarios que creamos anterior mente, click derecho, propiedades y en la ventana que aparece nos vamos a la opción de perfil. En la parte de carpeta  particular seleccionamos connectar, la letra que va a tener la unidad y la siguiente ruta: \\LBA.local\shares\$carpetaPersonal\%username%

Ahora si ponemos en el buscador de una carpeta la ruta de la carpeta personal del usuario nos tendria que aparecer un aviso indicandonos que no tenemos permitido acceder a dicha carpeta.

Para compartir una carpeta con un grupo volvemos al apratedo de Servicios de archivos y almacenamiento y creamos una carpeta llamada apuntes. Despues nos vamos a donde se ha creado la carpeta y hacemos click derecho sobre esta y en compartir con --> usuarios especificos. Ahí agregamos al grupo y le damos permisos de escritura y lectura.

A continuación nos vamos a la carpeta NETLOGON y creamos un fichero .bat con la ruta de la carpeta. Volvemos a usuarios y equipos de activiti directory, seleccionamos los dos usuarios y en propiedades nos vamos a perfil y marcamos la opcion de script de inicio de sesion y ponemos el nombre del fichero .bat que creamos antes y aceptamos.