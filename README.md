# DOE VFO Queue — Development

Lightweight Flask backend with a static HTML/CSS/JS frontend for a simple queuing system used by the DOE Visayas Field Office.

## Overview

- **Backend:** `app.py` — Flask app exposing REST endpoints for queue management and staff assignment.
- **Frontend:** `index.html` (operator UI) and `display.html` (public display).
- **Static assets:** `js/` (app.js, queue.js, data.js), `css/` (style.css).
- **Database:** SQL schema and migrations in `sql/`.

## Quick start (development)

1. (Optional) Create a virtual environment and activate it.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Install dependencies:

```powershell
python -m pip install -r requirements.txt
```

If you don't have `requirements.txt`, install the core packages:

```powershell
python -m pip install flask pymysql python-dotenv flask-cors
```

3. Copy `env.example` to `.env` and fill in your database credentials.

4. Initialize the database using the SQL files in the `sql/` folder (see `sql/schema.sql`).

5. Run the Flask server:

```powershell
```
python app.py
```

The server will listen on `http://0.0.0.0:5001` (or the address shown by Flask). Static pages are served from the project root.

## Running the frontend only

You can open `index.html` and `display.html` directly in a browser or use the Live Server extension in VS Code to serve them locally.

## Configuration

Environment variables read by the app (also in `env.example`):

- `DB_HOST` — database host
- `DB_USER` — database username
- `DB_PASSWORD` — database password
- `DB_NAME` — database name

## Database

Use the files under `sql/` to create or migrate the schema. Start with:

- `sql/schema.sql`
- `sql/migrate_fixes.sql`

The current schema expects tables such as `srf_servicerequest`, `auth_user`, and `accounts_userdata`.

## Main API endpoints

- GET /api/queue, GET /api/staff — read current state
- GET /api/add_to_queue/<ticket> — runs the round-robin assignment for a request
- PUT /api/queue/<id>/serve, /done, /notes — status transitions
- PUT /api/staff/<id>/toggle — mark staff absent/present
- GET /api/tracker/* — reporting/summary endpoints for a date range

## Project structure

```
├── app.py           # Flask backend and API
├── index.html       # Operator UI
├── display.html     # Public display
├── css/             # Styles
├── js/              # Frontend scripts
└── sql/             # Database schema & migrations
```

