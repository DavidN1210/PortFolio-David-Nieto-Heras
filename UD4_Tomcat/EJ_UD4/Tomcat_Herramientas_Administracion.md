# Tomcat: Herramientas de administración — Manager y Host Manager
## Ficha Descriptiva Manager

![Manager](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/manager_pagina.png)

### Acceso
* **URL:** http://localhost:8080/manager/html
* Requiere usuario con rol ``manager-gui`` definido en tomcat-users.xml.
### Funciones principales

| Función | Descripción |
|----------------|-------------|
| **Despliegue** | Permite subir y desplegar aplicaciones `.war` o desde rutas locales. |
| **Recargar aplicación** | Reinicia la aplicación sin reiniciar Tomcat. |
| **Parar aplicación** | Detiene la ejecución de una aplicación sin eliminarla. |
| **Replegar** | Borra completamente la aplicación del servidor. | 
| **Expirar sesiones inactivas** | Finaliza sesiones que llevan más de X minutos sin actividad. | 
| **Ver estado del servidor** | Muestra memoria, sesiones activas y datos de la JVM. | 
| **Listar aplicaciones** | Muestra todas las aplicaciones desplegadas y sus controles. |
| **Configurar** | Volver a leer los archivos de configuración de TLS |
| **Diagnosticar (fallos de memoria)** | Herramienta para detectar fugas de memoria (no usar en producción). |
| **Diagnosticar (Cifrados TLS)** | Enumerar los hosts virtuales TLS configurados y los cifrados para cada uno. |
| **Diagnosticar (Certificados TLS)** | Lista las cadenas de certificados configuradas para cada host TLS. |
| **Diagnosticar (Certificados confiables)** | Muestra los certificados raíz confiables configurados en el servidor. |

### Utilidad 
* Permite comprobar el funcionamiento de despliegues sin usar comandos ni editar `webapps`
* Ideal para entornos de desarrollo y pruebas locales.
  
## Ficha Descriptiva Host - Manager

![Host-Manager](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/host_manager_pagina.png)

### Acceso
* **URL:** http://localhost:8080/host-manager/html
* Requiere usuario con rol ``admin-gui`` definido en tomcat-users.xml.
### Funciones principales

| Función | Descripción |
|----------------|-------------|
| **Crear host virtual** | Permite definir nuevos hosts |
| **Eliminar host virtual** | Borra un host virtual existente. |
| **Iniciar / Detener host** | Controla el estado de los hosts virtuales definidos. |
| **Persistir configuración** | Guarda los cambios en los archivos XML de Tomcat.|

### Utilidad académica
* Permite simular entornos `multi-tenant` (varios sitios en un solo servidor).
* Útil para aprender sobre virtual hosting y segmentación de servicios.
