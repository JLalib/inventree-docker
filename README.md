# 📦 Inventree - Gestión de Inventario Profesional con Docker

![Inventree Logo](https://blogger.googleusercontent.com/img/a/AVvXsEixx4fTlCsU-vZDl5vniPD_oraaWXcG-fIR_PdlL0T0sEM9-jYYpO4Qg7rGRWguHhunDLSQLFjHgo4xOjnxBCCj17jAYHz-khO5qiW6pGkXN-q0IDmSf_E5KhFLKwoC_W3kNQiD9Bs04s4MwIWnL97bb6ls5ojFIcfjZhyNXRuR-GCF61Hqw5xCSrdFErM=w640-h206)

Control de stock potente, extensible y 100% bajo tu control.

## 📋 Descripción

InvenTree es un sistema de gestión de inventario de código abierto excepcionalmente potente, diseñado para ofrecer un control de stock intuitivo tanto para entornos profesionales como para aficionados a la electrónica y la fabricación. Su arquitectura está diseñada para ser extensible y capaz de integrarse con aplicaciones externas mediante una API robusta y un sistema de plugins personalizados.

Este repositorio proporciona un `docker-compose.yml` listo para desplegar InvenTree con Docker, incluyendo los servicios necesarios: aplicación, base de datos PostgreSQL, gestor de tareas Redis y proxy inverso Caddy (según la documentación oficial).

## 🛠️ Requisitos del Sistema

- Docker y Docker Compose instalados
- Al menos 2 GB de RAM recomendados
- Espacio en disco suficiente para la base de datos y los archivos de medios
- Puerto 8080 disponible (puede modificarse en el `docker-compose.yml`)

## 📦 Instalación

1. Clone este repositorio:
   ```bash
   git clone https://github.com/JLalib/inventree-docker.git
   cd inventree-docker
   ```

2. Cree el archivo `.env` (basándose en la plantilla si existe, o cree uno vacío) y configure las variables de entorno necesarias (como contraseñas de base de datos). **Importante:** No subir este archivo a GitHub.

   ```bash
   cp .env.example .env   # Si existe un ejemplo
   # o cree un archivo .env vacío y añada las variables necesarias manualmente
   ```

3. Inicie los contenedores:
   ```bash
   docker-compose up -d
   ```

4. Espere a que los servicios estén listos (unos minutos la primera vez). Luego acceda a la interfaz web en:
   ```
   http://<IP_DEL_SERVIDOR>:8080
   ```

5. En el primer acceso, configure los parámetros globales como la moneda por defecto y las categorías principales.

## ⚙️ Configuración

- **Puertos:** La aplicación se expone en el puerto 8080 (host:contenedor). Puede cambiar el puerto del host modificando el `docker-compose.yml`.
- **Volúmenes:**
  - `./media`: Almacena archivos subidos por los usuarios (imágenes de productos, etc.).
  - `./backups`: Directorio para respaldos de la base de datos.
  - `./postgres`: Persistencia de la base de datos PostgreSQL.
  - `./redis`: Persistencia de Redis.
- **Variables de entorno:** Puede ajustar variables como `TZ`, `INVENTREE_PORT`, etc., en el archivo `.env` o directamente en el `docker-compose.yml`.

## 🔧 Primeros Pasos / Configuración

1. Acceda a `http://<IP_DEL_SERVIDOR>:8080` con un navegador.
2. Inicie sesión con las credenciales predeterminadas (consulte la documentación oficial de InvenTree para las credenciales iniciales o establezca las suyas propias mediante variables de entorno).
3. Configure la moneda, categorías, ubicaciones y otros ajustes iniciales según sus necesidades.
4. Explore la interfaz y comience a agregar productos, proveedores y pedidos.

## 🛡️ Mantenimiento

- **Logs:** Puede ver los logs de cada servicio con:
  ```bash
  docker-compose logs -f inventree
  docker-compose logs -f db
  docker-compose logs -f redis
  ```
- **Copia de seguridad:** Realice copias de seguridad periódicas de los volúmenes `postgres`, `media` y `backups`.
- **Actualización:** Para actualizar a una nueva versión de InvenTree:
  ```bash
  docker-compose pull
  docker-compose up -d
  ```
  Se recomienda hacer una copia de seguridad antes de actualizar.

## 📚 Créditos

- Este repositorio sigue el tutorial del blog de Genbyte: [InvenTree: Gestión de Inventario Profesional con Docker](https://genbyte.blogspot.com/2026/04/inventree-gestion-de-inventario.html).
- Agradecimientos al equipo de InvenTree por desarrollar y mantener este excelente software de código abierto.
- Icono y imágenes tomados del artículo original del blog.

---

**Nota de seguridad:** Este `docker-compose.yml` incluye un archivo `.env` que **no debe subirse a GitHub**. Mantenga sus credenciales y configuraciones sensibles en su entorno local y añada `.env` a su `.gitignore`.

Happy hacking! 🥧