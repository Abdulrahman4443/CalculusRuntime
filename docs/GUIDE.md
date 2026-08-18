# Running CalculusRuntime Locally

This guide covers running the **backend** (`backend/`, Starlette API) and the **frontend**
(`frontend/`, React app) on your machine. Each runs in its own terminal.

---

## Prerequisites

| Tool    | Min version | Check              |
| ------- | ----------- | ------------------ |
| Python  | 3.10+       | `python --version` |
| pip     | 23+         | `pip --version`    |
| Node.js | 18+         | `node -v`          |
| npm     | 9+          | `npm -v`           |

`backend/` and `frontend/` are git submodules. If you just cloned the repo, initialize them first:

```powershell
git submodule update --init --recursive
```

---

## 1 — Backend (Starlette API)

**PowerShell**

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn main:app --reload --port 8002
```

**macOS / Linux**

```bash
cd backend
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8002
```

The API is now live at `http://127.0.0.1:8002`. Visit `http://127.0.0.1:8002/docs` for the
interactive endpoint reference, or check `http://127.0.0.1:8002/api/health`.

### Backend environment

`backend/.env` already exists in this repo with working local defaults (`PROGRESS_DB=sqlite`),
so no changes are required to get started. To reset it from scratch, copy the example:

```powershell
cp backend/.env.example backend/.env
```

Key variables (see `backend/.env.example` for the full list):

| Variable                    | Purpose                                                        |
| ---------------------------- | --------------------------------------------------------------- |
| `SECRET_KEY`                 | JWT signing secret                                              |
| `TOKEN_EXPIRE_MINUTES`       | JWT lifetime (default 10080 = 7 days)                           |
| `PROGRESS_DB`                | `sqlite` (default, zero setup) or `supabase`                    |
| `DB_PATH`                    | SQLite file path, created automatically on first run            |
| `SUPABASE_URL` / `SUPABASE_SERVICE_ROLE_KEY` | Required only when `PROGRESS_DB=supabase`        |
| `ALLOWED_ORIGINS`            | Comma-separated CORS allowlist — must include the frontend URL  |

With `PROGRESS_DB=sqlite` (the current default), the database file is created automatically
on first run — no extra setup needed.

---

## 2 — Frontend (React)

```powershell
cd frontend
npm install
npm start
```

This opens `http://localhost:3000` in your browser.

### Frontend environment

The frontend reads its backend URL from `frontend/.env`:

```env
REACT_APP_API_URL=http://127.0.0.1:8002
```

If this doesn't match the port the backend is running on, update it and restart `npm start`
(Create React App only reads `.env` at startup).

---

## Quick smoke test

1. Start the backend (Terminal 1) and confirm `http://127.0.0.1:8002/api/health` returns
   `{"status": "ok"}`.
2. Start the frontend (Terminal 2) and open `http://localhost:3000`.
3. Sign up for an account, complete a section, and open **Dashboard** — progress should sync
   through the backend.

---

## Running both together (quick reference)

```
Terminal 1 — Backend
  cd backend
  .\.venv\Scripts\Activate.ps1
  uvicorn main:app --reload --port 8002

Terminal 2 — Frontend
  cd frontend
  npm start
```

| Service                | URL                          |
| ----------------------- | ----------------------------- |
| Frontend                | http://localhost:3000        |
| Backend API              | http://127.0.0.1:8002        |
| Backend docs (Swagger-style) | http://127.0.0.1:8002/docs |

---

## Other services (optional)

This repo also includes two more submodules that the frontend can talk to, but neither is
required to run the core app:

- **`calculussolver/`** — the calculus-solving API. The frontend uses a hosted instance by
  default; see `docs/START.md` for local setup if you need to run it yourself.
- **`Calculus-AI-Chatbot/`** — the AI chat microservice. See its own `README.md` for setup.

---

## Troubleshooting

**`ModuleNotFoundError` when starting the backend**
The virtual environment isn't activated — re-run the `Activate.ps1` / `source .venv/bin/activate` step.

**CORS errors in the browser console**
Confirm the backend is running and that `ALLOWED_ORIGINS` in `backend/.env` includes
`http://localhost:3000`.

**`npm install` fails or the app won't start**
Delete `frontend/node_modules` and `frontend/package-lock.json`, then run `npm install` again.

**"database is locked" errors**
Only run one `uvicorn` worker locally with SQLite — the default `--reload` flag is fine, avoid
adding `--workers 2+`.

**Frontend can't reach the backend**
Check `frontend/.env` — `REACT_APP_API_URL` must match the host/port the backend is actually
running on, and the frontend must be restarted after changing it.
