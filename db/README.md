# Tienda de Alimentos para Perritos - Database (MySQL)

Repositorio para la gestión de la persistencia de datos de la aplicación.

## 🚀 Tecnologías Utilizadas
* **Motor:** MySQL 8.0
* **Docker:** Imagen oficial de MySQL sobre Alpine/Debian.
* **Persistencia:** Implementación de **Named Volumes** de Docker.

## 💾 Persistencia de Datos (Pauta IE4)
Para garantizar que los datos de los productos no se pierdan al reiniciar el contenedor, se utiliza un volumen nombrado:
```bash
docker run -d \
  --name tienda-db \
  -p 3306:3306 \
  -v db_data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=root_pass \
  [TU_URL_ECR_DB]:latest
