# E-Shopify Database Optimization Project

**Curso:** Diseño de Bases de Datos (S4)  
**Actividad:** Optimización y Rendimiento  
**Fecha:** Febrero 2026  
**Estudiante:** Luis David Flórez Pareja  

## 📁 Estructura del Proyecto

```
e-shopify-db-optimization/
├── README.md              # Este archivo
├── docker/                 # Configuración de Docker
│   ├── docker-compose.yml
│   ├── Dockerfile.benchmark
│   └── images/            # Imágenes del proyecto
├── sql/                   # Scripts SQL
│   ├── e-shopify-db.sql           # Schema base
│   ├── e-shopify-db-optimized.sql # Schema optimizado
│   └── init.sql                   # Inicialización
├── scripts/               # Scripts de automatización
│   ├── run_baseline.sh           # Benchmark base
│   ├── run_optimized.sh          # Benchmark optimizado
│   ├── script_benchmark.py       # Script de benchmark
│   └── populate_db.py            # Poblador de datos
├── results/               # Resultados de benchmarks
│   ├── benchmark_baseline.csv    # Resultados base
│   └── benchmark_optimized.csv   # Resultados optimizados
└── docs/                  # Documentación
    ├── informe.md                 # Informe original
    ├── informe_optimizacion.md    # Informe de optimización
    └── SCRIPTS_README.md          # Documentación de scripts
```

## 🚀 Inicio Rápido

### Prerrequisitos
- Docker y Docker Compose
- Bash (Linux/Mac) o Git Bash (Windows)

### Ejecutar Benchmarks

```bash
# Benchmark con índices básicos
cd scripts
./run_baseline.sh

# Benchmark con optimizaciones
./run_optimized.sh
```

Los resultados se guardan automáticamente en `../results/` como archivos CSV.

## 📊 Resultados

Los benchmarks generan archivos CSV con las siguientes columnas:
- **Operación/Consulta**: Nombre de la operación
- **Tiempo (ms)**: Tiempo de ejecución en milisegundos
- **Filas**: Número de filas retornadas
- **Descripción**: Descripción de la operación

## 📋 Contenido de Optimizaciones

### Índices Implementados
- Índice compuesto para productos por categoría y precio
- Índice para búsquedas de texto en nombres de productos
- Índice compuesto para historial de pedidos por usuario

### Técnicas de Optimización
- Desnormalización controlada (promedio_calificacion, total_resenas)
- Vista materializada para reportes de vendedores
- Triggers para mantenimiento automático de datos desnormalizados

### Mejoras de Rendimiento
- Consultas optimizadas con índices especializados
- Reducción de JOINs complejos mediante desnormalización
- Reportes eficientes usando vistas materializadas

## 🛠️ Scripts Disponibles

| Script | Descripción |
|--------|-------------|
| `run_baseline.sh` | Ejecuta benchmark con índices básicos |
| `run_optimized.sh` | Ejecuta benchmark con optimizaciones aplicadas |

## 📈 Comparación de Resultados

Para comparar los resultados manualmente:
1. Ejecutar ambos benchmarks
2. Abrir los CSVs en `results/` con Excel o similar
3. Comparar los tiempos de ejecución

## 🔧 Desarrollo

### Agregar Nueva Optimización
1. Modificar `sql/e-shopify-db-optimized.sql`
2. Actualizar `scripts/script_benchmark.py` si es necesario
3. Ejecutar `./scripts/run_optimized.sh` para validar

### Modificar Benchmark
Editar `scripts/script_benchmark.py` para agregar nuevas consultas o operaciones.

## 📚 Documentación Adicional

- [Informe de Optimización](docs/informe_optimizacion.md) - Detalles técnicos completos
- [Scripts README](docs/SCRIPTS_README.md) - Documentación detallada de automatización
- [Informe Original](docs/informe.md) - Documentación inicial del proyecto

## 🐳 Docker

El proyecto usa Docker Compose para:
- PostgreSQL 15 como base de datos
- PgAdmin como interfaz web
- Contenedor de benchmark automatizado

```bash
cd docker
docker-compose up -d  # Levantar servicios
docker-compose down   # Detener servicios
```

5. **Ejecutar evaluación de rendimiento (opcional)**:
   ```bash
   docker-compose up --build benchmark
   ```

   Este comando ejecutará un script Python que mide los tiempos de consultas frecuentes en la base de datos.

6. **Poblar con datos masivos (opcional, para pruebas realistas)**:
   ```bash
   docker-compose up --build populate
   ```

   Este comando poblará la base de datos con ~10,000 usuarios, 5,000 productos, 2,000 pedidos y 10,000 reseñas para pruebas de rendimiento más realistas.

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
e-shopify-db-optimization/
├── README.md              # Este archivo
├── der_eshopify-V2.drawio.svg  # Diagrama ER
├── docker/                 # Configuración de Docker
│   ├── docker-compose.yml
│   ├── Dockerfile.benchmark
│   └── images/            # Imágenes del proyecto
│       ├── admin_panel.png
│       ├── connection_config.png
│       ├── docker_ps.png
│       ├── order_data.png
│       ├── products_data.png
│       ├── tables_pgadmin.png
│       └── user_data.png
├── sql/                   # Scripts SQL
│   ├── e-shopify-db.sql           # Schema base
│   ├── e-shopify-db-optimized.sql # Schema optimizado
│   └── init.sql                   # Inicialización
├── scripts/               # Scripts de automatización
│   ├── run_baseline.sh           # Benchmark base
│   ├── run_optimized.sh          # Benchmark optimizado
│   ├── script_benchmark.py       # Script de benchmark
│   └── populate_db.py            # Poblador de datos
├── results/               # Resultados de benchmarks
│   ├── benchmark_baseline.csv    # Resultados base
│   └── benchmark_optimized.csv   # Resultados optimizados
└── docs/                  # Documentación
    ├── informe.md                 # Informe original
    ├── informe_optimizacion.md    # Informe de optimización
    └── SCRIPTS_README.md          # Documentación de scripts
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

### Optimización de Rendimiento ✅ COMPLETADO
Para la actividad S4, se implementaron optimizaciones de rendimiento que lograron resultados excepcionales:

**Optimizaciones implementadas:**
- **Índices compuestos** para consultas frecuentes
- **Desnormalización controlada** para lecturas rápidas
- **Vista materializada** para reportes
- **Script de benchmark** para medir tiempos

**Resultados del benchmark con datos realistas:**
- Dataset: 1,008 usuarios, 5,010 productos, 10,008 reseñas, 1,013 pedidos
- **Tiempo promedio de consultas:** 3.7 ms
- **Mejor rendimiento:** 0 ms (consultas COUNT optimizadas)
- **Consulta más compleja:** 16 ms (agregaciones con JOINs múltiples)

Ejecuta el benchmark con:
```bash
# Para datos pequeños
docker-compose up --build benchmark

# Para datos realistas (recomendado)
docker-compose up --build populate
docker-compose up --build benchmark
```

El informe detallado con análisis completo está en `informe_optimizacion.md`.

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