# Identificación de archivos de configuración

# Instalación de Tomcat
Antes de nada, es necesario instalar Tomcat. Para ello, he utilizado los siguientes comandos en el siguiente orden:
1. `sudo apt update`
2. `sudo apt install tomcat10 tomcat10-admin -y`: comando para instalar Tomcat

![Archivos clave](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/archivos_clave.png)
   
3. `systemctl status tomcat10`: para visualizar el estado del servicio y comprobar que Tomcat se ha instalado correctamente

![Archivos clave](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/archivos_clave.png)

## Localización de archivos clave
Archivos clave:
* **server.xml**
* **web.xml**
* **tomcat-users.xml**
* **context.xml**
  
Para encontrar estos archivos usado el comando `ls -l` para listar el contenido de `/etc/tomcat10`, donde se encuentra la configuración global

![Archivos clave](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/archivos_clave.png)

## Funcionalidad y elementos configurables
1. `server.xml`: Configura conectores (puertos, protocolos, SSL/HTTPS), hosts virtuales y contexts.
2. `web.xml`: Define servlets por defecto, filtros, tipos MIME, páginas de error.
3. `tomcat-users.xml`: Define usuarios y roles para acceder a aplicaciones internas como Manager y Host Manager.
4. `context.txt`: Se usa para definir recursos compartidos como datasources JDBC, parámetros de entorno, etc.

## Elementos configurables
