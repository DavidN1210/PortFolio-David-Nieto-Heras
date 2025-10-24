# Iniciación a la Virtualización
## Instalación de Ubuntu en VirtualBox
### 1. Descargar la ISO de Ubuntu 24.04 LTS desde la página oficial de Ubuntu.
Podemos descargar la ISO desde la página oficial de Ubuntu

![Descargo la ISO](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/EJ_UD2/Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/img_UD2/iso.png)

### 2. Crea una nueva máquina virtual con las siguientes características recomendadas:
* Nombre: Ubuntu-DAW2DAW
* RAM: 4096 MB
* Disco duro virtual: mínimo 50 GB

Empezamos creando una nueva máquina y poninendole el nombre, la iso y la ruta de la máquina, luego le asingnamos cuanta memoria base (RAM) queremos que tenga (4096 MB) y, después, seleccionamos la opción de Crear disco duro virtual (reservado dinamicamente) y le asignamos un tamaño de 50 GB

![Máquina virtual](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/EJ_UD2/Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/img_UD2/maquina.png)

Para la red NAT, tenemos que seguir la siguiente ruta Click derecho (sobre la máquina) -> Configuración -> Red. Luego, buscamos el adaptador 1, lo habilitamos y, en menú desplegable, seleccionamos que este conectado a NAT (permite acceso a Internet desde la VM).

* Tipo de red: NAT

![Máquina virtual](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/EJ_UD2/Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/img_UD2/nat.png)
  
### 3. Instalación de Ubuntu y de las Guest Additions
Luego de iniciar la máquina virtual, nos aparecerán tres opciones y selecionaremos "Try or Install Ubuntu". A continuación, en el escritorio, haremos click en una carpeta con nombre Intalar Ubuntu y pasaremos a configuar el idioma, horario, teclado, seleccionaremos la opción de borrar el disco e instalar Ubuntu y crearemos nuestro usuario. Finalmente, esperamos a que se complete la instalación y reiniciamos la máquina.

Para instalar las Guest Additions, seguiremos los siguientes pasos:
1. Accederemos a la ruta: Dispositivos (en la barra superior de la máquina) → Insertar imagen de CD de las Guest Additions
2. Luego de insertar el CD, nos aparecerá una ventana que nos preguntara que si queremos ejecutar el programa

![Ejecutar](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/EJ_UD2/Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/img_UD2/ejecutarguest.png)
   
4. Hacemos click en ejecutar y esperamos a que termine la instalación
5. Guest Additions instaladas

![Guest Additions](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/EJ_UD2/Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/img_UD2/guestaddinstall.png)

Las Guest Additions mejoran el rendimiento y la integración de Ubuntu en VirtualBox (mejor resolución, portapapeles compartido, carpetas compartidas, etc.).

### 4. Captura de pantalla del escritorio una vez instalado.
Por último, tomamos una captura del escritorio de Ubuntu 24.04 LTS mostrando el sistema correctamente instalado y en funcionamiento.

![Captura del escritorio](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/EJ_UD2/Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/img_UD2/desktop.png)

## Instalación de Docker en Ubuntu
### Actualización de repositorios
Antes de instalar Docker es necesario que el sistema esté completamente al día para evitar errores de dependencias o conflictos de versiones. Para ello utilizo los siguientes comandos:

`sudo apt update`: Este comando accede a los repositorios cinfigurados en mi sistema y me muestra los paquetes que puedo actualizar de Ubuntu.

![Update](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/EJ_UD2/Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/img_UD2/update.png)

`sudo apt "upgrade -y`: Este comando instala las actualizaciones disponibles para todos los paquetes que ya están instalados en mi sistema, usando la información más reciente obtenida previamente con sudo apt update.

![Upgrade](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/EJ_UD2/Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/img_UD2/upgrade.png)

### Instalo las dependencias
Instalo las dependencias con el comando: 

`sudo apt install ca-certificates curl gnupg -y`: Este comando instala tres paquetes esenciales en Ubuntu `ca-certificates`, `curl` y `gnupg` que se necesitan para descargar e instalar Docker de forma segura desde Internet. Sin estos tres paquetes, no podrías descargar ni validar los archivos del repositorio correctamente.

![Dependencias](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD2%3A%20Introducci%C3%B3n%20a%20las%20aplicaciones%20web/EJ_UD2/Iniciaci%C3%B3n%20a%20la%20Virtualizaci%C3%B3n/img_UD2/dependencias.png)

### Añado el repositorio de Docker y instalo DockerDesktop







