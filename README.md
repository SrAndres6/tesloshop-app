# tesloshop-app


## Descripción
Este proyecto consiste en la implementación de una arquitectura distribuida utilizando **Docker** y **Docker Compose**. Se ha contenerizado una aplicación completa que integra un frontend, un backend y una base de datos persistente, asegurando la orquestación y comunicación eficiente entre servicios.

## Arquitectura del Sistema
La solución se basa en una arquitectura de tres capas:


## 1. (Frontend): 
Basada en Angular 17+. Utiliza una estrategia de servidor web con Nginx que funciona como punto de entrada único (Puerto 80), eliminando la necesidad de exponer el backend directamente al cliente.

## 2. (Backend): 
Desarrollada en NestJS. Maneja la autenticación JWT, la lógica de productos y la comunicación con el ORM para la base de datos.

## 3. (Database): 
Motor PostgreSQL 14.3. Es el único servicio con persistencia de estado mediante volúmenes de Docker.

## 4. Red de Datos (teslo-network): 
Una red de tipo bridge que aísla los servicios. El frontend se comunica con el backend usando el hostname interno `http://backend:3000`, lo que resuelve problemas de CORS de forma nativa.


## Explicación de Servicios

### 1. Frontend (Angular + Nginx)
* **Tecnología:** Angular 17+.
* **Servidor:** Nginx.
* **Función:** Sirve la interfaz de usuario y actúa como proxy inverso.
* **Comunicación:** Se comunica con el backend usando el hostname `http://backend:3000`.
* **Puerto:** Expuesto al host en el puerto 8080.

### 2. Backend (NestJS)
* **Tecnología:** NestJS.
* **Función:** API REST con autenticación JWT y lógica de negocio.
* **Comunicación:** Se comunica con la base de datos usando el hostname `postgres`.
* **Puerto:** Expuesto al host en el puerto 3000.

### 3. Base de Datos (PostgreSQL)
* **Tecnología:** PostgreSQL 14.3.
* **Función:** Almacenamiento persistente de datos.
* **Persistencia:** Utiliza volúmenes de Docker para mantener los datos entre reinicios.
* **Puerto:** Expuesto al host en el puerto 5432.

### 4. Red de Datos (teslo-network)
* **Tipo:** Bridge.
* **Función:** Aísla los servicios y permite la comunicación entre ellos usando nombres de host.

## Pasos de Ejecución

### 1. Requisitos Previos
* Tener instalado [Docker Desktop](https://www.docker.com/products/docker-desktop/).

## 2. clonar el repositorio
```bash
git clone https://github.com/DEV-SENA-TRAINING/tesloshop-app.git
cd tesloshop-app/
```
## 3. Configurar variables de entorno:
Copie el archivo de ejemplo y editar las credenciales:
```bash
cp .env.example .env
```
Es obligatorio definir POSTGRES_PASSWORD y DB_PASSWORD con el mismo valor.

## 4. Otorgar permisos de ejecución:
```bash
chmod +x start.sh stop.sh
```

## 5. Ejecutar el script start.sh
```bash
./start.sh
```
## 6. Despliegue con Docker Compose
Para levantar todo el entorno (Frontend, Backend y DB), ejecuta:
```bash
docker compose up --build -d
```

## verificar contenedores
```bash
docker compose ps
```

## ver logs
```bash
docker compose logs -f
```

## Poblar la base de datos (Seed):
Dado que la DB inicia vacía, ejecute el proceso de carga inicial desde el navegador o terminal:
👉 URL: http://localhost:3000/api/seed

## detener contenedor
```bash
docker compose down
```