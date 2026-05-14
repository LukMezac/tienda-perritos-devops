# Tienda de Alimentos para Perritos - Backend API

API de microservicios que gestiona la lógica de negocio y la conexión con la base de datos MySQL.

## 🚀 Tecnologías Utilizadas
* **Lenguaje:** Node.js / Express
* **Docker:** Imagen base `node:18-alpine`.
* **Seguridad:** Variables de entorno para credenciales de BD.
* **Red:** Expone el puerto `3000`.

## ⚙️ Configuración de Variables de Entorno
El backend requiere las siguientes variables para conectar con la base de datos:
* `DB_HOST`: IP Privada de la instancia ec2-db.
* `DB_USER`: usuario_tienda
* `DB_PASSWORD`: password_seguro
* `DB_NAME`: tienda_perritos

## 📦 Ejecución
```bash
docker run -d -p 3000:3000 \
  -e DB_HOST=[IP_PRIVADA_DB] \
  --name tienda-backend [TU_URL_ECR_BACKEND]:latest
