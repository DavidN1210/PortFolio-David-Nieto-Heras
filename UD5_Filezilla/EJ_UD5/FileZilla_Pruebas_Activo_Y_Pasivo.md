# Actividad 5: Pruebas en modo activo y pasivo
# 1. Configuración del rango de puertos pasivos

En FileZilla Server, dentro de la configuracion (Protocol Settings → FTP and FTP over TLS → Passive Mode), marco la opción de **"Use custom port range"* y eligo un rango de puertos (por ejemplo 50000 -  50100).
Esto es necesario porque cuando la conexión se realiza en modo pasivo, el cliente necesita que el servidor abra puertos adicionales para la conexión de datos. Definir un rango fijo permite:

* Controlar qué puertos se usan.
* Abrir solo esos puertos en el firewall.
* Evitar problemas de conexión en redes protegidas.

Sin este rango, el modo pasivo puede fallar porque el firewall no sabe qué puertos permitir.

![Puertos pasivos](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/rango_de_puertos.png)

## 2. Conexiones
### En modo activo

Para relizar la conexión en modo activo, en la configuración de Filezilla Client (Editar → Configuración → FTP → Modo de tranferencia → Activo ), tenemos que cambiar el modo de trasferencia a modo activo.
En modo activo, la conexión puede fallar si el cliente está detrás de un firewall o router, porque las conexiones entrantes suelen bloquearse. Si funciona, significa que la red local no tiene restricciones (mi caso).

![Modo de transferencia activo](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/cliente_activo.png)

Por el lado del cliente: 

![Conexión modo activo cliente](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/prueba_activo_cliente.png)

Por el lado del servidor: 

![Conexión modo activo servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/prueba_activo_servidor.png)

### En modo pasivo

Al igual que en el modo activo, en la configuración de FileZilla Client, tenemos que cambiar el modo de transferencia a modo pasivo. Este modo es el más compatible con firewalls, porque no requiere conexiones entrantes hacia el cliente.

![Modo de transferencia pasivo](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/cliente_pasivo.png)

Por el lado del cliente: 

![Conexión modo pasivo cliente](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/prueba_pasivo_cliente.png)

Por el lado del servidor: 

![Conexión modo pasivo servidor](https://github.com/DavidN1210/PortFolio-David-Nieto-Heras/blob/main/UD5_Filezilla/img_UT5/prueba_pasivo_servidor.png)

## 3. Funcionamiento en redes con firewall

En conclusión, el modo pasivo funciona mejor en redes con firewall porque:

* El cliente no necesita aceptar conexiones entrantes.
* Solo realiza conexiones salientes, que normalmente están permitidas.
* El servidor usa un rango de puertos controlado y fácil de abrir.

El modo activo suele fallar porque el servidor intenta conectarse al cliente, y los firewalls bloquean ese tráfico.

## 4. Tabla comparativa

| Característica                               | Modo Activo                         | Modo Pasivo                          |
|----------------------------------------------|--------------------------------------|---------------------------------------|
| Quién inicia la conexión de datos            | Servidor → Cliente                   | Cliente → Servidor                    |
| Necesita puertos abiertos en el cliente      | Sí                                   | No                                    |
| Necesita puertos abiertos en el servidor     | No (solo puerto 21)                  | Sí (rango de puertos pasivos)         |
| Compatibilidad con firewalls                 | Baja                                 | Alta                                  |
| Riesgo de bloqueo                            | Alto                                 | Bajo                                  |
| Funcionamiento detrás de NAT                 | Problemático                         | Muy bueno                             |
| Uso recomendado                              | Redes sin firewall estricto          | Redes con firewall o routers NAT      |



