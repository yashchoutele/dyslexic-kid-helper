# 🧸 LexiRead — AI Reading Assistant for Kids with Dyslexia

> **Portfolio Project** · React + Flask · Deployed on Render (free tier)

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Click%20Here-brightgreen?style=for-the-badge&logo=render)](https://your-app.onrender.com)
[![GitHub](https://img.shields.io/badge/Source%20Code-GitHub-181717?style=for-the-badge&logo=github)](https://github.com/yashchoutele/dyslexic-kid-helper)

---

## 🎯 What Is This?

**LexiRead** is a full-stack AI-powered reading assistant designed specifically for children with dyslexia. Kids can upload a photo of any text (from a book, worksheet, or document) and instantly get:

- 🔊 **Read Aloud** — word-by-word highlighted text-to-speech
- 📖 **Word Definitions** — click any word for a child-friendly AI explanation
- 🪄 **Text Simplification** — select a hard paragraph and get a simpler version
- ❓ **Comprehension Quizzes** — auto-generated multiple-choice questions
- 🎨 **Dyslexia-friendly UI** — built with the [OpenDyslexic](https://opendyslexic.org/) font, pastel colors, and large spacing

---

## 🖼️ Screenshots

> *(Add your screenshots here after deploying)*

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | React 18, Axios, Web Speech API |
| **Backend** | Python 3.10, Flask, Flask-JWT-Extended |
| **OCR** | Tesseract OCR (via pytesseract), Pillow, pdf2image |
| **AI / LLM** | [Groq API](https://groq.com/) (llama-3.3-70b) |
| **Auth** | JWT tokens, bcrypt password hashing |
| **Database** | SQLite (local) / PostgreSQL (production) |
| **Containerization** | Docker & Docker Compose |
| **Deployment** | Render (free tier) |

---

## ✨ Features At a Glance

| Feature | Description |
|---|---|
| 📄 **File Upload & OCR** | Upload images (PNG, JPG, BMP, TIFF) or PDFs — text extracted automatically |
| 🔊 **Read Aloud** | Real-time word-by-word highlighting as the text is spoken |
| 📖 **Word Definitions** | Click any word → centered popup with a simple child-friendly definition |
| 🪄 **Simplify Paragraph** | Highlight complex text → AI rewrites it at a lower reading level |
| ❓ **Quiz Generation** | 2 multiple-choice comprehension questions generated from the text |
| 👤 **Profile System** | Up to 3 profiles per deployment with secure password auth (JWT) |
| 🗣️ **Pronunciation Checker** | Practice reading words aloud and get instant feedback |
| 🔒 **Rate Limiting** | Brute-force protection on login/signup endpoints |

---

## 🚀 Try It Live

**Live URL:** `https://your-app.onrender.com` *(update after deploying)*

### Demo Accounts

You can create your own profile directly in the app (up to 3 profiles supported). Just click **"Create New Profile"** on the login screen and set a username/password.

> ⚠️ This is a free-tier deployment — the backend spins down after 15 minutes of inactivity. First load may take **~30 seconds** to wake up.

---

## 💻 Run Locally

### Option A: Docker (Easiest)

```bash
# Clone the repo
git clone https://github.com/yashchoutele/dyslexic-kid-helper.git
cd dyslexic-kid-helper

# Copy and fill in your env vars
cp .env.example .env
# Edit .env: set GROQ_API_KEY and JWT_SECRET_KEY

# Build and start
docker-compose up --build
```

Open [http://localhost:3000](http://localhost:3000)

### Option B: Manual Setup

**Backend:**
```bash
cd backend
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate  # macOS/Linux
pip install -r requirements.txt
python app.py
```

**Frontend (new terminal):**
```bash
cd frontend
npm install
npm start
```

**Requirements:** [Tesseract OCR](https://github.com/UB-Mannheim/tesseract/wiki), [Poppler](https://github.com/oschwartz10612/poppler-windows/releases), [Groq API key](https://console.groq.com)

---

## 🌐 Deploy to Render (Free)

Full step-by-step instructions: **[DEPLOYMENT.md](./DEPLOYMENT.md)**

**Summary:**
1. Create a free [Render](https://render.com) account
2. Deploy the **backend** as a Web Service (`./backend`, Python, `gunicorn app:app`)
3. Deploy the **frontend** as a Static Site (`./frontend`, `npm run build`, `./build`)
4. Set environment variables: `GROQ_API_KEY`, `JWT_SECRET_KEY`, `REACT_APP_API_URL`

---

## 📁 Project Structure

```
dyslexic-kid-helper/
├── backend/
│   ├── app.py              # Flask API routes & JWT auth
│   ├── ai_services.py      # Groq AI (definitions, simplify, quiz)
│   ├── ocr_processor.py    # Tesseract OCR text extraction
│   ├── db_models.py        # SQLAlchemy Profile model
│   ├── requirements.txt    # Python dependencies
│   └── Dockerfile
├── frontend/
│   ├── src/
│   │   ├── App.js          # Main app + auth state
│   │   ├── components/
│   │   │   ├── ProfileSelector.js   # Login screen
│   │   │   ├── ProfileCreator.js    # Signup screen
│   │   │   ├── Uploader.js          # File upload + OCR trigger
│   │   │   ├── Reader.js            # TTS, word definitions, simplify
│   │   │   ├── Quiz.js              # Comprehension quiz
│   │   │   └── PronunciationChecker.js
│   ├── package.json
│   ├── nginx.conf          # SPA routing, gzip, security headers
│   └── Dockerfile
├── docker-compose.yml
├── .env.example            # Template for all required env vars
├── DEPLOYMENT.md           # Step-by-step Render deployment guide
└── README.md
```

---

## 📡 API Reference

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/api/health` | — | Health check |
| `GET` | `/api/profiles` | — | List all profiles |
| `POST` | `/api/profiles/create` | — | Create a new profile |
| `POST` | `/api/profiles/login` | — | Login & receive JWT |
| `DELETE` | `/api/profiles/:id` | JWT | Delete profile |
| `POST` | `/api/upload` | JWT | Upload file → OCR text |
| `POST` | `/api/define` | JWT | Get word definition |
| `POST` | `/api/simplify` | JWT | Simplify a paragraph |
| `POST` | `/api/quiz` | JWT | Generate comprehension quiz |

---

## 🔑 Environment Variables

Copy `.env.example` to `.env` and fill in:

```env
GROQ_API_KEY=your_groq_api_key_here      # Free at console.groq.com
JWT_SECRET_KEY=your_random_secret_here    # Generate: python -c "import secrets; print(secrets.token_hex(32))"
REACT_APP_API_URL=http://localhost:5000   # Backend URL
```

---

## ❓ Troubleshooting

| Problem | Solution |
|---|---|
| Backend won't start | Check `GROQ_API_KEY` is set in `.env` |
| OCR returns garbage | Ensure Tesseract is installed and in PATH |
| PDF upload fails | Install Poppler and add its `bin/` to PATH |
| Frontend can't reach backend | Check `REACT_APP_API_URL` matches your backend port |
| Quiz fails for Hindi text | Quiz only supports English — this is by design |

---

## 📝 License

This is a portfolio/educational project. Feel free to explore the code!

---

> **Built with ❤️ to help kids read better** 🌟
