...existing code...
# Medilearn (Team_59)

Short description: Medilearn is a medical learning tool (Team 59).

## Contents
- backend/ — backend (Flask/Python)
- frontend/ — frontend (Node)
- docker-compose.yml — docker config

## Quick start (Docker)
1. Copy example env:
   cp backend/.env.example backend/.env
2. Start:
   docker-compose up --build

## Local backend
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
flask run

## Local frontend
cd frontend
npm install
npm start

Notes:
- Do not commit backend/.env, backend/app.db, trained_models/, venv/, or node_modules/.
- If secrets were pushed earlier, rotate them.