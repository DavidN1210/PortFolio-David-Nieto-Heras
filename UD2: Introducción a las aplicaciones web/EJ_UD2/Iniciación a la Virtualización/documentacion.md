# Iniciación a la Virtualización
## Instalación de Ubuntu en VirtualBox
### 1. Descargar la ISO de Ubuntu 24.04 LTS desde la página oficial de Ubuntu.
Podemos descargar la ISO desde la página oficial de Ubuntu

![Descargo la ISO](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/iso.png)

### 2. Creo una nueva máquina virtual con las siguientes características recomendadas:
* Nombre: Ubuntu-DAW2DAW
* RAM: 4096 MB
* Disco duro virtual: mínimo 50 GB

Empezamos creando una nueva máquina y poninendole el nombre, la iso y la ruta de la máquina, luego le asingnamos cuanta memoria base (RAM) queremos que tenga (4096 MB) y, después, seleccionamos la opción de Crear disco duro virtual (reservado dinamicamente) y le asignamos un tamaño de 50 GB

![Máquina virtual](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/maquina.png)

Para la red NAT, tenemos que seguir la siguiente ruta Click derecho (sobre la máquina) -> Configuración -> Red. Luego, buscamos el adaptador 1, lo habilitamos y, en menú desplegable, seleccionamos que este conectado a NAT (permite acceso a Internet desde la VM).

* Tipo de red: NAT

![Red NAT](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/nat.png)
  
### 3. Instalación de Ubuntu y de las Guest Additions
Luego de iniciar la máquina virtual, nos aparecerán tres opciones y selecionaremos "Try or Install Ubuntu". A continuación, en el escritorio, haremos click en una carpeta con nombre Intalar Ubuntu y pasaremos a configuar el idioma, horario, teclado, seleccionaremos la opción de borrar el disco e instalar Ubuntu y crearemos nuestro usuario. Finalmente, esperamos a que se complete la instalación y reiniciamos la máquina.

Para instalar las Guest Additions, seguiremos los siguientes pasos:
1. Accederemos a la ruta: Dispositivos (en la barra superior de la máquina) → Insertar imagen de CD de las Guest Additions
2. Luego de insertar el CD, nos aparecerá una ventana que nos preguntara que si queremos ejecutar el programa

![Ejecutar programa](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/ejecutarguest.png)
   
4. Hacemos click en ejecutar y esperamos a que termine la instalación
5. Guest Additions instaladas

![Guest Additions](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/guestaddinstall.png)

Las Guest Additions mejoran el rendimiento y la integración de Ubuntu en VirtualBox (mejor resolución, portapapeles compartido, carpetas compartidas, etc.).

### 4. Captura de pantalla del escritorio una vez instalado.
Por último, tomamos una captura del escritorio de Ubuntu 24.04 LTS mostrando el sistema correctamente instalado y en funcionamiento.

![Captura del escritorio](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/desktop.png)

## Instalación de Docker en Ubuntu
### Actualización de repositorios
Antes de instalar Docker es necesario que el sistema esté completamente al día para evitar errores de dependencias o conflictos de versiones. Para ello utilizo los siguientes comandos:

`sudo apt update`: Este comando accede a los repositorios cinfigurados en mi sistema y me muestra los paquetes que puedo actualizar de Ubuntu.

![Update](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/update.png)

`sudo apt "upgrade -y`: Este comando instala las actualizaciones disponibles para todos los paquetes que ya están instalados en mi sistema, usando la información más reciente obtenida previamente con sudo apt update.

![Upgrade](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/upgrade.png)

### Instalo las dependencias
Instalo las dependencias con el comando: 

`sudo apt install ca-certificates curl gnupg -y`: Este comando instala tres paquetes esenciales en Ubuntu `ca-certificates`, `curl` y `gnupg` que se necesitan para descargar e instalar Docker de forma segura desde Internet. Sin estos tres paquetes, no podrías descargar ni validar los archivos del repositorio correctamente.

![Dependencias](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/dependencias.png)

### Instalación de Docker Desktop y Verificación
Para la instalación, primero el comando `wget https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb`, el cual descarga el instalador de Docker Desktop para Linux en formato .deb directamente desde los servidores oficiales de Docker.

![Instalador](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/instalador.png)

Luego, lo instalo definitivamente con `sudo apt install ./docker-desktop-amd64.deb`

![Instalar Docker](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/instalardocker.png)

Para comprobar que Docker se ha instalado correctamente utilizo: `docker --version` (muestra la versión de docker que he instalado) y `sudo docker run hello-world` (se ejecuta un contenedor de prueba llamado hello-world para verificar que Docker funcione correctamente)

![Comprobación Docker](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/prueba.png)

## Instalación de contenedores de servidor web y de aplicaciones

1. Utilizo dos comandos (`sudo docker search nginx` y `sudo docker search tomcat`) para buscar imágenes oficiales en Docker Hub, el repositorio público de contenedores.

![Imagenes](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/img.png)

2. Descargo y inicio los contenedores con los comandos: `sudo docker run -d -p 8080:80 --name webserver nginx` y `sudo docker run -d -p 8081:8080 --name appserver tomcat`

![Contenedores](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/contenedores.png)

3. Verifico si funciona, visulizando los contenedores activos, con el comando `sudodocker ps`

![Comprobación Contenedores](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/verificar_contenedores.png)

4. Ahora si pongo en el navegador estas las url http://localhost:8080 (Nginx) y http://localhost:8081 (Tomcat), puedo ver que los contenedores que hemos instalado están funcionando correctamente

![Comprobación en el navegador](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/img_UD2/navegador.png)

##  Requerimientos mínimos para implantar una aplicación web
### Hardware y Software
Hardware mínimo:
* Procesador: CPU moderna de al menos 2 núcleos (Intel i3 o equivalente).
* Memoria RAM: 4 GB como mínimo (8 GB recomendado para producción).
* Almacenamiento: 50 GB de disco duro/SSD libre para sistema operativo, bases de datos, y archivos de la aplicación.
* Red: Tarjeta de red compatible con 1 Gbps (mínimo 100 Mbps aceptable en entornos de prueba).

Software mínimo:
* Sistema operativo: Linux (Ubuntu, CentOS, Debian) o Windows Server (2019 o superior).
* Servidor web: Apache, Nginx o IIS según el sistema operativo.
* Servidor de aplicaciones: Dependiendo del stack (PHP, Node.js, Python/Django, Java/Tomcat).
* Base de datos: MySQL, PostgreSQL, SQL Server, MongoDB, según la aplicación.
* Lenguajes y frameworks: PHP ≥ 7.4, Node.js ≥ 18, Python ≥ 3.9, Java ≥ 11, según corresponda.

### Infraestructura de red

* Conectividad: Acceso a Internet estable con ancho de banda suficiente según la cantidad de usuarios concurrentes.
* Dirección IP fija: Recomendada para servidores de producción.
* DNS configurado: Para que el dominio apunte correctamente al servidor.
* Firewall: Configurado para filtrar puertos innecesarios (solo abrir los necesarios: HTTP/HTTPS, SSH/RDP).
* Opcional: Balanceador de carga para aplicaciones de alta disponibilidad.

### Configuración del servidor web y de aplicaciones
Servidor web:
* Instalación y configuración básica:
  * Apache/Nginx: habilitar módulos necesarios, configuraciones de logs, compresión gzip, cacheo básico.
* HTTPS: Certificado SSL/TLS válido (Let’s Encrypt o comercial).
* Redirecciones y URLs amigables: Configuración de .htaccess o reglas de Nginx.
  
Servidor de aplicaciones:
* Entorno de ejecución: Configurar versiones correctas de PHP, Node.js, Python, etc.
* Variables de entorno: Definir rutas, claves API, credenciales de base de datos.
* Gestión de dependencias: Composer, npm, pip, Maven según corresponda.
* Gestión de procesos: Supervisord, PM2 o systemd para asegurar ejecución continua.

### Seguridad y mantenimiento
Seguridad:
* Actualizaciones periódicas: Sistema operativo, servidor web, aplicaciones y dependencias.
* Firewall y seguridad de red: Solo puertos necesarios abiertos, IDS/IPS opcional.
* Copias de seguridad: Base de datos y archivos de la aplicación, con almacenamiento seguro fuera del servidor principal.
* Autenticación y permisos: Usuarios y grupos limitados, credenciales seguras.
* Protección frente a ataques comunes: SQL Injection, XSS, CSRF, configuraciones seguras de headers HTTP.

Mantenimiento:
* Monitoreo del servidor: CPU, RAM, almacenamiento, logs de errores.
* Logs de aplicación y servidor: Revisión periódica y rotación automática.
* Plan de recuperación ante desastres: Procedimientos documentados para restauración en caso de fallo.
* Optimización periódica: Base de datos y cacheo para mejorar rendimiento.




