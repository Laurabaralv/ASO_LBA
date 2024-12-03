# PR0402: El pipeline en Powershell
Realiza las siguientes tareas que se te piden utilizando Powershell. Para contestar lo mejor es que hagas una captura de pantalla donde se vea el comando que has introducido y las primeras líneas de la salida de este.

- El comando Get-Date muestra la fecha y hora actual. Muestra por pantalla únicamente el año en que estamos.

![alt text](image.png)

- Uno de los requisitos de Windows 11 es que es procesador tenga TPM habilitado. Powershell dispone del comando Get-TPM que nos muestra información sobre este módulo. Muestra por pantalla, en formato tabla, las propiedades TpmPresent, TpmReady, TpmEnabled y TpmActivated.

![alt text](image-1.png)

En los siguientes ejercicios trabajaremos con los ficheros devueltos por el comando Get-ChildItem C:\Windows\System32.

- Muestra por pantalla el número de ficheros y directorios que hay en ese directorio.

![alt text](image-2.png)

- Los objetos devueltos por el comando anterior tienen una propiedad denominada Extension, que indica la extensión del archivo. Calcula el número de ficheros en el directorio que tienen la extensión .dll.

![alt text](image-3.png)

- Muestra los ficheros del directorio con extensión .exe que tengan un tamaño superior a 50000 bytes.

![alt text](image-4.png)

![alt text](image-5.png)

- Muestra los ficheros de este directorio que tengan extensión .dll, ordenados por fecha de creación y mostrando únicamente las propiedades de fecha de creación (CreationTime), último acceso (LastAccessTime) y nombre (Name).

![alt text](image-6.png)

- Muestra el tamaño (Length) y nombre completo (FullName) de todos los ficheros del directorio ordenados por tamaño en sentido descendente.

![alt text](image-7.png)

- Muestra el tamaño y nombre completo de todos los ficheros del directorio que tengan un tamaño superior a 10MB (10000000 bytes) ordenados por tamaño.

![alt text](image-8.png)

- Muestra el tamaño y nombre completo de todos los ficheros del directorio que tengan un tamaño superior a 10MB y extensión .exe ordenados por tamaño.

![alt text](image-9.png)