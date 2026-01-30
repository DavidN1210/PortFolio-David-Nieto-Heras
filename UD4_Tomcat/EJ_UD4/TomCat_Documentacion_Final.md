# TomCat - Documentación Final

## Índice
1. Introducción  
2. Arquitectura básica de Tomcat  
3. Configuración del servidor  
4. Despliegue de aplicaciones  
5. Integración con servidor web  
6. Seguridad aplicada  
7. Pruebas de rendimiento  
8. Recomendaciones de administración  
9. Despliegue en contenedores  

## 1. Introducción
Apache Tomcat es un servidor de aplicaciones ligero diseñado para ejecutar aplicaciones web basadas en servlets y JSP. Su uso es muy común en entornos educativos y profesionales debido a su sencillez, estabilidad y facilidad de administración.  

A lo largo de estas prácticas se han explorado sus componentes internos, la estructura de configuración, el despliegue de aplicaciones, la integración con servidores web, la aplicación de medidas de seguridad, pruebas de rendimiento y su ejecución en contenedores Docker.

El objetivo de esta documentación final es ofrecer una visión resumida y ordenada de todo el trabajo realizado, destacando los aspectos esenciales necesarios para comprender, configurar y administrar un entorno Tomcat de forma correcta.

## 2. Aquitectura básica de Tomcat

### Componentes principales
- **Catalina**: Contenedor de servlets; ejecuta aplicaciones web.
- **Coyote**: Conector HTTP; recibe peticiones en el puerto 8080.
- **Jasper**: Compila JSP a servlets.
- **Manager**: Administración y despliegue de aplicaciones.
- **Host Manager**: Gestión de hosts virtuales.

### Estructura básica
- `bin/` → arranque y apagado.  
- `conf/` → configuración del servidor.  
- `webapps/` → aplicaciones desplegadas.  
- `lib/` → librerías.  
- `logs/` → registros.

### Funcionamiento interno
1. Coyote recibe la petición.  
2. Catalina la procesa.  
3. Jasper compila JSP si hace falta.  
4. Tomcat despliega WAR automáticamente.  
5. Administración vía Manager/Host Manager.

## 3. Configuración del servidor
### Instalación básica
- Actualización del sistema y paquete: `sudo apt update`.
- Instalación: `sudo apt install tomcat10 tomcat10-admin -y`.
- Comprobación del servicio: `systemctl status tomcat10`.

### Archivos clave de configuración
Ubicados en `/etc/tomcat10/`:

- **server.xml**  
  Configura conectores (puertos, HTTPS), hosts y parámetros del servidor.

- **web.xml**  
  Define servlets y filtros por defecto, tipos MIME, páginas de error y archivos de bienvenida.

- **tomcat-users.xml**  
  Gestiona usuarios y roles para acceder a Manager y Host Manager.

- **context.xml**  
  Configura recursos JNDI, parámetros de entorno y ajustes de sesión por aplicación.

## 4. Despligue de aplicaciones web
### Procedimiento
- Se crea la estructura básica: `HelloApp/WEB-INF/`.
- Se añade un `index.jsp` y un `web.xml` mínimo.
- Se empaqueta en un WAR usando `jar` (requiere JDK).
- El WAR se copia a `/var/lib/tomcat10/webapps/`.
- Tomcat lo despliega automáticamente: descomprime, crea el contexto y compila JSP.
- Acceso final: `http://localhost:8080/HelloApp`.

## 5. Integración con servidor web (Reverse Proxy)
### Configuración básica
- Se habilitan módulos de Apache: `proxy` y `proxy_http`.
- En `000-default.conf` se añaden:
  - `ProxyPass /HelloApp http://localhost:8080/HelloApp`
  - `ProxyPassReverse /HelloApp http://localhost:8080/HelloApp`
- Apache reenvía las peticiones a Tomcat sin exponer el puerto 8080.
- Pruebas correctas tanto en navegador como con `curl`.

## 6. Seguridad aplicada
### Roles y usuarios
- Configuración en `tomcat-users.xml`.
- Se crean usuarios y roles (`manager-gui`, `admin-gui`, etc.).
- Reinicio del servicio para aplicar cambios.

### Restricción de acceso al Manager
- En `manager.xml` se añade un `RemoteAddrValve` para permitir solo `127.0.0.1`.
- El Manager queda accesible únicamente desde localhost.

### Activación de HTTPS
- Se genera un keystore con `keytool`.
- Se habilita un conector SSL en `server.xml` usando el puerto **8443**.
- Tomcat cifra las conexiones mediante TLS.

### Security Manager
- Se define una política en `catalina.policy` con permisos específicos.
- Se activa añadiendo opciones en `/etc/default/tomcat10`.

### Comprobaciones
- Acceso correcto al Manager con usuario/contraseña configurados.
- Acceso bloqueado desde fuera de localhost.
- HTTPS funcionando en `https://localhost:8443`.

## 7. Pruebas de rendimiento
### Pruebas con ApacheBench
- Se ejecuta: `ab -n 1000 -c 50 http://localhost:8080/HelloApp/`.
- Se comparan dos configuraciones del conector: una por defecto y otra optimizada.

**Conclusiones:**
- El conector optimizado mejora ligeramente los *requests per second*.
- Reduce la latencia.
- No aparecen errores en ninguna prueba.
- Mayor estabilidad bajo concurrencia elevada.

### Pruebas con curl --parallel
- Se generan 1000 peticiones simultáneas usando:
  - `curl --parallel --parallel-max 50 --config urls.txt`.

**Conclusiones:**
- El conector optimizado reduce el tiempo total de ejecución.
- Menor uso de CPU en modo concurrente.
- Todas las respuestas fueron correctas y consistentes.
- Ambas configuraciones son estables, pero la optimizada gestiona mejor la carga real.

## 8. Recomendaciones de administración
### Manager
- Acceso: `http://localhost:8080/manager/html` (requiere rol `manager-gui`).
- Funciones principales:
  - Desplegar y eliminar aplicaciones.
  - Parar/arrancar apps sin reiniciar Tomcat.
  - Recargar configuraciones.
  - Ver estado del servidor (memoria, sesiones, JVM).
  - Diagnósticos de TLS y fugas de memoria.

### Host Manager
- Acceso: `http://localhost:8080/host-manager/html` (requiere rol `admin-gui`).
- Funciones principales:
  - Crear y eliminar hosts virtuales.
  - Iniciar/detener hosts.
  - Guardar cambios en configuración.

### Utilidad
- Manager → ideal para gestionar despliegues y supervisar el servidor.
- Host Manager → útil para practicar virtual hosting y entornos multi‑sitio.

## 9. Despliegue en contenedores
### Ejecución de Tomcat en Docker
- Se descarga la imagen oficial: `docker pull tomcat:latest`.
- Se ejecuta un contenedor mapeando el puerto 9090:
  - `docker run -d --name tomcat-miweb -p 9090:8080 tomcat:latest`.

### Despliegue de una aplicación en Docker
- Se crea la estructura `MiWeb/WEB-INF/`.
- Se añade un `index.jsp` y un `web.xml` básico.
- Se empaqueta en un WAR con `jar -cvf MiWeb.war *`.
- Se copia al contenedor:
  - `docker cp MiWeb.war tomcat-miweb:/usr/local/tomcat/webapps/`.
- Acceso final: `http://localhost:9090/MiWeb`.

### Diferencias Tomcat nativo vs Tomcat en Docker
- **Instalación:** nativo requiere paquetes; Docker usa imágenes.
- **Configuración:** nativo en `/etc/tomcat`; Docker dentro del contenedor o volúmenes.
- **Despliegue:** nativo → copiar WAR; Docker → `docker cp` o imágenes personalizadas.
- **Actualización:** nativo manual; Docker recreando contenedores.
- **Portabilidad:** Docker es idéntico en cualquier máquina.
- **Aislamiento:** Docker aísla procesos; nativo comparte sistema.
- **Escalabilidad:** Docker facilita escalar (Compose/Kubernetes).
- **Mantenimiento:** Docker es más simple y reproducible.






