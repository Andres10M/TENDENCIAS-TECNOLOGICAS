# WordPress con PostgreSQL y pgAdmin usando Docker Compose

## 1. Título
**Despliegue de WordPress con PostgreSQL y pgAdmin utilizando Docker Compose**

## 2. Tiempo de duración
Aproximadamente 1 hora.

## 3. Fundamentos:

El uso de **Docker Compose** permite definir y ejecutar aplicaciones multicontenedor de forma sencilla mediante archivos de configuración en formato YAML. En esta práctica se utilizó Docker Compose para estructurar un entorno con tres servicios principales: **WordPress**, **PostgreSQL** y **pgAdmin**.

Aunque WordPress está tradicionalmente asociado con MySQL/MariaDB, también es posible integrarlo con PostgreSQL mediante ciertos plugins o capas de compatibilidad. Esta práctica tiene como fin aprender a definir redes, volúmenes y dependencias entre servicios en un archivo `docker-compose.yml`.

Los conceptos clave que se aplicaron incluyen:
- Creación de servicios en Docker Compose.
- Conexión de servicios mediante una red definida.
- Persistencia de datos usando volúmenes.
- Gestión visual de PostgreSQL mediante pgAdmin.
- Exposición de puertos para acceder a WordPress y pgAdmin desde el navegador.

## 4. Conocimientos previos

- Manejo básico de Docker y Docker Compose.
- Conocimiento general de contenedores, redes y volúmenes.
- Familiaridad con bases de datos PostgreSQL.
- Nociones básicas de WordPress como CMS.

## 5. Objetivos a alcanzar

- Construir un archivo `docker-compose.yml` para desplegar WordPress, PostgreSQL y pgAdmin.
- Configurar la red y los volúmenes entre los servicios.
- Acceder a WordPress y pgAdmin desde el navegador.
- Verificar la conexión entre los servicios definidos.

## 6. Equipo necesario

- PC con Docker y Docker Compose instalados.
- Conexión a Internet.
- Editor de texto o entorno de desarrollo (como VS Code o Nano).

## 7. Material de apoyo

- [Documentación oficial de Docker Compose](https://docs.docker.com/compose/)
- [Documentación de WordPress](https://wordpress.org/support/)
- [Documentación de PostgreSQL](https://www.postgresql.org/docs/)
- [Documentación de pgAdmin](https://www.pgadmin.org/)

## 8. Procedimiento

### Paso 1: Crear el archivo `docker-compose.yml`

```yml
version: '3.8'

services:
  postgres:
    image: postgres:latest
    container_name: postgres
    restart: always
    environment:
      POSTGRES_USER: wp_user
      POSTGRES_PASSWORD: wp_password
      POSTGRES_DB: wp_db
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - wp_net

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin
    restart: always
    ports:
      - "5050:80"
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@example.com
      PGADMIN_DEFAULT_PASSWORD: admin
    depends_on:
      - postgres
    networks:
      - wp_net

  wordpress:
    image: wordpress:latest
    container_name: wordpress
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: postgres
      WORDPRESS_DB_USER: wp_user
      WORDPRESS_DB_PASSWORD: wp_password
      WORDPRESS_DB_NAME: wp_db
    depends_on:
      - postgres
    networks:
      - wp_net

volumes:
  pgdata:

networks:
  wp_net:
