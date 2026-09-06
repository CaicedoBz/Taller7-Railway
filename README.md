# Taller 7 — Despliegue continuo en PaaS

Taller del curso **Proyecto: Desarrollo de Soluciones** (MAIA — Universidad de los Andes).
Despliegue de una API de predicción de abandono de clientes (*bank churn*) en un contenedor
Docker sobre **Railway**, conectado a este repositorio para que cada push dispare
automáticamente un nuevo build y despliegue.

## Estructura

- `Dockerfile` — receta de la imagen: parte de `python:3.12-slim`, crea un usuario sin
  privilegios, instala las dependencias y arranca la API con `run.sh`.
- `bankchurn-api/` — código de la API (FastAPI + uvicorn)
  - `app/` — rutas `/health` y `/predict`, esquemas y configuración
  - `model-pkg/` — el `.whl` del modelo, instalado como dependencia vía `requirements.txt`
  - `run.sh` — `uvicorn app.main:app --host 0.0.0.0 --port $PORT`

El puerto no está fijo en el código: se lee de la variable de entorno `PORT`, lo que permite
que la plataforma de despliegue asigne el suyo sin modificar la imagen.
