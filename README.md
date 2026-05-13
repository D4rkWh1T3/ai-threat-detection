# AngelusVigil — AI Threat Detection System

![Detection Mode](https://img.shields.io/badge/Detection-Hybrid%20ML-red)
![Stack](https://img.shields.io/badge/Stack-FastAPI%20%7C%20React%20%7C%20PostgreSQL-blue)
![Docker](https://img.shields.io/badge/Deploy-Docker%20Compose-informational)

![Dashboard](dashboard.png)

> Real-time AI-powered threat detection engine for web server access logs.
> Detects SQL injection, directory traversal, brute force, and scanner attacks
> using a hybrid ML ensemble (Autoencoder + Random Forest + Isolation Forest).

## Features
- Real-time nginx log analysis with ML ensemble scoring
- Hybrid detection: rules-based + 3 ML models via ONNX inference
- Live dashboard with threat feed, severity levels, top IPs
- FastAPI backend + React/TypeScript frontend
- PostgreSQL + Redis stack
- Auto-trains models on first startup

## Tech Stack
| Layer | Technology |
|---|---|
| Backend | FastAPI, Python 3.14, SQLAlchemy, asyncpg |
| ML | PyTorch, scikit-learn, ONNX Runtime |
| Frontend | React 19, TypeScript, Vite, Zustand |
| Database | PostgreSQL 16, Redis 7 |
| Infra | Docker Compose, Nginx |

## Quick Start
### 1. Clone
```bash
git clone https://github.com/YOUR_USERNAME/ai-threat-detection.git
cd ai-threat-detection
```
### 2. Configure
```bash
cp .env.example .env
nano .env  # Set POSTGRES_PASSWORD (no special chars) and API_KEY
```
### 3. Create Docker resources
```bash
docker network create certgames_default
docker volume create certgames_nginx_logs
```
### 4. Run
```bash
docker compose -f compose.yml up --build
```
### 5. Open
## Simulate Attacks
```bash
for i in {1..20}; do curl -s "http://localhost:46969/search?q=1'+OR+'1'='1"; done
for i in {1..20}; do curl -s "http://localhost:46969/../../etc/passwd"; done
for i in {1..20}; do curl -s -A "sqlmap/1.0" "http://localhost:46969/admin"; done
```

## Project Structure
## Known Setup Fixes
| Issue | Fix |
|---|---|
| CUDA packages failing | CPU-only torch via --extra-index-url |
| @ in password breaking DB URL | Use alphanumeric password only |
| Missing @/core/lib module | Created frontend/src/core/lib/index.ts |
| External Docker network missing | docker network create certgames_default |
| PostgreSQL 18 volume issue | Downgraded to postgres:16-alpine |

## License
MIT
