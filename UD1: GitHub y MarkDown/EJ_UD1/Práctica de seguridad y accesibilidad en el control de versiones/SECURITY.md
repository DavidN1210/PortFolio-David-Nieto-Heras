# Seguridad en el control de versiones
## Archivos excluidos con `.gitignore`

1. **Contraseñas y configuraciones privadas (`.env`, `*.env`, `config.local.*`, `*.secret.*`)**
   
   Estos archivos contienen credenciales, claves API, configuraciones sensibles o datos específicos de un entorno local y incluirlos en el           repositorio puede exponer información importante a terceros no autorizados.  
   En su lugar, se recomienda usar gestores de secretos o variables de entorno.  

2. **Logs y archivos temporales (`*.log`, `*.tmp`, `*.swp`)**  

   Son generados automáticamente durante la ejecución del software o por editores de texto y no tienen relevancia para el código fuente y solo       generan problemas en el control de versiones.  

3. **Binarios y compilados (`*.exe`, `*.dll`, `*.so`, `*.o`, `*.a`, `*.class`)**
   
   Se producen como resultado de la compilación y no deben versionarse, por lo que mantenerlos fuera del repositorio garantiza que cada              desarrollador genere su propia versión a partir del código fuente.  

4. **Directorios de build/dist (`dist/`, `build/`, `out/`)**

   Contienen artefactos generados automáticamente durante el proceso de compilación o empaquetado. Estos no deben subirse, ya que se pueden          regenerar en cualquier entorno de desarrollo o integración continua.

## Prácticas de seguridad para proteger la documentación

Para proteger la documentación y el código en nuestro repositorio, se recomienda:
* **Revisar los Pull Request:** todos los cambios que ocurren en nuestro repositorio deben ser revisados, para redicir la posibilidad de errores o fugas de información
* **Proteger las ramas:** es importante que la rama principal (main) este protegida. Para ello, debemos revisar los Pull Request antes de aceptarlos.
* **Llevar control de quien accede nuestro repositorio:** tenemos que controlar los permisos de cada usuario/colaborador que accede a nuesto repositorio y evitar compartir información sensible en los Pull Request o en los comentarios.

## Recuperación del repositorio por pérdida de datos

Es necesario garantizar la seguridad de nuestro repositorio en caso de errores graves o pédida de datos. Para ello, es recomendable:

* Hacer copias de seguridad regularmente: podemos hacer backups de repositorio mediante scripts que hagan capturas regulares del repositorio (incluyendo ramas y etiquetas) y guardarlos en un lugar seguro
* Usar plataformas confiables: como GitHub, GitLab o Bitbucket, que ofrecen un historial completo de las ramas del repositorio y los cambios que se han hecho.
* Tener documentado como clonar o restaurar la versión más reciente del repositorio.
  
    


