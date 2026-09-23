# Bariatric Patient Support Forum

A standalone web application built as a peer-support discussion forum for people who have had (or are considering) bariatric surgery. Patients can browse and start discussion threads on topics like post-op diet, recovery, mental health, and exercise, reply and like posts, and log their day-to-day mood in a personal mood journal with a calendar view of past entries.

## About this project

This app was built as part of a funded, compensated research initiative between **Mayo Clinic** and the **University of Wisconsin–Eau Claire**. Team members were selected for the initiative through a faculty-run selection process. Several student teams worked in parallel under this same initiative, but **each team designed, built, and shipped its own independent, standalone mini-application with its own repository and its own executable** — this was never one shared or integrated codebase across teams. This repository is this team's project: a bariatric surgery patient support forum. At the end of the initiative, the completed application was demoed to stakeholders from Mayo Clinic.

## What the app does

- **Discussion forum** — Browse existing discussion threads, search by title, and sort by date, alphabetically, or by unanswered threads.
- **Threads & replies** — Start a new discussion, view a thread's full content, reply to it, and like/unlike both threads and individual replies.
- **Ownership-based moderation** — Thread/comment authors (or an authenticated admin) can delete their own posts and comments.
- **Admin login** — A simple username/password admin login issues a session token that grants delete privileges across the forum.
- **Mood journal** — Log a mood, a 1–10 rating, and a reason; view your mood history in a list or browse a monthly calendar and click any day to see that day's entries.
- **Recently viewed sidebar** — Tracks the last few threads you've opened (stored in the browser) for quick access.

User "login" in this app is a lightweight, demo-level display-name system (not a real authentication system) — it was built for demo purposes to show functionality to Mayo Clinic stakeholders, not as a production-ready patient-facing deployment.

## Tech stack

Verified directly from the codebase (`package.json`, `requirements.txt`, and imports):

**Frontend**
- React 19 + React Router 7 (`react-router-dom`)
- Bootstrapped with Create React App (`react-scripts` 5)
- Axios for HTTP requests to the backend
- Plain CSS per-component (no CSS framework)

**Backend**
- Python / Flask (`flask`, `flask-cors`)
- MySQL via `mysql-connector-python`

**Data**
- MySQL database with `discussions`, `comments`, `admins`, and `mood_entries` tables (see `flask-server/forum_db.sql`)

## Running it locally

This project has two parts that both need to be running: a MySQL database + Flask API, and a React frontend.

**1. Database**
```bash
mysql -u root -p
```
Then run the schema and (optionally) seed data:
```sql
SOURCE flask-server/forum_db.sql;
SOURCE flask-server/populate_forum.sql;   -- optional sample discussions/admin/mood data
```
> `flask-server/server.py` currently connects with `host="localhost"`, `user="root"`, `password=""`, `database="your_database"` — update these to match your local MySQL setup if different.

**2. Backend (Flask API)**
```bash
cd flask-server
python -m venv venv
venv\Scripts\activate        # Windows; use `source venv/bin/activate` on macOS/Linux
pip install -r requirements.txt
python server.py
```
The API runs on `http://localhost:5001`.

**3. Frontend (React)**
```bash
npm install
npm start
```
The app runs on `http://localhost:3000` and talks to the Flask API at `http://localhost:5001`.

## My Contribution

I'm Gabriel Tapia Martinez (GitHub: `grtm23`). Based on this repository's git history (excluding a `node_modules/` directory and `package-lock.json` that were briefly committed and later removed, which otherwise skew the diff stats):

- **38.9%** of commits (14 of 36)
- **65.2%** of line insertions, **84.0%** of line deletions

I built the **thread detail page** (viewing threads, replies, like/unlike, owner/admin delete menus, comment posting), the **mood journal** (mood/rating/reason flow, history, and calendar view), the **forum home page** (discussion list, search, sort, login and admin login UI), and most of the **Flask backend API** (discussions, comments, likes, admin login, mood endpoints, and owner/admin authorization logic), plus the new-thread modal and routing in `App.js`.

