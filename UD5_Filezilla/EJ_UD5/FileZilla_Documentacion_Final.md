# Documentación Final - Filezilla
# Actividad 1: Introducción y arquitectura de FileZilla Server

## Canales

- **Canal de CONTROL** → puerto 21 (comandos y respuestas)
- **Canal de DATOS** → transferencia de archivos y listados

---

## MODO ACTIVO

### Canal de CONTROL (puerto 21)

Cliente ────────────────▶ Servidor  
`PORT h1,h2,h3,h4,p1,p2`  
*(PORT es un comando con el que el cliente indica su IP y el puerto donde escuchará los datos)*

### Canal de DATOS

Servidor ────────────────▶ Cliente  
*(el servidor inicia la conexión desde su puerto 20 al puerto indicado por el cliente)*

### Flujo simplificado

Cliente ─▶ Servidor : comando `PORT`  
Servidor ─▶ Cliente : abre conexión de datos  
Cliente ⇄ Servidor : transferencia de datos (LIST, RETR, STOR)  
Servidor ─▶ Cliente : `226 Transferencia completa`

### Características

* El **servidor inicia** la conexión de datos  
* Puede dar problemas con **firewalls y NAT**

---

## MODO PASIVO

### Canal de CONTROL (puerto 21)

Cliente ────────────────▶ Servidor  
`PASV`
*(PASV es un comando que utiliza el cliente para solicitar una IP y puerto pasivo al servidor para lograr la conexión y así tranferir datos, ya que no es posible con el modo activo)*

Servidor ────────────────▶ Cliente  
`227 Modo Pasivo (IP, puerto)`
*(el servidor indica la IP y puerto pasivo)*

### Canal de DATOS

Cliente ────────────────▶ Servidor  
*(el cliente se conecta al puerto pasivo indicado por el servidor)*

### Flujo simplificado

Cliente ─▶ Servidor : comando `PASV`  
Servidor ─▶ Cliente : indica IP y puerto pasivo  
Cliente ─▶ Servidor : abre conexión de datos  
Cliente ⇄ Servidor : transferencia de datos (LIST, RETR, STOR)  
Servidor ─▶ Cliente : `226 Transferencia completa`

### Características

* El **cliente inicia** la conexión de datos  
* Más compatible con **firewalls y NAT**

# Actividad 2: Instalación y configuración inicial del servidor

## 1. Actualización del sistema y instalación de dependencias

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install wget gdebi-core -y
```

## 2. Descarga y instalación de Filezilla Server

1. Descargo en la página oficial el paqueta `.deb` para Linux
   
![Descarga del paquete .deb](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_pagina_oficial.png)

2. Una vez descargado, instalo FileZilla Server con el comando `sudo dpkg -i filezilla-server.deb`
   
![Instalación](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_comando_instalacion.png)

3. Se nos pide introducir una contraseña

![Contrasena](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/fillezilla_password_config.png)

```bash
sudo dpkg -i filezilla-server.deb (nombre del paquete)
sudo apt -f install -y (en caso de errores de dependencias)
```

4. Una vez instalado, inicio el servicio con `sudo systemctl start filezilla-server` y compruebo que esta activo `sudo systemctl status filezilla-server`

![Estado](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_enabled.png)

```bash
sudo systemctl start filezilla-server
sudo systemctl status filezilla-server
```

## 3. Consola de administración
Para accede a la consola, buscaremos en el menú de aplicaciones `FileZilla Server Administration` y la abriremos y en la ventana de conexión nos podemos conectar a un servidor, introduciendo el host, puerto y la contraseña. En mi caso me he conectado a localhost.

![Conexión Servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_consola_admin.png)

## 4. Configurar puerto de escucha FTP y la dirección IP
Para configurar el puerto de escucha FTP y la dirección IP, tenemos que acceder a la sección de `Server listeners` (Server -> Configure -> Server listeners)

![Conexión Servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_puerto_config.png)

## 5 Configurar inicio automático
Utilizaremos dos comandos: `sudo systemctl enable filezilla-server`, para habilitar el inicio automático, y 
`systemctl is-enabled filezilla-server`, para verificar que esta habilitado.

![Conexión Servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/inicio_auto.png)

```bash
sudo systemctl enable filezilla-server
systemctl is-enabled filezilla-server
```

# Actividad 3: Creación de usuarios y grupos
## 1. Creación del grupo
Para crear un grupo tenemos que dirigirnos a la configuración de la interfaz de Fillezilla Server (Server → Configure → Rights management → Groups). Luego he seguido los siguientes pasos: 
1. Hago clic en Add y creo el grupo llamado **grupo_permisos_limitados**
2. Defino el directorio raíz `/srv/ftp/clientes`
3. Establezco los permisos de solo lectura

![Grupo Creación 1](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/creacion_grupo_parte1.png)

4. Establezco los límites de conexión:
   * Máximo de conexiones simultáneas: 2
   * Límite de velocidad de todas las sesiones: 100 KB/s
   * Límites de sistema de archivos por sesión: Archivos: 100, Directorios: 10

![Grupo Creación 2](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/creacion_grupo_parte1.png)

5. Creo el directorio /srv/ftp/grupoPL

![Grupo Creación 2](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/estructura_directorios.png)

```bash
sudo mkdir -p /srv/ftp/anon
sudo chown -R ftp:ftp /srv/ftp/anon
```

## 2. Creación de los usuarios
Para crear los usuarios hago clik Add, les asigno una contraseña, y les declaro como miembros del grupo creado anteriormente. Los permisos y configuraciones del grupo serán heredados por estos dos usuarios.
### Usuario 1

![Usuarios Creación 2](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/usuario1.png)

### Usuario 2

![Usuarios Creación 2](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/usuario2.png)

## 3. Definiciones

**Directorio raíz:** Es la carpeta principal a la que un usuario o grupo accede cuando inicia sesión en el servidor FTP. Desde ese directorio, el usuario ve todos los archivos y subcarpetas permitidos según sus permisos.

**Límites de conexión:** Son restricciones que controlan cuántas conexiones puede abrir un usuario o grupo y cuánta velocidad de transferencia puede usar. Incluyen:
* Número máximo de sesiones simultáneas
* Velocidad máxima de descarga
* Velocidad máxima de subida
  
**Permisos:** Existen 3 tipos de permisos:
  * **De lectura:** Permite ver y descargar archivos o listar el contenido de carpetas.
  * **De escritura:** Permite subir archivos nuevos o modificar archivos existentes dentro del directorio.
  * **De borrado:** Permite eliminar archivos o carpetas dentro del directorio asignado.

## 4. Diferencias entre permisos de usuario y de grupo

Los permisos de grupo son reglas generales que se aplican automáticamente a todos los usuarios que pertenecen a ese grupo, permitiendo gestionar de forma centralizada qué pueden hacer dentro del servidor (por ejemplo, si pueden leer, escribir o borrar archivos). 

En cambio, los permisos de usuario son configuraciones individuales que se aplican a un usuario concreto y que pueden modificar o sobrescribir lo que el grupo establece. Esto significa que, si un usuario tiene permisos propios definidos, estos tienen prioridad sobre los del grupo; pero si no se le asigna nada específico, heredará exactamente los permisos del grupo al que pertenece.

# Actividad 4: Configuración de acceso anónimo

## 1. Activar el acceso anónimo
### Creación del usuario anónimo
Se creó un usuario llamado anonymous en FileZilla Server, configurado sin contraseña para permitir el acceso anónimo. 

Este usuario quedó habilitado para iniciar sesión sin autenticación adicional y solo se establecieron permisos exclusivamente de lectura, desactivando las opciones de escritura y borrado.

![Usuario Anónimo](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/usuario_anonimo.png)

## 2. Limitación del directorio accesible
Al usuario anónimo se le asignó un mountpoint específico, de forma que solo pudiera acceder al directorio autorizado del servidor.
El directorio físico configurado fue el destinado al acceso público, evitando que el usuario anónimo pudiera navegar por otras rutas del sistema.

### Creación del directorio

![Directorio](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/creacion_directorio.png)

``` bash
sudo mkdir -p /srv/ftp/anon
sudo chown -R ftp:ftp srv/ftp/anon
```

## 3. Conexión desde un cliente FTP y verificación
### Instalación de FileZilla Client
Para realizar a conexión he tenido que intalarme en mi máquina virtual FileZilla Client (el cliente FTP)
con el comando `sudo apt install filezilla -y`.

![Filezilla Client](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/filezilla_client.png)

## Cambiar la dirección IP del servidor FTP
Antes de realizar la conexión, tengo que configurar la dirección ip del servidor. Por ello, en la configuración de Filezilla Server he puesto como direccion ip 127.0.0.1 (localhost)

![Dirección IP](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/direccion_ip_servidor.png)

## Resultado de la conexión 
He realizado la conexión desde Filezilla Client, introduciendo los siguientes datos:

* **Servidor:** 127.0.0.1
* **Nombre de usuario:** anónimo
* **Contraseña:** vaciá
* **Puerto:** 21

Y el resultado ha sido el siguiente por el lado del cliente:

![Cliente FTP](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/resultado_client.png)

Y por el lado del servidor:

![Servidor FTP](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/resultado_servidor.png)

Como se puede ver en la última imagen, la conexión se realizo correctamente entre cliente-servidor

# Actividad 5: Pruebas en modo activo y pasivo
# 1. Configuración del rango de puertos pasivos

En FileZilla Server, dentro de la configuracion (Protocol Settings → FTP and FTP over TLS → Passive Mode), marco la opción de **"Use custom port range"* y eligo un rango de puertos (por ejemplo 50000 -  50100).
Esto es necesario porque cuando la conexión se realiza en modo pasivo, el cliente necesita que el servidor abra puertos adicionales para la conexión de datos. Definir un rango fijo permite:

* Controlar qué puertos se usan.
* Abrir solo esos puertos en el firewall.
* Evitar problemas de conexión en redes protegidas.

Sin este rango, el modo pasivo puede fallar porque el firewall no sabe qué puertos permitir.

![Puertos pasivos](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/rango_de_puertos.png)

## 2. Conexiones
### En modo activo

Para relizar la conexión en modo activo, en la configuración de Filezilla Client (Editar → Configuración → FTP → Modo de tranferencia → Activo ), tenemos que cambiar el modo de trasferencia a modo activo.
En modo activo, la conexión puede fallar si el cliente está detrás de un firewall o router, porque las conexiones entrantes suelen bloquearse. Si funciona, significa que la red local no tiene restricciones (mi caso).

![Modo de transferencia activo](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/cliente_activo.png)

Por el lado del cliente: 

![Conexión modo activo cliente](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/prueba_activo_cliente.png)

Por el lado del servidor: 

![Conexión modo activo servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/prueba_activo_servidor.png)

### En modo pasivo

Al igual que en el modo activo, en la configuración de FileZilla Client, tenemos que cambiar el modo de transferencia a modo pasivo. Este modo es el más compatible con firewalls, porque no requiere conexiones entrantes hacia el cliente.

![Modo de transferencia pasivo](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/cliente_pasivo.png)

Por el lado del cliente: 

![Conexión modo pasivo cliente](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/prueba_pasivo_cliente.png)

Por el lado del servidor: 

![Conexión modo pasivo servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/prueba_pasivo_servidor.png)

## 3. Funcionamiento en redes con firewall

En conclusión, el modo pasivo funciona mejor en redes con firewall porque:

* El cliente no necesita aceptar conexiones entrantes.
* Solo realiza conexiones salientes, que normalmente están permitidas.
* El servidor usa un rango de puertos controlado y fácil de abrir.

El modo activo suele fallar porque el servidor intenta conectarse al cliente, y los firewalls bloquean ese tráfico.

## 4. Tabla comparativa

| Característica                               | Modo Activo                         | Modo Pasivo                          |
|----------------------------------------------|--------------------------------------|---------------------------------------|
| Quién inicia la conexión de datos            | Servidor → Cliente                   | Cliente → Servidor                    |
| Necesita puertos abiertos en el cliente      | Sí                                   | No                                    |
| Necesita puertos abiertos en el servidor     | No (solo puerto 21)                  | Sí (rango de puertos pasivos)         |
| Compatibilidad con firewalls                 | Baja                                 | Alta                                  |
| Riesgo de bloqueo                            | Alto                                 | Bajo                                  |
| Funcionamiento detrás de NAT                 | Problemático                         | Muy bueno                             |
| Uso recomendado                              | Redes sin firewall estricto          | Redes con firewall o routers NAT      |

# Actividad 7: Pruebas con clientes gráficos
## Usuario anónimo 
Voy a realizar la transferencia con el usuario anónimo de prácticas anteriores.

![Usuario Anónimo](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/anon_user.png)

## Transferencia bidireccional
## Transferencia exitosa del lado del cliente (Subida)
Como se puede ver en la imagen el fichero txt ahora se encuentra en el directorio destinado al usuario anónimo y que ha sido una trasferencia satisfactoria

![Transferencia Cliente](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/trasferencia_exitosa_client.png)

## Transferencia exitosa del lado del servidor (Subida)
También podemos confirmar la tranferencia en FileZilla Server 

![Transferencia Servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/trasferencia_exitosa_server.png)

## Transferencia exitosa del lado del cliente (Descarga)
He borrado el fichero txt en la carpeta `home/usuario` y se lo he pasado otra vez desde el directorio del usuario anónimo. Como podemos ver en la imagen, todo ha funcionado correctamente.

![Transferencia Cliente](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/descarga_exitosa_client.png)

## Transferencia exitosa del lado del servidor (Descarga)
También podemos confirmar la tranferencia en FileZilla Server 

![Transferencia Servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/descarga_exitosa_server.png)

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

# Actividad 9: Uso del navegador como cliente FTP
## Ventajas del navegador como cliente FTP

- **No requiere instalación adicional**: se puede acceder al servidor FTP desde un navegador ya instalado.
- **Interfaz sencilla y familiar**: la navegación funciona igual que en una página web.
- **Acceso rápido para consultas puntuales**: útil para visualizar contenido o descargar archivos.
- **Compatibilidad inmediata**: funciona en cualquier sistema operativo si el navegador soporta FTP.

## Desventajas del navegador como cliente FTP

- **Funciones muy limitadas**: normalmente solo permite navegar y descargar archivos.
- **Soporte reducido o eliminado**: navegadores como Chrome y Edge ya no soportan FTP.
- **Sin soporte para FTPS/SFTP**: no permite conexiones seguras.
- **Gestión deficiente de errores**: no ofrece información detallada ni reconexiones automáticas.
- **Sin automatización ni funciones avanzadas**: no permite colas de transferencia, sincronización ni gestión avanzada como un cliente dedicado.

# Conclusión
El navegador puede utilizarse como cliente FTP únicamente para tareas básicas como consultar directorios o descargar archivos. Para operaciones avanzadas subida de archivos, gestión de permisos, conexiones seguras o automatización es necesario usar un cliente FTP dedicado.

# Actividad 11: Disponibilidad y buenas prácticas

# 1. Límites de conexión
- **Establecer un número máximo de conexiones simultáneas** para evitar saturación del servicio.
- **Limitar conexiones por IP** para prevenir abusos o ataques de fuerza bruta.
- **Configurar límites de ancho de banda** por usuario o grupo para asegurar un reparto equilibrado de recursos.
- **Definir tiempos de inactividad (timeouts)** para cerrar sesiones que permanezcan abiertas sin actividad.
- **Evitar el uso de usuarios anónimos** o, si es imprescindible, restringirlos al mínimo.

# 2. Logs y auditoría
- **Activar el registro detallado (logs)** de accesos, transferencias y errores.
- **Registrar intentos fallidos de autenticación** para detectar ataques o accesos sospechosos.
- **Almacenar logs en un servidor externo o sistema centralizado** para evitar su manipulación.
- **Configurar rotación de logs** para evitar que ocupen demasiado espacio en disco.
- **Revisar periódicamente los registros** como parte de las tareas de mantenimiento.

# 3. Copias de seguridad
- **Realizar copias de seguridad periódicas** de los datos almacenados en el servidor FTP.
- **Incluir en las copias la configuración del servidor**, usuarios, permisos y certificados.
- **Aplicar la regla 3-2-1**:  
  - 3 copias de los datos  
  - 2 soportes distintos  
  - 1 copia fuera del servidor o en la nube
- **Probar la restauración de las copias** para garantizar que son funcionales.
- **Automatizar las copias** para evitar errores humanos.
  
# 4. Firewall y NAT
- **Permitir únicamente los puertos necesarios** para FTP (21 para control y rango pasivo configurado).
- **Configurar correctamente el modo pasivo**, indicando el rango de puertos y abriéndolos en el firewall.
- **Restringir el acceso por IP o rangos** cuando sea posible.
- **Activar protección contra ataques comunes**, como:
  - Fuerza bruta  
  - Escaneo de puertos  
  - Conexiones repetidas
- **Usar FTPS o SFTP** para cifrar las comunicaciones y evitar robo de credenciales.
- **Asegurar la correcta traducción de puertos (NAT)** si el servidor está detrás de un router o firewall perimetral.

# Conclusión
La disponibilidad de un servidor FTP en producción depende de una combinación de límites adecuados, auditoría constante, copias de seguridad fiables y una configuración segura del firewall y la red. Aplicar estas buenas prácticas garantiza un servicio estable, seguro y preparado para entornos reales.
