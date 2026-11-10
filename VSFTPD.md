Habilitar e iniciar el servicio:

sudo yum install vsftpd -y


sudo systemctl status vsftpd


sudo systemctl start vsftpd


sudo systemctl enable vsftpd


sudo systemctl status vsftpd


ls /etc/vsftpd/


sudo cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.backup


ls /etc/vsftpd/


sudo nano /etc/vsftpd/vsftpd.conf


entramos y eliminamos el # donde dice chroot_local_user=YES


crtl+o  , crtl+x para guardar y salir


entramos al terminal del CentOS y verificamos el serivicio ftp localhost , si nos sale no encontrada temenos que instalarlo colocando y , ademas nos saldra otra vez colocamos y y luego verificamso de nuevo con el commando local host y ahora si nos saldra name y colocamos el usuario nuestro de la misma manera colocamos la contraseña , y nos salgra 230 login successful
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


colcoamos el usuario creado en este caso usuario_ftp


ademas de la contraseña


y nos deberia salir 230 login successful


con estos paso engtrasmo al moba y colocamso el servicio ftp , introduccimso la ip, usuario y Puerto 21 ademas de la contraseña que colocamos en el terminal de CentOS

