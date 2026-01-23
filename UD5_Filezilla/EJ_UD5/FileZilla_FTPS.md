# Actividad 8: Configuración de FTP seguro (FTPS)
## 1. Generación del certificado
Para habilitar FTPS es necesario disponer de un certificado TLS. En este caso se ha generado un certificado autofirmado, adecuado para entornos locales y de prácticas.

Este certificado permite cifrar la comunicación entre el cliente y el servidor, evitando que credenciales y archivos viajen en texto plano.

![Creación certificado](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/crear_certificado_autofirmado.png)

![Creación certificado](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/datos_certificado.png)

## 2. Configuración de FileZilla Server para FTPS explícito.
En la sección Server listeners, se configuró el servidor para aceptar únicamente conexiones seguras mediante FTPS explícito. Esto obliga al cliente a iniciar la sesión con el comando AUTH TLS, activando el cifrado antes de enviar usuario y contraseña.

Ambos listeners (IPv4 e IPv6) se configuraron con:

*Puerto: 21
*Protocolo: Require explicit FTP over TLS

![Creación certificado](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/protocolo_localhost.png)

## 3. Conexión segura para todos los usuarios
Aunque la pestaña de usuarios muestra que las políticas están determinadas por el sistema, la configuración global del servidor ya obliga a todos los usuarios a conectarse mediante FTPS.

Para verificarlo se realizaron dos pruebas:

* Conexión sin cifrado: rechazada por el servidor
* Conexión con FTPS explícito: aceptada correctamente

Esto demuestra que ningún usuario puede usar FTP sin cifrar.

![Creación certificado](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/ftps_conexion.png)

## 4. Conexión FTPS y certificado
Al conectar desde FileZilla Client, el servidor presenta su certificado TLS. El cliente muestra los detalles del certificado y confirma que la sesión se establece usando TLS 1.3 con cifrado AES-256-GCM, garantizando la confidencialidad e integridad de los datos.

![Creación certificado](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/certificado.png)
