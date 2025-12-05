# Tomcat: Investigación y descripción

![Logo Tomcat](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/logo.jpeg)

# Apache Tomcat: Componentes y Funcionamiento
## Resumen

### Catalina
Es el **contenedor de servlets** de Tomcat. Se encarga de ejecutar las aplicaciones web y gestionar los ciclos de vida de servlets y JSP. Se carga desde los scripts en `bin/` y se configura principalmente en `conf/server.xml`.

### Coyote
Es el **conector HTTP/1.1** de Tomcat. Escucha en un puerto TCP (por defecto **8080**) y redirige las peticiones al motor interno para su procesamiento. Se define como `<Connector>` dentro de `conf/server.xml`.

### Jasper
Es el **motor JSP** de Tomcat. Compila las páginas JSP en servlets Java que luego son gestionados por Catalina. Sus librerías se encuentran en el directorio `lib/`.

### Manager
Aplicación web incluida en Tomcat que permite **desplegar, detener y administrar aplicaciones** desde la interfaz web o línea de comandos. Se despliega en `webapps/manager/`.

### Host Manager
Aplicación web que permite **crear y gestionar hosts virtuales** dentro de Tomcat. Se despliega en `webapps/host-manager/`.

## Estructura básica de directorios
- `bin/` → scripts de arranque y apagado.  
- `conf/` → archivos de configuración (`server.xml`, `web.xml`, etc.).  
- `webapps/` → aplicaciones desplegadas (WAR y directorios).  
- `lib/` → librerías compartidas.  
- `logs/` → registros de actividad y errores.  

## Flujo interno de funcionamiento
1. Tomcat recibe peticiones a través de **Coyote**.  
2. Las entrega a **Catalina**, que gestiona los contenedores de servlets.  
3. **Jasper** compila JSPs en servlets cuando es necesario.  
4. El despliegue de aplicaciones se realiza automáticamente al detectar **WARs en `webapps/`**.  
5. La administración se realiza mediante **Manager** y **Host Manager**.  
