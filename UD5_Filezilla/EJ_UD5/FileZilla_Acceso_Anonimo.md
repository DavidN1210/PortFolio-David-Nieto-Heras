<img width="985" height="393" alt="image" src="https://github.com/user-attachments/assets/78eff67f-2845-4619-801c-2cded1e43739" /># Actividad 4: Configuración de acceso anónimo

## 1. Activar el acceso anónimo
### Creación del usuario anónimo
Se creó un usuario llamado anonymous en FileZilla Server, configurado sin contraseña para permitir el acceso anónimo. 

Este usuario quedó habilitado para iniciar sesión sin autenticación adicional y solo se establecieron permisos exclusivamente de lectura, desactivando las opciones de escritura y borrado.

![Usuario Anónimo](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/usuario_anonimo.png)

## 2. Limitación del directorio accesible
Al usuario anónimo se le asignó un mountpoint específico, de forma que solo pudiera acceder al directorio autorizado del servidor.
El directorio físico configurado fue el destinado al acceso público, evitando que el usuario anónimo pudiera navegar por otras rutas del sistema.

### Creación del directorio

![Directorio](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/creacion_directorio.png)

``` bash
sudo mkdir -p /srv/ftp/anon
sudo chown -R ftp:ftp srv/ftp/anon
```

## 3. Conexión desde un cliente FTP y verificación
### Instalación de FileZilla Client
Para realizar a conexión he tenido que intalarme en mi máquina virtual FileZilla Client (el cliente FTP)
con el comando `sudo apt install filezilla -y`.

![Filezilla Client](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_client.png)

## Cambiar la dirección IP del servidor FTP
Antes de realizar la conexión, tengo que configurar la dirección ip del servidor. Por ello, en la configuración de Filezilla Server he puesto como direccion ip 127.0.0.1 (localhost)

![Dirección IP](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/dirreccion_ip_servidor.png)

## Resultado de la conexión 
He realizado la conexión desde Filezilla Client, introduciendo los siguientes datos:

* **Servidor:** 127.0.0.1
* **Nombre de usuario:** anónimo
* **Contraseña:** vaciá
* **Puerto:** 21

Y el resultado ha sido el siguiente por el lado del cliente:

![Dirección IP](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/resultado_client.png)

Y por el lado del servidor:

![Dirección IP](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/resultado_servidor.png)

Como se puede ver en la última imagen, la conexión se realizo correctamente entre cliente-servidor
