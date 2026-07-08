<div align="center">
  <h1>🏠 Refugia</h1>
  <p><strong>Conectamos familias con niñeras de confianza.</strong></p>
  <p>Una plataforma moderna, segura y orientada a la tranquilidad del hogar.</p>
</div>

---

## 📖 Sobre Refugia

**Refugia** es una plataforma web integral diseñada para resolver la necesidad de encontrar cuidado infantil seguro y confiable. Permite a las familias descubrir niñeras cercanas, revisar sus certificaciones, reservar horarios específicos y realizar pagos de forma completamente digital y automatizada.

El sistema cuenta con tres portales principales diseñados para ofrecer una experiencia fluida a cada tipo de usuario:
- 👨‍👩‍👧 **Panel de Familias**
- 👩‍🍼 **Panel de Niñeras**
- 🛡️ **Panel de Administración**

---

## 🎨 Diseño y UI/UX

Refugia fue diseñada bajo los principios de **Modernidad, Confianza y Calidez**, lo cual se refleja en su interfaz de usuario.

### Estética y Colores (Design System)
- **Brand (Warm Lavender / Violet)**: El color primario de la marca (`#7c3aed`). Transmite profesionalismo pero con un toque moderno y acogedor. Utilizado en botones primarios, enlaces y acentos visuales.
- **Fondos (Warm Cream)**: En lugar de blancos puros y grises fríos, la app utiliza fondos color crema (`#fffbf5`) que hacen que la interfaz se sienta mucho más cálida y humana.
- **Trust Green**: Un verde esmeralda (`#059669`) utilizado exclusivamente para elementos de confianza como insignias de "Verificada", checkmarks y confirmaciones de pago.
- **Gradientes Suaves**: La aplicación hace uso extensivo de `gradient-warm` y `gradient-hero` para crear profundidad sin abrumar la vista.

### Experiencia Interactiva
- **Micro-animaciones**: Transiciones suaves en toda la plataforma (`fade-in`, `slide-up` y elementos `float` en el hero) para que la app se sienta viva y responsiva.
- **Glassmorphism**: Efectos de desenfoque (`backdrop-blur`) en tarjetas superpuestas y modales, lo que entrega un look premium y de última generación.
- **Tipografía**: Basada en `Inter` para máxima legibilidad, combinando pesos `font-black` para precios y `font-medium` para la lectura diaria.

---

## 🚀 Tecnologías (Tech Stack)

La aplicación está construida sobre un stack moderno y escalable:

### Frontend
- **Framework**: Next.js 16 (App Router)
- **Librería de UI**: React
- **Estilos**: Tailwind CSS (con Design System personalizado)
- **Componentes**: Construidos desde cero (sin depender de pesadas librerías de componentes) para mantener el HTML semántico y un CSS mínimo y rápido.

### Backend & Datos
- **Base de Datos**: PostgreSQL
- **ORM**: Prisma (para type-safety y migraciones declarativas)
- **Autenticación**: NextAuth.js v4 (Estrategia JWT y Credenciales con contraseñas hasheadas en `bcrypt` de 12 rondas)

### Integraciones Externas
- **Pasarela de Pagos**: [Flow.cl](https://www.flow.cl/) (Webpay Plus, Servipag, Mach, etc.) a través de webhooks seguros.
- **Emailing**: [Resend API](https://resend.com/) para el envío de notificaciones y recibos con plantillas HTML nativas.

### Infraestructura
- **Docker**: El repositorio incluye `Dockerfile` y `docker-compose.yml` listos para ser desplegados en cualquier VPS (junto con NGINX para reverse proxy).

---

## ⚙️ Características Principales

* 🔍 **Algoritmo de Matching**: Ordena a las niñeras basándose en distancia (cálculo radial), habilidades, disponibilidad de calendario y bonificaciones de confianza.
* 💬 **Chat Integrado**: Sistema de mensajería contextual ligada a una reserva, permitiendo que la familia y la niñera conversen solo cuando la reserva ha sido pre-aprobada.
* 📅 **Disponibilidad Semanal**: Las niñeras pueden editar su grilla de horarios disponibles, y el sistema automáticamente bloquea cruces de reservas.
* 💳 **Pagos Seguros**: Al confirmar un servicio, la familia es redirigida a la pasarela y el sistema espera el Webhook de Flow para marcar la reserva como pagada.
* 🔒 **Seguridad de Rutas (Middleware)**: Protección robusta en el borde (Edge) mediante `next-auth/middleware` que asegura que una familia no pueda entrar al dashboard de admin o de niñera y viceversa.

---

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
   ```bash
   cp .env.example .env
   ```
   Edita el `.env` con tus credenciales de PostgreSQL, Flow y Resend.

4. **Sincronizar la Base de Datos**
   ```bash
   npx prisma generate
   npx prisma db push
   ```

5. **Correr el servidor**
   ```bash
   npm run dev
   ```

## 📦 Despliegue (VPS / Producción)

Refugia está diseñada para correr de manera contenida.

```bash
# Dentro del servidor VPS
git clone https://github.com/nicvroyz/nannyconnect.git
cd nannyconnect
cp .env.example .env # (No olvides configurarlo)

# Levantar infraestructura
docker-compose up -d --build

# Aplicar base de datos
docker exec -it nannyconnect_app npx prisma migrate deploy
```

## 📄 Licencia

Propiedad intelectual privada. Todos los derechos reservados.