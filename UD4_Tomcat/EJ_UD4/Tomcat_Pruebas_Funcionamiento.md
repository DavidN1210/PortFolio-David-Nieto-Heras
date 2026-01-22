# Tomcat: Pruebas de funcionamiento y rendimiento
## Prueba 1
Esta prueba se realizará con la configuración por defecto en `server.xml`.

![Server.xml 1](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba1_server_xml.png)

## Prueba 2
Esta prueba se realizará con una configuración, en `server.xml`, más optimizada que la anterior.

![Server.xml 2](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba2_server_xml.png)

## 1. Prueba con ApacheBench
La primera prueba va a ser con `ApacheBench`, que es una herramienta de benchmarking diseñada para medir el rendimiento de un servidor web. Viene incluida con Apache, pero sirve para probar cualquier servidor HTTP, incluido Tomcat. Con esta herramienta se puede medir:
* **Requests per second (RPS)** → cuántas peticiones puede servir el servidor por segundo.
* **Tiempo por petición** → cuánto tarda en responder cada petición.
* **Latencias por percentiles** → cómo se comporta el servidor en situaciones reales (50%, 90%, 95%, 99%).
* **Errores** → si el servidor se cae o devuelve códigos incorrectos.
* **Estabilidad bajo concurrencia** → cómo responde cuando muchas peticiones llegan a la vez.

```bash
ab -n 1000 -c 50 http://localhost:8080/HelloApp/
```
### Resultado de la Prueba 1

![Prueba 1 Resultado ApacheBench 1](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba1_apacheBench2.png)

![Prueba 1 Resultado ApacheBench 2](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba1_apacheBench3.png)

### Resultado de la Prueba 2

![Prueba 2 Resultado ApacheBench 1](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba2_apacheBench.png)

![Prueba 2 Resultado ApacheBench 2](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba2_apacheBench2.png)

### Conclusión Prueba con ApacheBench

Tras analizar los resultados de ambas configuraciones, se observa que:

* El conector optimizado ofrece una ligera mejora en Requests per second y tiempo medio por petición.
* La mejora más notable aparece en los percentiles altos (95% y 99%), donde el conector optimizado reduce significativamente la latencia.
* Ninguna de las configuraciones presenta errores, lo que indica estabilidad en ambos casos.
* El conector optimizado gestiona mejor los picos de carga, manteniendo tiempos más consistentes.
* En resumen, aunque la diferencia en RPS es pequeña, el conector optimizado demuestra un comportamiento más robusto y estable bajo concurrencia elevada.


## 2. Prueba con curl --parallel
La segunda prueba sera con `curl --parallel`, que es una funcionalidad de curl que permite enviar múltiples peticiones HTTP al mismo tiempo, simulando concurrencia real. Es muy útil para:

* **Simulación de múltiples peticiones simultáneas** → permite enviar muchas peticiones HTTP al mismo tiempo usando `--parallel` y `--parallel-max`.
* **Tiempo total de ejecución (real)** → mide cuánto tarda el servidor en completar todas las peticiones desde el punto de vista del usuario.
* **Tiempo de CPU (user y sys)** → indica cuánta carga genera la prueba en el sistema local.
* **Consistencia de la respuesta** → comprueba si el servidor devuelve siempre el contenido esperado (por ejemplo, el HTML de Tomcat).
* **Detección de errores HTTP** → permite ver si alguna petición devuelve códigos incorrectos (404, 500, 503, etc.).
* **Estabilidad bajo carga real** → muestra si el servidor se mantiene estable cuando recibe muchas peticiones a la vez, sin bloquearse ni ralentizarse en exceso.

```bash
yes "url = http://localhost:8080/HelloApp/" | head -n 1000 > urls.txt // Para generar el txt con 1000 lineas con la url 
time curl --parallel --parallel-max 50 --config urls.txt // Lanza las 1000 peticiones simultáneas usando curl --parallel y muestra varios datos sobre el rendimiento para comparar configuraciones del conector.
```

### Resultado de la Prueba 1

![Prueba 1 Resultado Curl](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba1_curl.png)

### Resultado de la Prueba 2

![Prueba 2 Resultado Curl](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD4_Tomcat/img_UT4/prueba2_curl.png)

### Conclusión Prueba con curl --parallel
Tras analizar los resultados de ambas configuraciones, se observa que:

* El conector optimizado reduce el tiempo total de ejecución en un 44%, lo que indica una mejora clara en concurrencia real.
* El tiempo de CPU (sys) también disminuye, lo que sugiere mejor eficiencia en el manejo de conexiones.
* Ambos conectores responden correctamente a las 1000 peticiones, sin errores ni bloqueos.
* La respuesta HTML fue consistente en todas las peticiones, confirmando estabilidad funcional.









