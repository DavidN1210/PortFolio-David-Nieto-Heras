# Diario Unidad 3
## ¿Que he aprendido?
En esta unidad he aprendido obre la administración avanzada de servidores web en un entorno Linux, centrándome en la configuración. Los puntos más importantes son:
1. **Configuración de Virtual Hosts:** para alojar múltiples sitios (como gci.example.com) en un solo servidor Apache.
2. **Archivos de Configuración Clave:** Comprendí la importancia de DocumentRoot (directorio raíz) y ServerName (dominio asociado) en la configuración de un sitio.
3. **Localhost:** Entendí que, para probar un dominio que no existe públicamente (como example.com), es necesario mapear manualmente esa dirección al localhost (127.0.0.1).
## ¿Que no entiendo?
Aunque logré configurar el Virtual Host, no entiendo del todo cómo se integra esto con un sistema DNS público real. Es decir, si quisiera hacer público gci.example.com, no me queda claro cómo se enlazaría mi servidor con los registros de Internet para que otros usuarios pudieran acceder.
## ¿Qué es lo que más me ha gustado y qué es lo que menos?
Lo que más me gustó fue el proceso de resolución de problemas con el dominio gci.example.com.
Lo que menos me gustó fue tener que crear y renombrar manualmente los archivos de configuración.
## ¿Qué más me gustaría saber relacionado con la Unidad?
Me gustaría saber cómo implementar la seguridad avanzada en Apache, más allá de la configuración básica. Por ejemplo:
* Cómo configurar certificados SSL/TLS (HTTPS) para cifrar la comunicación (Aunque ya estamos en ello).
* Cómo aplicar reglas de firewall específicas para Apache para proteger el servidor de accesos no deseados.
