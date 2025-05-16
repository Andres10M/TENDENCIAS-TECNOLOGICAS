# Informe del Proyecto Frontend + Backend Simulado (mockAPI) con Docker

## 1. Título  
**Despliegue y prueba de aplicación frontend consumiendo backend simulado con Docker**

## 2. Tiempo de duración  
Aproximadamente 1 hora y 30 minutos.

## 3. Fundamentos

En esta práctica se trabajó con un proyecto frontend construido con React (o similar) y un backend simulado usando **json-server** para mockAPI. Se utilizó Docker para contenerizar la aplicación frontend y Docker Compose (de forma manual o sugerida) para levantar el backend simulado en un puerto diferente.

Los conceptos clave aplicados incluyen:  
- Uso de Docker para contenerización de aplicaciones.  
- Ejecución de backend simulado con json-server.  
- Comunicación entre frontend y backend mediante puertos expuestos.  
- Manejo de errores comunes en Docker, como puertos ocupados.  
- Clonación y configuración de repositorios GitHub para ambos proyectos.  

## 4. Conocimientos previos

- Conocimientos básicos de Docker y contenedores.  
- Manejo de comandos Git para clonar repositorios.  
- Familiaridad con proyectos frontend basados en Node.js.  
- Conceptos básicos de APIs REST y consumo desde frontend.  

## 5. Objetivos a alcanzar

- Clonar el repositorio backend simulado (mockAPI) y ejecutar el servicio json-server.  
- Clonar el repositorio frontend y verificar su funcionamiento localmente.  
- Crear un Dockerfile para contenerizar la aplicación frontend.  
- Construir y ejecutar la imagen Docker del frontend en un puerto específico (3000).  
- Ejecutar ambos servicios simultáneamente y verificar comunicación.  

## 6. Equipo necesario

- PC con Docker instalado y configurado correctamente.  
- Git para clonar los repositorios.  
- Node.js y npm para instalar dependencias y correr backend simulado.  
- Editor de código (VS Code o similar).  

## 7. Material de apoyo

- [Repositorio Backend MockAPI](https://github.com/Daviddotcoms/mockAPI)  
- Documentación oficial de Docker: [https://docs.docker.com/](https://docs.docker.com/)  
- json-server: [https://github.com/typicode/json-server](https://github.com/typicode/json-server)  

## 8. Procedimiento

### Paso 1: Clonar y ejecutar backend simulado

```bash
git clone https://github.com/Daviddotcoms/mockAPI.git
cd mockAPI
npm install
npm start
```
El backend quedó disponible en [http://localhost:3100](http://localhost:3100) con endpoints:

- `/classmates`
- `/teachers`

## Paso 2: Clonar y ejecutar frontend localmente

Se verificó que el proyecto frontend funciona bien en modo desarrollo, accediendo al puerto 3000.

## Paso 3: Crear Dockerfile para frontend

Archivo `Dockerfile` creado con instrucciones para contenerizar la app frontend, incluyendo instalación de dependencias y build.

Ejemplo básico:

```dockerfile
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

## Paso 4: Construir imagen Docker

```bash
docker build -t suda-frontend .
```
## Paso 5: Ejecutar contenedor frontend

```bash
docker run -d -p 3000:80 suda-frontend
```

Se cambió el puerto de exposición a 3000 para evitar conflictos con otros contenedores (antes 8080 estaba ocupado).

## Paso 6: Verificar que frontend consume backend

Frontend muestra correctamente datos consumidos desde el backend mockAPI corriendo en el puerto 3100.

## 9. Resultados esperados

- Backend json-server corriendo estable en el puerto 3100.
- Frontend funcionando en contenedor Docker expuesto en puerto 3000.
- Comunicación exitosa entre frontend y backend.
- Solución de error de puerto ocupado en Docker al cambiar puerto.

## 🔊 Audio Explicativo del proyecto Contenedores MySQL y phpMyAdmin

[Escuchar audio explicativo](https://drive.google.com/file/d/1kBJrE-8EDo8s6kAbm8MpG--bMTyyoDeQ/view?usp=sharing)



## 10. Bibliografía

- Docker, Inc. (2024). *Documentación oficial de Docker*. Recuperado de: [https://docs.docker.com/](https://docs.docker.com/)
- Typicode. (2024). *json-server: Fake REST API*. Recuperado de: [https://github.com/typicode/json-server](https://github.com/typicode/json-server)
- ReactJS. (2024). *Documentación oficial de React*. Recuperado de: [https://react.dev/](https://react.dev/)
- Node.js Foundation. (2024). *Documentación oficial de Node.js*. Recuperado de: [https://nodejs.org/en/docs](https://nodejs.org/en/docs)
- GitHub, Inc. (2024). *Repositorio mockAPI utilizado en el proyecto*. Recuperado de: [https://github.com/Daviddotcoms/mockAPI](https://github.com/Daviddotcoms/mockAPI)
- NGINX. (2024). *Using NGINX for serving static files*. Recuperado de: [https://docs.nginx.com/](https://docs.nginx.com/)
