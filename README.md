# Project INDRA

Project INDRA is a cyber-fraud monitoring and response platform for ATM cash-out threat detection.  
It combines:

- A **FastAPI backend** that serves health/dispatch endpoints and streams fraud alerts.
- A **Next.js frontend** dashboard for visual threat monitoring and operator workflows.
- CSV-based demo data for rapid local testing.

## Repository Structure

- `/app` – FastAPI backend (`app/main.py`, `app/threat_streamer.py`)
- `/data` – threat input data (`flagged_transactions.csv`)
- `/frontend` – primary Next.js dashboard app
- `/docker-compose.yml` + `/Dockerfile` – backend container setup

## Features

- Real-time-style threat feed using CSV alert data.
- Health endpoint for service monitoring.
- Dispatch action endpoint scaffold.
- Security-focused dashboard UI with role-based dispatch gating in frontend logic.

## Prerequisites

- Python 3.12+
- Node.js 20+ and npm
- (Optional) Docker + Docker Compose

## Backend Setup (FastAPI)

From repository root:

```bash
cd /home/runner/work/Project_indra/Project_indra
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

Backend runs at: `http://localhost:8000`  
Health check: `http://localhost:8000/health`

## Frontend Setup (Next.js)

From repository root:

```bash
cd /home/runner/work/Project_indra/Project_indra/frontend
npm install
npm run dev
```

Frontend runs at: `http://localhost:3000`

### Optional WebSocket Configuration

If you have a live websocket stream, set:

```bash
NEXT_PUBLIC_COMMAND_CORE_WS_URL=ws://localhost:8000/ws/threats
```

## Run Backend with Docker

From repository root:

```bash
cd /home/runner/work/Project_indra/Project_indra
docker compose up --build
```

Backend container exposes port `8000`.

## API Endpoints

- `GET /health` – backend health status
- `POST /api/dispatch` – dispatch trigger endpoint
- `WS /ws/threats` – websocket threat stream

## Data

Threat data is loaded from:

- `/home/runner/work/Project_indra/Project_indra/data/flagged_transactions.csv`

The frontend also reads CSV data from its public directory:

- `/home/runner/work/Project_indra/Project_indra/frontend/public/flagged_transactions.csv`

## Security Notes

- Do **not** hardcode bot/chat credentials in production.
- Replace placeholder dispatch integration values with secure environment-based secrets.

## License

Add your project license information here.