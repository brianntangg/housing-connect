# 🏠 Housing Connect

**A full-stack web application that helps individuals and families find low-income housing and related support services.**

## 📚 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [API Endpoints](#api-endpoints)
- [Environment Variables](#environment-variables)
- [Testing](#testing)
- [Deployment](#deployment)

## 🧠 Overview

Housing Connect is designed to simplify the housing search journey by centralizing affordable housing listings, eligibility filters, and support resources for individuals and families in need.

## 🚀 Features

- 🔍 Search low-income housing listings by location, family size, and income
- 📑 Save and track housing applications
- 🧭 Access support services such as legal aid, shelters, and financial assistance
- 🧾 Personalized document checklist for application readiness
- 🔐 Secure authentication and user dashboard
- 🌐 Mobile-friendly, multilingual-ready interface

## 🛠 Tech Stack

**Frontend**
- React + TypeScript
- Vite
- Material UI
- TanStack Query
- Mapbox

**Backend**
- FastAPI
- SQLModel + Pydantic
- PostgreSQL
- Redis

**DevOps**
- Docker
- GitHub Actions
- Azure WebApps

## 🏗️ Architecture

```text
             ┌────────────────────────────┐
             │     Client (React App)     │
             │  (Vite + TypeScript + MUI) │
             └────────────┬───────────────┘
                          │  REST API
                          ▼
             ┌────────────────────────────┐
             │      FastAPI Backend       │
             │  (Python + Pydantic + ORM) │
             └────────────┬───────────────┘
          ┌───────────────┴───────────────┐
          ▼                               ▼
┌─────────────────┐           ┌─────────────────┐
│   PostgreSQL    │           │     Redis       │
│ (SQLModel ORM)  │           │ (Caching / TTL) │
└─────────────────┘           └─────────────────┘
```

## 🛠 Project Structure
```
housing-connect/
├── .env.example
├── README.md
├── docker-compose.yml
├── backend/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── alembic.ini
│   ├── alembic/
│   │   ├── env.py
│   │   └── versions/
│   └── app/
│       ├── __init__.py
│       ├── main.py
│       ├── api/
│       ├── core/
│       ├── models/
│       │   └── user.py
│       ├── schemas/
│       │   └── user.py
│       └── services/
│           └── auth.py
├── frontend/
│   ├── Dockerfile
│   ├── index.html
│   ├── package.json
│   ├── tsconfig.json
│   ├── vite.config.ts
│   └── src/
│       ├── main.tsx
│       ├── App.tsx
│       ├── api/
│       ├── components/
│       │   └── Navbar.tsx
│       ├── hooks/
│       └── pages/
│           ├── Home.tsx
│           └── Login.tsx

```

## 🧰 Getting Started
Prerequisites
- Docker + Docker Compose
- Node.js ≥ 18.x
- Python ≥ 3.11

Setup
```
git clone https://github.com/brianntangg/housing-connect.git
cd housing-connect
cp .env.example .env
```

Start App
```
# From root directory
docker-compose up --build
```
- Frontend: http://localhost:5173
- Backend: http://localhost:8000/docs

## 🧩 API Endpoints

### 🔐 Auth & User
| Method | Endpoint             | Description                            |
|--------|----------------------|----------------------------------------|
| POST   | `/api/auth/register` | Register a new user                    |
| POST   | `/api/auth/login`    | Log in and receive access token (JWT) |
| GET    | `/api/users/me`      | Get profile of the logged-in user     |

### 🏠 Listings
| Method | Endpoint              | Description                            |
|--------|-----------------------|----------------------------------------|
| GET    | `/api/listings`       | Retrieve housing listings (filterable) |
| GET    | `/api/listings/{id}`  | Get a specific listing by ID           |
| POST   | `/api/listings`       | Create a new listing *(admin/internal)*|

### 📄 Applications
| Method | Endpoint                  | Description                               |
|--------|---------------------------|-------------------------------------------|
| GET    | `/api/applications`       | List saved/submitted applications by user |
| POST   | `/api/applications`       | Save or submit a new application          |
| GET    | `/api/applications/{id}`  | Retrieve a single application by ID       |

### 🧭 Resources
| Method | Endpoint         | Description                                 |
|--------|------------------|---------------------------------------------|
| GET    | `/api/resources` | List of support resources (shelters, aid)   |

### 🛠 Miscellaneous
| Method | Endpoint   | Description            |
|--------|------------|------------------------|
| GET    | `/ping`    | Health check endpoint  |
| GET    | `/docs`    | Swagger UI (OpenAPI)   |

## 🔐 Environment Variables
Create a .env file in the root and fill in:
```
# Shared
MAPBOX_API_KEY=your-mapbox-api-key
JWT_SECRET=your-secret

# Backend
DATABASE_URL=postgresql://user:pass@db:5432/housingconnect
REDIS_URL=redis://redis:6379/0

# Frontend
VITE_API_BASE_URL=http://localhost:8000
```

## ✅ Testing
General Testing Commands
```
# Backend
cd backend
pytest

# Frontend
cd frontend
npm test
```

Linting and formatting:
```
# Backend
ruff . && black .

# Frontend
npm run lint && npm run format
```

## 🚀 Deployment
Use GitHub Actions or Azure DevOps to deploy Docker containers:
- Azure WebApps (Docker)
- GitHub CI for tests and builds
- Auto-deploy on merge to main


