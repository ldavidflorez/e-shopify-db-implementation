# E-Shopify Database Implementation

## Descripción

Este proyecto implementa la base de datos para el caso de estudio E-Shopify, un sistema de comercio electrónico. La implementación utiliza PostgreSQL como sistema de gestión de bases de datos relacionales (RDBMS) y Docker para la contenerización y despliegue automático.

El proyecto incluye:
- Esquema de base de datos normalizado en 3FN/BCNF
- Scripts SQL para creación de tablas, relaciones y datos de prueba
- Consultas SQL de validación
- Configuración Docker completa
- Informe académico detallado

## Prerrequisitos

Antes de ejecutar el proyecto, asegúrate de tener instalados:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)
- Git (opcional, para clonar el repositorio)

## Instalación y Configuración

1. **Clona el repositorio** (si aplica):
   ```bash
   git clone <url-del-repositorio>
   cd <directorio-del-proyecto>
   ```

2. **Navega al directorio src**:
   ```bash
   cd src
   ```

3. **Inicia los contenedores**:
   ```bash
   docker-compose up --build -d
   ```

   Este comando:
   - Construirá las imágenes de PostgreSQL y pgAdmin
   - Iniciará los contenedores
   - Creará automáticamente la base de datos y cargará los datos de prueba

4. **Verifica que los contenedores estén ejecutándose**:
   ```bash
   docker ps
   ```

   Deberías ver dos contenedores: `e-shopify-db` (PostgreSQL) y `e-shopify-pgadmin` (pgAdmin).

## Acceso a la Base de Datos

### Conexión Directa
- **Host:** localhost
- **Puerto:** 5432
- **Usuario:** postgres
- **Contraseña:** password
- **Base de datos:** e_shopify_db

### A través de pgAdmin
- Abre tu navegador en: http://localhost:8080
- **Usuario:** admin@example.com
- **Contraseña:** admin

### Conexión desde Terminal
```bash
docker exec -it e-shopify-db psql -U postgres -d e_shopify_db
```

## Estructura del Proyecto

```
src/
├── docker-compose.yml          # Configuración de contenedores Docker
├── e-shopify-db.sql           # Script SQL completo de referencia
├── init.sql                   # Script SQL optimizado para inicialización Docker
├── informe.md                 # Informe académico completo
├── images/                    # Imágenes y diagramas
│   ├── admin_panel.png
│   ├── connection_config.png
│   ├── der_eshopify-V2.drawio.svg
│   ├── docker_ps.png
│   ├── order_data.png
│   ├── products_data.png
│   ├── tables_pgadmin.png
│   └── user_data.png
└── README.md                  # Este archivo
```

## Uso

### Ejecutar Consultas
Una vez conectada la base de datos, puedes ejecutar las consultas SQL incluidas en `e-shopify-db.sql` o directamente en pgAdmin.

Ejemplos de consultas disponibles:
1. Productos por categoría
2. Detalles de pedidos
3. Producto más caro
4. Carrito de compras por usuario
5. Productos con alta calificación
6. Vendedores con más productos vendidos

### Ver el Informe
El archivo `informe.md` contiene el informe académico completo con:
- Metodología de implementación
- Detalles técnicos
- Resultados de consultas
- Imágenes ilustrativas
- Conclusiones

## Diagrama ER

El diagrama Entidad-Relación completo se encuentra en `der_eshopify-V2.drawio.svg`. Puedes abrirlo con Draw.io o cualquier visor SVG.

## Datos de Prueba

La base de datos incluye datos de prueba para:
- Usuarios
- Múltiples productos en diferentes categorías
- Pedidos y detalles de pedidos
- Reseñas y calificaciones
- Datos de inventario

## Detener los Contenedores

Para detener la base de datos:
```bash
docker-compose down
```

Para detener y eliminar volúmenes (datos persistentes):
```bash
docker-compose down -v
```

## Solución de Problemas

### Puerto 5432 ocupado
Si el puerto 5432 está en uso, modifica el puerto en `docker-compose.yml`:
```yaml
ports:
  - "5433:5432"  # Cambia 5432 por otro puerto disponible
```

### Puerto 8080 ocupado
Para pgAdmin:
```yaml
ports:
  - "8081:80"  # Cambia 8080 por otro puerto disponible
```