# 🐶 Tienda Perritos DevOps

Proyecto desarrollado para la Evaluación Parcial 3 de la asignatura **Introducción a Herramientas DevOps (ISY1101)**.

El proyecto implementa una arquitectura basada en **Amazon EKS**, utilizando Kubernetes para la orquestación de contenedores, GitHub Actions para la automatización del despliegue y Amazon ECR como repositorio de imágenes Docker.

---

# 👥 Integrantes

- Lukas Meza
- Christian Sandoval

---

# 📌 Tecnologías utilizadas

- Amazon Web Services (AWS)
- Amazon EKS
- Amazon ECR
- Docker
- Kubernetes
- GitHub Actions
- MySQL
- HTML
- JavaScript
- Node.js
- Nginx

---

# 🏗 Arquitectura

```
Usuario
   │
   ▼
LoadBalancer (Frontend)
   │
   ▼
Frontend (Nginx)
   │
   ▼
Backend (Node.js)
   │
   ▼
MySQL
```

Todos los componentes se ejecutan dentro de un clúster de Amazon EKS.

---

# 📂 Estructura del proyecto

```
tienda-perritos-devops-deploy/

├── .github/
│   └── workflows/
│       └── deploy-eks.yml
│
├── backend/
│   ├── Dockerfile
│   ├── package.json
│   └── server.js
│
├── frontend/
│   ├── Dockerfile
│   ├── default.conf
│   ├── index.html
│   └── app.js
│
├── db/
│   ├── init.sql
│   └── Dockerfile
│
├── k8s/
│   ├── backend.yaml
│   ├── frontend.yaml
│   ├── db.yaml
│   ├── service.yaml
│   ├── secret.yaml
│   ├── namespace.yaml
│   └── hpa.yaml
│
└── README.md
```

---

# 🚀 Despliegue

El proyecto utiliza GitHub Actions para automatizar el despliegue.

Cada vez que se realiza un **push** a la rama configurada para el workflow:

1. Se construyen las imágenes Docker.
2. Se publican en Amazon ECR.
3. Se actualizan los Deployments del clúster EKS.
4. Kubernetes realiza un Rolling Update sin detener la aplicación.

---

# ☁ Amazon EKS

El clúster fue configurado con:

- Amazon EKS
- Node Group administrado
- Instancias t3.medium
- VPC dedicada
- Subredes públicas y privadas
- IAM Roles
- Security Groups

---

# 📦 Kubernetes

Se utilizaron los siguientes recursos:

- Namespace
- Deployments
- Services
- Secrets
- Horizontal Pod Autoscaler
- Rolling Update

---

# 🔐 Gestión de Secrets

Las credenciales de la base de datos se administran mediante **Kubernetes Secrets**, evitando incorporar información sensible directamente en el código fuente.

Variables utilizadas:

- DB_HOST
- DB_NAME
- DB_USER
- DB_PASSWORD
- MYSQL_ROOT_PASSWORD

> **Importante:** Para fines académicos, el archivo `secret.yaml` contiene valores de ejemplo. En un entorno productivo se recomienda utilizar GitHub Secrets o AWS Secrets Manager.

---

# 📈 Escalabilidad

El Backend implementa un **Horizontal Pod Autoscaler (HPA)**.

Configuración:

- Mínimo: 1 réplica
- Máximo: 5 réplicas
- Umbral CPU: 70%

Esto permite incrementar automáticamente la cantidad de Pods cuando aumenta la carga del sistema.

---

# 🔄 Pipeline CI/CD

El flujo implementado es:

```
Commit
      │
      ▼
GitHub Actions
      │
      ▼
Docker Build
      │
      ▼
Push Amazon ECR
      │
      ▼
kubectl apply
      │
      ▼
Amazon EKS
```

---

# ✅ Validación

Durante las pruebas se verificó:

- Correcto despliegue del Frontend.
- Comunicación Frontend → Backend.
- Conectividad con MySQL.
- Ejecución correcta del Pipeline.
- Estado de los Pods.
- Estado de los Services.
- Correcta creación del HPA.

Comandos utilizados:

```bash
kubectl get pods
kubectl get svc
kubectl get deployments
kubectl get hpa
kubectl describe hpa
kubectl logs
```

---

# ▶ Ejecución

Una vez desplegado el proyecto:

Acceder al Frontend mediante la IP o DNS del servicio LoadBalancer.

El Backend expone la API utilizada por el Frontend para consultar los productos almacenados en MySQL.

---

# 📸 Evidencias

Las capturas del proceso de implementación se encuentran documentadas en el informe entregado junto al proyecto.

Incluyen:

- Creación del clúster EKS
- Configuración de Node Group
- Creación del Namespace
- Deployments
- Services
- Secrets
- HPA
- GitHub Actions
- Amazon ECR
- Validación funcional

---

# 📚 Conclusión

La solución implementada demuestra la aplicación de herramientas DevOps para automatizar el despliegue de aplicaciones contenerizadas en la nube.

Se logró implementar:

- Orquestación mediante Kubernetes.
- Automatización CI/CD con GitHub Actions.
- Almacenamiento de imágenes en Amazon ECR.
- Gestión de credenciales mediante Kubernetes Secrets.
- Escalabilidad mediante Horizontal Pod Autoscaler.
- Despliegue continuo sobre Amazon EKS.
