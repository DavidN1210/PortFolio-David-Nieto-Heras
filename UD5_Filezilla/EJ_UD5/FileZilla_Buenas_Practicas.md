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

