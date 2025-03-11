# Iterando-Pares-Docker

Este proyecto consiste en un scraper de la web de Pares que extrae información de descripciones y sus imágenes, almacenando los datos en un archivo JSON y utilizando Redis para la gestión de URLs.
Este proyecto es la parte de [Iterando-Pares](https://github.com/0Vinylo0/Iterando-Pares) pero usando docker

## Requisitos de Instalación

Para ejecutar este contenedor Docker, es necesario tener instalado:

- Docker
- Docker Compose
- Redis (Se ejecuta dentro del contenedor)
- Tor (Integrado en el contenedor)

## Estructura del Proyecto

El proyecto contiene los siguientes archivos y carpetas:

```
.
├── data/                     # Carpeta para almacenar datos del scraper
│   ├── img/                  # Carpeta donde se guardan las imágenes descargadas
│   ├── description_data.json  # Archivo JSON donde se almacenan las descripciones
│   └── todo_urls.txt         # Archivo con las URLs a procesar
│
├── html/                     # Carpeta con la interfaz web
│   └── index.html            # Página web para visualizar los datos
│
├── iterado/                  # Carpeta con los archivos del scraper
│   ├── Dockerfile            # Archivo para construir la imagen de Docker
│   ├── requirements.txt      # Dependencias de Python necesarias para el proyecto
│   ├── controller.py         # Archivo principal para gestionar el scraper
│   ├── iterando.py           # Clase principal con la lógica del scraper
│   ├── delete.py             # Script para limpiar Redis
│
│
├── docker-compose.yml         # Archivo para levantar el servicio con Docker Compose
├── torrc                      # Archivo de configuracion de contenedor de tor
```

## Instalación y Ejecución

### 1. Clonar el repositorio

Si el proyecto no está clonado, puedes hacerlo con:

```sh
 git clone <URL-DEL-REPO>
 cd <CARPETA-DEL-REPO>
```

### 2. Construir y levantar los contenedores

### Agregar URLs a procesar

Las URLs deben agregarse en `data/todo_urls.txt`, y luego iniciar el scraper con:

```sh
 echo "url-a-cargar" > todo_urls.txt
```

### Ejecutar contenecor

Ejecuta el siguiente comando para levantar el contenedor Docker:

```sh
 docker-compose up --build -d
```

Esto iniciará los servicios de Redis, Tor y el scraper.

### 3. Verificar que el scraper esté corriendo

Para ver los logs del scraper:

```sh
 docker-compose logs -f scraper
```

Para ingresar a la terminal del contenedor:

```sh
 docker exec -it scraper bash
```

### Limpiar Redis

Si es necesario eliminar los datos almacenados en Redis, ejecuta:

```sh
 python iterado/delete.py
```

### Acceder a la interfaz web

El proyecto incluye una interfaz web (`html/index.html`) que puede ser servida con un servidor local o cualquier servicio de archivos estáticos.

## Configuración de Tor

El archivo `iterado/torrc` permite configurar el proxy Tor dentro del contenedor. Es importante asegurarse de que el servicio de Tor esté activo antes de ejecutar el scraper.

## Consideraciones Adicionales

- Asegúrate de que Redis esté corriendo correctamente.
- Si las URLs no se están procesando, verifica la conexión a Tor.
- El scraper usa múltiples procesos para optimizar la extracción de datos.

---

**Autor:** Tu Nombre
**Fecha:** \$(date +%Y-%m-%d)

