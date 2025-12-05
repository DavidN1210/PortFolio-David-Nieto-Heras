# Tomcat: Despliegue simple de una aplicación web

## Proceso de despliegue en Tomcat
Para crear un archivo WAR he seguido los siguientes pasos:
1. Creo una carpeta personal (`mkdir -p HelloApp/WEB-INF`), llamada HelloApp, que actuará como directorio raíz de la aplicación web y dentro de él una carpeta WEB-INF donde se guardan configuraciones y recursos protegidos.
2. Dentro de la carpeta creada, creo un archivo JSP (`index.jsp`) que contiene el codigo que se va a mostrar al final en el navegador

![Archivo JSP](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/archivoJSP.png)

3. Creo descriptor de despliegue

![Descriptor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/descriptor_despliegue.png)

4. Empaqueto ese archivo JSP como WAR, sin embargo, no es posible porque es necesario instalarse el JDK

![JDK y Archivo WAR](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/paquete_jar_y_jdk.png)

5. Luego de instalar el JDK, puedo empaquetar el archivo JSP

![Archivo WAR](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/jar_helloapp.png)
   
6. Una vez empaquetado, puedo desplegarlo en Tomcat con el comando `sudo cp HelloApp.war /var/lib/tomcat10/webapps/`, en el que copio el WAR en la carpeta webapps. Tomcat despliegará automáticamente cualquier WAR que se encuentre en esa carpeta.

![Despligue en Tomcat](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/desplegar_war.png)

7. Finalmente, puedo acceder a la aplicación a través del navegador con la siguiente ruta en localhost: `http://localhost:8080/HelloApp`

![Navegador Funcionamiento](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/hello_world.png)



