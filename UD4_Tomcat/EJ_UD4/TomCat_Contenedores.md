# Tomcat en contenedores (Docker)
## 1. Descarga de la imagen oficial

![Imagen oficial](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/descarga_imagen_of.png)

```bash
docker pull tomcat:latest
```

## 2. Creación de la App

### Puerto 9090
Ya que el puerto 8080 ya lo tengo ocupado, lanzo Tomcat en el puerto 9090.

![9090](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/ejecutar_tomcat_9090.png)

```bash
docker run -d --name tomcat-miweb -p 9090:8080 tomcat:latest
```
### App `MiWeb`

1. Creo la estructura de carpetas `MiWeb/WEB-INF`
```bash
mkdir -p MiWeb/WEB-INF
```
2. Creo el archivo JSP
```bash
sudo nano MiWeb/index.jsp
// Contenido del fichero:
<h1>Bienvenido a MiWeb desplegada en Docker</h1>
<p>Esta es una aplicación sencilla para pruebas de Tomcat en contenedores.</p>
```
3. Creo el descriptor de despliegue
```bash
sudo nano MiWeb/WEB-INF/web.xml
// Contenido del fichero:
<web-app xmlns="http://jakarta.ee/xml/ns/jakartaee"
         version="5.0">
</web-app>
```
4. Empaqueto MiWeb como archivo WAR
```bash
cd MiWeb
jar -cvf MiWeb.war *
cd ..
```
5. Despliego MiWeb en `/usr/local/tomcat/webapps/`

![Despliege](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/desplegar_web_contenedor.png)

```bash
sudo docker cp MiWeb/MiWeb.war tomcat-miweb:/usr/local/tomcat/webapps/
```
6. Accedo a la web desde el navegador

![Navegador](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/navegador_miWeb.png)

## 3. Diferencias entre Tomcat nativo y Tomcat en contenedor (Docker)

| Característica | Tomcat nativo | Tomcat en Docker |
|----------------|---------------|------------------|
| **Instalación** | Requiere instalar paquetes o descomprimir manualmente Tomcat en el sistema | Se obtiene directamente con `docker pull tomcat:latest` |
| **Configuración** | Archivos locales en `/etc/tomcat/` o `conf/` | Configuración dentro del contenedor o montando volúmenes |
| **Despliegue de aplicaciones** | Copiar el WAR a `/var/lib/tomcat/webapps/` | `docker cp`, volúmenes o imágenes personalizadas |
| **Actualización** | Manual, reinstalando Tomcat | Cambiando la imagen (`docker pull`) y recreando el contenedor |
| **Portabilidad** | Depende del sistema operativo | Funciona igual en cualquier máquina con Docker |
| **Aislamiento** | Comparte el sistema con otros servicios | Cada contenedor está aislado del host y de otros contenedores |
| **Rendimiento** | Acceso directo al sistema, sin capa adicional | Ligera sobrecarga por virtualización ligera |
| **Escalabilidad** | Limitada, requiere configuración manual | Muy fácil con Docker Compose o Kubernetes |
| **Mantenimiento** | Más complejo, requiere gestionar dependencias | Muy sencillo: se elimina y recrea el contenedor |
| **Reproducibilidad** | Puede variar según el entorno | Siempre idéntico gracias a las imágenes |


