# Practica servidor web

## 1. Titulo
**Despliegue de dos servidores web con Nginx usando Docker**

En esta práctica, se creó y personalizó dos servidores web basados en Nginx mediante contenedores Docker. Se editaron archivos HTML para personalizar el contenido de cada servidor y mostrar información institucional en uno y personal en el otro.

## 2. Tiempo de duración
El tiempo estimado para realizar esta práctica fue de **45 minutos**.

## 3. Fundamentos
Docker es una herramienta de contenedores que permite ejecutar aplicaciones en entornos aislados. En esta práctica, se utilizó Docker para crear contenedores con la imagen oficial de Nginx, un servidor web muy popular por su alta eficiencia y facilidad de configuración.

### ¿Qué es un contenedor?
Un contenedor es un entorno aislado que incluye todo lo necesario para ejecutar una aplicación, como el código, las dependencias, las bibliotecas y los archivos de configuración. Docker facilita la creación y gestión de estos contenedores, permitiendo ejecutar aplicaciones en cualquier lugar sin preocuparse por las dependencias del sistema operativo host.

### Nginx y su configuración
Nginx es un servidor web y proxy inverso que se utiliza para distribuir contenido estático y dinámico. Se destaca por su capacidad para manejar múltiples solicitudes concurrentes de manera eficiente, lo que lo convierte en una excelente opción para aplicaciones con alto tráfico.

En esta práctica, se utilizaron dos contenedores Nginx, cada uno configurado para mostrar diferentes contenidos en su página de inicio (`index.html`). Este archivo puede ser modificado directamente dentro del contenedor utilizando comandos de Docker.

#### Figura 3-1. Contenedores Docker
![Contenedores Docker](./imagenes/contenerores_docker.png)
La imagen muestra dos contenedores Nginx corriendo en diferentes puertos.

## 4. Conocimientos previos
Para realizar esta práctica, el estudiante necesita tener claros los siguientes temas:

- **Comandos básicos de Docker**: Crear, iniciar, detener contenedores, copiar archivos y ejecutar comandos dentro de contenedores.
- **Linux**: Conocimiento básico de la terminal para navegar, editar archivos y ejecutar comandos.
- **Navegadores web**: Saber cómo acceder a un servidor web mediante la URL y comprobar que los cambios en el contenido son reflejados.

## 5. Objetivos a alcanzar
- **Implementar contenedores con Nginx**: Aprender a crear y ejecutar servidores web con Nginx en contenedores Docker.
- **Manipular archivos de configuración dentro de contenedores**: Editar los archivos `index.html` para personalizar el contenido de los servidores web.
- **Verificación y prueba de servidores web**: Asegurarse de que los cambios realizados en los contenedores se reflejan correctamente al acceder a los servidores desde un navegador.

## 6. Equipo necesario
- Computador con sistema operativo **Windows/Linux/Mac**.
- Cuenta en **Docker Hub** para obtener la imagen oficial de Nginx.
- Docker v20.x o superior.
- Editor de texto como **Visual Studio Code** o **nano** para editar archivos.
- Un navegador web (Google Chrome, Firefox, etc.).

## 7. Material de apoyo
- **Documentación oficial de Docker**: [Docker Docs](https://docs.docker.com/)
- **Guía de asignatura** proporcionada por el profesor.
- **Cheat sheet Linux** para comandos rápidos.

## 8. Procedimiento

**Paso 1**: Crear el primer contenedor Nginx con el siguiente comando:

```bash
docker run -d --name nginx1 -p 8089:80 nginx

```
## Paso 2: Crear el segundo contenedor Nginx:
```bash
docker run -d --name nginx2 -p 8090:80 nginx


**Paso 1**: Crear el primer contenedor Nginx con el siguiente comando:

```bash
docker run -d --name nginx1 -p 8089:80 nginx

```
## 9. Resultados esperados:
Después de completar los pasos anteriores, se espera que los dos servidores Nginx estén ejecutándose en los puertos 8089 y 8090, cada uno mostrando contenido personalizado en su archivo `index.html`. Al acceder a las siguientes URLs en un navegador:

- **http://localhost:8089**: Debería mostrar el contenido institucional.
- **http://localhost:8090**: Debería mostrar el contenido personalizado.

**Capturas de pantalla del resultado final de la práctica:**

- **Servidor 1:**
  
  ![Servidor 1](./imagenes/servidor1.png)

- **Servidor 2:**
  
  ![Servidor 2](./imagenes/servidor2.png)

## 10. Bibliografía:

- Apellido, Nombre. (Año). *Título del libro o artículo*. Editorial.
- Apellido, Nombre. (Año). *Título del libro o artículo*. Editorial.
- Docker, Inc. (2021). *Docker Documentation*. Recuperado de [https://docs.docker.com/](https://docs.docker.com/)
- Smith, J. (2019). *Learning Nginx*. O'Reilly Media.

