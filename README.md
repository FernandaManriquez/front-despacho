Front Despacho

Frontend del sistema de gestión de despachos desarrollado con React y Vite.
Este proyecto fue contenedorizado con Docker, publicado en Docker Hub y desplegado en una instancia EC2 de AWS como parte de la Evaluación Parcial N°2 de Introducción a Herramientas DevOps.

Tecnologías utilizadas
React
Vite
JavaScript
Docker
Docker Compose
Docker Hub
GitHub Actions
AWS EC2
Repositorio
https://github.com/FernandaManriquez/front-despacho
Imagen en Docker Hub
ninii04/front-despacho:latest
Puerto utilizado
5173
Descripción del proyecto

Este frontend permite visualizar el dashboard principal del sistema de despachos.

Desde la interfaz se pueden:

Consultar órdenes de compra.
Consultar órdenes de despacho.
Comunicarse con los microservicios backend desplegados en AWS EC2.

El frontend fue desplegado en una instancia EC2 pública utilizando Docker y Docker Compose.

Arquitectura general
Usuario / Navegador
        |
        v
Frontend React + Vite
EC2 pública - Puerto 5173
        |
        v
Backend Despachos - Puerto 8081
Backend Ventas - Puerto 8082
Ejecución local

Instalar dependencias:

npm install

Ejecutar aplicación:

npm run dev

Aplicación disponible en:

http://localhost:5173
Construcción de imagen Docker
docker build -t front-despacho .
Ejecución con Docker
docker run -p 5173:5173 front-despacho
Docker Compose utilizado en EC2

Archivo docker-compose.yml utilizado para desplegar el frontend:

services:
  frontend:
    image: ninii04/front-despacho:latest
    container_name: front-despacho
    restart: always
    ports:
      - "5173:5173"
Instalación de Docker en EC2
sudo dnf update -y
sudo dnf install docker -y
sudo systemctl start docker
sudo systemctl enable docker
Instalación de Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
Creación de carpeta de despliegue
mkdir -p app
cd app
Levantamiento del contenedor
sudo docker-compose up -d

Verificación de contenedores:

sudo docker ps
Actualización del contenedor
sudo docker-compose pull

sudo docker-compose down

sudo docker-compose up -d
CI/CD con GitHub Actions

El proyecto utiliza GitHub Actions para automatizar la construcción y publicación de imágenes Docker.

El workflow se ejecuta automáticamente al realizar push sobre la rama:

deploy
Pipeline implementado

El pipeline realiza automáticamente:

Checkout del repositorio.
Login en Docker Hub.
Build de la imagen Docker.
Push de la imagen hacia Docker Hub.
Secrets utilizados
DOCKER_HUB_USERNAME
DOCKER_HUB_TOKEN

Estos secrets fueron configurados dentro de GitHub Actions para autenticar Docker Hub de forma segura.

Comunicación con backend

El frontend consume los siguientes endpoints públicos desplegados en EC2:

Backend Despachos:
http://3.238.144.162:8081

Backend Ventas:
http://3.238.144.162:8082
Evidencias de funcionamiento

Se verificó correctamente:

Imagen publicada en Docker Hub.
Pipeline ejecutado exitosamente en GitHub Actions.
Contenedor ejecutándose en AWS EC2.
Frontend accesible desde navegador mediante IP pública.
Comunicación entre frontend y backend.
Consideraciones

El frontend quedó desplegado exitosamente utilizando contenedores Docker y Docker Compose.

La arquitectura permitió separar frontend y backend en distintas instancias EC2, simulando un entorno distribuido basado en microservicios y herramientas DevOps.
