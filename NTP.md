Pasos para el NTP server


Comprobar la dirección IP de CentOS
Abre la terminal de CentOS y ejecuta:
ip a



También puedes utilizar:
hostname -I


Debería aparecer una dirección IP de tu red local, por ejemplo:
192.168.1.20


Comprueba la conexión a Internet:
ping -c 4 8.8.8.8


Y comprueba la resolución DNS:
ping -c 4 google.com


Si hay respuesta, la conectividad está funcionando.

Si tu máquina recibe una IP diferente a la de Windows, comprueba que ambos equipos estén en la misma red y que el router permita la comunicación entre dispositivos.

Instalar y activar SSH en CentOS
SSH permitirá controlar CentOS desde Windows mediante MobaXterm.


En CentOS ejecuta:
sudo dnf install openssh-server -y


Activa el servicio:
sudo systemctl enable --now sshd


Comprueba su estado:
sudo systemctl status sshd


Debe mostrar:
Active: active (running)


Permite SSH en el firewall:
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --reload


5. Conectar Windows con CentOS utilizando MobaXterm



1. Abre MobaXterm en Windows.
2. Haz clic en Session.
3. Selecciona SSH.
4. En Remote host, escribe la IP de CentOS.
5. Marca Specify username e introduce tu usuario de CentOS.
6. Deja el puerto 22.
7. Haz clic en OK.


Por ejemplo:
Remote host: 192.168.1.20
Username: tu_usuario
Port: 22


Introduce la contraseña de tu usuario de CentOS cuando te la solicite.

Una vez conectado, puedes ejecutar todos los comandos siguientes directamente desde la terminal de MobaXterm.
6. Instalar el servidor NTP con Chrony
En CentOS Stream 10 utilizaremos Chrony, que permite sincronizar el reloj de CentOS y proporcionar la hora a otros dispositivos mediante NTP. 
Installation Guide documentation+1


Desde MobaXterm ejecuta:
sudo dnf update -y


Instala Chrony:
sudo dnf install chrony -y


Activa el servicio:
sudo systemctl enable --now chronyd


Comprueba su funcionamiento:
sudo systemctl status chronyd


Debe aparecer:
Active: active (running)


Para salir de la pantalla de estado, presiona Q.
7. Configurar el servidor NTP
Primero realiza una copia de seguridad del archivo de configuración:
sudo cp /etc/chrony.conf /etc/chrony.conf.bak


Abre el archivo:
sudo nano /etc/chrony.conf


Busca las líneas que comienzan con pool o server. Puedes conservar las fuentes NTP que vienen configuradas por defecto si funcionan.

Por ejemplo, una fuente válida sería:
pool pool.ntp.org iburst


Después agrega al final del archivo:
# Permitir clientes de la red local
allow 192.168.1.0/24

# Ajustar el reloj al iniciar
makestep 1.0 3

# Sincronizar el reloj de hardware
rtcsync


Importante: La dirección 192.168.1.0/24 es un ejemplo. Debes sustituirla por la subred real de tu red local. Si makestep y rtcsync ya existen, no necesitas repetirlos.

La directiva allow permite que Chrony responda a solicitudes NTP de los equipos autorizados. 
Frequently Asked Questions+1


Para guardar en Nano:
1. Presiona Ctrl + O.
2. Presiona Enter.
3. Presiona Ctrl + X.
8. Configurar la zona horaria
Para Ecuador continental utiliza:
sudo timedatectl set-timezone America/Guayaquil


Comprueba la fecha y hora:
timedatectl


La salida debería incluir algo similar a:
Time zone: America/Guayaquil (-05, -0500)
NTP service: active


9. Reiniciar el servidor NTP
Ejecuta:
sudo systemctl restart chronyd


Comprueba nuevamente:
sudo systemctl status chronyd


También puedes verificar que se inicia automáticamente:
sudo systemctl is-enabled chronyd


Resultado esperado:
enabled


10. Abrir el puerto NTP en el firewall
El protocolo NTP utiliza el puerto UDP 123.

Ejecuta:
sudo firewall-cmd --permanent --add-service=ntp


Aplica los cambios:
sudo firewall-cmd --reload


Verifica:
sudo firewall-cmd --list-services


Entre los servicios permitidos debería aparecer:
ssh ntp


El listado puede incluir otros servicios. Estas reglas se aplican a la zona predeterminada; si tu interfaz utiliza otra zona, debes configurar esa zona. 
Installation Guide documentation+1

11. Verificar que el servidor NTP funciona
Ejecuta los siguientes comandos desde MobaXterm.

Comando 1. Verificar sincronización
chronyc tracking


Ejemplo de información que puedes obtener:
Reference ID    : ...
Stratum         : 3
System time     : ...
Leap status     : Normal


Comando 2. Consultar servidores NTP
chronyc sources -v


Un servidor seleccionado suele aparecer marcado con ^*.

Comando 3. Verificar el puerto 123
sudo ss -ulnp | grep ':123'


Deberías observar que chronyd está escuchando en UDP 123.

Comando 4. Consultar clientes conectados
sudo chronyc clients


Este último comando permite consultar clientes NTP que han realizado solicitudes al servidor, si existen registros disponibles. 
Red Hat Documentation+1

12. Comprobar la conectividad desde Windows
En Windows abre PowerShell y ejecuta:
ping 192.168.1.20


Sustituye esa dirección por la IP real de CentOS.

Después comprueba que Windows puede consultar la hora del servidor:
w32tm /stripchart /computer:192.168.1.20 /samples:5 /dataonly


Si funciona, verás mediciones de diferencia horaria.

Esta prueba verifica la respuesta NTP, pero todavía no cambia la configuración de sincronización de Windows.
13. Configurar Windows como cliente NTP (opcional)
Si tu práctica requiere que Windows sincronice su hora con CentOS, abre PowerShell como administrador.

En un equipo personal que no esté administrado por un dominio, ejecuta:
w32tm /config /manualpeerlist:"192.168.1.20,0x8" /syncfromflags:manual /update


Reinicia el servicio de hora:
Restart-Service w32time


Solicita sincronización:
w32tm /resync


Comprueba la fuente de sincronización:
w32tm /query /source


Y consulta su estado:
w32tm /query /status


Si se ha sincronizado correctamente, la fuente debería corresponder a tu servidor CentOS.

No realices este cambio en un equipo institucional o administrado sin autorización, porque podría reemplazar su configuración de hora.


COMANDOS UTILIZADOS 


Instalar Chrony
sudo dnf install chrony -y

Activar el servicio
sudo systemctl enable --now chronyd

Editar configuración
sudo nano /etc/chrony.conf

Reiniciar Chrony
sudo systemctl restart chronyd

Permitir NTP en el firewall
sudo firewall-cmd --permanent --add-service=ntp
sudo firewall-cmd --reload

Verificar el servicio
sudo systemctl status chronyd

Verificar sincronización
chronyc tracking
chronyc sources -v

Consultar clientes
sudo chronyc clients

Verificar puerto NTP
sudo ss -ulnp | grep ':123'
