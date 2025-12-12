# Práctica Tomcat: Integración Tomcat + Servidor web
##  Opción B: Reverse proxy hacia Tomcat
### 1. Habilitar los módulos necesarios
Lo primero que hay que hacer sería habitar los módulos necesarios en Apache
```bash
sudo a2enmod proxy proxy_http
sudo systemctl restart apache2
```
### 2. Editar el archivo de configuarción por defecto
Con el comando `sudo nano /etc/apache2/sites-available/000-default.conf` añadimos a la configuración las siguientes dos líneas:
```bash
ProxyPass /HelloApp http://localhost:8080/HelloApp
ProxyPassReverse /HelloApp http://localhost:8080/HelloApp
```
### 3. Prueba de funcionamiento
Podemos realizar la prueba en el navegador
![Navegador]()
O por comando (`curl -I http://localhost/HelloApp/`)
![Comando]()
