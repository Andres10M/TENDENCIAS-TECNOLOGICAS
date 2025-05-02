# Contenedores MySQL, phpMyAdmin y WordPress

## 1. Título
**Creación de Contenedores MySQL, phpMyAdmin y WordPress en Docker y Configuración de Red para Comunicación**

## 2. Tiempo de duración
Aproximadamente 1 hora.

## 3. Fundamentos

El uso de **contenedores Docker** permite desplegar entornos completos de aplicaciones web de forma rápida, reproducible y aislada. En esta práctica se implementan tres aplicaciones clave:

- **MySQL**: sistema gestor de bases de datos relacional.
- **phpMyAdmin**: interfaz web para administrar bases de datos MySQL.
- **WordPress**: sistema de gestión de contenido (CMS) para crear sitios web.

Gracias a **Docker**, se pueden desplegar estos servicios como contenedores individuales conectados mediante una red interna, lo que simula un entorno de servidor real para desarrollo y pruebas.

El flujo general de la práctica incluye:
1. Crear una red personalizada en Docker.
2. Crear un volumen para persistir datos.
3. Levantar un contenedor de MySQL con credenciales definidas.
4. Levantar un contenedor de phpMyAdmin conectado a MySQL.
5. Levantar un contenedor de WordPress conectado a MySQL.

## 4. Conocimientos previos

Para realizar esta práctica el estudiante necesita:
- Saber usar comandos básicos de **Docker** (`docker run`, `docker ps`, `docker network`, etc.).
- Tener nociones de bases de datos, en particular **MySQL**.
- Conocer el uso básico de **phpMyAdmin**.
- Tener una idea general del funcionamiento de **WordPress**.

## 5. Objetivos a alcanzar

- Crear contenedores Docker para **MySQL**, **phpMyAdmin** y **WordPress**.
- Configurar la red entre los contenedores para su comunicación.
- Acceder a WordPress para completar su instalación web.
- Usar phpMyAdmin para visualizar y gestionar las bases de datos de WordPress.

## 6. Equipo necesario

- Computadora con **Windows/Linux/Mac**.
- **Docker Desktop** instalado.
- Versión de Docker 20.10 o superior.
- Conexión a Internet para descargar imágenes.
- Terminal o PowerShell.

## 7. Material de apoyo

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Documentación oficial de WordPress](https://wordpress.org/support/)
- [Documentación oficial de phpMyAdmin](https://www.phpmyadmin.net/docs/)

## 8. Procedimiento

### Paso 1: Crear una red personalizada en Docker
```bash
docker network create wordpress-net
```
<img src = "WORDPRES/Captura de pantalla 2025-04-30 152545.png" width = "400">

## Paso 2: Crear un volumen para persistir datos (opcional pero recomendado)

```bash
docker volume create wordpress-data
```
<img src = "WORDPRES/Captura de pantalla 2025-04-30 152545.png" width = "400">

## Paso 3: Crear el contenedor de MySQL

```bash
docker run -d --name mysql-container \
  --network wordpress-net \
  -e MYSQL_ROOT_PASSWORD=mi_contraseña_segura \
  -e MYSQL_DATABASE=wordpress \
  -p 3306:3306 \
  mysql:latest

  ```
<img src = "WORDPRES/Captura de pantalla 2025-04-30 152641.png" width = "400">

  ## Paso 4: Crear el contenedor de phpMyAdmin

```bash
docker run -d --name phpmyadmin-container \
  --network wordpress-net \
  -e PMA_HOST=mysql-container \
  -p 8080:80 \
  phpmyadmin/phpmyadmin
```
<img src = "WORDPRES/Captura de pantalla 2025-04-30 152735.png" width = "400">

## Paso 5: Crear el contenedor de WordPress

```bash
docker run -d --name wordpress-container \
  --network wordpress-net \
  -e WORDPRESS_DB_HOST=mysql-container:3306 \
  -e WORDPRESS_DB_USER=root \
  -e WORDPRESS_DB_PASSWORD=mi_contraseña_segura \
  -e WORDPRESS_DB_NAME=wordpress \
  -p 8000:80 \
  wordpress:latest

```
<img src = "WORDPRES/Captura de pantalla 2025-04-30 153341.png" width = "400">

## Paso 6: Acceder a las aplicaciones

- **WordPress**: [http://localhost:8000](http://localhost:8000)

  <img src = "WORDPRES/Captura de pantalla 2025-04-30 161212.png" width = "400">

  
- **phpMyAdmin**: [http://localhost:8080](http://localhost:8080)


  <img src = "WORDPRES/Captura de pantalla 2025-04-30 152820.png" width = "400">

Inicia sesión en **phpMyAdmin** con:
- **Usuario**: `root`
- **Contraseña**: `mi_contraseña_segura`
- **Servidor**: `mysql-container`

---

<img src = "WORDPRES/Captura de pantalla 2025-04-30 164527.png" width = "400">

## Paso 7: Completar la instalación de WordPress

Accede a WordPress en el navegador, elige idioma, configura el título del sitio, usuario, contraseña y correo electrónico.

---
<img src = "WORDPRES/Captura de pantalla 2025-04-30 161336.png" width = "400">

<img src = "WORDPRES/Captura de pantalla 2025-04-30 164446.png" width = "400">

## 9. Resultados esperados

Al completar los pasos:
- WordPress estará disponible en el puerto **8000**.
- phpMyAdmin estará disponible en el puerto **8080**.
- phpMyAdmin mostrará la base de datos **wordpress** y permitirá administrarla gráficamente.
- WordPress estará listo para crear publicaciones, páginas y personalizaciones.

---

## 🔊 Audio Explicativo del proyecto

https://drive.google.com/file/d/1-vHjz3bZA-30u6mHOAcPhXm3z_XqdvC4/view?usp=sharing

---

## 10. Bibliografía

- Docker, Inc. (2025). *Docker Documentation*. [https://docs.docker.com/](https://docs.docker.com/)
- WordPress.org (2025). *WordPress Support*. [https://wordpress.org/support/](https://wordpress.org/support/)
- phpMyAdmin (2025). *phpMyAdmin Documentation*. [https://www.phpmyadmin.net/docs/](https://www.phpmyadmin.net/docs/)


