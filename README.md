# bankchurn-docker-api

API de predicción de abandono de clientes (*bank churn*) empaquetada en un contenedor Docker.
Repositorio base de los talleres 7, 8 y 9 del curso **Proyecto: Desarrollo de Soluciones**
(MAIA — Universidad de los Andes), que comparten el mismo material de partida.

- **Taller 7** — despliegue continuo en Railway (PaaS) conectado a este repositorio.
- **Taller 8** — construcción de la imagen y ejecución del contenedor sobre una instancia EC2.
- **Taller 9** — publicación de la imagen en AWS ECR y despliegue en ECS.

## Estructura

- `Dockerfile` — receta de la imagen: parte de `python:3.12-slim`, crea un usuario sin
  privilegios, instala las dependencias y arranca la API con `run.sh`.
- `bankchurn-api/` — código de la API (FastAPI + uvicorn)
  - `app/` — rutas `/health` y `/predict`, esquemas y configuración
  - `model-pkg/` — el `.whl` del modelo, instalado como dependencia vía `requirements.txt`
  - `run.sh` — `uvicorn app.main:app --host 0.0.0.0 --port $PORT`

El puerto no está fijo en el código: se lee de la variable de entorno `PORT`, lo que permite
que la plataforma de despliegue asigne el suyo sin modificar la imagen.
