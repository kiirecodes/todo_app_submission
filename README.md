# Unique Full-Stack To-Do App (React + Django)

This repository contains a **full-stack To-Do List application** built for job submissions. The project was created to be both practical and attractive to hiring managers: it includes clear code structure, inline comments explaining intent, unit tests for backend and frontend, and UX features that show product thinking.

## Highlights
- Django REST Framework backend with per-user tasks
- React frontend with search, filtering (status & priority), and a small stats dashboard
- Clear comments and tests to show engineering discipline
- CORS and simple session auth included for local dev
- Ready-to-run (see instructions below)

## Quick start (development)
### Backend
1. Create virtualenv and install:
```bash
cd todo_backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pip install django-filter
python manage.py migrate
python manage.py createsuperuser  # optional: create an admin
python manage.py runserver
```
The API is available at `http://localhost:8000/api/tasks/`. For browser login, use `http://localhost:8000/api-auth/login/`.

### Frontend
1. Install & start:
```bash
cd todo_frontend
npm install
npm start
```
Open `http://localhost:3000`.

## Testing
### Backend
```bash
cd todo_backend
source venv/bin/activate
python manage.py test
```

### Frontend
```bash
cd todo_frontend
npm test
```

## Notes for reviewers / hiring managers
- The project keeps the backend API focused and secure: tasks are filtered by owner in `get_queryset`.
- The frontend is componentized, and small product decisions (search, stats, priority) are present to show product sensibility.
- Replace `SECRET_KEY` in `settings.py` and tighten CORS/DEBUG for production.

Good luck with your submission — feel free to ask for a custom theme, additional features (drag-and-drop ordering, recurring tasks, CI config), or a polished production-ready deployment config.

## Added polish (automatically included)
- Drag-and-drop reordering (persisted to backend via `order` field) powered by `react-beautiful-dnd`.
- GitHub Actions CI workflow to run backend and frontend tests on push / PR.
- Dockerfiles and a `docker-compose.yml` for quick local demos (development mode).

## Migrations after pulling changes
Because the `Task` model now includes an `order` field, create migrations:
```bash
cd todo_backend
python manage.py makemigrations
python manage.py migrate
```

## UI upgrade: Tailwind + Framer Motion
- The frontend now uses Tailwind CSS for a modern utility-first design.
- Framer Motion is used for subtle animations (entrance, hover, reorder).
- New dashboard layout with sidebar, overview card, and a polished glass-like theme.

### Dev notes for Tailwind
After pulling:
```bash
cd todo_frontend
npm ci
# build tailwind output if you want the compiled css file:
npm run build:css
npm start
```
(You can also run the postcss build step during CI or integrate with a bundler.)


## Deployment (Render backend + Vercel frontend)

### Backend (Render)
1. Push this repo to GitHub.
2. Create a new **Web Service** on Render and connect your GitHub repo.
3. Use the `render.yaml` as a starting point; set environment variable `DJANGO_SECRET_KEY` in Render's dashboard.
4. Render will run `pip install -r todo_backend/requirements.txt` and migrate automatically if you keep the buildCommand.
5. After deploy, copy the backend URL (e.g. `https://unique-todo-backend.onrender.com`) — you'll use it for the frontend.

### Frontend (Vercel)
1. Connect your GitHub repo on Vercel and import the project.
2. Set the Root Directory to `.` and the Build Command as `npm run --prefix todo_frontend build` and Output Directory `todo_frontend/build`.
3. Set an environment variable `REACT_APP_API_URL` to your Render backend API base, e.g. `https://unique-todo-backend.onrender.com/api/`.
4. Deploy — Vercel will build and serve the optimized React app.

### Credits
Developed by **Kiire Constantine** — use this app in your job submission. It demonstrates: product thinking, clean REST API design, responsive UI, animations, DnD, CI, and production deploy readiness.

Deploy notes generated on: 2025-10-21T17:49:15.765178 UTC
