# QEMU-KVM
Proyecto para instalar QEMU/KVM en Ubuntu.

![alt text](https://github.com/JuanRodenas/QEMU-KVM/blob/main/Logo.jpg)

* Vamos a ejecutar el siguiente comando con el fin de instalar KVM y las dependencias asociadas a este como `virt-manager` y `bridge-utils`:
~~~
sudo apt install -y qemu qemu-kvm libvirt-daemon libvirt-clients bridge-utils virt-manager
~~~

Las dependencias que hemos instalado han sido:
* El paquete `qemu` (emulador rápido) el cual es una aplicación que tiene como misión habilitar realizar la virtualización de hardware
* El paquete `qemu-kvm` el cual es el paquete KVM principal
* El `libvritd-daemon` el cual actúa como el demonio de virtualización
* El paquete bridge-utils con el cual se crea la conexión de puente permitiendo que los demas usuarios puedan acceder a la máquina virtual la cual no es el sistema host
* El `virt-manager` que es una aplicación con la cual es posible administrar máquinas virtuales usando una interfaz gráfica de usuario

Vamos a comprobar si el demonio libvritd-daemon esta corriendo, para ello usamos el siguiente comando:
~~~
sudo systemctl status libvirtd
~~~
Habilitamos este servicio con el arranque de Ubuntu 20.04 y 20.10:
~~~
sudo systemctl enable --now libvirtd
~~~
Luego comprobamos que los módulos KVM estén ejecutándose con la siguiente orden:
~~~
lsmod | grep -l kvm
~~~

#### crear maquina virtual con KVM en Ubuntu 20.4 o 20.10 comandos
Para este caso será útil el comando “virt-install” y debemos ingresar lo siguiente, por ejemplo, en este caso para instalar Debian 10:
~~~
sudo virt-install --name=Debian --os-variant=debian10 --vcpu=412 --ram=2048 --graphics spice --location=/home/solvetic/Descargas/debian-10.4.0-amd64-netinst.iso --network bridge:enp0s3
~~~

Al dar Enter podemos ver que se inicia el proceso de creación de la máquina virtual.

El indicador --os-variant hace referencia a la familia del sistema operativo o derivado de la VM, para consultar todas las opciones disponibles podemos ejecutar la siguiente orden:
Primero instalamos el paquete `libosinfo-bin`, para ello usamos el siguiente comando:
~~~
sudo apt install libosinfo-bin
~~~
Una vez instalado el paquete `libosinfo-bin`, ejecutar la siguiente orden para consultar todas las opciones disponibles:
~~~
osinfo-query os
~~~

![alt text](https://github.com/JuanRodenas/QEMU-KVM/blob/main/paso%20comandos.png)

#### crear maquina virtual con KVM en Ubuntu 20.4 o 20.10 modo gráfico
Antes de esto vamos a instalar una serie de utilidades de KVM con el siguiente comando:
~~~
sudo apt install uvtool
~~~

Ahora podemos acceder a la interfaz gráfica ejecutando en la consola `virt-manager` o bien directamente desde Actividades de Ubuntu, al hacerlo se desplegará lo siguiente:
~~~
virt-manager
~~~

![alt text](https://github.com/JuanRodenas/QEMU-KVM/blob/main/paso%20grafico.png)

### Comandos:

Iniciar máquina:
~~~
virsh start [VM]
~~~

Parar una máquina:
~~~
virsh shutdown [VM]
~~~

Eliminar una máquina:
~~~
virsh destroy [VM]
~~~

Listar máquinas:
~~~
virsh list
~~~


## ☑️ Ready!
