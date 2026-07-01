# Front Despacho - Innovatech Chile

Frontend del sistema de gestión de despachos para el caso Innovatech Chile.  
La aplicación permite visualizar información relacionada con órdenes de compra y órdenes de despacho, consumiendo los servicios backend de ventas y despachos.

## Tecnologías utilizadas

- React
- Vite
- Axios
- Tailwind CSS
- Docker
- Nginx
- AWS ECS Fargate
- Application Load Balancer
- GitHub Actions

## Arquitectura del sistema

La solución está compuesta por tres componentes principales:

- Frontend: aplicación React/Vite servida con Nginx.
- Backend Ventas: API REST desarrollada con Spring Boot.
- Backend Despachos: API REST desarrollada con Spring Boot.

En el despliegue en AWS, el frontend se publica como un servicio independiente en ECS Fargate.  
El acceso público se realiza mediante un Application Load Balancer, el cual redirige las solicitudes según la ruta utilizada.

## Rutas utilizadas en AWS

El Application Load Balancer centraliza el acceso a la aplicación:

- Frontend: `/`
- Backend Ventas: `/api/v1/ventas`
- Backend Despachos: `/api/v1/despachos`
- Health Ventas: `/api/v1/ventas/health`
- Health Despachos: `/api/v1/despachos/health`

## Ejecución local con npm

Instalar dependencias:

```bash
npm install