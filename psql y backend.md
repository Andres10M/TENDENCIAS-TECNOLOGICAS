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
```
## **Paso 2: Crear el archivo `.env`**

```env
POSTGRES_USER=admin
POSTGRES_PASSWORD=admin123
POSTGRES_DB=mi_base
PGADMIN_DEFAULT_EMAIL=admin@correo.com
PGADMIN_DEFAULT_PASSWORD=admin123
```
## Paso 3: Crear el `docker-compose.yml`

```yaml
services:
  postgres:
    image: postgres:15
    container_name: postgres_container
    restart: always
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: pegaso20
      POSTGRES_DB: admin
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - backend_network

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin_container
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@example.com
      PGADMIN_DEFAULT_PASSWORD: admin123
    ports:
      - "5050:80"
    volumes:
      - pgadmin_data:/var/lib/pgadmin
    networks:
      - backend_network
    depends_on:
      - postgres

  backend:
    build:
      context: .               # <-- Aquí, la ruta correcta de tu backend (raíz)
      dockerfile: Dockerfile
    container_name: backend_container
    restart: always
    ports:
      - "8081:8080"            # Cambia puerto si es necesario
    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://postgres:5432/admin
      SPRING_DATASOURCE_USERNAME: postgres
      SPRING_DATASOURCE_PASSWORD: pegaso20
    depends_on:
      - postgres
    networks:
      - backend_network

volumes:
  postgres_data:
  pgadmin_data:

networks:
  backend_network:
    driver: bridge

```
# Etapa de construcción
FROM maven:3.9.2-eclipse-temurin-17 AS builder
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Etapa final
FROM eclipse-temurin:17-jdk
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]

## **Paso 5: Levantar todos los servicios**

```bash
docker-compose --env-file .env up --build
```
## **Paso 6: Acceder a pgAdmin**

Abrir en el navegador: [http://localhost:5050](http://localhost:5050)

Iniciar sesión con:

- **Email:** admin@correo.com
- **Contraseña:** admin123

Agregar un nuevo servidor:

- **Nombre:** PostgreSQL Local
- **Host:** db
- **Usuario:** admin
- **Contraseña:** admin123
- **Base de datos:** mi_base

---

## **Paso 7: Verificar conexión del backend**

Ir a [http://localhost:8080](http://localhost:8080) y verificar que la aplicación se conecta correctamente a la base de datos.

---

## **9. Resultados esperados**

- Acceso exitoso a pgAdmin desde el navegador.
- Conexión establecida entre pgAdmin y PostgreSQL.
- Backend desplegado con acceso funcional a la base de datos.
- Imagen del backend optimizada mediante multi-stage builds.
- Persistencia de datos gracias al uso de volúmenes Docker.

---

## **🔊 Audio Explicativo del Proyecto**

Enlace al audio explicativo aquí

---

## **10. Bibliografía**

- Docker, Inc. (2024). Docker Documentation. Recuperado de: https://docs.docker.com/
- PostgreSQL Global Development Group. (2024). PostgreSQL Documentation. https://www.postgresql.org/docs/
- pgAdmin Team. (2024). pgAdmin Documentation. https://www.pgadmin.org/docs/
- Oracle Java. (2024). Java 17 Documentation. https://docs.oracle.com/en/java/javase/17/
- Apache Maven. (2024). Maven Documentation. https://maven.apache.org/




