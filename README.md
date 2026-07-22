
# AI Rural Learning Assistant — Local Development

This repository contains a Next.js frontend (`client/`) and an Express backend (`server/`).

This document explains how to run both locally and how to push the combined repository to GitHub.

**Prerequisites**
- Node.js (v18+ recommended)
- npm
- Git
- Docker (optional, recommended for running MongoDB locally)

## Quick start (recommended)

1) Start MongoDB (docker-compose)

```bash
cd <repo-root>
docker compose up -d
# this starts a MongoDB instance at mongodb://localhost:27017
```

2) Start backend

```bash
cd server
npm install
# Create or update .env with at least:
# MONGO_URI=mongodb://127.0.0.1:27017/ai_education
# JWT_SECRET=your_jwt_secret
# GEMINI_API_KEY=optional_gemini_key
npm start
```

Backend health check:

```bash
curl http://localhost:5000/health
```

3) Start frontend (dev)

```bash
cd client
npm install
npx next dev -H 0.0.0.0 -p 3000
# open http://localhost:3000
```

4) Build frontend (production)

```bash
cd client
npm run build
npm start
```

## Alternative: Use MongoDB Atlas
- Create a free cluster on MongoDB Atlas and update `server/.env` `MONGO_URI` with the provided connection string.

## Running both concurrently
- Open two terminals: run backend in one and frontend in the other using the commands above.
- Optionally install `concurrently` and create a top-level `npm` script to run both.

## Git: push combined repository to GitHub

This workspace contains a nested `client/.git` (a separate repo). To push the whole workspace as a single repository, remove the nested Git folder and push from the root.

1) Remove nested repo (only if you want a single repository):

Windows (PowerShell):
```powershell
Remove-Item -Recurse -Force client\.git
```

macOS / Linux:
```bash
rm -rf client/.git
```

2) Configure git (if needed), commit and push

```bash
cd <repo-root>
git init
git config user.name "Your Name"
git config user.email "you@example.com"
git add .
git commit -m "chore: initial combined project"
git branch -M main
git remote add origin https://github.com/YOUR_USER/YOUR_REPO.git
git push -u origin main
```

If you prefer to keep `client` as a separate repo, push it separately (enter `client/` and push to its own remote).

## Notes & troubleshooting
- If the backend fails to connect to MongoDB: ensure the service is running (docker compose up -d) or that `MONGO_URI` points to a working MongoDB.
- If the frontend build complains about types or empty pages: I added minimal placeholder pages to allow successful builds. Replace them with real pages as you develop.
- To enable Gemini AI, set `GEMINI_API_KEY` in `server/.env`. Without it, AI endpoints return a fallback message.

## Files added to help local dev
- `docker-compose.yml`: starts a MongoDB container for local development.
- Updated `client` and `server` to be runnable locally (see scripts in each folder).

If you want, I can now:
- remove `client/.git` and push the combined repo to your GitHub (please provide the repo URL), or
- guide you step-by-step through running Docker or installing MongoDB locally.
AI Rural Learning Assistant

Starter repository scaffold for the AI Rural Learning Assistant hackathon project.

Overview
- Frontend: React (Vite)
- Backend: Node.js + Express
- Database: MongoDB (mongoose)

Features included in this scaffold
- Express server with health check
- OCR route integrated with Google Vision API
- QA route integrated with OpenAI / LLM provider (fallback stub available)
- MongoDB connection helper
- Minimal React app with image upload and question UI

Getting started
1. Backend
   cd backend
   npm install
   Create a .env file with:
     MONGO_URI=your_mongodb_connection_string
     GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account.json
     # or GOOGLE_API_KEY=your_vision_api_key
     OPENAI_API_KEY=your_openai_api_key
   npm start

2. Frontend
   cd frontend
   npm install
   npm run dev

Notes
- OCR now uses Google Vision API and accepts multipart image uploads or base64 payloads.
- For local development, run backend and frontend separately and keep the backend at http://localhost:4000.





