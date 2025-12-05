# Tomcat: Investigación y descripción

![Logo Tomcat](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/logo.jpeg)

## Elementos de Tomcat: Utilidad y Localización

* **Catalina:** Contenedor de servlets de Tomcat. Se encarga de ejecutar las aplicaciones web dentro del servidor y se carga desde los scripts en `bin/` y se configura en `conf/server.xml`.
* **Coyote:** Conector HTTP/1.1. Escucha en un puerto TCP (por defecto 8080) y redirige las peticiones al motor de Tomcat para su procesamiento. Es definido como Connector dentro de `conf/server.xml`
* **Jasper**: Motor JSP. Compila las páginas JSP en servlets Java que luego son gestionados por Catalina. Sus librerías están en `lib/`
* **Manager:** Aplicación web incluida en Tomcat para desplegar, detener y administrar aplicaciones desde la interfaz web o línea de comandos. Desplegada en `webapps/manager/`
* **HostManager:** Permite crear y gestionar hosts virtuales dentro de Tomcat. Desplegada en `webapps/host-manager/`
