# Práctica UT3 Apache: HTTPS

![Imagen HTTPS](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/https.jpeg)

## Resumen
Este proyecto documenta el proceso de instalación y configuración del servidor web Apache en el sistema operativo Ubuntu, centrándose en la implementación de HTTPS mediante un certificado autofirmado. Se explica la naturaleza de Apache como servidor de código abierto y sus funciones principales, incluyendo la atención de solicitudes HTTP y HTTPS. El trabajo detalla paso a paso la creación de un Virtual Host para el dominio simulado `daviddominio.com`, demostrando la capacidad de Apache para gestionar sitios seguros incluso en entornos locales. Además, se documenta la resolución de un problema de acceso al dominio mediante la modificación del archivo /etc/hosts, lo que permitió simular la resolución de nombres sin necesidad de un dominio real. La experiencia culmina con una valoración personal que resalta la importancia de comprender la interacción entre la configuración del servidor, la gestión de certificados y la resolución de nombres local para garantizar un entorno de pruebas funcional y seguro.

## Palabras Clave
Apache, Servidor Web, Ubuntu, Configuración, Virtual Hosts, HTTPS, SSL, Certificado Autofirmado, Linux, Despliegue, daviddominio.com, /etc/hosts.

## Índice 
1. **Introducción**
2. **Investigación**
3. **Ejecución técnica**
   1. Estado de Apache y Instalación de módulos
   2. Generación del certificado autofirmado (Opción A)
   3. VirtualHost (Puerto 433)
   4. Dominio en Localhost
   5. Prueba de acceso
4. **Conclusión y Valoración Personal y Dificultades encontradas**
5. **Bibliografía y Anexos**

## Introducción
Este proyecto se desarrolla en el IES Juan Bosco, dentro del módulo de Despliegue de Aplicaciones Web del ciclo de DAW (Desarrollo de Aplicaciones Web). El entorno de trabajo es una máquina virtual con Ubuntu 24.04 LTS, donde se instala y configura el servidor web Apache2.

Para comprender mejor la práctica, es necesario introducir el protocolo HTTP (Hypertext Transfer Protocol), que es el estándar utilizado para la transmisión de información en la web. HTTP permite que los navegadores soliciten páginas y recursos a los servidores, y que estos respondan con el contenido correspondiente. Fue creado en los años 90 por Tim Berners-Lee como parte del desarrollo de la World Wide Web, y desde entonces ha evolucionado hasta convertirse en la base de la comunicación en Internet. Posteriormente, surgió HTTPS, que añade seguridad mediante cifrado y autenticación, garantizando la integridad de los datos transmitidos.

El motivo principal de este proyecto es adquirir competencias prácticas en la administración de servidores web, centrándose en la implementación de HTTPS para asegurar las comunicaciones entre cliente y servidor. La práctica busca simular un despliegue real, permitiendo al alumnado enfrentarse a situaciones comunes como la configuración de Virtual Hosts, la gestión de certificados digitales y la resolución de problemas de acceso a dominios.

## Investigación
### Funcionamiento y importancia del protocolo HTTPS
HTTPS (Hypertext Transfer Protocol Secure) es la versión segura de HTTPS. Su objetivo, dentro de la seguridad web, es proteger la comunicación entre el cliente (navegador) y el servidor web utilizando cifrado, autenticación e integridad.
En cuanto a su funcionamiento, HTTPS utiliza un protocolo de encriptación para las comunicaciones. Este protocolo es el TLS (antes SSL), el cual asegura las comunicaciones mediante un sistema de seguridad que utiliza dos claves diferentes para la encriptación:
1. **La clave privada:** esta clave la controla el propietario de un sitio web. Esta clave está ubicada en un servidor web y se utiliza para desencriptar la información encriptada por la clave pública.
2.  **La clave pública:** esta clave está disponible para todos los que quieran interactuar con el servidor de forma segura. La información encriptada por la clave pública solo puede ser desencriptada por la clave privada.
### Tipos de certificados
* **Autofirmados:** son aquellos firmados por el propietario del servidor. Estos certificados muestran una notificación en el navegador de que el sitio no está protegido y, por tanto, no es seguro visitarlo sin realizar previamente las comprobaciones básicas, ya que son muy utilizados para fraudes online.
* **CA confiable:** son aquellos firmados por una Autoridad de Certificación (CA). La CA verifica la identidad de una página web, empresa o persona y asegura que la comunicación entre el servidor y el usuario se realice de forma cifrada y segura. Cuando visitamos una página con el prefijo HTTPS, significa que existe un certificado digital válido emitido por una CA.
### Módulos para hablilitar SSL/TLS
* `ssl`: habilita soporte para conexiones HTTPS.
* `headers`: permite gestionar cabeceras HTTP (ej. seguridad, redirecciones).
* `socache_shmcb`: requerido para almacenar información de certificados
## Ejecución Técnica
Durante esta práctica se llevó a cabo la implementación del protocolo HTTPS en un servidor Apache2 sobre Ubuntu, utilizando un certificado SSL/TLS autofirmado. A continuación se resumen los pasos realizados:
### 1. Estado de Apache y Instalación de módulos
Primero verificare el estado y funcionamiento de Apache (que instalamos en la práctica anterior) con `sudo systemctl status apache2`

![Systemctl status](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/systemctl_status.png)

Y, a continuación instalaré los módulos:
1. Módulo SSL:
   
![SSL](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/ssl_module.png)

2. Módulo headers y socache_shmcb (ya están instalados):
   
![Modules](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/modules.png)

Por último, reinicio Apache con `sudo systemctl restart apache2`.
## 2. Generación del certificado autofirmado (Opción A)
Al principio, creare una carpeta (`sudo mkdir /etc/apache2/ssl`) donde se almacenan los certificados SSL/TLS y las claves privadas que usarán Apache. Luego, generare el certificado correspondiente con `sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/apache2/ssl/apache.key \
  -out /etc/apache2/ssl/apache.crt
`

![Certificado](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/sudo_openssl.png)

Como podemos ver en la imagen, luego de ejecutar el comando, no piden datos como el país, provincia, correo... y la dirección del dominio que será **daviddominio.com**

## 3. VirtualHost (Puerto 433)
Para configurar el VirtualHost, creo un archivo de configuracion llamado daviddominio-ssl.conf con el siguiente comando `sudo nano /etc/apache2/sites-available/daviddominio-ssl.conf`. Después, le introduzco el contenido que podemos ver en la imagen:

![VirtualHost 433](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/virtualhost_443.png)

## 4. Dominio en Localhost
Como no tengo un dominio real, edito /etc/hosts de forma que cuando busque daviddominio.com me rediriga a localhost. Para ello agrege la siguiente linea: `127.0.0.1 daviddominio.com`

![Localhost](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/etchosts.png)

## 5. Prueba de acceso
Para probar el funcionamiento, he introducido `daviddominio.com` en el navegador

![Navegador Alerta](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/navegador_aviso.png)

Como se puede ver en la imagen, en el navegador se nos alerta de el sitio no es seguro ya que se trata de un cerificado autofirmado. Luego si pulsamos en "Aceptar el riesgo y continuar", se puede observar que todo funciona correctamente

![Navegador Resultado](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UT_3%20Apache/img_UD3/itworks.png)

## Conclusión, Valoración Personal y Dificultades encontradas
La práctica permitió comprender de manera integral el proceso de instalación y configuración de Apache2 en Ubuntu, así como la implementación de HTTPS mediante un certificado autofirmado. Aunque inicialmente se intentó utilizar Let’s Encrypt, se evidenció la necesidad de contar con un dominio público y registrado para poder completar la validación. Ante esta limitación, se optó por la generación de un certificado autofirmado, lo que permitió activar el cifrado en el servidor y garantizar la seguridad de las comunicaciones en un entorno local. El resultado final fue satisfactorio, ya que se logró desplegar un sitio web accesible por HTTPS y verificar su correcto funcionamiento.

La experiencia fue enriquecedora porque no solo implicó seguir instrucciones técnicas, sino también resolver problemas reales que surgen en la administración de servidores. El hecho de tener que cambiar de estrategia (de Let’s Encrypt a certificado autofirmado) me ayudó a entender mejor las diferencias entre entornos de producción y entornos de pruebas. Considero que este tipo de prácticas son fundamentales para adquirir confianza en la gestión de servicios web y en la seguridad de las comunicaciones. Además, me permitió valorar la importancia de conceptos como la resolución de nombres, la configuración de Virtual Hosts y la gestión de certificados.

En cuanto a las dificultades que he tenido:

* **Problema con el dominio:** el intento inicial con Let’s Encrypt falló porque el dominio daviddominio.com no estaba registrado ni tenía registros DNS válidos.

* **Errores de validación en Certbot:** se recibieron mensajes de error relacionados con NXDOMAIN, lo que evidenció que la autoridad certificadora no podía verificar la propiedad del dominio.

* **Advertencias del navegador:** al usar el certificado autofirmado, los navegadores mostraron alertas de seguridad, lo que puede resultar confuso si no se entiende la diferencia entre certificados confiables y autofirmados.

## Bibliografía y Anexos

[https://www.cloudflare.com/es-es/learning/ssl/what-is-https/](https://www.cloudflare.com/es-es/learning/ssl/what-is-https/)

[https://www.ssl.com/es/art%C3%ADculo/ssl-tls-certificados-autofirmados/](https://www.ssl.com/es/art%C3%ADculo/ssl-tls-certificados-autofirmados/)

[https://aws.amazon.com/es/what-is/ssl-certificate/](https://aws.amazon.com/es/what-is/ssl-certificate/)

[https://cibersafety.com/certificate-authority-ca-seguridad/](https://cibersafety.com/certificate-authority-ca-seguridad/)

