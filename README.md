# 💈 AppSalon – Backend

API REST de **AppSalon**, una aplicación para reservar citas en un salón de belleza y barbería. Los clientes crean una cuenta, eligen servicios y agendan su cita; el administrador consulta las citas próximas.

Está construida con **Node.js** y **Express**, usa **MongoDB** con **Mongoose** como base de datos, autenticación con **JWT** y envío de correos con **Nodemailer**. Forma parte de un proyecto **MEVN** (MongoDB, Express, Vue, Node).

> 🔗 El frontend de este proyecto está en [appsalon-frontend](https://github.com/SuemyDzib/appsalon-frontend).

## ✨ Características

- **Registro de usuarios** con confirmación de cuenta por email.
- **Inicio de sesión** con JWT (vigencia de 30 días) y contraseñas cifradas con bcrypt.
- **Recuperación de contraseña** mediante un enlace enviado por email.
- **Gestión de citas**: crear, consultar, editar y cancelar. Cada usuario solo puede ver y modificar sus propias citas.
- **Consulta de horarios ocupados** por fecha, para que el frontend no permita reservar un horario ya tomado.
- **Rol de administrador**, que puede ver todas las citas próximas con los datos del cliente.
- **Notificaciones por email** al administrador cuando se crea, modifica o cancela una cita.
- **CRUD de servicios** del salón, con un seeder de servicios de ejemplo.
- **CORS configurado** para aceptar solo peticiones del frontend.

## 🛠️ Tecnologías

- [Node.js](https://nodejs.org/) y [Express](https://expressjs.com/)
- [MongoDB](https://www.mongodb.com/) con [Mongoose](https://mongoosejs.com/)
- [JSON Web Token](https://github.com/auth0/node-jsonwebtoken) y [bcrypt](https://github.com/kelektiv/node.bcrypt.js)
- [Nodemailer](https://nodemailer.com/) para el envío de correos
- [date-fns](https://date-fns.org/) para el manejo de fechas

## 📋 Requisitos

- [Node.js](https://nodejs.org/) 18 o superior
- Una base de datos MongoDB, local o en [MongoDB Atlas](https://www.mongodb.com/atlas)
- Un servidor SMTP para los correos. Para desarrollo se recomienda [Mailtrap](https://mailtrap.io/), que captura los correos sin enviarlos realmente.

## 🚀 Instalación y uso

1. Clona el repositorio:

   ```bash
   git clone https://github.com/SuemyDzib/appsalon-backend.git
   cd appsalon-backend
   ```

2. Instala las dependencias:

   ```bash
   npm install
   ```

3. Crea un archivo `.env` a partir del ejemplo y completa tus datos:

   ```bash
   cp .env.example .env
   ```

4. Carga los servicios de ejemplo:

   ```bash
   npm run seed:import
   ```

5. Inicia el servidor en modo desarrollo:

   ```bash
   npm run dev
   ```

   La API quedará disponible en `http://localhost:4000/api`.

### Crear un administrador

No existe un formulario para crear administradores. Regístrate normalmente desde el frontend, confirma la cuenta y después cambia el campo `admin` a `true` en el documento de ese usuario dentro de la colección `users` de MongoDB (por ejemplo, desde MongoDB Compass o Atlas).

### Variables de entorno

| Variable       | Descripción                                                        |
| -------------- | ------------------------------------------------------------------ |
| `PORT`         | Puerto del servidor (opcional, por defecto `4000`)                 |
| `MONGO_URI`    | Cadena de conexión a MongoDB                                       |
| `FRONTEND_URL` | URL del frontend; se usa para CORS y para los enlaces de los correos |
| `JWT_SECRET`   | Clave secreta para firmar los tokens JWT                           |
| `EMAIL_HOST`   | Host del servidor SMTP                                             |
| `EMAIL_PORT`   | Puerto del servidor SMTP                                           |
| `EMAIL_USER`   | Usuario del servidor SMTP                                          |
| `EMAIL_PASS`   | Contraseña del servidor SMTP                                       |

### Scripts

| Comando                | Descripción                                                                  |
| ---------------------- | ---------------------------------------------------------------------------- |
| `npm run dev`          | Inicia el servidor con recarga automática                                    |
| `npm run dev:postman`  | Igual que `dev`, pero permite peticiones sin origen (útil para Postman)     |
| `npm start`            | Inicia el servidor en modo producción                                       |
| `npm run seed:import`  | Inserta los servicios de ejemplo                                             |
| `npm run seed:destroy` | Elimina todos los servicios                                                  |

## 🔌 Endpoints

Todas las rutas tienen el prefijo `/api`. Las marcadas con ✅ requieren el encabezado `Authorization: Bearer <token>`.

## 📝 Notas

Las rutas de servicios no requieren autenticación, por lo que cualquier persona podría crear, editar o eliminar servicios a través de la API. Es un proyecto de práctica; para producción convendría protegerlas para que solo un administrador pueda modificarlas.

## 👤 Autor

Desarrollado por **Suemy Dzib** – [@SuemyDzib](https://github.com/SuemyDzib) a través del curso de Udemy impartido por Juan de la Torre.