# PR0101: Introducción a Vagrant

Primero nos dirigimos a la carpeta donde queremos crear la MV, en este caso es *D:\ASO_LBA\UT01_introduccion\practicas\PR0101*, donde comenzamos descargando la imagen de la máquina virtual con el comando: 

```
vagrant box add ubuntu/focal64 
``` 

El siguiente comando es: 

```
vagrant init ubuntu/focal64 --minimal 
```

Este comando crea el archivo *vagrantfile* que es con el que seguiremos trabajando. al añadirle la extensión *--minimal* nos crea el fichero sin comentarios.  

A continuación, editaremos dicho fichero en PowerShell. Las líneas que añadiremos son: 

```
config.vm.hostname = "server-lba" 
```
--> Esta nos cambia el nombre de la MV. 

```
 config.vm.provider "virtualbox" do | vb|  

```
 --> Este comando nos permite comenzar a editar las especificaciones del providor. cuando hayamos terminado de editarlo solo hace falta poner un *end*. 

```
vb.name = "Ubuntu Server"  
```
 --> Nombre del servidor 

```
 vb.memory = 2048  
``` 
--> Asignación de la RAM 

```
vb.cpus = 2 
```
--> Cores virtuales 