# Kristyco Studio · Frontend

Aplicación web de **Kristyco Studio**, una tienda online de **invitaciones de boda y papelería artesanal**, desarrollada como Trabajo de Fin de Grado del Ciclo Formativo de Grado Superior en **Desarrollo de Aplicaciones Web (DAW)**.

Este repositorio contiene el **frontend** (Angular 19). La API REST está en [TFG_Backend](https://github.com/Daniel0611CN/TFG_Backend).

🔗 **Demo:** [kristyco-studio.vercel.app](https://kristyco-studio.vercel.app) · también en [integrated-proyect-fp.vercel.app](https://integrated-proyect-fp.vercel.app/home)

![Angular](https://img.shields.io/badge/Angular-19-DD0031?logo=angular&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.7-3178C6?logo=typescript&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?logo=bootstrap&logoColor=white)
![Vercel](https://img.shields.io/badge/Deploy-Vercel-000000?logo=vercel&logoColor=white)

---

## Tabla de contenidos

1. [Descripción](#descripción)
2. [Funcionalidades](#funcionalidades)
3. [Tecnologías](#tecnologías)
4. [Requisitos previos](#requisitos-previos)
5. [Instalación y ejecución](#instalación-y-ejecución)
6. [Configuración del entorno](#configuración-del-entorno)
7. [Scripts disponibles](#scripts-disponibles)
8. [Rutas de la aplicación](#rutas-de-la-aplicación)
9. [Estructura del proyecto](#estructura-del-proyecto)
10. [Autenticación y seguridad en el cliente](#autenticación-y-seguridad-en-el-cliente)
11. [Flujo de pago con PayPal](#flujo-de-pago-con-paypal)
12. [Diseño y recursos](#diseño-y-recursos)
13. [Despliegue](#despliegue)
14. [Relación con el backend](#relación-con-el-backend)
15. [Autor](#autor)

---

## Descripción

Kristyco Studio es una tienda de invitaciones de boda y papelería artesanal. Los productos se organizan en **colecciones** (Aire, Aqua, Nature…), cada una con sus **invitaciones**. Los usuarios pueden explorar el catálogo, registrarse, realizar pedidos y pagarlos con PayPal. Las personas administradoras gestionan colecciones, invitaciones y pedidos desde un panel propio.

El frontend es una **SPA** hecha con componentes standalone de Angular, rutas protegidas con guards y comunicación con el backend mediante `HttpClient` y un interceptor que adjunta el token de sesión.

## Funcionalidades

### Zona pública
- Página de inicio, **sobre mí** y **contacto**.
- Catálogo de **colecciones** y listado de **invitaciones por colección**, con detalle de cada una.
- Secciones informativas: acabados, detalles y regalos.
- Páginas legales: **política de privacidad** y **términos y condiciones**.

### Autenticación
- **Registro** con validaciones de formulario y **confirmación de cuenta por correo**.
- **Inicio de sesión** (solo accesible para usuarios no autenticados).
- **Recuperación y restablecimiento de contraseña** mediante enlace con token enviado por email.

### Zona de usuario (requiere login)
- **Perfil** del usuario.
- **Realizar pedido** y consultar **mis pedidos**.
- **Pago con PayPal**, con pantallas de pago exitoso y pago cancelado.

### Panel de administración (rol administrador)
- **Dashboard** con gráficos de pedidos (por mes y distribución) construidos con CSS.
- **Listados con alta, edición y borrado** de colecciones, invitaciones y pedidos.
- Tablas con **búsqueda, ordenación por columnas y paginación**.

## Tecnologías

| Categoría | Tecnología |
|---|---|
| Framework | Angular 19.2 (CLI 19.2.4), componentes standalone |
| Lenguaje | TypeScript 5.7 |
| Programación reactiva | RxJS 7.8 |
| Estilos | Bootstrap 5.3, Sass (SCSS con parciales: variables, mixins, fuentes, SweetAlert) |
| Iconos | Font Awesome 6.7 |
| Alertas y modales | SweetAlert2 (envuelto en `SwalService`) |
| Pagos | PayPal (a través del backend) |
| Testing | Jasmine + Karma |
| Despliegue | Vercel |

## Requisitos previos

- **Node.js** `^18.19.1`, `^20.11.1` o `>=22.0.0` (requisito de Angular 19)
- **npm**
- **Angular CLI** (opcional): `npm install -g @angular/cli@19`
- El **backend** en marcha en `http://localhost:8080` para probar todas las funcionalidades en local, o bien usar la API desplegada (ver más abajo).

## Instalación y ejecución

```bash
git clone https://github.com/Daniel0611CN/TFG_Frontend.git
cd TFG_Frontend
npm install
npm start
```

La aplicación estará en <http://localhost:4200/> y se recarga automáticamente al guardar cambios.

## Configuración del entorno

La URL de la API se define en `src/environments/`:

| Archivo | Uso | `apiUrl` |
|---|---|---|
| `environment.development.ts` | Desarrollo (`ng serve`) | `http://localhost:8080/api/v1` |
| `environment.ts` | Producción (`ng build`) | `https://kristyco-studio-proyect.onrender.com/api/v1` |

Si despliegas tu propio backend, cambia `apiUrl` en `environment.ts` y asegúrate de que el backend permita tu dominio en CORS.

## Scripts disponibles

| Comando | Descripción |
|---|---|
| `npm start` | Servidor de desarrollo (`ng serve`) |
| `npm run build` | Build de producción en `dist/frontend` |
| `npm run watch` | Build en modo desarrollo con recarga |
| `npm test` | Pruebas unitarias (Karma + Jasmine) |

## Rutas de la aplicación

| Ruta | Pantalla | Acceso |
|---|---|---|
| `/home` | Inicio | Público |
| `/colecciones` | Listado de colecciones | Público |
| `/colecciones/:nombre` | Detalle de una colección | Público |
| `/colecciones/:nombre/invitaciones` | Invitaciones de la colección | Público |
| `/acabados`, `/detalles`, `/regalos` | Secciones informativas | Público |
| `/sobre-mi`, `/contacto` | Información y contacto | Público |
| `/politica-privacidad`, `/terminos-condiciones` | Páginas legales | Público |
| `/login`, `/register` | Acceso y registro | Solo invitados (`guestGuard`) |
| `/confirmar-token/:token` | Confirmación de cuenta | Público |
| `/reset-password/:token` | Restablecer contraseña | Público |
| `/perfil` | Perfil de usuario | Autenticado |
| `/realizar-pedido` | Crear un pedido | Autenticado |
| `/mis-pedidos` | Historial de pedidos | Autenticado |
| `/paypal/:id` | Pago de un pedido | Autenticado |
| `/payment/success`, `/payment/cancel` | Resultado del pago | Autenticado |
| `/admin` | Dashboard | Administrador |
| `/listado/colecciones`, `/listado/invitaciones`, `/listado/pedidos` | Gestión | Administrador |

Cualquier ruta desconocida redirige a `/home`.

## Estructura del proyecto

```
TFG_Frontend/
├── public/
│   ├── fonts/                 # Tipografías propias (.woff2)
│   ├── img/                   # Imágenes de colecciones (aire, aqua, nature) y recursos
│   └── files/                 # Documentación del diseño (PDF y prototipo Adobe XD)
├── src/
│   ├── app/
│   │   ├── components/
│   │   │   ├── admin/         # Dashboard y listados/formularios de gestión
│   │   │   ├── auth/          # Login y registro
│   │   │   ├── content/
│   │   │   │   ├── open/      # Páginas públicas (home, colecciones, contacto, sobre mí...)
│   │   │   │   ├── secured/   # Perfil, realizar pedido, mis pedidos
│   │   │   │   ├── privacy-policy/ y terms-and-conditions/
│   │   │   ├── shared/        # Navbar, PayPal, tablas (paginador, búsqueda, orden), servicios UI
│   │   │   └── tokens/        # Confirmación de cuenta y reset de contraseña
│   │   ├── core/
│   │   │   ├── guards/        # auth, guest y admin
│   │   │   └── middleware/    # Interceptor HTTP (Authorization: Bearer)
│   │   ├── models/            # Interfaces y enums (rol)
│   │   ├── pipes/             # Estado de pago/pedido, método de pago, safe
│   │   ├── services/          # Acceso a la API (auth, pedidos, categorías, productos...)
│   │   ├── app.config.ts
│   │   └── app.routes.ts
│   ├── environments/          # apiUrl de desarrollo y producción
│   └── styles/                # Parciales SCSS
├── angular.json
└── package.json
```

## Autenticación y seguridad en el cliente

- Tras el login, el usuario y su token se guardan mediante `StorageService`.
- `HttpRequestInterceptor` añade la cabecera `Authorization: Bearer <token>` a cada petición cuando hay sesión.
- Tres **guards** controlan el acceso: `auth.guard` (usuarios autenticados), `guest.guard` (solo no autenticados) y `admin.guard` (rol administrador).
- La seguridad real se aplica en el backend; los guards solo mejoran la experiencia de navegación.

## Flujo de pago con PayPal

1. El usuario crea su pedido en **Realizar pedido**.
2. En `/paypal/:id` el frontend pide al backend crear la orden de PayPal.
3. PayPal gestiona la aprobación y redirige a `/payment/success` o `/payment/cancel`.
4. Al volver con éxito, el frontend confirma el pago en el backend (`/payment/success?orderId=...`) y lleva al usuario a su perfil.

> El backend usa actualmente el entorno **sandbox** de PayPal, así que no se realizan cargos reales.

## Diseño y recursos

- Tipografías personalizadas: Celestine, Chopin, Josefin Sans, Julius Sans One, Raleway y Sophia Morgant.
- El prototipo de diseño (Adobe XD) y el documento *Proyecto Final Bootstrap* están en `public/files/`.

## Despliegue

El frontend se despliega en **Vercel**. Para generar el build manualmente:

```bash
npm run build
```

Los archivos quedan en `dist/frontend`. Al ser una SPA con rutas del lado del cliente, el hosting debe redirigir todas las rutas a `index.html`.

## Relación con el backend

| Parte | Repositorio | Tecnología |
|---|---|---|
| Frontend (este repo) | [TFG_Frontend](https://github.com/Daniel0611CN/TFG_Frontend) | Angular 19 |
| Backend | [TFG_Backend](https://github.com/Daniel0611CN/TFG_Backend) | Spring Boot 3 · Java 21 · PostgreSQL |

## Autor

**Daniel** — [@Daniel0611CN](https://github.com/Daniel0611CN)

Proyecto realizado como TFG del Ciclo Formativo de Grado Superior en Desarrollo de Aplicaciones Web.
