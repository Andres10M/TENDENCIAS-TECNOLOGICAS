# Práctica: Configuración de un Proyecto Angular en Linux (WSL)

## 1. Título

**Configuración y Ejecución de un Proyecto Angular en WSL2**

## 2. Tiempo de duración

Aproximadamente **90 minutos**.

## 3. Fundamentos

Para desarrollar aplicaciones modernas con Angular, es importante comprender el entorno de desarrollo y las herramientas necesarias. En este caso, usaremos **WSL2** (*Windows Subsystem for Linux*), que permite ejecutar un sistema Linux dentro de Windows sin necesidad de una máquina virtual.

**Angular** es un framework de desarrollo basado en TypeScript que permite la creación de aplicaciones web SPA (*Single Page Applications*). Se ejecuta en un entorno Node.js y usa paquetes gestionados por npm (*Node Package Manager*).

 - Captura: 

<img src = "Linux/Captura de pantalla 2025-04-02 205826.png" width = "500">
### Conceptos clave:

- **WSL2**: Permite ejecutar Linux dentro de Windows sin virtualización pesada.
- **Ubuntu**: Es una distribución de Linux utilizada en este entorno.
- **Node.js**: Plataforma que permite la ejecución de JavaScript en el backend.
- **Angular CLI**: Herramienta de línea de comandos para la creación y gestión de proyectos Angular.

(Se incluirán imágenes explicativas de cada concepto)

## 4. Conocimientos previos

Para realizar esta práctica, el estudiante necesita conocer:

- Comandos básicos de Linux.
- Uso de terminal en Windows.
- Conceptos de desarrollo web.
- Instalación de software en Linux.

## 5. Objetivos a alcanzar

- Configurar y ejecutar un proyecto Angular en Linux usando WSL2.
- Comprender la instalación y configuración de **Node.js** y **Angular CLI**.
- Servir una aplicación Angular en `localhost:4200` desde un entorno Linux dentro de Windows.

## 6. Equipo necesario

- Computador con **Windows 10/11**.
- **WSL2** habilitado con **Ubuntu** instalado.
- **Node.js** y **npm** instalados.
- **Angular CLI** instalado.

## 7. Material de apoyo

- [Documentación de Angular](https://angular.io/)
- [Documentación de WSL](https://learn.microsoft.com/en-us/windows/wsl/)
- Guía de comandos básicos de Linux.

## 8. Procedimiento

### Paso 1: Instalar WSL2 y Ubuntu
Ejecutar en **PowerShell**:

```sh
wsl --install -d Ubuntu
```

### Paso 2: Instalar Node.js y npm
Ejecutar en la terminal de **Ubuntu**:

```sh
sudo apt update && sudo apt upgrade -y
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
node -v  # Verificar versión
npm -v   # Verificar versión
```

### Paso 3: Instalar Angular CLI

```sh
npm install -g @angular/cli
ng version
```

### Paso 4: Crear un proyecto Angular

```sh
ng new linux-angular
cd linux-angular
```

### Paso 5: Ejecutar el servidor de desarrollo

```sh
ng serve
```

**Figura 1-1:** Captura de pantalla del servidor corriendo en `localhost:4200`.

## 9. Resultados esperados

- Instalación correcta de **WSL2** con **Ubuntu**.
- Instalación de **Node.js**, **npm** y **Angular CLI**.
- Creación y ejecución exitosa de un proyecto Angular.
- Visualización de la aplicación en el navegador en `localhost:4200`.

## 10. Bibliografía

- Angular Developers. (s.f.). *Angular Documentation*. Recuperado de [https://angular.io/docs](https://angular.io/docs)
- Microsoft. (s.f.). *Windows Subsystem for Linux Documentation*. Recuperado de [https://learn.microsoft.com/en-us/windows/wsl/](https://learn.microsoft.com/en-us/windows/wsl/)
