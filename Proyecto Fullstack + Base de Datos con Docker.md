# Proyecto Fullstack + Base de Datos con Docker

## 1. Título  
**Despliegue completo de aplicación frontend en modo producción con Nginx, backend y base de datos con Docker**

## 2. Tiempo de duración  
Aproximadamente 2 horas.

## 3. Fundamentos

En esta práctica se desplegó una aplicación frontend en modo producción utilizando Nginx como servidor de archivos estáticos. También se incluyó un backend (Node.js, Express o similar) y una base de datos (MySQL o PostgreSQL), todo orquestado con Docker y `docker-compose` para facilitar su ejecución conjunta.

Los conceptos clave aplicados incluyen:

- Construcción de imágenes Docker personalizadas para producción.  
- Separación del proceso de build del frontend y el servicio de despliegue con Nginx.  
- Configuración de múltiples servicios en un solo entorno con `docker-compose`.  
- Exposición de puertos y conexión entre contenedores.  
- Persistencia de datos mediante volúmenes en la base de datos.

## 4. Conocimientos previos

- Creación de proyectos frontend con React, Angular o Vue.  
- Backend con Express.js u otro framework similar.  
- Comandos básicos de Docker, creación de Dockerfile.  
- Uso de `docker-compose` para levantar múltiples servicios.  
- Configuración básica de bases de datos relacionales (MySQL o PostgreSQL).

## 5. Objetivos a alcanzar

- Construir imagen del frontend utilizando Node.js (fase de build).  
- Servir frontend en modo producción con Nginx (fase de despliegue).  
- Configurar backend funcional (conexión a base de datos).  
- Levantar contenedor de base de datos con usuario, contraseña y volumen persistente.  
- Integrar todo en un archivo `docker-compose.yml` para ejecución unificada.  
- Probar que el frontend se conecta correctamente al backend y este a la base de datos.

## 6. Equipo necesario

- PC con Docker y Docker Compose instalados.  
- Node.js, npm/yarn y Git instalados.  
- VS Code o similar como editor.  
- Conexión a internet para clonar repositorios y descargar imágenes.

## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)  
- [Documentación de Nginx](https://docs.nginx.com/)  
- [Documentación de json-server](https://github.com/typicode/json-server)  
- [Documentación oficial de React](https://react.dev/)  
- [Documentación de PostgreSQL](https://www.postgresql.org/docs/)  
- [Documentación de docker-compose](https://docs.docker.com/compose/)

## 8. Procedimiento

### Paso 1: Crear el backend y el frontend en mi proyecto llamado ¨cooperativa-app¨

<img src = "cap2/Captura de pantalla 2025-06-13 121211.png" width = "400">


### Crear el build del frontend y backend



```dockerfile
# Dockerfile.build
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
```
"<img src = "cap2/Captura de pantalla 2025-06-13 214309.png" width = "400">" 

### Paso 2: Crear Dockerfile para servir el frontend con Nginx

 "<img src = "cap2/Captura de pantalla 2025-06-13 214309.png" width = "400">" 


```dockerfile
# Dockerfile.nginx
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

 "<img src = "cap2/Captura de pantalla 2025-06-13 214309.png" width = "400">" 

### Paso 3: Configurar archivo `docker-compose.yml`

```yaml
version: '3.8'

services:
  frontend:
    build:
      context: .
      dockerfile: Dockerfile.nginx
    ports:
      - "3000:80"
    depends_on:
      - backend

  backend:
    build: ./backend
    ports:
      - "4000:4000"
    environment:
      - DB_HOST=db
      - DB_USER=postgres
      - DB_PASS=pegaso20
      - DB_NAME=appdb
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: pegaso20
      POSTGRES_DB: appdb
    volumes:
      - pgdata:/var/lib/postgresql/data
    ports:
      - "5432:5432"

volumes:
  pgdata:
```

 "<img src = "cap2/Captura de pantalla 2025-06-13 214334.png" width = "400">" 
### Paso 4: Construir y levantar la aplicación

```bash
docker-compose up --build
```
 "<img src = "cap2/Captura de pantalla 2025-06-13 204341.png" width = "400">"

## 9. Resultados esperados

- La base de datos **PostgreSQL** está corriendo en el contenedor `db` en el puerto `5432`.
- El **backend** está activo y puede conectarse a la base de datos.
- El **frontend** es accesible desde el navegador en [http://localhost:3000](http://localhost:3000), sirviendo archivos estáticos desde **Nginx**.
- La comunicación entre **frontend**, **backend** y **base de datos** es exitosa.
- Toda la aplicación está contenida y ejecutándose con **Docker**.

## 10. Bibliografía

- **Docker, Inc.** (2024). *Documentación oficial de Docker*. Recuperado de: https://docs.docker.com/
- **NGINX** (2024). *Using NGINX for serving static files*. Recuperado de: https://docs.nginx.com/
- **Node.js Foundation** (2024). *Documentación oficial de Node.js*. Recuperado de: https://nodejs.org/en/docs
- **PostgreSQL Global Development Group** (2024). *Documentación oficial de PostgreSQL*. Recuperado de: https://www.postgresql.org/docs/
- **ReactJS** (2024). *Documentación oficial de React*. Recuperado de: https://react.dev/
- **GitHub, Inc.** (2024). *json-server*. Recuperado de: https://github.com/typicode/json-server
- **Docker Compose** (2024). *Documentación oficial*. Recuperado de: https://docs.docker.com/compose/


