EVIDENCIAS


Integrantes: Francisco Morillo y Esteban Nievencela

Cambiar de puerto 22 a 2237


PASO 1: para cambiar de puerto hay que saber el ip en el Centos utilizamos el comadno : ip a


PASO 2: para modificar el puerto : sudo nano /etc/ssh/ssh_config


PASO 3: aqui buscamos el apartado que dice #port 22 , y le boro el # y coloco mi puerto personalizado 2237 quedando port 2237 


PASO 4: bloquea por defecto cualquier puerto SSH que no sea el 22 sudo manage port -a -t ssh_port_t -p tcp


PASO 5: permite que las conexiones entrantes dirigidas al puerto p. 2237  sudo firewall-cmd --zone public --permanent --add-port 2237/tcp


PASO 6: para aplicar los cambios realizados: sudo firewall-cmd --reload


paso 7: para recargar la nueva configuracione sshd: sudo systemctl restart sshd


PASO 8: para ver el estado actual del sshd:  sudo systemctl status sshd



<img width="600" height="473" alt="image" src="https://github.com/user-attachments/assets/f046d63e-8ce6-44fd-98a0-d9077cdd3d23" />
