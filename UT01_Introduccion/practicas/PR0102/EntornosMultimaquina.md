# PR0102 Entornos multimáquina

Para conectar dos máquinas virtuales en vagrant tenemos que modificar el fichero *vagrantfile* de la siguiente manera:

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "server" do | m1 |
    m1.vm.box = "StefanScherer/windows_2019"
    m1.vm.network "private_network", ip: "172.19.0.10"
    m1.vm.hostname = "server-lba"
    m1.vm.provider "virtualbox" do |vb|
      vb.name = "server-lba"
      vb.memory = 4096
      vb.cpus = 4
    end
  end

  config.vm.define "client" do | m2 |
    m2.vm.box = "scotch/box"
    m2.vm.network "private_network", ip: "172.19.0.11"
    m2.vm.hostname = "client-lba"
    m2.vm.provider "virtualbox" do |vb|
      vb.name = "client-lba"
      vb.memory = 2048
      vb.cpus = 2
    end
  end

end
```

Las dos primeras líneas con el # son comentarios que se crean con el propio documento y que no modificamos. Lo que si configuramos son las siguientes líneas.

Con la tercera línea abrimos la configuración para la máquina virtual. Hay que tener en cuenta que cada *do* a de tener siempre un *end* que lo cierre.

A continuación, continuamos configurando cada máquina, comenzamos poniendo:

`` 
config.vm.define "server" do | m1 |
``

Entre comillas ponemos si es server o cliente y entre las tuberías ponemos un nombre para la MV.

Las siguientes cuatro líneas comenzaran todas por el nombre que hayamos puesto entre las tuberías, comenzando por el nombre de la máquina que hemos instalado, seguido por la dirección de red, el hostname y provider. Cada uno en una línea distinta.

En la configuracíon *provider* podemos definir el nombre de la máquina, su memoria y el número de cps.

Ahora volveríamos a poner otra vez la configuración *define* para la otra máquina virtual, hay que tener en cuenta que las dos máquinas tienen que estar en la misma red. Indicando si es privada o pública.