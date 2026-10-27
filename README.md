# CanchApp - Backend

API REST para gestionar usuarios, canchas y reservas de pádel y pelota paleta. Trabajo final para la Práctica Supervisada (PPS).

- Node.js + Express
- MySQL (XAMPP / phpMyAdmin)
- JWT para autenticación
- Deploy en Vercel

Frontend: https://github.com/Macahuarte09/canchapp-frontend
API desplegada: https://canchapp-backend-4cdk-red.vercel.app/api

## Requisitos

- Node.js
- MySQL (por ejemplo XAMPP)

## Configuración local

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

## Postman

En la carpeta `postman` está la colección para importar y probar todos los endpoints. Tiene una variable `base_url`: por defecto apunta a `http://localhost:3000`, y se puede cambiar por la dirección de la API en Vercel.

## Deploy

Está subido a Vercel (la configuración está en `vercel.json`). Hay que cargar las variables del `.env` en el panel de Vercel y usar una base de datos MySQL que sea accesible desde internet.
