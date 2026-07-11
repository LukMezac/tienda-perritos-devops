# 🐶 Tienda Perritos DevOps

Proyecto desarrollado para la Evaluación Final Transversal de la asignatura **Introducción a Herramientas DevOps (ISY1101)**.

El proyecto implementa una arquitectura basada en **Amazon EKS**, utilizando Kubernetes para la orquestación de contenedores, GitHub Actions para la automatización del despliegue y Amazon ECR como repositorio de imágenes Docker.

---

## 👥 Integrantes
* Lukas Meza
* Christian Sandoval

---

## 📌 Tecnologías utilizadas
* Amazon Web Services (AWS)
* Amazon EKS & Amazon ECR
* AWS CloudWatch (Observabilidad y Métricas)
* Docker (Imágenes optimizadas Alpine)
* Kubernetes (HPA, Secrets, ClusterIP, LoadBalancer)
* GitHub Actions
* MySQL
* HTML & JavaScript
* Node.js
* Nginx

---

## 🏗 Arquitectura

```text
Usuario
   │
   ▼
LoadBalancer (Frontend / AWS)
   │
   ▼
Frontend (Nginx)
   │
   ▼
Backend (Node.js / Red Interna ClusterIP)
   │
   ▼
MySQL (Red Interna ClusterIP)

```

Todos los componentes se ejecutan dentro de un clúster de Amazon EKS aplicando el principio de mínimo privilegio.

---

## 📂 Estructura del proyecto

```text
TIENDA-PERRITOS-DEVOPS/
├── .github/
│   └── workflows/
│       └── deploy-eks.yml
├── backend/
│   ├── .dockerignore
│   ├── Dockerfile
│   ├── package.json
│   ├── README.md
│   ├── server.js
│   └── server.test.js
├── db/
│   ├── Dockerfile
│   ├── init.sql
│   └── README.md
├── frontend/
│   ├── .dockerignore
│   ├── app.js
│   ├── default.conf
│   ├── Dockerfile
│   ├── index.html
│   └── README.md
├── k8s/
│   ├── backend.yaml
│   ├── db.yaml
│   ├── frontend.yaml
│   ├── hpa.yaml
│   ├── namespace.yaml
│   └── secret.yaml
├── docker-compose.yml
└── README.md

```

---

## 🚀 Despliegue

El proyecto utiliza GitHub Actions para automatizar el despliegue. Cada vez que se realiza un push a la rama configurada para el workflow:

1. Se construyen las imágenes Docker multietapa.
2. Se publican en Amazon ECR usando el hash del commit para trazabilidad.
3. Se actualizan los Deployments del clúster EKS.
4. Kubernetes realiza un Rolling Update sin detener la aplicación.

---

## ☁ Amazon EKS

El clúster fue configurado con la siguiente infraestructura para alta disponibilidad:

* Amazon EKS
* Node Group administrado
* 3 instancias `t3.large` operando como nodos trabajadores
* VPC dedicada
* Subredes públicas y privadas
* IAM Roles
* Security Groups restrictivos

---

## 📦 Kubernetes

Se utilizaron los siguientes recursos:

* Namespace
* Deployments
* Services
* Secrets
* Horizontal Pod Autoscaler
* Rolling Update

---

## 🔐 Gestión de Secrets

Las credenciales de la base de datos se administran mediante **Kubernetes Secrets**, evitando incorporar información sensible directamente en el código fuente.

Variables utilizadas:

* `DB_HOST`
* `DB_NAME`
* `DB_USER`
* `DB_PASSWORD`
* `MYSQL_ROOT_PASSWORD`

> ⚠️ **Importante:** Para fines académicos, el archivo `secret.yaml` contiene valores de ejemplo. En un entorno productivo se recomienda utilizar GitHub Secrets o AWS Secrets Manager.

---

## 📈 Escalabilidad

El Backend implementa un **Horizontal Pod Autoscaler (HPA)**.

Configuración:

* **Mínimo:** 1 réplica
* **Máximo:** 5 réplicas
* **Umbral CPU:** 70%

Esto permite incrementar automáticamente la cantidad de Pods cuando aumenta la carga del sistema.

---

## 🔄 Pipeline CI/CD

El flujo automatizado implementado es:

```text
Commit
   │
   ▼
GitHub Actions
   │
   ▼
Docker Build & Test
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

## ✅ Validación

Durante las pruebas en la nube se verificó:

* Correcto despliegue del Frontend.
* Comunicación Frontend → Backend.
* Conectividad con MySQL.
* Ejecución correcta del Pipeline.
* Estado de los Pods.
* Estado de los Services (ClusterIP y LoadBalancer).
* Correcta creación del HPA.

Comandos utilizados para verificación:

```bash
kubectl get pods -n tienda-perritos
kubectl get svc -n tienda-perritos
kubectl get deployments -n tienda-perritos
kubectl get hpa -n tienda-perritos
kubectl describe hpa -n tienda-perritos
kubectl logs -l app=backend -n tienda-perritos

```

---

## ▶ Ejecución

Una vez desplegado el proyecto: Acceder al Frontend mediante la IP o DNS público del servicio LoadBalancer de AWS. El Backend (operando en red interna) expone la API utilizada por el Frontend para consultar los productos almacenados en MySQL.

---

## 📸 Evidencias

Las capturas del proceso de implementación y monitoreo se encuentran documentadas en el Informe Técnico Final entregado. Incluyen evidencias de:

* Diagrama de Arquitectura de EKS.
* Contenedorización local (Docker Compose y multietapa).
* GitHub Actions y Amazon ECR.
* Creación de recursos Kubernetes (Namespace, Deployments, Services, Secrets, HPA).
* Verificación funcional (URLs públicas y kubectl logs).
* Monitoreo en AWS CloudWatch.

---

## 📚 Conclusión

La solución implementada demuestra la aplicación de prácticas avanzadas de herramientas DevOps para automatizar el despliegue de aplicaciones contenerizadas en la nube. Se logró implementar:

* Orquestación segura mediante Kubernetes.
* Automatización CI/CD con GitHub Actions.
* Almacenamiento seguro de imágenes en Amazon ECR.
* Gestión de credenciales inyectadas en ejecución mediante Kubernetes Secrets.
* Escalabilidad dinámica mediante Horizontal Pod Autoscaler.
* Observabilidad en AWS CloudWatch.

```

```