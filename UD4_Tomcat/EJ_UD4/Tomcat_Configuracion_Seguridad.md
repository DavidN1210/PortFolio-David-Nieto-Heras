# Tomcat: Configuración de seguridad en Tomcat
## 1. Definición de roles y usuarios
Dentro de `/etc/tomcat10/tomcat-users.xml` se añaden los roles necesarios para acceder al Manager y se crearon usuarios con permisos adecuados.

**Comandos utilizados:**
```bash
sudo nano /etc/tomcat10/tomcat-users.xml
sudo systemctl restart tomcat10 
```
![tomcat-users.xml](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/tomcat.xml.png)

## 2. Restricción de acceso al Manager
En mi caso, he restringido el acceso al Manager en todos los sitios que no son localhost. Para ello, he añadido las siguientes línea en manager.xml (donde se encuantra la configuración del manager): `<Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="127\.0\.0\.1"/>`.

**Comandos utilizados:**
```bash
sudo nano /etc/tomcat10/Catalina/localhost/manager.xml
sudo systemctl restart tomcat10 
```
![Restriccion Manager](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/manager.png)

## 3. Configuración de HTTPS en Tomcat 10
Este punto consiste en activar HTTPS en Tomcat 10, lo que significa que el servidor podrá cifrar las conexiones usando TLS.
### 3.1 Creación del KeyStore
Antes de nada, Tomcat necesita un archivo donde guardar la clave privada y el certificado. Ese archivo es el keystore. 
Para crear el keystore nos pedirán algunos datos como el nombre y apellido, provincia, localidad, nombre de empresa o organización... etc.

**Comandos utilizados:**
```bash
sudo keytool -genkeypair -alias tomcatssl -keyalg RSA \
-keystore /etc/tomcat10/keystore.jks -keysize 2048 -validity 365
```

![KeyStore](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/creacion_keystore.png)

### 3.2 Activación del conector SSL
Luego de crear el keystore, tomcat necesita saber dónde está el keystore y qué puerto usar. Para ello, añado un conector con puerto 8443 en `server.xml`.

**Comandos utilizados:**
```bash
sudo nano /etc/tomcat10/server.xml
sudo systemctl restart tomcat10
```

![Conector SSL](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/conectorssl.png)

## 4. Security Manager
El Security Manager es un sistema de permisos que limita lo que Tomcat y las aplicaciones pueden hacer dentro de la JVM.
### 4.1 Crear el archivo de políticas
He creado y editado el archivo de políticas `catalina.policy` y le he añadido varios permisos de lectura y escritura.

**Comandos utilizados:**
```bash
sudo nano /etc/tomcat10/catalina.policy
sudo systemctl restart tomcat10
```

![Catalina Policy](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/catalinaPolicy.png)

### 4.2 Activación del Security Manager
Si quieres activarlo es necesario editar en `/etc/default/tomcat10` y añadir/modificar la siguiente línea: `JAVA_OPTS="-Djava.awt.headless=true -Djava.security.manager -Djava.security.policy=/etc/tomcat10/catalina.policy"`

**Comandos utilizados:**
```bash
sudo nano /etc/default/tomcat10
sudo systemctl restart tomcat10
```
![Activacion SM](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/security_manager.png)

## 5. Comprobaciones
### 5.1 Comprobación de funcionamiento tras inicar sesión
Para comprobar que todo funciona correctamente, escribimos en el navegador la siguiente ruta: `http://localhost:8080/manager/html`. Luego, la página nos pedirá un nombre de usuario y su contraseña, que son aquellos que pusimos en tomcat-users.xml para iniciar sesión.

![Inicio sesión](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/inicio_sesion.png)

Una vez inicie sesión, podemos ver que todo ha funcionado como se esperaba

![Funcionamiento Inicio Sesión](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/com_final.png)

### 5.2 Comprobación de funcionamiento de la restricción de acceso al Manager
Ya que el Manager solo puede acceder desde localhost (**http://localhost:8080/manager/html**, **http://127.0.0.1:8080/manager/html**), he probado con esas url fuera de la máquina virtual y como resultado se me niega el acceso:

![Funcionamiento Acceso al Manager](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/conexion_rechazada.png)

### 5.3 Comprobación HTTPS con el puerto 8443

![Funcionamiento HTTPS](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/https_8443.png)

En el caso de que ponga http, me aparece el siguiente mensaje: **Bad Request
This combination of host and port requires TLS.**

![Funcionamiento HTTPS](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/tls.png)

