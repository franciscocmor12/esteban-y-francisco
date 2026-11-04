PASOS PARA ENTRAR AL SERVIDOR WEB

PASO 1: para instalar nuestro httpd hay que poner el comando "sudo dnf install httpd"


PASO 2: para ver la versión de nuestra página hay que colocar el comando "httpd -v"


PASO 3: Ahora, para ver el estado del servidor de nuestra página web, colocamos el comando "sudo systemctl status httpd"


PASO 4: Si aparece la palabra dead, está deshabilitado; para habilitarlo, se coloca el comando "sudo systemctl start httpd"


<img width="936" height="482" alt="image" src="https://github.com/user-attachments/assets/9f0b03e8-c271-407e-b239-7a15e7283548" />


PASO 5: Ahora, para ver el estado del servidor de nuestra página web, colocamos el comando "sudo systemctl status httpd". Vemos si la página está habilitada a través de nuestra máquina virtual en el navegador buscando 127.0.0.1; si funciona, es que sí está activo, pero al abrir en el navegador de nuestro sistema operativo nativo no va a aparecer funcionando; para esto usamos el comando.




PASO 6: Para habilitar nuestra página web completamente, --add-service=http --permanent firewall usamos el comando "sudo firewall-cmd --add-service=http --permanent"  


Ahora recargamos la página usando el comando "sudo firewall-cmd --reload” para recargar el firewall.


Y, como último, el “sudo firewall-cmd --list-all” para ver si está en la lista.


<img width="938" height="527" alt="image" src="https://github.com/user-attachments/assets/ceff4c03-b57e-48ea-856f-d7858db1f425" />


PASO 7: para editar en la página httpd, dentro del CentOS en la terminal colocamos 
sudo nano /usr/share/httpd/noindex/index -- html
