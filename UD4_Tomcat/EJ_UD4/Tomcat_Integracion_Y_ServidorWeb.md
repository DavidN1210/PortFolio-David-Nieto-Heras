# Práctica Tomcat: Integración Tomcat + Servidor web
##  Opción B: Reverse proxy hacia Tomcat
### 1. Habilitar los módulos necesarios
Lo primero que hay que hacer sería habitar los módulos necesarios en Apache
```bash
sudo a2enmod proxy proxy_http // Activa los módulos de Apache necesarios para que funcione el reverse proxy
sudo systemctl restart apache2 // Tras la habilitacion del modulo es necesario reiniciar Apache
```
![Modulos](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/sudo_proxyhttp.png)
### 2. Editar el archivo de configuarción por defecto
Con el comando `sudo nano /etc/apache2/sites-available/000-default.conf` añadimos a la configuración las siguientes dos líneas:
```bash
ProxyPass /HelloApp http://localhost:8080/HelloApp // ProxyPass: reenvía las peticiones entrantes hacia Tomcat.
ProxyPassReverse /HelloApp http://localhost:8080/HelloApp // ProxyPassReverse: corrige las respuestas/redirecciones de Tomcat para que el cliente siempre vea la URL pública de Apache.
```
![Configuración](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/default.png)
### 3. Prueba de funcionamiento
Podemos realizar la prueba en el navegador

![Navegador](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba_navegador.png)

O por comandos (`curl -I http://localhost/HelloApp/`)

![Comandos](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba_curl.png)

Como podemos ver, la prueba fue exitosa porque se puede ver la página inicial de HelloApp y el usuario nunca ve el puerto 8080 ni sabe que Tomcat está detrás
