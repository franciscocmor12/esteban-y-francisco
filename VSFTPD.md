Habilitar e iniciar el servicio:

sudo yum install vsftpd -y


sudo systemctl status vsftpd


sudo systemctl start vsftpd


sudo systemctl enable vsftpd


sudo systemctl status vsftpd


ls /etc/vsftpd/

Antes de modificar, se realiza una copia con el siguiente comando:
sudo cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.backup

Ver si se creo la copia:
ls /etc/vsftpd/

Entramos para poder editar:
sudo nano /etc/vsftpd/vsftpd.conf

entramos y eliminamos el simbolo # donde dice chroot_local_user=YES

crtl+o enter , crtl+x para guardar y salir


Hacemos ctrl+alt+t para ingresar ala terminal del CentOS y verificamos el serivicio ftp localhost , si nos aparece tendremos que instalarlo nuevamente y seleccionamos y/n para seguir , nos saldra otra vez para confirmar y/n y luego verificamos de nuevo con el comando local host  Nos tendra que salir name y colocamos el usuario nuestro (ejemplo@ejemplo) de la misma manera colocamos la contraseña , y nos salgra 230 login successful
entramos al maxterm:


sudo firewall-cmd –list-all
aqui revisamoq que solo temenos el serivicio http y ssh , para actviar el ftp continuamos con estos commandos:


sudo firewall-cmd –add-service=ftp


sudo firewall-cmd –list-all  , verificamos de nuevo y ya nos saldra el serivicio

 
 tail /etc/passwd    para verificar    los usuarios recien creados


sudo adduser usuario_ftp      sirve para crear una nueva cuenta de usuario


sudo usermod -s /sbin/nologin usuario_ftp sirve para desactivar el acceso interactivo al sistema para el usuario


sudo cat /etc/shells sirve para mostrar la lista completa de intérpretes de comandos (shells) válidos y permitidos


El comando sudo nano /etc/shells abre el editor de texto en terminal nano con permisos de superusuario 


Entramos a una lista y colocamos en la parte final  /sbin/nologin , crtl+o  , crtl+x 


ftp localhost


colocamos el usuario creado en este caso usuario_ftp


ademas de la contraseña


y nos deberia salir 230 login successful


con estos paso entramos al moba y colocamos el servicio ftp , introduccimos la ip, usuario y Puerto 21 ademas de la contraseña que colocamos en el terminal de CentOS

