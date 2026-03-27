# Despliegue Docker

Proyecto independiente para desplegar el sistema completo de reclamos usando Docker.
Orquesta 3 contenedores: **PostgreSQL**, **Backend (Spring Boot)** y **Frontend (Angular + Nginx)**.

---

## Requisitos Previos

- **Docker** >= 24.x
- **Docker Compose** >= 2.x

Verificar instalación:
```bash
docker --version
docker compose version
```

---

## Estructura del Proyecto

```
banco-reclamos-docker/
├── docker-compose.yml          ← Orquestación de los 3 servicios
├── .env                        ← Variables de entorno
│
├── backend/
│   ├── Dockerfile              ← Imagen del backend (Java 21)
│   ├── app.jar                 ← Compilado del backend (tú lo copias aquí)
│   └── application.properties  ← Config que sobreescribe la del JAR
│
├── frontend/
│   ├── Dockerfile              ← Imagen del frontend (Nginx)
│   ├── nginx.conf              ← Configuración de Nginx + proxy reverso
│   └── dist/                   ← Build de Angular (tú lo copias aquí)
│       └── (archivos del build)
│
├── database/
│   └── init.sql                ← Script de inicialización de PostgreSQL
│
└── README.md
```

---

## Ejecutar

```bash
# Levantar todo (primera vez)
docker compose up -d --build

# Ver logs
docker compose logs -f

# Ver logs de un servicio específico
docker compose logs -f backend
docker compose logs -f frontend
docker compose logs -f postgres

# Detener
docker compose down

# Detener y eliminar volúmenes
docker compose down -v
```

---

## Acceso

| Servicio         | URL                                           |
|------------------|-----------------------------------------------|
| **Frontend**     | http://localhost:4200/app-reclamos/            |
| **Backend API**  | http://localhost:8080/api/                     |
| **Swagger UI**   | http://localhost:8080/swagger-ui.html          |
| **PostgreSQL**   | localhost:5432 (user_reclamos / useradmin)     |

---

## Credenciales de Prueba

| Cédula       | Nombre                    | Contraseña  |
|--------------|---------------------------|-------------|
| 1712345678   | Juan Carlos Pérez López   | juan1234    |
| 1798765432   | María Elena González Ruiz | maria1234   |
| 0501234567   | Carlos Andrés Ramírez T.  | carlos1234  |
| 0912345678   | Ana Gabriela Mendoza S.   | ana1234     |
| 1104567890   | Luis Fernando Castillo H. | luis1234    |

> Se cargan automáticamente al iniciar el backend (DataLoader).

---

**Nginx** sirve el frontend y actúa como proxy reverso: las peticiones a `/v1/api/` las redirige al backend. Esto elimina problemas de CORS en Docker.
