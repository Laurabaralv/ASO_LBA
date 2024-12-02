## Configuración de SSh para varios usuarios

1. Preparación de la máquina y la configuración de la red

Lo primero que se ha realizado ha sido crear la MV con los comandos de vagrant en Visual Studio. Una vez creada hemos ido al VirtualBox para apagar la máquina iniciada y añadirle un segundo adaptador de red con la configuración de adaptador puente.

Desde VirtualBox la iniciamos con inicio desacoplado y nos conectamos con *vagrant ssh* desde el Visual Studio, es importante que estemos situados en el directorio donde hemos creado la máquina virtual.

Una vez dentro lo primero que vamos a hacer es cambiarle el hostname con el siguiente comando:

```
sudo hostnamectl set-hostname lba-server
```

A continuación, tenemos que configurar el fichero de red. Para ello tenemos que acceder de la siguiente forma:

```
sudo nano /etc/netplan/00-installer-config.yaml
```

Una vez abierto tenemos que añadirle el eth1 y la ip 10.10.0.0/8.

- Diego: 10.10.0.1/8
- Christelt: 10.10.0.2/8
- Laura: 10.10.0.3/8
- Mario: 10.10.0.4/8

A continuación, creamos los cuatro usuarios con *adduser*. Iniciaremos sesión con el nuestro y creamos la clave pública y la privada.

```
ssh-keygen -b 1024
```

Lo siguiente es copiar la clave publica en la carpeta propia del usuario en otro equipo (a partir de aquí se deben repetir los pasos en los otros tres equipos). Por ejemplo, si se quiere copiar en el equipo de Mario es:

```
scp .ssh/id_rsa.pub laura@10.10.0.4:/home/laura
```

Ahora nos conectamos al otro equipo mediante:

```
ssh laura@10.10.0.4
```

Sino existe la carpeta .ssh la crearemos

```
mkdir .ssh
```

Y por último moveremos el .pub en ella cambiándole el nombre.

```
mv id_rsa.pub .ssh/authorized-keys
```

