# Tienda de Alimentos para Perritos - Frontend

Este repositorio contiene la interfaz de usuario de la aplicación "Tienda de Perritos", desarrollada para la Evaluación Parcial N°2 de DevOps.

## 🚀 Tecnologías Utilizadas
* **Framework:** React / Node.js
* **Docker:** Imagen base `node:alpine` para optimización de recursos.
* **Cloud:** Desplegado en Amazon EC2.
* **CI/CD:** GitHub Actions con despliegue automático en rama `deploy`.

## 📦 Dockerización
El proyecto utiliza un **Dockerfile multi-stage** para reducir el tamaño de la imagen final y mejorar la seguridad:
1. **Stage 1 (Build):** Compilación de la aplicación.
2. **Stage 2 (Production):** Servido mediante un servidor ligero.

## 🛠️ Despliegue
Para levantar el contenedor manualmente:
```bash
docker pull [TU_URL_ECR_FRONTEND]:latest
docker run -d -p 80:80 --name tienda-frontend [TU_URL_ECR_FRONTEND]:latest
