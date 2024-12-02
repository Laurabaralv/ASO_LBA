## 1. Permisos de usuario

1. cuando vamos a crear el directorio en /home con el comando mkdir, la interfaz nos devuelve un mensaje comunicando de que no tenemos los permisos suficientes para realizar la acción. Pero si añadimos sudo al principio del comando entonces si podremos crear el directorio.
Para crear los otros dos directorios lo hacemos con sudo kdir.
Los permisos del dirtectorio dir1 son los heredados del directorio pr0201.

2. para la notacion simbólica usamos el comando:
   
   ``
   chmod a-w pro201/dir2
   ``

3. En la notación octal calculamos los permisos que queremos usar pasamdo a binario los permisos el resultado de juntar tres cifras nos da los numeros que debemos poner. En este caso queda como:

    ``
    chmod 551 pr0201/dir2
    ``

4. Con el comando 
   ``
   ls pr0201/dir2 -l
   ``
   vemos los permisos del fichero en cuestion.

## Notacón octal y simbólica

1. Notación simbólica

- rwxrwxr-x :

- rwxr--r-- :

- r--r----- :

- rwxr-xr-x :

- rwxr-xr-x :

- r-x--x--x :

- -w-r----x :

- -----xrwx :

- r---w---x :

- -w------- :

- rw-r----- :

- rwx--x--x :

2. Notación octal

- rwxrwxrwx : 777
 
- --x--x--x : 111

- r---w---x : 421

- -w------- : 200

- rw-r----- : 640

- rwx--x--x : 711

- rwxr-xr-x : 755

- r-x--x--x : 511

- -w-r----x : 241

- -----xrwx : 017

## El bit setgid

1. creamos el gupo con el comando 
  
   ``
   sudo groupadd asir 
   ``

   Para crear los usuarios y meterlos en el grupo es poniendo
   
   ``
   sudo usermod -G asir lba1
   ``

   ``
   sudo usermod -G asir lba1
   ``
  
   y
  
   `` 
   sudo usermod -G asir lba2
    ``

   ``
   sudo usermod -G asir lba2
   ``

2. Creamos el directorio */compartido* mediante
   
   ``
   sudo mkdir compartido
   ``

   asignación de root como propietario

   ``
   sudo chown :root compartido/
   ``

   asignación de asir como grupo propietario

   ``
   sudo chown :asir compartido/
   ``

