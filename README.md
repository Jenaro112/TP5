# TP5 - Gestor de Tareas Fullstack (React, Express, PostgreSQL y Docker)

**Materia:** Programación Avanzada  
**Estudiante:** Jenaro Galdini  
**Tecnologías:** React, Vite, Express, PostgreSQL, Docker Compose  

## Descripción

Aplicación web Fullstack para la gestión de tareas de proyectos (estilo Jira / Trello simplificado).
Permite crear, listar, filtrar y gestionar tareas clasificadas por proyecto, tipo de actividad (Feature, Bug, etc.), prioridad y estado.

## Arquitectura

El sistema se compone de 3 servicios contenerizados y orquestados mediante **Docker Compose**:
1. **Frontend:** React + Vite (puerto `5173`)
2. **Backend:** Node.js + Express REST API (puerto `3001`)
3. **Base de Datos:** PostgreSQL 16 con volumen Docker para persistencia de datos (puerto `5432`)

## Estructura del Proyecto

```text
TP5/
├── backend/
│   ├── src/
│   │   ├── controllers/   # Lógica de controladores (tareas.controller.js)
│   │   ├── routes/        # Definición de rutas Express (tareas.routes.js)
│   │   ├── db.js          # Pool de conexión a PostgreSQL
│   │   └── index.js       # Punto de entrada de la API Express
│   ├── init.sql           # Script SQL inicial (tabla tareas y datos iniciales)
│   ├── Dockerfile         # Imagen Docker del backend
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/    # Componentes React (TareaForm, ListadoTareas)
│   │   ├── App.jsx        # Componente principal
│   │   └── main.jsx
│   ├── Dockerfile         # Imagen Docker del frontend
│   ├── vite.config.js
│   └── package.json
├── docker-compose.yml     # Orquestación de contenedores
└── .gitignore
```

## Cómo ejecutar

### Con Docker Compose (Recomendado)

1. En la raíz del proyecto `TP5`, ejecutar:
   ```bash
   docker compose up --build
   ```

2. Acceder a los servicios:
   - **Frontend:** [http://localhost:5173](http://localhost:5173)
   - **Backend API:** [http://localhost:3001/api/tareas](http://localhost:3001/api/tareas)
   - **PostgreSQL:** accesible en el puerto `5432` (`POSTGRES_USER: postgres`, `POSTGRES_DB: tp5_tareas`)

3. Para detener los contenedores:
   ```bash
   docker compose down
   ```
   *(Para borrar también el volumen de datos persistente: `docker compose down -v`)*

### Ejecución Local (sin Docker)

1. **Backend:**
   ```bash
   cd backend
   npm install
   npm run dev
   ```

2. **Frontend:**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```
