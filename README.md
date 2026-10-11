<div align="center">

# ⛓️ BlockNova

### A Production-Grade Blockchain Simulation Built from Scratch

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-3.x-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com)
[![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://www.sqlite.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

*Full-stack blockchain with SHA-256 Proof of Work, RSA wallet generation, cryptographically signed transactions, real-time dashboard, and a REST API — all in Python.*

[Features](#-features) · [Architecture](#-architecture) · [Quick Start](#-quick-start) · [API Reference](#-api-reference) · [Tech Stack](#-tech-stack)

</div>

---

## 🎯 Why BlockNova?

Most blockchain tutorials stop at theory. **BlockNova** is a fully functional blockchain node you can run locally — complete with cryptographic wallets, digitally signed transactions, PoW consensus, and a live analytics dashboard. It's designed to demonstrate real-world blockchain engineering concepts through clean, production-quality code.

---

## ✨ Features

| Category | Details |
|---|---|
| 🔗 **Blockchain Core** | Genesis block auto-creation · SHA-256 hashing with sorted JSON encoding · Chain integrity validation |
| ⛏️ **Proof of Work** | Configurable difficulty (4-leading-zero target) · Nonce discovery · Full hash verification |
| 🔐 **Cryptographic Wallets** | RSA-2048 key pair generation · PKCS#1 v1.5 digital signatures · Server-side transaction signing |
| 💰 **Transactions** | Cryptographic signature verification · Real-time balance tracking per address · Transaction pool management |
| 🌐 **REST API** | Mine blocks · Submit transactions · Query chain · Register peer nodes |
| 📊 **Live Dashboard** | Chain statistics · Block growth chart · Transaction volume visualization · Wallet management panel |
| 💾 **Persistence** | SQLAlchemy ORM · SQLite storage for blocks & transactions |

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────┐
│                   Browser (Dashboard)                │
│         Charts · Wallet Panel · Transaction UI       │
└──────────────────────┬───────────────────────────────┘
                       │ HTTP
┌──────────────────────▼───────────────────────────────┐
│                  Flask REST API (app.py)              │
│     /mine  /transactions  /chain  /wallet  /nodes    │
└──────────────────────┬───────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────┐
│             Blockchain Engine (blockchain.py)         │
│      Block Creation · PoW · Chain Validation         │
├──────────────────┬───────────────────────────────────┤
│  core/crypto.py  │         core/database.py          │
│  RSA Wallets     │         SQLAlchemy Models          │
│  Sign & Verify   │         Block & Tx Persistence     │
└──────────────────┴───────────────┬───────────────────┘
                                   │
                        ┌──────────▼──────────┐
                        │   SQLite Database    │
                        │  (blockchain.db)     │
                        └─────────────────────┘
```

---

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/prasenjitshinde11/blocknova.git
cd blocknova

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the blockchain node
python app.py
```

Open `http://127.0.0.1:5000` in your browser to access the dashboard.

---

## 📡 API Reference

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/chain` | Returns the full blockchain |
| `GET` | `/mine` | Mines a new block with pending transactions |
| `POST` | `/transactions/new` | Submits a new signed transaction |
| `POST` | `/wallet/new` | Generates a new RSA wallet keypair |
| `GET` | `/wallet/balance/<address>` | Returns balance for a given wallet |
| `POST` | `/nodes/register` | Registers a new peer node |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| **Language** | Python 3.10+ |
| **Web Framework** | Flask |
| **Cryptography** | PyCryptodome (RSA-2048, PKCS#1 v1.5) |
| **Database** | SQLite + SQLAlchemy ORM |
| **Frontend** | Jinja2 Templates, Chart.js |
| **Hashing** | SHA-256 (hashlib) |

---

## 📁 Project Structure

```
blocknova/
├── app.py              # Flask routes & REST API
├── blockchain.py       # Block creation, PoW, chain validation
├── core/
│   ├── crypto.py       # RSA wallet generation, signing, verification
│   └── database.py     # SQLAlchemy models & DB config
├── templates/          # Jinja2 frontend templates
├── static/             # CSS, JS, Chart.js assets
├── requirements.txt    # Python dependencies
└── README.md
```

---

## 🔑 Key Engineering Decisions

- **RSA-2048 for wallet security** — Industry-standard asymmetric encryption for transaction signing
- **PKCS#1 v1.5 signatures** — Deterministic signing scheme for transaction integrity
- **SHA-256 with sorted JSON** — Ensures consistent block hashing regardless of key ordering
- **SQLAlchemy ORM** — Clean data layer with easy migration to PostgreSQL for production
- **Blueprint-ready Flask** — Modular architecture prepared for horizontal scaling

---

## 📬 Contact

**Prasenjit Shinde** — CS Undergrad @ SIRT Bhopal

[![GitHub](https://img.shields.io/badge/GitHub-prasenjitshinde11-181717?style=flat-square&logo=github)](https://github.com/prasenjitshinde11)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-prasenjitshinde11-0A66C2?style=flat-square&logo=linkedin)](https://linkedin.com/in/prasenjitshinde11)

---

<div align="center">

**If you found this project useful, consider giving it a ⭐**

</div>
