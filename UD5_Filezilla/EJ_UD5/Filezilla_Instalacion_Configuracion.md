# Actividad 2: Instalación y configuración inicial del servidor

## 1. Actualización del sistema y instalación de dependencias

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install wget gdebi-core -y
```

## 2. Descarga y instalación de Filezilla Server

1. Descargo en la página oficial el paqueta `.deb` para Linux
   
![Descarga del paquete .deb](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_pagina_oficial.png)

2. Una vez descargado, instalo FileZilla Server con el comando `sudo dpkg -i filezilla-server.deb`
   
![Instalación](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_comando_instalacion.png)

3. Se nos pide introducir una contraseña

![Contrasena](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/fillezilla_password_config.png)

```bash
sudo dpkg -i filezilla-server.deb (nombre del paquete)
sudo apt -f install -y (en caso de errores de dependencias)
```

4. Una vez instalado, inicio el servicio con `sudo systemctl start filezilla-server` y compruebo que esta activo `sudo systemctl status filezilla-server`

![Estado](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_enabled.png)

```bash
sudo systemctl start filezilla-server
sudo systemctl status filezilla-server
```

## 3. Consola de administración
Para accede a la consola, buscaremos en el menú de aplicaciones `FileZilla Server Administration` y la abriremos y en la ventana de conexión nos podemos conectar a un servidor, introduciendo el host, puerto y la contraseña. En mi caso me he conectado a localhost.

![Conexión Servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_consola_admin.png)

# 4. Configurar puerto de escucha FTP y la dirección IP
Para configurar el puerto de escucha FTP y la dirección IP, tenemos que acceder a la sección de `Server listeners` (Server -> Configure -> Server listeners)

![Conexión Servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_puerto_config.png)

# 5 Configurar inicio automático
Utilizaremos dos comandos: `sudo systemctl enable filezilla-server`, para habilitar el inicio automático, y 
`systemctl is-enabled filezilla-server`, para verificar que esta habilitado.

![Conexión Servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/inicio_auto.png)

```bash
sudo systemctl enable filezilla-server
systemctl is-enabled filezilla-server
```





