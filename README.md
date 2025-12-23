# Trading Platform

A simple trading-data platform for querying, visualising and exporting trade and share information.

This repository contains a Python backend, a React frontend, and basic Terraform infra used to deploy supporting resources.

## Repository layout

- `backend/` — Flask-based API and data utilities.
	- `app.py` — main Flask application entrypoint.
	- `fetch_trades.py` — utilities to ingest trade data.
	- `query_implementation.py` — query helpers used by the API.
	- `create_visualisation.py` — scripts to produce charts/visualisations.
	- `requirements.txt` — Python dependencies.
	- `Dockerfile` — container image for the backend.

- `frontend/` — React single-page application.
	- `src/` — React source files and components.
	- `public/` — static HTML and manifest.
	- `Dockerfile` — container image for the frontend.

- `tfinfra/` — Terraform configuration used to provision cloud resources.

## Prerequisites

- Python 3.10+ (backend)
- Node.js 16+ and npm (frontend)
- Docker (optional, for container builds)
- Terraform (if planning to apply infra in `tfinfra/`)

## Quick start (local development)

Backend (venv):

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r backend/requirements.txt
cd backend
FLASK_APP=app.py flask run --host=127.0.0.1 --port=5000
```

Frontend (dev server):

```bash
cd frontend
npm install
npm start
```

The frontend expects the backend API at `http://localhost:5000` by default.

## Docker

Build and run backend image:

```bash
docker build -t trading-backend ./backend
docker run -p 5000:5000 trading-backend
```

Build and run frontend image:

```bash
docker build -t trading-frontend ./frontend
docker run -p 3000:3000 trading-frontend
```

## Terraform

See the `tfinfra/` directory for Terraform configuration and state files. Review `main.tf` before running `terraform init` and `terraform apply`.
