# **Diario Unidad 4 — Tomcat**

## **¿Qué he aprendido?**
En esta unidad he aprendido a administrar y configurar **Apache Tomcat**, profundizando tanto en su arquitectura interna como en su despliegue real de aplicaciones web. He comprendido cómo funciona un contenedor de servlets y cómo se estructura una aplicación Java dentro de un servidor de aplicaciones.

Los puntos más importantes han sido:

- **Instalación y localización de archivos clave** como `server.xml`, `web.xml`, `tomcat-users.xml` y `context.xml`.
- **Comprensión de los componentes internos** de Tomcat: Catalina, Coyote, Jasper, Manager y Host Manager.
- **Despliegue de aplicaciones web** mediante archivos WAR y estructura `WEB-INF`.
- **Integración de Tomcat con Apache mediante reverse proxy**, ocultando el puerto 8080.
- **Aplicación de medidas de seguridad**, incluyendo roles, restricciones de acceso, HTTPS y Security Manager.
- **Pruebas de rendimiento reales** usando ApacheBench y curl --parallel.
- **Ejecución de Tomcat en contenedores Docker**, comparando diferencias con la instalación nativa.

En conjunto, esta unidad me ha permitido entender Tomcat no solo como un servidor, sino como un entorno completo para ejecutar aplicaciones Java de forma profesional.

## **¿Qué no entiendo?**
Aunque he entendido la instalación, configuración y despliegue en Tomcat, aún me cuesta ver cómo se gestionan entornos de producción reales, especialmente cuando hay varias aplicaciones, certificados de CA oficiales o configuraciones avanzadas de conectores para cargas muy altas.

## **¿Qué es lo que más me ha gustado y lo que menos?**

### **Lo que más me ha gustado**
- El proceso de **desplegar aplicaciones WAR** y ver cómo Tomcat las detecta, descomprime y ejecuta automáticamente.
- Las **pruebas de rendimiento**, porque permiten ver diferencias reales entre configuraciones y entender cómo responde el servidor bajo carga.
- La integración con Apache mediante **reverse proxy**, ya que demuestra cómo se combinan tecnologías en un entorno profesional.
- El uso de **Docker**, que facilita muchísimo la portabilidad y el despliegue.

### **Lo que menos me ha gustado**
- La configuración de seguridad, especialmente el **Security Manager**, que es muy estricta y requiere precisión.
- Tener que editar manualmente tantos archivos XML, ya que un error pequeño puede romper el despliegue.
- La gestión de certificados SSL en Tomcat, que es más compleja que en Apache.

## **¿Qué más me gustaría saber relacionado con la Unidad?**
Me gustaría aprender más sobre optimización avanzada de Tomcat, uso de certificados reales, automatización del despliegue con Docker/Kubernetes y sobre alginas buenas prácticas de monitorización y seguridad en entornos profesionales.




