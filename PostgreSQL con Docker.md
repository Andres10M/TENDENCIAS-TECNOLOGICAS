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
- Guía de la asignatura
- Apuntes de clase
- Cheat sheet de comandos Docker

## 8. Procedimiento

**Parte 1: Sin volumen**

Paso 1: Crear contenedor PostgreSQL sin volumen  
```bash
docker run --name server_db1 -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
```
Paso 2: Conectar pgAdmin a server_db1  
*Agregar imagen con pgAdmin conectado*

Paso 3: Crear base de datos test  
*Agregar imagen de creación de base*

Paso 4: Crear tabla customer con columnas id, fullname, status  
*Agregar imagen de la estructura de la tabla*

Paso 5: Insertar un registro  
*Agregar imagen de la tabla con datos*

Paso 6: Eliminar contenedor
```bash
docker stop server_db1
docker rm server_db1
```

Paso 7: Verificar que la base test ya no existe  
*Agregar captura mostrando que no hay datos*

**Figura 8-1. Diagrama de contenedor sin volumen**  
*Agrega aquí una imagen representativa*

---

**Parte 2: Con volumen**

Paso 1: Crear volumen
```bash
docker volume create pgdata
```

Paso 2: Crear contenedor server_db2 con volumen
```bash
docker run --name server_db2 -e POSTGRES_PASSWORD=postgres -p 5433:5432 -v pgdata:/var/lib/postgresql/data -d postgres
```

Paso 3: Conectar pgAdmin a server_db2  
*Agregar imagen*

Paso 4: Crear base de datos test  
Paso 5: Crear tabla customer con columnas id, fullname, status  
Paso 6: Insertar un registro  
*Agregar imágenes correspondientes*

Paso 7: Detener y eliminar el contenedor
```bash
docker stop server_db2
docker rm server_db2
```

Paso 8: Volver a crear server_db2 con mismo volumen
```bash
docker run --name server_db2 -e POSTGRES_PASSWORD=postgres -p 5433:5432 -v pgdata:/var/lib/postgresql/data -d postgres
```

Paso 9: Verificar que la base de datos y los datos aún existen  
*Agregar imagen final con los datos persistentes*

**Figura 8-2. Diagrama de contenedor con volumen**  
*Agrega aquí una imagen representativa*

## 9. Resultados esperados

- **Sin volumen:** al eliminar el contenedor, se pierden todos los datos.
- **Con volumen:** al eliminar el contenedor y recrearlo con el mismo volumen, los datos persisten.

**Captura del resultado sin volumen:**  
*Agregar imagen donde se ve que no hay base de datos*

**Captura del resultado con volumen:**  
*Agregar imagen donde se ve que la tabla y datos están presentes después de eliminar y recrear el contenedor*

## 10. Bibliografía

- Docker Inc. (s.f.). *Docker Documentation*. Recuperado de https://docs.docker.com/
- PostgreSQL Global Development Group. (s.f.). *PostgreSQL Documentation*. https://www.postgresql.org/docs/
- pgAdmin Team. (s.f.). *pgAdmin Documentation*. https://www.pgadmin.org/


