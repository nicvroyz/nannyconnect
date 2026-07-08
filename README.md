# 🏠 Refugia (NannyConnect)

Refugia (internamente "NannyConnect") es una plataforma web moderna que conecta a familias con niñeras de confianza. Permite la búsqueda, reserva y pago de servicios de cuidado infantil, con perfiles verificados y un sistema de reseñas.

## 🚀 Tecnologías

* **Frontend & Backend**: Next.js 16 (App Router) + React + Turbopack
* **Base de Datos**: PostgreSQL
* **ORM**: Prisma
* **Autenticación**: NextAuth.js (Credenciales/JWT)
* **Estilos**: Tailwind CSS + Componentes UI personalizados
* **Pagos**: Integración con Flow.cl (Webpay)
* **Emails**: Resend API
* **Despliegue**: Docker & Docker Compose (listo para VPS)

## ✨ Características Principales

* **🏢 Panel de Familias**: Buscar niñeras por comuna, ver perfiles detallados, enviar solicitudes de reserva, gestionar favoritos y pagar servicios a través de Flow.
* **👩‍🍼 Panel de Niñeras**: Gestionar calendario de disponibilidad, aceptar/rechazar solicitudes de cuidado, ver historial de trabajos y configurar tarifas.
* **🛡️ Panel de Administración**: Aprobar nuevos perfiles de niñeras, gestionar usuarios, monitorear todas las reservas y ver métricas globales.
* **🔔 Sistema de Notificaciones**: Notificaciones por correo electrónico transaccional (Resend) para nuevas solicitudes, confirmaciones y recordatorios.
* **🔒 Seguridad**: Protección de rutas por roles (Admin, Nanny, Family), contraseñas hasheadas con bcrypt (rounds: 12), y variables de entorno protegidas.

## ⚙️ Requisitos Previos

* Node.js 18+ o superior
* Docker y Docker Compose (para despliegue en producción)
* Una cuenta en [Flow.cl](https://www.flow.cl/) para procesar pagos (sandbox o prod)
* Una cuenta en [Resend](https://resend.com/) para el envío de correos

## 🛠️ Instalación y Configuración Local

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/nicvroyz/nannyconnect.git
   cd nannyconnect
   ```

2. **Instalar dependencias**
   ```bash
   npm install
   ```

3. **Configurar Variables de Entorno**
   Copia el archivo de ejemplo y completa las variables:
   ```bash
   cp .env.example .env
   ```
   Asegúrate de llenar las variables de base de datos, `NEXTAUTH_SECRET`, y tus APIs de Flow y Resend.

4. **Configurar la Base de Datos**
   Asegúrate de tener un servidor PostgreSQL corriendo en el puerto 5432 (puedes usar el `docker-compose.yml` para levantar solo la BD si lo deseas).
   ```bash
   # Generar el cliente Prisma
   npx prisma generate
   
   # Empujar el esquema a la base de datos
   npx prisma db push
   ```

5. **Iniciar el servidor de desarrollo**
   ```bash
   npm run dev
   ```
   La app estará disponible en `http://localhost:3000`.

## 📦 Despliegue a Producción (VPS con Docker)

El proyecto incluye un entorno Docker completo con la aplicación, PostgreSQL y NGINX configurados.

1. En tu servidor VPS, clona el repositorio y configura el `.env` con tus claves reales de producción y el dominio de tu sitio.
2. Ejecuta Docker Compose:
   ```bash
   docker-compose up -d --build
   ```
3. Aplica las migraciones de base de datos dentro del contenedor:
   ```bash
   docker exec -it nannyconnect_app npx prisma migrate deploy
   ```

## 🧹 Tareas Programadas (Cron)

Para limpiar los pagos que quedaron estancados (expirados) sin ser pagados en Flow, puedes configurar un Cron Job (ej. Vercel Cron o crontab en linux) que llame al endpoint:
`GET /api/cron/cleanup-payments`
Pasando el header `Authorization: Bearer <TU_CRON_SECRET>`.

## 📄 Licencia

Este proyecto es de uso privado.