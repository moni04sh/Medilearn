# MEDILEARN — AR-Based Medical Training Platform

Short description
- MEDILEARN is an AR-enabled medical learning platform that combines immersive 3D anatomy visualization with explainable AI diagnostics to support interactive medical training.

Key highlights
- Frontend: immersive WebAR viewer with responsive SPA UX built in React + TypeScript using Three.js and WebXR.
- AI: hybrid medical image classifier (EfficientNet‑B0 + ViT) with Grad-CAM explainability (backend/ML).
- Deployment: containerized services with Docker / docker-compose for reproducible local and cloud deployments.

Technologies
- Frontend: React, TypeScript, WebXR APIs, Three.js, GLTFLoader, CSS modules / Tailwind (if used)
- Backend & ML: Python (Flask or FastAPI — verify repo), PyTorch 2.x, Grad-CAM, trained model artifacts
- DevOps: Docker, docker-compose, PostgreSQL (if used)
- Misc: Git, npm/yarn, venv (Mac/Linux)

Repository layout
- backend/ — backend server and ML integration (Python)
- frontend/ — React + TypeScript single-page application and WebAR viewer
- trained_models/ — (gitignored) saved model checkpoints and artifacts
- docker-compose.yml — multi-service development / deployment config
- README.md — this file

Quick start (macOS / Linux)

1. Prerequisites
- Docker & docker-compose installed
- Node.js (v16+) and npm or yarn (for local frontend dev)
- Python 3.9+ (for local backend dev)

2. Run with Docker (recommended)
- Copy backend env example and update secrets:
    cp backend/.env.example backend/.env
- Build & start:
    docker-compose up --build
- Services:
  - Frontend: http://localhost:3000 (or port set in docker-compose)
  - Backend: http://localhost:8000 (or port set in docker-compose)

Local development: backend
- Change to backend directory:
    cd backend
- Create venv and activate:
    python -m venv venv
    source venv/bin/activate
- Install requirements:
    pip install -r requirements.txt
- Configure environment:
    cp .env.example .env
- Run (Flask example):
    flask run --host=0.0.0.0 --port=8000
  (If the repo uses FastAPI, use: uvicorn app.main:app --reload --host 0.0.0.0 --port 8000)

Local development: frontend
- Change to frontend directory:
    cd frontend
- Install dependencies:
    npm install
- Start dev server:
    npm start
- Build for production:
    npm run build
- Common scripts (adjust per package.json): lint, test, build

Frontend developer notes (focus / suggestions to include in PRs or resume)
- Component architecture: document top-level layout, key reusable components (ARViewer, ModelLoader, HeatmapOverlay, Auth flows), and global state approach (Context + reducers or Zustand/Redux).
- AR/3D load strategy: lazy-load GLTF models, implement LOD, use compressed textures, and code-split heavy modules to speed initial load.
- Grad-CAM integration: fetch heatmap images or masks from backend, apply as texture overlays on 3D meshes and synchronize with UI controls.
- Browser compatibility: provide WebXR detection and graceful fallbacks (2D viewer) for non-WebXR browsers.
- Testing: unit tests for components (React Testing Library + Jest) and end-to-end (Playwright or Cypress) for key user flows.
- Performance tools: browser devtools, FPS monitoring, and memory profiling for mobile AR sessions.

Environment variables (examples)
- FRONTEND:
  - REACT_APP_API_BASE_URL=http://localhost:8000
  - REACT_APP_AR_ENABLED=true
- BACKEND (.env.example):
  - SECRET_KEY=...
  - DATABASE_URL=postgres://...
  - MODEL_PATH=/app/trained_models/model.pt

Deployment (production)
- Build frontend: npm run build
- Serve static build via nginx or static file server
- Ensure backend points to production DB and model artifacts
- Use docker-compose or Kubernetes manifests for multi-service orchestration
- Use CI/CD to build images and push to registry (GitHub Actions / GitLab CI example)

Troubleshooting
- WebXR not available: check feature detection in browser (Chrome on Android with WebXR flags) and fall back to 2D viewer.
- Large model downloads: host model artifacts on a CDN or ensure Docker images do not embed large model files; mount model volumes instead.
- CORS errors: ensure backend allows requests from frontend origin in development and production.

Contributing
- Fork the repo, create a feature branch, add focused commits, and open a PR with a clear description and testing steps.
- Keep secrets out of git. If secrets were committed, rotate them immediately.
