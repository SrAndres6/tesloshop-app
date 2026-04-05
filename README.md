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
* Asegúrese de que su sistema cumple con:

* Docker Desktop (versión 24.0 o superior).
* Docker Compose V2 (incluido en las versiones modernas).
* Mínimo 4GB de RAM disponibles para el clúster.

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
IMPORTANTE: Debe abrir el archivo .env y asegurarse de que POSTGRES_PASSWORD sea idéntico a DB_PASSWORD. De lo contrario, el backend fallará al intentar autenticarse con la base de datos.

## 4. Otorgar permisos de ejecución:
```bash
chmod +x start.sh stop.sh
```

## 5. Ejecutar el script start.sh
Para iniciar el despliegue automático que construye imágenes y levanta la red:
```bash
./start.sh
```
## 6. Despliegue con Docker Compose
Para levantar todo el entorno (Frontend, Backend y DB), ejecuta:
```bash
docker compose up --build -d
```

## verificar contenedores
Una vez el comando finalice, ejecute:

```docker compose ps```: Verifique que los 3 servicios tengan el estado Up (o healthy en el caso de la DB).


```docker compose logs -f```: Observe el flujo de salida. Busque el mensaje "Nest application successfully started".

## ver logs
```bash
docker compose logs -f
```

## Poblar la base de datos (Seed):
Dado que la DB inicia vacía, ejecute el proceso de carga inicial desde el navegador o terminal:
👉 URL: http://localhost:3000/api/seed

## 8. Finalización y Limpieza
Para detener los servicios y liberar recursos de su computadora:

```Bash
docker compose down
```
Si desea borrar también los volúmenes (empezar de cero total): ```docker compose down -v```

## anexo de imagenes
* imgane de structura del proyecto
  
  <img width="254" height="588" alt="image" src="https://github.com/user-attachments/assets/e13f4fe0-1e4a-4d67-b389-fb5fde7edf72" />

* imagen de backend/dockerfile
  
  <img width="673" height="740" alt="image" src="https://github.com/user-attachments/assets/1ffcf61e-f1b8-4ff8-b2f1-1bd61dd6f240" />


*  imagen de frontend/dockerfile
  
  <img width="661" height="524" alt="image" src="https://github.com/user-attachments/assets/a6f5ff1a-14ed-4eac-a78c-3a3096892dbc" />

* contrucion de imagen creacion de docker-compose.yml
  
  <img width="679" height="694" alt="image" src="https://github.com/user-attachments/assets/22f91c3e-78c3-47f7-9a8c-28a24a79bfa9" />
  <img width="668" height="368" alt="image" src="https://github.com/user-attachments/assets/df389a5f-e7f7-45a6-bc39-84292f0152a9" />

* configuracion de variables de entrono
* .env.example
  
  <img width="669" height="385" alt="image" src="https://github.com/user-attachments/assets/ad1dfa4e-2646-4759-859c-dac1424c441a" />
  
* .env
  
  <img width="705" height="385" alt="image" src="https://github.com/user-attachments/assets/795e33d2-b0b1-452f-8507-3f49b6ea0443" />

* imagen de ```docker compose up --build -d```
  
<img width="705" height="377" alt="image" src="https://github.com/user-attachments/assets/eae108b0-dbca-464f-b3f8-6c0ca648d7f9" />
<img width="707" height="245" alt="image" src="https://github.com/user-attachments/assets/1d6227a8-2cbf-4f93-a7ad-3f82e1e58895" />

* imagen de contenedores activos
  
  <img width="794" height="100" alt="image" src="https://github.com/user-attachments/assets/f8612fd9-59a8-46b5-9bec-0a4c14264664" />

* imagen de frontent en el navegador
  
  <img width="931" height="904" alt="image" src="https://github.com/user-attachments/assets/9c1bbfaf-6d95-456c-8bf4-4f4de100c11a" />

* imagen de api backend
  
  <img width="936" height="968" alt="image" src="https://github.com/user-attachments/assets/b299329f-2aaf-4387-b36f-86c2794fa3ea" />

* imagen de ejecucion del seed
  
  <img width="794" height="66" alt="image" src="https://github.com/user-attachments/assets/bdc1cf60-6beb-4910-a519-9648a204c5f8" />

* imagen de conexion de datos
  
<img width="802" height="205" alt="image" src="https://github.com/user-attachments/assets/7369212b-b092-4858-b87f-64a9ba141d81" />
