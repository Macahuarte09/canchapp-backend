# CanchApp - Backend

API de CanchApp, una app para reservar turnos de canchas de pádel y pelota paleta. Hecha como trabajo final para la Práctica Supervisada (PPS).

El frontend que usa esta API está en: https://github.com/Macahuarte09/canchapp-frontend

## Links

- API desplegada: https://canchapp-158d.vercel.app/api
- App: https://canchapp-blue.vercel.app

## Qué usé

- Node.js + Express
- MySQL
- JWT (para el login) y bcryptjs (para encriptar las contraseñas)

## Carpetas

```
├── database/    ← el .sql con las tablas
├── postman/     ← colección de Postman para probar la API
├── src/
│   ├── controllers/   ← la lógica de cada endpoint
│   ├── routes/        ← las rutas
│   └── db.js          ← conexión a MySQL
└── index.js           ← archivo principal del servidor
```

## Base de datos

Son 4 tablas:

- **usuarios**: nombre, email, contraseña (encriptada) y teléfono
- **canchas**: nombre, tipo (padel o pelota_paleta), precio por hora y si está activa
- **reservas**: qué usuario reservó qué cancha, fecha, hora de inicio y fin, y el estado (pendiente, confirmada o cancelada)
- **pagos**: el pago de cada reserva (monto, método y estado)

Relaciones: un usuario puede tener muchas reservas, una cancha puede tener muchas reservas, y una reserva puede tener pagos.

## Cómo correrlo en tu compu

Necesitás tener instalado Node.js y MySQL (yo usé XAMPP).

### 1. Clonar el repo

```bash
git clone https://github.com/Macahuarte09/canchapp-backend.git
cd canchapp-backend
npm install
```

### 2. Base de datos

1. Abrir phpMyAdmin y crear una base de datos que se llame `canchapp`.
2. Ir a **Importar** y subir el archivo `database/canchapp.sql`.

### 3. Variables de entorno

Crear un archivo `.env` en la raíz del proyecto con esto:

```
PORT=3000

DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=tu_password
DB_NAME=canchapp

JWT_SECRET=cualquier_clave_secreta
```

### 4. Levantar el servidor

```bash
node index.js
```

La API queda en http://localhost:3000

## Endpoints

### Usuarios

| Método | Ruta | Qué hace |
|--------|------|----------|
| POST | `/api/usuarios/register` | Registra un usuario |
| POST | `/api/usuarios/login` | Inicia sesión y devuelve un token |

### Canchas

| Método | Ruta | Qué hace |
|--------|------|----------|
| GET | `/api/canchas` | Trae todas las canchas |
| POST | `/api/canchas` | Crea una cancha |
| PUT | `/api/canchas/:id` | Modifica una cancha |
| DELETE | `/api/canchas/:id` | Elimina una cancha |

### Reservas

| Método | Ruta | Qué hace |
|--------|------|----------|
| GET | `/api/reservas` | Trae todas las reservas |
| GET | `/api/reservas/usuario/:id` | Trae las reservas de un usuario |
| POST | `/api/reservas` | Crea una reserva (si el horario está ocupado, devuelve error) |
| PUT | `/api/reservas/cancelar/:id` | Cancela una reserva |

## Postman

En la carpeta `postman` está la colección para importar y probar todos los endpoints. Tiene una variable `base_url`: por defecto apunta a `http://localhost:3000`, y se puede cambiar por la dirección de la API en Vercel.

## Deploy

Está subido a Vercel (la configuración está en `vercel.json`). Hay que cargar las variables del `.env` en el panel de Vercel y usar una base de datos MySQL que sea accesible desde internet.
