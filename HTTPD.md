PASOS PARA ENTRAR AL SERVIDOR WEB


sudo dnf install httpd


httpd -v


sudo systemctl status httpd


sudo systemctl start httpd


sudo systemctl status httpd


sudo firewall-cmd –list-all


sudo firewall-cmd –add-service=http –permanent


sudo firewall-cmd –reload


sudo firewall-cmd –list-all


target: default

  
  ingress-priority: 0
  
  
  egress-priority: 0
  
  
  icmp-block-inversion: no
  
  
  interfaces: enp0s3
  
  
  sources:
  
  
  services: cockpit dhcpv6-client http ssh
  
  
  ports: 2234/tcp 2237/tcp
  
  
  protocols:
  
  
  forward: yes
  
  
  masquerade: no
  
  
  forward-ports:
  
  
  source-ports:
  
  
  icmp-blocks:
  
  
  rich rules:


ANTES DE MODIFICAR HACER UNA COPIA


sudo cp /usr/share/httpd/noindex/index.html /usr/share/httpd/noindex/index.html.backup


sudo nano /usr/share/httpd/noindex/index.html

