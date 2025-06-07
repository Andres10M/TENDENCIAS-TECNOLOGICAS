# React + NestJS + PostgreSQL usando Docker Compose

## 1. Título
**Despliegue de una aplicación fullstack con React, NestJS y PostgreSQL utilizando Docker Compose**

## 2. Tiempo de duración
Aproximadamente 1 hora y 30 minutos.

## 3. Fundamentos:

El uso de **Docker Compose** permite definir y desplegar entornos de desarrollo multicontenedor. En esta práctica se usó Docker Compose para levantar un entorno con tres servicios principales: **Frontend en React**, **Backend en NestJS** y **Base de datos PostgreSQL**.

Esto facilita el desarrollo y despliegue de sistemas distribuidos, permitiendo que cada componente del sistema se ejecute de forma independiente pero comunicada dentro de la misma red de contenedores.

Los conceptos clave aplicados fueron:
- Definición de servicios en Docker Compose.
- Comunicación entre contenedores vía red virtual.
- Exposición de puertos para frontend, backend y base de datos.
- Persistencia de datos mediante volúmenes.
- Creación de imágenes a partir de Dockerfiles personalizados para cada servicio.

## 4. Conocimientos previos

- Uso básico de Docker y Docker Compose.
- Fundamentos de desarrollo web con React.
- Fundamentos de desarrollo backend con NestJS.
- Conceptos básicos de bases de datos relacionales (PostgreSQL).

## 5. Objetivos a alcanzar

- Crear un archivo `docker-compose.yml` que levante tres servicios: frontend, backend y base de datos.
- Desarrollar y utilizar `Dockerfile` para React y NestJS.
- Verificar que los servicios se comunican correctamente.
- Acceder al frontend desde el navegador y observar la conexión con el backend.

## 6. Equipo necesario

- Computadora con Docker y Docker Compose instalados.
- Acceso a Internet.
- Editor de código como Visual Studio Code.

## 7. Material de apoyo

- [Documentación oficial de Docker Compose](https://docs.docker.com/compose/)
- [Documentación de React](https://reactjs.org/)
- [Documentación de NestJS](https://docs.nestjs.com/)
- [Documentación de PostgreSQL](https://www.postgresql.org/docs/)

## 8. Procedimiento
### Se crea tanto el frontend como el backend y se descargan sus paquetes y dependencias
## Backend-socios

<img src = "frontback/Captura de pantalla 2025-06-07 123533.png" width = "400">

<img src = "frontback/Captura de pantalla 2025-06-07 123802.png" width = "400">

<img src = "frontback/Captura de pantalla 2025-06-07 124020.png" width = "400">

### Paso 1: Crear el archivo `docker-compose.yml`



<img src = "frontback/Captura de pantalla 2025-06-07 124823.png" width = "400">




```yaml
version: '3.8'

services:
  frontend:
    container_name: frontend-socios
    build:
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - "5173:5173"
    depends_on:
      - backend
    environment:
      - REACT_APP_API_URL=http://backend:3000

  backend:
    container_name: backend-socios
    build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    depends_on:
      - db
    environment:
      DB_HOST: db
      DB_PORT: 5432
      DB_USERNAME: postgres
      DB_PASSWORD: pegaso20
      DB_DATABASE: MINOSDB

  db:
    image: postgres:14
    container_name: postgres-db
    restart: always
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: pegaso20
      POSTGRES_DB: MINOSDB
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```
## Levantar la base de Datos

<img src = "frontback/Captura de pantalla 2025-06-07 130249.png" width = "400">

## Paso 2: Creación y Dockerfile para el frontend (React)

<img src = "frontback/Captura de pantalla 2025-06-07 130812.png" width = "400">

<img src = "frontback/Captura de pantalla 2025-06-07 131009.png" width = "400">

<img src = "frontback/Captura de pantalla 2025-06-07 164918.png" width = "400">

<img src = "frontback/Captura de pantalla 2025-06-07 164926.png" width = "400">




**Ubicado en `frontend/Dockerfile`:**

```Dockerfile
# Build
FROM node:18 as build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

# Serve
FROM node:18
WORKDIR /app
RUN npm install -g serve
COPY --from=build /app/dist ./dist
CMD ["serve", "-s", "dist", "-l", "5173"]
```

## Paso 3: Dockerfile para el backend (NestJS)

**Ubicado en `backend/Dockerfile`:**

```Dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
CMD ["node", "dist/main"]
```

## Paso 4: Iniciar los servicios

En la terminal, ejecutar:

```bash
docker-compose up --build
```
<img src = "frontback/Captura de pantalla 2025-06-07 154007.png" width = "400">
## Paso 5: Acceder a los servicios

- **Frontend (React):** [http://localhost:5173](http://localhost:5173)
<img src = "frontback/Captura de pantalla 2025-06-07 154057.png" width = "400">

- **Backend (NestJS API):** [http://localhost:3000](http://localhost:3000)

<img src = "frontback/Captura de pantalla 2025-06-07 153329.png" width = "400">
- **Base de datos PostgreSQL:** Puerto `5432` (accesible desde pgAdmin o DBeaver)

---
## Prueba de correcta conexión del back y frontd

<img src = "frontback/Captura de pantalla 2025-06-07 154057.png" width = "400">


<img src = "frontback/Captura de pantalla 2025-06-07 154146.png" width = "400">

## Estructura del proyecto

```
tu-proyecto/
├── docker-compose.yml
├── frontend/
│ ├── Dockerfile
│ └── (código React)
├── backend/
│ ├── Dockerfile
│ └── (código NestJS)
```

---

## Capturas de pantalla (opcional)

*(Agregar imágenes si se desea)*

---

## 9. Resultados esperados

- Aplicación frontend (React) accesible en navegador.
- API backend (NestJS) funcionando y respondiendo a peticiones.
- Base de datos PostgreSQL levantada correctamente y accesible.
- Comunicación efectiva entre los tres servicios gracias a Docker Compose.
- Persistencia de datos en PostgreSQL mediante volúmenes.

---

## 🔊 Audio Explicativo del Proyecto Fullstack con Docker

**Audio Explicativo:** *(agregar enlace o insertar reproductor si se publica online)*

---

## 10. Bibliografía

- Docker, Inc. (2024). *Docker Compose Documentation*. Recuperado de: [https://docs.docker.com/compose/](https://docs.docker.com/compose/)
- Facebook. (2024). *React Documentation*. [https://reactjs.org/](https://reactjs.org/)
- NestJS Devs. (2024). *NestJS Docs*. [https://docs.nestjs.com/](https://docs.nestjs.com/)
- PostgreSQL Global Development Group. (2024). *PostgreSQL Documentation*. [https://www.postgresql.org/docs/](https://www.postgresql.org/docs/)
