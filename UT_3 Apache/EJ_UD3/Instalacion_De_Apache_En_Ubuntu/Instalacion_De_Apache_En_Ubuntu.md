# Instalación y Configuración de Apache en Ubuntu
![Img Inicio](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/apache_img.jpg)
## Resumen
Este proyecto documenta el proceso de instalación y configuración del servidor web Apache en el sistema operativo Ubuntu, centrándose en el despliegue de un sitio web personalizado. Se explica la naturaleza de Apache como servidor de código abierto y sus funciones principales, incluyendo la atención de solicitudes HTTP. El trabajo detalla paso a paso la creación de un Virtual Host para el dominio gci.example.com, demostrando la capacidad de Apache para gestionar múltiples proyectos. Además, se documenta la resolución de un problema de acceso al dominio mediante la modificación del archivo /etc/hosts. La experiencia culmina con una valoración personal que resalta la importancia de comprender la interacción entre la configuración del servidor y la resolución de nombres local.

## Palabras Clave
Apache, Servidor Web, Ubuntu, Configuración, Virtual Hosts, HTTP, Linux, Despliegue, gci.example.com, index.html.

## Índice 
1. **Introducción**
2. **Instalación de Apache**
3. **Confuguración de Apache**
4. **Conclusión y Valoración Personal**
5. **Bibliografía y Anexos**

## Introducción

Este proyecto se realizará como parte de las actividades formativas del IES Juan Bosco, especificamente en el módulo de Despligue de Aplicacones Web del ciclo de DAW (Desarrollo de Aplicaciones Web). El trabajo se concibe como una simulación de despliegue real, en la que el objetivo es adquirir experiencia práctica en la administración de servicios web. El proyecto se lleva a cabo en clase, utilizando una máquina virtual con el sistema operativo de Ubuntu 24.04 LTS.

Utilizaremos Apache que es un software de servidor web gratuito y de código abierto que se utiliza principalmente para alojar sitios web y aplicaciones. Como todo servidor web es responsable de atender las solicitudes de los clientes cuando quieren consultar una URL. Apache está atento a las solicitudes, que llegan mediante el protocolo HTTP y se encarga de enviar las respuestas a los clientes. 

Nació en 1995 como una mejora del servidor web NCSA HTTPd. En aquel momento, la mayoría de los servidores web eran software propietario o tenían muchas limitaciones. Apache cambió esto ofreciendo una alternativa de código abierto, gratuita y con una comunidad activa que mejoraba constantemente su funcionamiento.
Durante años, Apache fue el servidor web más utilizado del mundo y aún hoy sigue siendo una opción sólida para muchos proyectos web.

Aunque Apache sigue siendo utilizado, podemos distinguir otras alternativas: 

![Servidores Web](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/alternativas_a_apache.png)

El **motivo principal** de este proyecto es la adquisición de competencias prácticas en la administración de servidores web. Nos basamos en Apache  para comprender de forma integral su arquitectura, desde la instalación inicial hasta la configuración avanzada de Virtual Hosts. El objetivo final es conseguir la capacidad de desplegar, gestionar y diagnosticar problemas en un entorno de servidor real.

# Instalación de Apache
Luego de todo el proceso de instalacuión de apache comprobamos que todo funciona:

![It works!](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/localhost_itworks.png)

# Configuración de Apache
Una vez intalado Apache, pasaremos a configurarlo:
1. Crearemos una carpeta para nuestro nuevo sitio web /var/www/. Se llamará gci.
   
![Carpera GCI!](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/nueva_carpeta_gci.png)

2. Luego, dentro de esa carpeta, crearemos nuevo archivo HTML (index.html) con el código que podemos ver en la siguiente imagen:

![index.html](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/index_html.png)

3. A continuación, vamos a crear un archivo VirtualHost para que cuando escribamos gci.example.com veamos el archivo html. Para ello, dentro del directorio de archivos de cofiguración (/etc/apache2/sites-available/) crearemos una copia del archivo de configuración por defecto de Apache y la guardaremos como gci.conf con el comando `sudo cp 000-default.conf gci.conf`. Después, editaremos gci.conf para registrar nuestro correo eléctronico en ServerAdmin, así podrán contactarte en caso de que Apache experimente algún error.

![Correo ServerAdmin](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/correo_david_example.png)

Tambien he puesto el directorio raíz del sitio web (DocumentRoot /var/www/gci/) y el nombre del dominio que Apache usará para saber cuándo debe servir este sitio (ServerName gci.example.com), de forma que cuando escribamos en el navegador http://gci.example.com podremos visulizar el archivo index.html.

4. Finalmente, tenemos que activar el archivo de configuración de hosts virtuales con el comando `sudo a2ensite gci.conf` y luego reiniciaremos Apache escribiendo `service apache2 reload`.

![Activacion Hosts](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/archivo_configuracion_host.png)

Después de hacer todos estos pasos y buscar en el navegador la dirección gci.example.com, debería de funcionar, sin embargo sucedió lo siguiente:

![No funciona](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/resultado_nofunciona.png)

Como podemos ver en la imagen, no se pudo encontrar el sitio web.

El problema es que el navegador no encuentra “example.com” y para solucionarlo tenemos que agragar la siguiente linea en /etc/hosts: **127.0.0.1 gci.example.com**. De esta forma, cada vez que queramos acceder a gic.example.com, nos llevará a localhost.

![Solución](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/solucion.png)

Como podemos ver ahora sí funciona:

![Si funciona](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/resultado_sifunciona.png)

## Conclusión y Valoración Personal
La instalación y configuración de Apache en Ubuntu permite comprender de forma práctica como funciona uno de los servidores web más importantes y utilizados. A través de este proceso, desde la creacion de un sitio web hasta la configuración de hosts virtuales, se demuestra la capacidad de Apache para gestionar proyectos en un mismo servidor. Además, cabe resaltar la importancia de entender la relación entre los archivos de configuración, el DNS y localhost para dar una solución a los problemas vistos durante la implementación.

Realizar este trabajo ha sido una gran experiencia, porque me permitió no solo conocer los pasos para instalar y configurar Apache en Ubuntu, sino tambien aprender a desplegar una aplicación web. La parte que más me gusto fue ver el código implementado y cada configuración que hizo lo posible.

## Bibliografía y Anexos

[https://axarnet.es/blog/que-es-apache](https://axarnet.es/blog/que-es-apache)

[https://www.arsys.es/blog/que-es-apache-y-para-que-sirve](https://www.arsys.es/blog/que-es-apache-y-para-que-sirve)

[https://ubuntu.com/tutorials/install-and-configure-apache#1-overview](https://ubuntu.com/tutorials/install-and-configure-apache#1-overview)

[https://foro.puntocomunica.com/viewtopic.php?t=312](https://foro.puntocomunica.com/viewtopic.php?t=312)






