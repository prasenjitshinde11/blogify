<div align="center">

# 📝 Blogify

### A Production-Ready Blogging Platform with Full Authentication & Social Features

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-3.1-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org)
[![Render](https://img.shields.io/badge/Deployed_on-Render-46E3B7?style=for-the-badge&logo=render&logoColor=white)](https://blogify-jitt.onrender.com)

*Full-stack blog with Bcrypt auth, AJAX likes, email password reset, avatar uploads, full-text search, and PostgreSQL — deployed on Render.*

[Live Demo](https://blogify-jitt.onrender.com) · [Features](#-features) · [Architecture](#-architecture) · [Quick Start](#-quick-start) · [Tech Stack](#-tech-stack)

</div>

---

## 🎯 Why Blogify?

Building a real-world web application means handling **authentication**, **authorization**, **file uploads**, **email services**, **database migrations**, and **deployment** — all at once. **Blogify** tackles every one of these concerns in a clean, modular Flask codebase using industry-standard patterns like the Application Factory and Blueprint architecture.

> 🌐 **Live Demo:** [blogify-jitt.onrender.com](https://blogify-jitt.onrender.com)

---

## ✨ Features

| Category | Details |
|---|---|
| 🔐 **Authentication** | Registration · Bcrypt password hashing · Flask-Login session management · CSRF protection |
| 📧 **Password Reset** | Time-limited email tokens via `itsdangerous` · SMTP integration via Flask-Mail |
| ✍️ **Content Management** | Full CRUD for blog posts · Rich text editing · Draft management |
| 💬 **Social Interactions** | Comments on posts · AJAX-powered like system (no page reload) |
| 👤 **User Profiles** | Avatar upload & processing (Pillow) · Profile editing · Account management |
| 🔍 **Discovery** | Full-text post search · Welcome landing page with platform statistics |
| 🗄️ **Database** | SQLAlchemy ORM · Flask-Migrate for schema migrations · SQLite (dev) / PostgreSQL (prod) |
| 🚀 **Deployment** | Gunicorn WSGI · ProxyFix for HTTPS behind reverse proxy · Environment-based config |

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────┐
│                    Browser Client                     │
│          Read Posts · Like · Comment · Search         │
└──────────────────────┬───────────────────────────────┘
                       │ HTTPS
┌──────────────────────▼───────────────────────────────┐
│              Gunicorn WSGI Server                     │
│                   (Production)                        │
└──────────────────────┬───────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────┐
│          Flask Application (Factory Pattern)          │
│                fast.py → create_app()                │
├──────────────┬──────────────────┬────────────────────┤
│  Blueprint:  │   Blueprint:     │   Blueprint:       │
│    main      │     users        │     posts          │
│  Home, Feed  │  Auth, Profile   │  CRUD, Comments    │
│  Search      │  Password Reset  │  Likes             │
└──────────────┴────────┬─────────┴────────────────────┘
                        │
┌───────────────────────▼──────────────────────────────┐
│              SQLAlchemy ORM Layer                     │
│     Models: User · Post · Comment · Like             │
├──────────────────────┬───────────────────────────────┤
│   SQLite (dev)       │      PostgreSQL (prod)        │
└──────────────────────┴───────────────────────────────┘
```

---

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/prasenjitshinde11/blogify.git
cd blogify

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set environment variables
export SECRET_KEY="your-secret-key"
export SQLALCHEMY_DATABASE_URI="sqlite:///site.db"

# Initialize the database
flask db upgrade

# Run the development server
python fast.py
```

Open `http://127.0.0.1:5000` — you'll see the welcome landing page.

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| **Language** | Python 3.10+ |
| **Framework** | Flask 3.1 (Application Factory + Blueprints) |
| **ORM** | SQLAlchemy + Flask-Migrate (Alembic) |
| **Auth** | Flask-Login + Flask-Bcrypt |
| **Security** | Flask-WTF (CSRF) · `itsdangerous` (timed tokens) |
| **Email** | Flask-Mail (SMTP) |
| **Media** | Pillow (image processing for avatars) |
| **Database** | SQLite (dev) · PostgreSQL (prod) |
| **WSGI** | Gunicorn |
| **Deployment** | Render |
| **Frontend** | Jinja2 · Bootstrap · JavaScript (AJAX) |

---

## 📁 Project Structure

```
blogify/
├── fast.py                 # Entry point + ProxyFix
├── config.py               # Environment-based configuration
├── models.py               # SQLAlchemy models (User, Post, Comment, Like)
├── main/                   # Blueprint: Home feed, search, landing page
├── users/                  # Blueprint: Auth, profile, password reset
├── posts/                  # Blueprint: CRUD, comments, likes
├── templates/              # Jinja2 templates
├── static/                 # CSS, JS, uploaded avatars
├── migrations/             # Flask-Migrate (Alembic) migrations
├── requirements.txt
└── README.md
```

---

## 🔑 Key Engineering Decisions

- **Application Factory Pattern** — Enables testing with multiple app instances and clean configuration management
- **Blueprint Architecture** — Separates concerns (users, posts, main) for maintainability and team scalability
- **Bcrypt + Timed Tokens** — Industry-standard password hashing and secure, expirable reset links
- **AJAX Likes** — Smooth UX with no page reloads, demonstrating async frontend-backend communication
- **ProxyFix Middleware** — Correct HTTPS handling behind Render's reverse proxy for production security
- **Dual Database Support** — SQLite for rapid development, PostgreSQL for production via `DATABASE_URL`

---

## 📬 Contact

**Prasenjit Shinde** — CS Undergrad @ SIRT Bhopal

[![GitHub](https://img.shields.io/badge/GitHub-prasenjitshinde11-181717?style=flat-square&logo=github)](https://github.com/prasenjitshinde11)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-prasenjitshinde11-0A66C2?style=flat-square&logo=linkedin)](https://linkedin.com/in/prasenjitshinde11)

---

<div align="center">

**If you found this project useful, consider giving it a ⭐**

</div>
