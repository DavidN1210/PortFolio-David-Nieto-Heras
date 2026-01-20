# Tomcat: Herramientas de administración — Manager y Host Manager
## Ficha Descriptiva Manager
### Acceso
* **URL:** http://localhost:8080/manager/html
* Requiere usuario con rol ``manager-gui`` definido en tomcat-users.xml.
### Funciones principales

| Función | Descripción |
|----------------|-------------|
| **Despliegue (Deploy)** | Permite subir y desplegar aplicaciones `.war` o desde rutas locales. |
| **Recarga (Reload)** | Recarga una aplicación sin reiniciar el servidor completo. |
| **Parada / Inicio (Stop / Start)** | Detiene o inicia aplicaciones individuales. |
| **Eliminación (Undeploy)** | Borra una aplicación del servidor. |
| **Listado de aplicaciones** | Muestra todas las apps desplegadas, su estado y su ruta. |

### Utilidad 
* Permite comprobar el funcionamiento de despliegues sin usar comandos ni editar `webapps`
* Ideal para entornos de desarrollo y pruebas locales.
## Ficha Descriptiva Host - Manager
### Acceso
* **URL:** http://localhost:8080/host-manager/html
* Requiere usuario con rol ``admin-gui`` definido en tomcat-users.xml.
### Funciones principales

| Función | Descripción |
|----------------|-------------|
| **Crear host virtual** | Permite definir nuevos hosts virtuales con su propio `appBase` |
| **Eliminar host virtual** | Borra un host virtual existente. |
| **Iniciar / Detener host** | Controla el estado de los hosts virtuales definidos. |
| **Persistir configuración** | Guarda los cambios en los archivos XML de Tomcat.|
| **Información del servidor** | Muestra detalles del entorno Tomcat y del sistema operativo. |

### Utilidad académica
* Permite simular entornos `multi-tenant` (varios sitios en un solo servidor).
* Útil para aprender sobre virtual hosting y segmentación de servicios.
