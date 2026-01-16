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








