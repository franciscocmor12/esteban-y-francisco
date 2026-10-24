PASOS PARA ENTAR AL SERVIDOR WEB

PASO 1: para instalar nuestro httpd hay que poner el comando "sudo dnf install httpd"


PASO 2: para ver la version de nuestra pagina hay que colocar el comando "httpd -v"


PASO 3: Ahora para ver el estado del servidor de nuestra pagina web colocamos el comando "sudo systemctl status httpd"


PASO 4: Si aparece que esta dead esta desabilitado, para habilitar se coloca el comando "sudo systemctl start httpd"
