# 🐶 Tienda Perritos DevOps

Proyecto desarrollado para la asignatura **Introducción a Herramientas DevOps**, cuyo objetivo es implementar una arquitectura basada en contenedores utilizando Docker, Kubernetes y Amazon Web Services (AWS), automatizando el proceso de integración y despliegue continuo mediante GitHub Actions.

---

# 📋 Integrantes

- **Lukas Meza**
- **Christian Sandoval**
- Ingeniería en Informática
- Introducción a Herramientas DevOps

---

# 🎯 Objetivos

- Contenerizar una aplicación Full Stack.
- Automatizar la construcción de imágenes Docker.
- Publicar imágenes en Amazon Elastic Container Registry (ECR).
- Desplegar automáticamente la aplicación en Amazon Elastic Kubernetes Service (EKS).
- Implementar alta disponibilidad mediante múltiples réplicas.
- Configurar escalado automático (Horizontal Pod Autoscaler).
- Gestionar información sensible mediante Kubernetes Secrets.
- Aplicar buenas prácticas DevOps utilizando un pipeline CI/CD.

---

# 🏗 Arquitectura

```
                    GitHub
                       │
                 Push a main
                       │
                       ▼
              GitHub Actions CI/CD
                       │
        ┌──────────────┴──────────────┐
        │                             │
        ▼                             ▼
 Build imágenes Docker         Ejecuta Pipeline
        │
        ▼
 Amazon Elastic Container Registry (ECR)
        │
        ▼
 Amazon Elastic Kubernetes Service (EKS)
        │
 ┌──────┴─────────┐
 │                │
 ▼                ▼
Frontend      Backend
 (Nginx)      (Node.js)
                   │
                   ▼
               MySQL 8
```

---

# 🛠 Tecnologías utilizadas

- Docker
- Docker Hub / Amazon ECR
- Kubernetes
- Amazon EKS
- Amazon EC2
- Amazon IAM
- Amazon VPC
- GitHub Actions
- Node.js
- Express
- MySQL 8
- Nginx

---

# 📁 Estructura del proyecto

```
tienda-perritos-devops
│
├── backend/
│   ├── Dockerfile
│   ├── package.json
│   └── server.js
│
├── frontend/
│   ├── Dockerfile
│   ├── app.js
│   ├── index.html
│   └── default.conf
│
├── database/
│   ├── Dockerfile
│   └── init.sql
│
├── k8s/
│   ├── namespace.yaml
│   ├── secret.yaml
│   ├── mysql.yaml
│   ├── backend.yaml
│   ├── frontend.yaml
│   ├── hpa-backend.yaml
│   └── hpa-frontend.yaml
│
├── .github/
│   └── workflows/
│       └── deploy-eks.yml
│
└── README.md
```

---

# 🐳 Contenedores

El proyecto está compuesto por tres contenedores:

## Backend

- Node.js
- Express
- API REST
- Puerto 3001

## Frontend

- Nginx
- HTML
- JavaScript
- Puerto 80

## Base de datos

- MySQL 8
- Puerto 3306

---

# ☁ Infraestructura AWS

La infraestructura fue implementada utilizando:

- Amazon EKS
- Amazon ECR
- Amazon IAM
- Amazon VPC
- Security Groups
- Auto Scaling
- Kubernetes Services
- Kubernetes Deployments

---

# 🚀 Pipeline CI/CD

Cada vez que se realiza un **Push** hacia la rama principal del repositorio:

1. GitHub Actions inicia automáticamente el pipeline.
2. Se construyen las imágenes Docker.
3. Las imágenes se publican en Amazon ECR.
4. Se actualiza el kubeconfig.
5. Kubernetes despliega automáticamente los cambios.
6. Los Pods son reiniciados con la nueva versión.

---

# 🔐 Gestión de Secrets

Las credenciales sensibles no se almacenan dentro del código fuente.

Se utilizan:

- GitHub Secrets
- Kubernetes Secrets

para administrar:

- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_SESSION_TOKEN
- Credenciales MySQL

---

# 📈 Alta disponibilidad

Para garantizar la disponibilidad del servicio se configuraron múltiples réplicas.

| Servicio | Réplicas |
|----------|---------:|
| Frontend | 2 |
| Backend | 2 |

---

# 📊 Escalado automático

Se implementó Horizontal Pod Autoscaler (HPA).

Configuración utilizada:

- Réplicas mínimas: 2
- Réplicas máximas: 5
- CPU objetivo: 70%

---

# ▶ Despliegue

Aplicar todos los manifiestos Kubernetes:

```bash
kubectl apply -f k8s/
```

Verificar Pods:

```bash
kubectl get pods
```

Verificar Servicios:

```bash
kubectl get svc
```

Verificar Deployments:

```bash
kubectl get deployments
```

Verificar Horizontal Pod Autoscaler:

```bash
kubectl get hpa
```

---

# 📌 Endpoints

## Frontend

```
http://<LOAD_BALANCER>
```

## Backend

```
http://<LOAD_BALANCER>/api/productos
```

---

# 📋 Funcionalidades

- Obtener productos
- Buscar producto por ID
- Crear productos
- Actualizar productos
- Eliminar productos
- Health Check
- Comunicación Frontend ↔ Backend
- Persistencia en MySQL

---

# 📷 Evidencias recomendadas

Agregar capturas de:

- Clúster EKS
- Node Group
- Pods en ejecución
- Servicios Kubernetes
- Horizontal Pod Autoscaler
- GitHub Actions exitoso
- Amazon ECR
- Aplicación funcionando

---

# 📖 Buenas prácticas implementadas

- Contenedores independientes
- Arquitectura desacoplada
- Integración Continua (CI)
- Despliegue Continuo (CD)
- Uso de Secrets
- Alta disponibilidad
- Escalado automático
- Infraestructura en AWS
- Orquestación con Kubernetes

---

# 👨‍💻 Autor

**Lukas Meza**
**Christian Sandoval**

Ingeniería en Informática

Introducción a Herramientas DevOps

2026
