Habilitar e iniciar el servicio:


bash

1.sudo systemctl enable vsftpd --now

2.realizar una copia   sudo cp /etc/vsftpd/vsftpd.conf /etc/vsftpd.conf.backup

3.sudo nano /etc/vsftpd/vsftpd.conf

4.sudo systemctl enable --now vsftpd


5.sudo firewall-cmd --permanent --add-service=ftp
sudo firewall-cmd --reload


6.instalar el firezilla.client y configurar todo para tener una correcta instalacion, se debe abrir automaticamente servidor 10.21.165.163 nombre de usuario:efnievecela y contraseña ******


7.sudo useradd -m -s /sbin/nologin efnievecela_ftp y no tener un shell (interfaz grfica)
sudo passwd efnivencela_ftp
******* (contraseña: 123cuatro)

