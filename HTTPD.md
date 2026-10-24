PASOS PARA ENTAR AL SERVIDOR WEB

PASO 1: para instalar nuestro httpd hay que poner el comando "sudo dnf install httpd"


PASO 2: para ver la version de nuestra pagina hay que colocar el comando "httpd -v"


PASO 3: Ahora para ver el estado del servidor de nuestra pagina web colocamos el comando "sudo systemctl status httpd"


PASO 4: Si aparece que esta dead esta desabilitado, para habilitar se coloca el comando "sudo systemctl start httpd"


<img width="936" height="482" alt="image" src="https://github.com/user-attachments/assets/9f0b03e8-c271-407e-b239-7a15e7283548" />


PASO 5: Vemos si esta la pagina habilitada atravez de nuestra Maquina Virtual en el navegador buscando 127.0.0.1, si funciona es que si esta activo pero al abrir en nuestro navegador de nuestro sistema operativo nativo no va a aparecer funcionando.


PASO 6: Para habilitar nuestra pagina web completamente vamos a darle accesos a nuestra firewall atravez del uso de comandos "sudo firewall-cmd - -all-service-http - - permanent" como primer comando para desactivar el firewall, segundo el “sudo firewall-cmd - -reload” para recargar el firewall y como ultimo el “sudo firewall-cmd - -list-all” para ver si esta en la lista que ya se desactivo


<img width="938" height="527" alt="image" src="https://github.com/user-attachments/assets/ceff4c03-b57e-48ea-856f-d7858db1f425" />
