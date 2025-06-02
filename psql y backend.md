# Contenedores PostgreSQL, pgAdmin y Aplicación Backend con Docker

## 1. Título
**Despliegue Automatizado de Contenedores PostgreSQL, pgAdmin y una Aplicación Backend con Docker y Docker Compose**

## 2. Tiempo de duración
Aproximadamente 1 hora y 30 minutos.

## 3. Fundamentos:

Docker ha revolucionado la manera en que las aplicaciones se desarrollan, despliegan y administran, permitiendo encapsularlas junto con sus dependencias en contenedores portables y reproducibles. En esta práctica, se abordó el despliegue automatizado de un entorno de desarrollo backend, compuesto por tres servicios:

- **PostgreSQL**, una base de datos relacional de código abierto robusta y confiable.
- **pgAdmin**, una herramienta de administración web para PostgreSQL.
- Una **aplicación backend Java Spring Boot**, tomada del repositorio [tendencias-mar22-security](https://github.com/maguaman2/tendencias-mar22-security.git).

Se utilizó Docker Compose para definir y coordinar múltiples servicios, incluyendo la red compartida y volúmenes persistentes. Además, se implementó una estrategia de construcción **multi-stage** para la aplicación backend, optimizando el tamaño de la imagen resultante y mejorando la eficiencia del despliegue.

### Flujo general:
1. Crear una red personalizada y volúmenes para persistencia.
2. Configurar los servicios de PostgreSQL y pgAdmin en `docker-compose.yml`.
3. Crear un Dockerfile multi-stage para construir y empaquetar la aplicación backend.
4. Integrar el backend como un servicio adicional en el archivo `docker-compose.yml`.
5. Definir variables de entorno en un archivo `.env`.
6. Verificar conectividad entre servicios y acceso vía pgAdmin.

## 4. Conocimientos previos

- Fundamentos de Docker y Docker Compose.
- Conocimientos básicos de redes, volúmenes y variables de entorno en Docker.
- Experiencia previa con PostgreSQL y pgAdmin.
- Conocimiento en construcción de aplicaciones Java Spring Boot.
- Uso de comandos de consola en sistemas Linux.

## 5. Objetivos a alcanzar

- Desplegar una base de datos PostgreSQL y su cliente pgAdmin en contenedores conectados.
- Construir una imagen optimizada del backend utilizando Docker y multi-stage builds.
- Automatizar el despliegue de todos los servicios con Docker Compose.
- Verificar la conexión del backend con la base de datos.
- Acceder y gestionar la base de datos desde la interfaz de pgAdmin.

## 6. Equipo necesario

- Computadora con Docker y Docker Compose instalados.
- Acceso a terminal (Linux, Windows o Mac).
- Acceso a Internet para clonar el repositorio y descargar imágenes.
- Editor de texto para modificar `Dockerfile`, `.env` y `docker-compose.yml`.

## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Documentación oficial de PostgreSQL](https://www.postgresql.org/docs/)
- [Documentación de pgAdmin](https://www.pgadmin.org/docs/)
- Guía de proyecto Java Spring Boot proporcionada en GitHub.

## 8. Procedimiento

### Paso 1: Clonar el proyecto base

```bash
git clone https://github.com/maguaman2/tendencias-mar22-security.git
cd tendencias-mar22-security
