# Actividad 1: Introducción y arquitectura de FileZilla Server

## Canales

- **Canal de CONTROL** → puerto 21 (comandos y respuestas)
- **Canal de DATOS** → transferencia de archivos y listados

---

## MODO ACTIVO

### Canal de CONTROL (puerto 21)

Cliente ────────────────▶ Servidor  
`PORT h1,h2,h3,h4,p1,p2`  
*(PORT es un comando con el que el cliente indica su IP y el puerto donde escuchará los datos)*

### Canal de DATOS

Servidor ────────────────▶ Cliente  
*(el servidor inicia la conexión desde su puerto 20 al puerto indicado por el cliente)*

### Flujo simplificado

Cliente ─▶ Servidor : comando `PORT`  
Servidor ─▶ Cliente : abre conexión de datos  
Cliente ⇄ Servidor : transferencia de datos (LIST, RETR, STOR)  
Servidor ─▶ Cliente : `226 Transferencia completa`

### Características

* El **servidor inicia** la conexión de datos  
* Puede dar problemas con **firewalls y NAT**

---

## MODO PASIVO

### Canal de CONTROL (puerto 21)

Cliente ────────────────▶ Servidor  
`PASV`
*(PASV es un comando que utiliza el cliente para solicitar una IP y puerto pasivo al servidor para lograr la conexión y así tranferir datos, ya que no es posible con el modo activo)*

Servidor ────────────────▶ Cliente  
`227 Modo Pasivo (IP, puerto)`
*(el servidor indica la IP y puerto pasivo)*

### Canal de DATOS

Cliente ────────────────▶ Servidor  
*(el cliente se conecta al puerto pasivo indicado por el servidor)*

### Flujo simplificado

Cliente ─▶ Servidor : comando `PASV`  
Servidor ─▶ Cliente : indica IP y puerto pasivo  
Cliente ─▶ Servidor : abre conexión de datos  
Cliente ⇄ Servidor : transferencia de datos (LIST, RETR, STOR)  
Servidor ─▶ Cliente : `226 Transferencia completa`

### Características

* El **cliente inicia** la conexión de datos  
* Más compatible con **firewalls y NAT**
