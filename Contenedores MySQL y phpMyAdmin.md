# Contenedores MySQL y phpMyAdmin

## 1. Título
**Creación de Contenedores MySQL y phpMyAdmin en Docker y Configuración de Red para Comunicación**

## 2. Tiempo de duración
Aproximadamente 45 minutos.

## 3. Fundamentos:

El uso de **contenedores Docker** ha transformado la forma en que desarrolladores y administradores de sistemas manejan aplicaciones. Docker permite crear, ejecutar y administrar aplicaciones en entornos aislados llamados **contenedores**, los cuales funcionan de manera consistente sin importar el sistema operativo subyacente. Esto facilita la administración y escalabilidad de aplicaciones complejas.

En esta práctica, se trabajó con dos aplicaciones populares en el ecosistema web: **MySQL** y **phpMyAdmin**. 

- **MySQL** es un sistema de gestión de bases de datos relacional que permite almacenar y gestionar datos estructurados. 
- **phpMyAdmin** es una herramienta escrita en PHP destinada a gestionar bases de datos MySQL a través de una interfaz web.

**Docker** ofrece la posibilidad de usar contenedores para crear entornos de desarrollo y producción aislados, lo que facilita la configuración, despliegue y escalabilidad de las aplicaciones. En esta práctica, se creó una red personalizada en Docker para permitir la comunicación entre dos contenedores: uno con MySQL y otro con phpMyAdmin.

El flujo general de la práctica incluye:
1. Crear una red personalizada en Docker.
2. Levantar un contenedor de MySQL, configurando las credenciales.
3. Levantar un contenedor de phpMyAdmin, configurando las credenciales y estableciendo la conexión con el contenedor de MySQL.
4. Crear una base de datos de prueba utilizando la interfaz gráfica de phpMyAdmin.



## 4. Conocimientos previos.

Para realizar esta práctica el estudiante necesita tener claro los siguientes temas:
- Uso básico de **Docker**: crear y gestionar contenedores, redes y volúmenes.
- **Comandos básicos de Linux**: como `docker run`, `docker ps`, `docker network`, etc.
- Comprensión de conceptos básicos de bases de datos, especialmente **MySQL**.
- Conocimiento básico de **phpMyAdmin** como interfaz para gestionar bases de datos MySQL.

## 5. Objetivos a alcanzar

- Crear contenedores Docker para **MySQL** y **phpMyAdmin**.
- Configurar la red entre contenedores para permitir su comunicación.
- Utilizar **phpMyAdmin** para gestionar una base de datos MySQL.
- Crear una base de datos de prueba desde la interfaz de phpMyAdmin.

## 6. Equipo necesario:

- Computador con sistema operativo **Windows/Linux/Mac**.
- **Docker Desktop** instalado en el sistema.
- **Docker** versión 20.10 o superior.
- Conexión a Internet para descargar las imágenes de Docker.
- Acceso al terminal o línea de comandos.

## 7. Material de apoyo.

- [Documentación oficial de Docker](https://docs.docker.com/)
- Guía de asignatura.
- **Cheat Sheet** de Docker.
- Tutoriales básicos de MySQL y phpMyAdmin.

## 8. Procedimiento

### Paso 1: Crear una red personalizada en Docker
Ejecutar el siguiente comando para crear una red personalizada que permita la comunicación entre los contenedores:

```bash
sudo docker network create mi_red

```
<img src = "docker base/Captura de pantalla 2025-04-23 164218.png" width = "400">

### Paso 2: Crear el contenedor de MySQL
Ejecutar el siguiente comando para crear el contenedor de MySQL, definiendo las credenciales de acceso:

```bash
sudo docker run --name mysql-container --network mi_red -e MYSQL_ROOT_PASSWORD=rootpassword -d mysql:latest
```

<img src = "docker base/Captura de pantalla 2025-04-23 164218.png" width = "400">

docker base/Captura de pantalla 2025-04-23 164227.png

### Paso 3: Crear el contenedor de phpMyAdmin
Ejecutar el siguiente comando para crear el contenedor de phpMyAdmin, configurando las credenciales de acceso a la base de datos MySQL:

```bash
sudo docker run --name phpmyadmin-container --network mi_red -d -p 8080:80 phpmyadmin/phpmyadmin
```

<img src = "docker base/Captura de pantalla 2025-04-23 164227.png" width = "400">


### Paso 4: Acceder a phpMyAdmin
Abrir el navegador y acceder a [http://localhost:8080](http://localhost:8080). Iniciar sesión con las siguientes credenciales:

- **Usuario**: `root`
- **Contraseña**: `rootpassword`
- **Servidor**: `mysql-container`

---

<img src = "docker base/Captura de pantalla 2025-04-23 163356.png" width = "400">


### Paso 5: Crear una base de datos de prueba
Una vez dentro de phpMyAdmin, podrás crear una base de datos de prueba desde la interfaz gráfica.

**Figura 1-2**: Interfaz de phpMyAdmin para la creación de bases de datos.

---

<img src = "docker base/Captura de pantalla 2025-04-23 163829.png" width = "400">

## 9. Resultados esperados

Al completar los pasos anteriores, deberías poder:

- Acceder a phpMyAdmin en [http://localhost:8080](http://localhost:8080)
- Iniciar sesión con el usuario y contraseña configurados
- Crear una base de datos de prueba en MySQL

  ## 🔊 Audio Explicativo del proyecto Nginx usando Docker
https://drive.google.com/file/d/1qaPFPWd0cJNMswMb0ZCt5gNy18vn9A4W/view?usp=sharing

## 10. Bibliografía

- Docker, Inc. (2021). *Docker Documentation*. Recuperado de: [https://docs.docker.com/](https://docs.docker.com/)
- MySQL, Inc. (2021). *MySQL Documentation*. Recuperado de: [https://dev.mysql.com/doc/](https://dev.mysql.com/doc/)
- phpMyAdmin. (2021). *phpMyAdmin Documentation*. Recuperado de: [https://www.phpmyadmin.net/docs/](https://www.phpmyadmin.net/docs/)


