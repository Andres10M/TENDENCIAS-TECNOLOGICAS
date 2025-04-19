# Práctica base de datos PostgreSQL con Docker

## 1. Título  
Persistencia de datos en contenedores PostgreSQL con y sin volumen usando Docker y pgAdmin

## 2. Tiempo de duración  
120 minutos

## 3. Fundamentos

PostgreSQL es un sistema de gestión de bases de datos relacional (RDBMS) de código abierto, muy utilizado por su estabilidad, escalabilidad y compatibilidad con SQL estándar. Docker, por su parte, es una plataforma de virtualización basada en contenedores que permite ejecutar software de manera aislada, asegurando portabilidad y consistencia entre entornos.

En esta práctica se implementaron contenedores que ejecutan una instancia de PostgreSQL. Se trabajó con dos enfoques: sin volumen (donde los datos se pierden al eliminar el contenedor) y con volumen (donde los datos persisten a través de recreaciones del contenedor). Esto permitió entender la importancia del uso de volúmenes para la persistencia de datos.

Además, se utilizó pgAdmin, una herramienta gráfica para la administración de PostgreSQL, que permitió visualizar la base de datos, crear tablas, insertar registros y comprobar el estado de los datos después de eliminar y volver a crear contenedores.

El enfoque principal fue comprobar el comportamiento del almacenamiento de datos, usando el volumen Docker para mapear el directorio interno de la base de datos (`/var/lib/postgresql/data`) a un volumen externo persistente.

**Figura 3-1. Esquema de persistencia sin volumen**  
*Agrega aquí una imagen representativa (ancho máx. 800px)*

**Figura 3-2. Esquema de persistencia con volumen**  
*Agrega aquí una imagen representativa (ancho máx. 800px)*

## 4. Conocimientos previos

Para realizar esta práctica el estudiante necesita tener claro los siguientes temas:

- Comandos básicos de Docker
- Manejo de pgAdmin o algún administrador de base de datos
- Fundamentos de bases de datos relacionales
- Uso básico de CLI (Command Line Interface)
- Conocimiento general de imágenes, contenedores y volúmenes Docker

## 5. Objetivos a alcanzar

- Crear contenedores PostgreSQL en Docker
- Configurar pgAdmin para conectarse a contenedores PostgreSQL
- Comprobar persistencia de datos con y sin volumen
- Familiarizarse con el manejo de volúmenes Docker para bases de datos

## 6. Equipo necesario

- Computador con sistema operativo Windows/Linux/Mac
- Docker Desktop instalado (versión recomendada: 24.0 o superior)
- pgAdmin o cualquier administrador de PostgreSQL
- Terminal o consola de comandos
- Conexión a Internet

## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Documentación oficial de PostgreSQL](https://www.postgresql.org/docs/)
- [Documentación de pgAdmin](https://www.pgadmin.org/)


## 8. Procedimiento

**Parte 1: Sin volumen**

Paso 1: Crear contenedor PostgreSQL sin volumen  
```bash
docker run --name server_db1 -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
```

<img src = "postgres docker/Captura de pantalla 2025-04-16 130322.png" width = "400">

Paso 2: Conectar pgAdmin a server_db1  

<img src = "postgres docker/Captura de pantalla 2025-04-16 130852.png" width = "400">

<img src = "postgres docker/Captura de pantalla 2025-04-16 130858.png" width = "400">

Paso 3: Crear base de datos test  

<img src = "postgres docker/Captura de pantalla 2025-04-16 131837.png" width = "400">

Paso 4: Crear tabla customer con columnas id, fullname, status  

<img src = "postgres docker/Captura de pantalla 2025-04-16 132253.png" width = "400">


Paso 5: Insertar un registro  

<img src = "postgres docker/Captura de pantalla 2025-04-17 185348.png" width = "400">

Comprobación de registro

<img src = "postgres docker/Captura de pantalla 2025-04-17 185502.png" width = "400">

Servidor corriendo

<img src = "postgres docker/Captura de pantalla 2025-04-17 190006.png" width = "400">

Paso 6: Eliminar contenedor
```bash
docker stop server_db1
docker rm server_db1
```
<img src = "postgres docker/Captura de pantalla 2025-04-17 190056.png" width = "400">

Paso 7: Verificar que la base test ya no existe  

<img src = "postgres docker/Captura de pantalla 2025-04-17 190356.png" width = "400">

**Figura 8-1. Diagrama de contenedor sin volumen**  

<img src = "postgres docker/Captura de pantalla 2025-04-17 190135.png" width = "400">



**Parte 2: Con volumen**

Paso 1: Crear volumen
```bash
docker volume create pgdata
```

```bash
docker run --name server_db2 -e POSTGRES_PASSWORD=postgres -p 5433:5432 -v pgdata:/var/lib/postgresql/data -d postgres
```
<img src = "postgres docker/Captura de pantalla 2025-04-17 190947.png" width = "400">

Paso 2: Conectar pgAdmin a server_db2  

<img src = "postgres docker/Captura de pantalla 2025-04-17 190833.png" width = "400">

Paso 3: Crear tabla customer con columnas id, fullname, status 

<img src = "postgres docker/Captura de pantalla 2025-04-17 192204.png" width = "400">

Paso 4: Insertar un registro 

<img src = "postgres docker/Captura de pantalla 2025-04-17 192238.png" width = "400">

Paso 5: Detener y eliminar el contenedor
```bash
docker stop server_db2
docker rm server_db2
```


<img src = "postgres docker/Captura de pantalla 2025-04-17 192601.png" width = "400">

Paso 6: Volver a crear server_db2 con mismo volumen
```bash
docker run --name server_db2 -e POSTGRES_PASSWORD=postgres -p 5433:5432 -v pgdata:/var/lib/postgresql/data -d postgres
```
<img src = "postgres docker/Captura de pantalla 2025-04-17 192620.png" width = "400">

Paso 7: Verificar que la base de datos y los datos aún existen  

<img src = "postgres docker/Captura de pantalla 2025-04-17 192704.png" width = "400">



## 9. Resultados esperados

- **Sin volumen:** al eliminar el contenedor, se pierden todos los datos.
- **Con volumen:** al eliminar el contenedor y recrearlo con el mismo volumen, los datos persisten.

  ## 🔊 Audio Explicativo del Proyecto Angular en WSL2
https://drive.google.com/file/d/1mXtHhZEFujZg_6AHTyE7z8aRfiMtnSlP/view?usp=sharing

## 10. Bibliografía

- Docker Inc. (s.f.). *Docker Documentation*. Recuperado de https://docs.docker.com/
- PostgreSQL Global Development Group. (s.f.). *PostgreSQL Documentation*. https://www.postgresql.org/docs/
- pgAdmin Team. (s.f.). *pgAdmin Documentation*. https://www.pgadmin.org/


