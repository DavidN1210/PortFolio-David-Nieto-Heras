# Identificación de archivos de configuración

## Instalación de Tomcat
Antes de nada, es necesario instalar Tomcat. Para ello, he utilizado los siguientes comandos en el siguiente orden:
1. `sudo apt update`
2. `sudo apt install tomcat10 tomcat10-admin -y`: comando para instalar Tomcat

![Sudo Install](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/instalacion_tomcat.png)
   
3. `systemctl status tomcat10`: para visualizar el estado del servicio y comprobar que Tomcat se ha instalado correctamente

![SystemCTL Status](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/comprobacion_instalacion.png)

## Localización de archivos clave
Archivos clave:
* **server.xml**
* **web.xml**
* **tomcat-users.xml**
* **context.xml**
  
Para encontrar estos archivos usado el comando `ls -l` para listar el contenido de `/etc/tomcat10`, donde se encuentra la configuración global

![Archivos clave](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/archivos_clave.png)

## Funcionalidad y elementos configurables
1. `server.xml`: Configura conectores (puertos, protocolos, SSL/HTTPS), hosts virtuales y contexts. Elementos configurables:
   
   * **Connectors:** puertos, protocolos (HTTP/1.1, AJP, HTTPS), configuración SSL/TLS.
   * **Engine / Host / Context:** jerarquía de contenedores (motor global, hosts virtuales, aplicaciones).
   * **Valves:** filtros de seguridad, acceso, logging.
   * **Thread pools:** número de hilos, timeout de conexiones.
   * **Session settings:** gestión de sesiones, cookies, persistencia.
     
2. `web.xml`: Define servlets por defecto, filtros, tipos MIME, páginas de error. Elementos configurables:
   
   * **Servlets y filtros:** servlets comunes y filtros aplicables a todas las apps.
   * **MIME types:** asociación de extensiones con tipos de contenido.
   * **Error pages:** páginas personalizadas para códigos de error (404, 500, etc.).
   * **Welcome files:** archivos de inicio por defecto (ej. index.html, index.jsp).
   * **Security constraints:** reglas de acceso globales.
     
3. `tomcat-users.xml`: Define usuarios y roles para acceder a aplicaciones internas como Manager y Host Manager. Elementos configurables:
   
   * **Usuarios:** nombre y contraseña
   * **Roles:** permisos como `manager-gui`, `manager-script`, `admin-gui`, `admin-script`.
   * **Asignación:** la asignación de roles al usuario
     
4. `context.txt`: Se usa para definir recursos compartidos como datasources JDBC, parámetros de entorno, etc. Elementos configurables:
   
   * **Recursos JNDI:** conexiones JDBC a bases de datos, colas JMS, etc.
   * **Parámetros de entorno:** variables accesibles desde las aplicaciones.
   * **Session settings:** configuración de sesiones por aplicación.
   * **Reloading:** control de recarga automática de aplicaciones.
   * **Security:** restricciones de acceso a recursos.

## Mapa de dependencias

![Mapa Dependencias](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/mapa_visual.png)



