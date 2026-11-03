# Kristyco Studio · TFG DAW

Tienda online de papelería artesanal para bodas (invitaciones y papelería personalizada). Proyecto de fin de grado del ciclo formativo de grado superior en Desarrollo de Aplicaciones Web (DAW).

**Demo:** [integrated-proyect-fp.vercel.app](https://integrated-proyect-fp.vercel.app)

<!-- Añade aquí una captura o un GIF de la web: ![Captura de Kristyco Studio](docs/captura.png) -->

## Tecnologías

| Capa | Tecnologías |
|---|---|
| Frontend | Angular 19, TypeScript, Bootstrap |
| Backend | Java, Spring Boot, Maven |
| Base de datos | MySQL |
| Despliegue | Vercel (frontend) · Docker (backend) |

## Estructura del repositorio

```
.
├── frontend/   # Aplicación web en Angular
└── backend/    # API REST en Java con Spring Boot
```

El frontend consume la API REST del backend, que gestiona los datos en MySQL.

## Funcionalidades

<!-- Rellena con lo que ofrece tu tienda, por ejemplo: -->
- Catálogo de invitaciones de boda y papelería artesanal
- <!-- carrito, pedidos, registro e inicio de sesión, panel de administración... -->

## Cómo ejecutarlo en local

### Requisitos

- Node.js y npm
- Angular CLI (`npm install -g @angular/cli`)
- JDK <!-- versión que uses, por ejemplo 17 o 21 -->
- MySQL en ejecución

### 1. Backend

```bash
cd backend
```

Configura la conexión a MySQL en `src/main/resources/application.properties` (o con variables de entorno):

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/<nombre_de_la_base_de_datos>
spring.datasource.username=<usuario>
spring.datasource.password=<contraseña>
```

Arranca la API:

```bash
./mvnw spring-boot:run
```

Por defecto queda disponible en `http://localhost:8080`.

### 2. Frontend

```bash
cd frontend
npm install
ng serve
```

Abre `http://localhost:4200/`. La aplicación se recarga sola al modificar el código.

> Asegúrate de que la URL de la API en el frontend apunta a tu backend local.

## Compilación y pruebas

```bash
# Frontend
cd frontend
ng build        # genera la carpeta dist/
ng test         # pruebas unitarias con Karma

# Backend
cd backend
./mvnw test
./mvnw package
```

## Despliegue

- **Frontend:** desplegado en Vercel. Directorio raíz del proyecto: `frontend`.
- **Backend:** incluye un `Dockerfile` en `backend/` para construir la imagen y desplegarla.

```bash
cd backend
docker build -t kristyco-backend .
```

## Autor

**Daniel Clavijo Núñez** · [GitHub](https://github.com/Daniel0611CN) · [LinkedIn](https://www.linkedin.com/in/daniel-clavijo-nu%C3%B1ez/)
