# 🐳 Contenerización de Servidor Web con Docker

## 🎯 Objetivo del Proyecto
Modernizar el despliegue de aplicaciones pasando de un modelo de servidores virtuales tradicionales (EC2) a un modelo basado en contenedores. El objetivo es crear entornos aislados, efímeros y 100% portables.

## 🏗️ Arquitectura y Tecnologías
* **Contenedores:** Docker, Docker Engine.
* **Automatización de Imagen:** Dockerfile.
* **Servicio Web:** Apache (httpd).

## ⚙️ Proceso de Despliegue
1. Instalación de Docker en el entorno local.
2. Desarrollo de un archivo `Dockerfile` para empaquetar el sistema operativo base, el servicio web y un archivo `index.html` personalizado.
3. Construcción (Build) de la imagen personalizada.
4. Despliegue del contenedor mapeando el puerto 80 del contenedor al puerto local de la máquina host.

> **Mi Dockerfile:**
> ```dockerfile
> FROM ubuntu:latest
> RUN apt-get update && apt-get install -y apache2
> COPY index.html /var/www/html/
> EXPOSE 80
> CMD ["apache2ctl", "-D", "FOREGROUND"]
> ```

## 🛠️ Troubleshooting (Resolución de Problemas)
**Problema:** Al ejecutar el comando `docker run -p 80:80 mi-imagen`, la terminal arrojaba un error de "Bind for 0.0.0.0:80 failed: port is already allocated".
**Solución:** El puerto 80 de la máquina host ya estaba siendo utilizado por otro proceso local. Se solucionó mapeando el contenedor a un puerto externo distinto utilizando el comando `docker run -p 8080:80 mi-imagen`, logrando acceder a la web exitosamente desde `localhost:8080`.
