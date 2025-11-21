# Practica UT3 Apache: HTTPS
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
Solo se necesita el módulo mod_ssl
