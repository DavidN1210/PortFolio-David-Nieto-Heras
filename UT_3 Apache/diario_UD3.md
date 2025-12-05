# Diario Unidad 3

## ¿Qué he aprendido?
En esta unidad he aprendido sobre la **administración avanzada de servidores web en Linux**, centrándome en la instalación y configuración de **Apache2** y en la implementación de **HTTPS**.  
Los puntos más importantes han sido:
- Configuración de **Virtual Hosts** para alojar múltiples sitios en un mismo servidor.
- Uso de archivos clave como **DocumentRoot** y **ServerName** para definir la estructura de un sitio.
- Implementación de **certificados SSL/TLS** (autofirmados) para habilitar HTTPS.
- Modificación de `/etc/hosts` para simular dominios locales como `daviddominio.com` o `gci.example.com`.

## ¿Qué no entiendo?
Aunque logré configurar correctamente los Virtual Hosts y los certificados autofirmados, todavía me cuesta comprender cómo se integra esto con un **DNS público real**.  
Es decir, si quisiera hacer público un dominio como `gci.example.com`, no tengo claro cómo se enlazaría mi servidor con los registros de Internet para que otros usuarios pudieran acceder.

## ¿Qué es lo que más me ha gustado y qué es lo que menos?
* **Lo que más me gustó:** el proceso de resolución de problemas, especialmente al simular dominios locales y ver cómo funcionaban en el navegador.
* **Lo que menos me gustó:** tener que crear y editar manualmente los archivos de configuración, ya que requiere mucha precisión y cualquier error puede romper el despliegue.

## ¿Qué más me gustaría saber relacionado con la Unidad?
Me gustaría profundizar en:
- Configuración avanzada de **seguridad en Apache** (más allá de HTTPS básico).
- Uso de **certificados de Autoridades de Certificación (CA)** en lugar de autofirmados.
- Aplicación de **reglas de firewall** específicas para Apache.
- Buenas prácticas de **monitorización y logs** para detectar accesos no deseados.

## 📌 Conclusión y Valoración Personal
La unidad me permitió comprender de manera práctica cómo funciona Apache y cómo se implementa HTTPS.  
Aprendí a **instalar, configurar y desplegar sitios web** en Ubuntu, a manejar **Virtual Hosts**, y a resolver problemas de acceso mediante la edición de `/etc/hosts`.  
La experiencia fue enriquecedora porque no solo seguí pasos técnicos, sino que también enfrenté dificultades reales (errores de certificados, problemas de DNS, advertencias del navegador).  
Considero que estas prácticas son fundamentales para adquirir confianza en la administración de servidores y en la seguridad de las comunicaciones web.
