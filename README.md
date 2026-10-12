# AI-Powered Vendor Performance Analytics System

An enterprise full-stack platform for vendor management, Mobile OTP authentication, multi-step vendor registration, performance analytics, and AI/ML risk assessment.

## Phases Implemented

- ✅ **Phase 1: Project Foundation** (FastAPI backend + modular architecture + SQLite/PostgreSQL setup + Docs)
- ✅ **Phase 2: Professional UI/UX** (React + TypeScript + Tailwind CSS + Recharts + Responsive Dashboards)
- ✅ **Phase 3: Vendor Mobile + OTP Authentication** (Mobile number auth, Mock OTP service, JWT sessions, Protected routes)
- ✅ **Phase 4: Vendor Registration & Profile** (Multi-step registration wizard, Vendor profile view/edit, Category model, Dynamic profile check)
- ✅ **Phase 5: Performance Analytics** (7 KPI scoring, performance history, analytics dashboard)
- ✅ **Phase 6: Admin Dashboard** (Admin auth, vendor management, audit views)
- ✅ **Phase 7: XGBoost ML Risk Prediction + SHAP** (ML pipeline, risk scoring, explainability)
- ✅ **Phase 8A–8C: AI Vendor Research Agent** (Web retrieval, intelligence extraction, research persistence)
- ✅ **Phase 8D: Recommendations, Alerts, Reports, Settings + Fast2SMS OTP**
- ✅ **Phase 9: AI Vendor Assistant + RAG + SQLite Vector Store + Multi-turn Chat**
- ✅ **Phase 10A: Security Audit & Hardening** (128 tests passing)
- ✅ **Phase 10B: Comprehensive Testing & QA**
- ✅ **Phase 10C: Docker & Production Configuration** (See [docs/PHASE_10C_DOCKER.md](docs/PHASE_10C_DOCKER.md))
- ✅ **Phase 10D: Production Readiness, Security Hardening & Final Integration** (See [docs/FINAL_PRODUCTION_READINESS_REPORT.md](docs/FINAL_PRODUCTION_READINESS_REPORT.md))

---

## Quick Start — Local Development

### 1. Backend Setup (FastAPI)

```bash
cd backend
python -m venv venv

# Windows PowerShell:
.\\venv\\Scripts\\Activate.ps1
# Linux/macOS:
# source venv/bin/activate

pip install -r requirements.txt
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

Backend runs at `http://localhost:8000` · API health: `http://localhost:8000/api/v1/health`

### 2. Frontend Setup (React + Vite)

```bash
cd frontend
npm install
npm run dev
```

Frontend runs at `http://localhost:5173`

### 3. Demo Authentication

| Mode | Instructions |
|------|-------------|
| **Mock OTP (dev)** | Enter any 10-digit mobile number → OTP is `123456` |
| **Real SMS (Fast2SMS)** | Set `OTP_PROVIDER=fast2sms` and `FAST2SMS_API_KEY=<your_key>` in `.env` |

---

## Quick Start — Docker (Production)

### Prerequisites

- Docker Engine ≥ 24.0
- Docker Compose plugin ≥ 2.20

### Steps

```bash
# 1. Configure environment
cp .env.example .env
# Edit .env: set POSTGRES_USER, POSTGRES_PASSWORD, SECRET_KEY, ADMIN_PASSWORD

# 2. Build images and start all services
docker compose up --build -d

# 3. Verify services are healthy
docker compose ps

# 4. Access the application
# Frontend: http://localhost
# API Health (via nginx proxy): http://localhost/api/v1/health
# API Health (direct backend): http://localhost:8000/api/v1/health
```

### Docker Services

| Service    | Host Port | Role                          |
|------------|-----------|-------------------------------|
| `frontend` | 80        | nginx + React SPA + API proxy |
| `backend`  | 8000      | FastAPI REST API              |
| `db`       | (none)    | PostgreSQL — internal only    |

> **PostgreSQL is not exposed to the host.** Only the backend container can reach it.

### Persistence

| Volume          | Contents                                |
|----------------|-----------------------------------------|
| `postgres_data` | PostgreSQL data                        |
| `rag_data`      | Backend data directory (SQLite/RAG)    |
| `reports`       | Generated reports directory            |

### Stop & Clean Up

```bash
# Stop containers (preserve volumes)
docker compose down

# Stop and delete all data (WARNING: irreversible)
docker compose down -v
```

---

## Real SMS Integration (Fast2SMS)

```env
OTP_PROVIDER=fast2sms
FAST2SMS_API_KEY=your_fast2sms_api_key
FAST2SMS_ROUTE=otp
FAST2SMS_TIMEOUT_SECONDS=10
```

> **Fast2SMS API keys are backend-only.** Never set them as `VITE_*` environment variables.

---

## Documentation

- [Architecture](docs/ARCHITECTURE.md)
- [Docker & Production Configuration](docs/PHASE_10C_DOCKER.md)
- [Security Audit (Phase 10A)](docs/PHASE_10A_SECURITY.md)
- [Testing & QA (Phase 10B)](docs/PHASE_10B_QA.md)
- [Project Plan](docs/PROJECT_PLAN.md)
