# BLOGIFY

A full-featured blogging web application built with Flask, featuring user authentication, post management, comments, likes, avatar uploads, and password reset via email.

## Problem

Building a blogging platform that handles user accounts, content management, and social interactions (likes, comments) while maintaining security and being deployable to a production server.

## Solution

BLOGIFY is a Flask web application using the application factory pattern and Blueprint architecture. It provides a complete blogging experience — users can register, write posts, interact via comments and likes, manage their profile, and reset their password via email.

## Features

- User registration and login with Bcrypt password hashing
- Session management via Flask-Login
- Create, read, update, and delete blog posts
- Comment on posts
- AJAX-powered post likes
- Profile avatar upload and management (Pillow)
- Password reset via time-limited email tokens (itsdangerous)
- CSRF protection on all forms (Flask-WTF)
- Full-text post search
- Database migrations with Flask-Migrate
- Blueprint architecture (users, posts, main)
- Application factory pattern
- ProxyFix for correct HTTPS handling behind Render's reverse proxy
- Welcome landing page for unauthenticated visitors showing platform stats

## Architecture

```
Browser
   ↓
Gunicorn (WSGI server)
   ↓
fast.py (entry point + ProxyFix)
   ↓
Flask App (create_app factory)
   ↓
Blueprints: main / users / posts
   ↓
SQLAlchemy ORM
   ↓
SQLite (dev) / PostgreSQL (prod via DATABASE_URL)
```

**Blueprints:**
- `main` — home feed, welcome page, search
- `users` — register, login, logout, profile, account update, password reset
- `posts` — create, view, edit, delete posts, comments, likes

**Models:** `User`, `Post`, `Comment`, `Like`

## Tech Stack

**Backend**
- Python
- Flask 3.1.3
- Flask-SQLAlchemy 3.1.1
- Flask-Migrate 4.0.5
- Flask-Bcrypt 1.0.1
- Flask-Login 0.6.3
- Flask-WTF 1.2.1
- Flask-Mail 0.9.1
- itsdangerous (JWT-style password reset tokens)
- Pillow (avatar image processing)
- Gunicorn 23.0.0

**Database**
- SQLite (local development)
- PostgreSQL (production via `DATABASE_URL`)

**Frontend**
- Jinja2 templates
- Custom CSS (glassmorphic UI)

**Deployment**
- Render (render.yaml)

## Project Structure

```
BLOGIFY/
├── fast.py                   # Entry point — create_app() + ProxyFix
├── render.yaml               # Render deployment config
├── requirements.txt
├── flaskblog/
│   ├── __init__.py           # App factory, extensions init
│   ├── config.py             # Config class — reads env vars
│   ├── models.py             # User, Post, Comment, Like models
│   ├── main/
│   │   └── routes.py         # Home feed, search, welcome page
│   ├── users/
│   │   ├── routes.py         # Register, login, profile, password reset
│   │   ├── forms.py
│   │   └── utils.py          # Avatar save, reset email sender
│   └── posts/
│       ├── routes.py         # Post CRUD, comments, likes
│       └── forms.py
└── tests/                    # Directory exists — no tests implemented yet
```

## Getting Started

### Prerequisites

- Python 3.10+
- A Gmail account (or SMTP provider) for password reset emails

### Installation

```bash
git clone https://github.com/prasenjitshinde11/BLOGIFY.git
cd BLOGIFY
pip install -r requirements.txt
```

## Environment Variables

Create a `.env` file in the project root:

```env
SECRET_KEY=your-secret-key-here
DATABASE_URL=sqlite:///site.db
MAIL_USERNAME=your-email@gmail.com
MAIL_PASSWORD=your-email-app-password
```

> **Note:** Never commit your real `.env` file. Generate `SECRET_KEY` with:
> ```bash
> python -c "import secrets; print(secrets.token_hex(32))"
> ```

## Running Locally

```bash
# Apply database migrations
flask db upgrade

# Run the development server
flask run
```

Open `http://localhost:5000` in your browser.

## Demo

Live at: https://blogify-jitt.onrender.com

## Deployment

Deployed on **Render** via `render.yaml`:
- **Build command:** `pip install -r requirements.txt`
- **Start command:** `gunicorn fast:app`

`fast.py` applies `ProxyFix` so Flask correctly handles HTTPS behind Render's reverse proxy.

## Testing

No automated tests are currently implemented. A `tests/` directory exists but is empty.

## Future Improvements

- Write actual unit and integration tests using pytest
- Fix `Pillow==1` pin in requirements.txt (should be `Pillow==10.x`)
- Add GitHub Actions CI/CD pipeline
- Add `.env.example` file
- Add a Dockerfile for containerised deployment
- Add `.gitattributes` to correct language detection (currently shows HTML instead of Python)
- Switch to PostgreSQL in local development to match production

## Author

**Prasenjit Shinde**
