# BLACKROCK · MediMind AI

> AI-powered personal health intelligence platform for medical report understanding, prescription extraction, alerts, reminders, doctor/lab booking, secure sharing, PDF export, and safe AI chat.

## Overview

BLACKROCK is an end-to-end health intelligence system that transforms medical reports and prescriptions into actionable insights. Upload PDFs, images, or prescriptions—get instant AI-powered summaries, abnormality detection, risk assessments, and medicine reminders. Share securely, export PDFs, and chat with a medical-aware AI assistant.

---

## Technology Stack

### Frontend
- **React 18** with Vite for fast builds
- **Tailwind CSS** for responsive design
- **React Router** for navigation
- **Axios** for HTTP requests
- **Framer Motion** for animations
- **Recharts** for medical data visualization
- **Lucide Icons** for UI
- **React Hot Toast** for notifications

### Backend
- **FastAPI** for high-performance async API
- **SQLAlchemy** for ORM
- **SQLite** for persistent storage
- **Pydantic** for data validation
- **JWT** with email/password authentication
- **Passlib + bcrypt** for password hashing
- **python-jose** for token management

### AI & Storage
- **Google Gemini** for report analysis and chat (backend only)
- **Groq** for assisted prescription/chat (optional)
- **Local file storage** under `backend/storage/` for uploaded files

---

## Project Structure

```
ai-services/
├── backend/              # FastAPI REST API
│   ├── app/
│   │   ├── main.py       # FastAPI app initialization
│   │   ├── config.py     # Environment & settings
│   │   ├── database.py   # SQLAlchemy setup
│   │   ├── models.py     # Database ORM models
│   │   ├── schemas.py    # Pydantic request/response schemas
│   │   ├── security.py   # JWT & auth utilities
│   │   ├── routers/      # API route handlers
│   │   └── services/     # Business logic (AI, PDF, storage, etc.)
│   ├── requirements.txt  # Python dependencies
│   ├── .env.example      # Example environment variables
│   └── storage/          # File storage (user uploads, generated PDFs)
│
├── frontend/             # React/Vite web application
│   ├── src/
│   │   ├── pages/        # Page components
│   │   ├── components/   # Reusable components
│   │   ├── context/      # Auth & app state
│   │   ├── services/     # API service layer
│   │   ├── utils/        # Helper functions
│   │   └── styles/       # Custom CSS & animations
│   ├── package.json      # Node dependencies
│   ├── vite.config.js    # Vite configuration
│   ├── tailwind.config.js # Tailwind settings
│   └── index.html        # Entry HTML
│
└── medimind_flutter/     # Flutter mobile scaffold (future)
```

---

## Key Features

### 📄 Medical Report Management
- Upload PDFs, PNG, JPG, JPEG with automatic validation
- Size and type checking for security
- Instant AI-generated summaries and findings
- Abnormality detection with risk level badges
- Timeline visualization of medical events

### 💊 Prescription Intelligence
- Extract medicines and dosages from prescriptions
- Smart medicine reminders and follow-ups
- Alert system for critical conditions

### 👨‍⚕️ Healthcare Navigation
- Doctor appointment booking
- Lab test booking and tracking
- Health insights and recommendations

### 🔐 Secure Sharing
- Generate shareable links with random tokens
- Expiry dates and optional password protection
- Password hashing for privacy
- No public file serving

### 📊 Dashboard & Analytics
- Personal health card with key metrics
- Report history and timeline
- Diet suggestions and wellness tracking
- Voice narration for accessibility

### 🤖 AI Health Assistant
- Non-diagnostic, safety-focused chat
- Medical terminology support
- Secure, backend-only API key usage

### 📥 Data Export
- Generate formatted PDFs from reports
- Download health summaries

---

## Quick Start

### Prerequisites
- Python 3.9+
- Node.js 16+
- Git

### Backend Setup

```bash
cd backend

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env and add your API keys:
#   GEMINI_API_KEY=your_key_here
#   DATABASE_URL=sqlite:///./app.db

# Run server
uvicorn app.main:app --reload
```

Backend runs on `http://localhost:8000`. API docs at `http://localhost:8000/docs`.

### Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Configure environment
cp .env.example .env
# Edit .env:
#   VITE_API_BASE_URL=http://localhost:8000

# Start dev server
npm run dev
```

Frontend runs on `http://localhost:5173`.

### Launch

1. Open [http://localhost:5173](http://localhost:5173)
2. Sign up with email and password
3. Upload a medical report (PDF, PNG, JPG)
4. View AI-generated summary, findings, and risk level
5. Explore dashboard, alerts, reminders, bookings, and chat

---

## Core API Routes

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/auth/signup` | POST | User registration |
| `/auth/login` | POST | User login (returns JWT) |
| `/auth/logout` | POST | User logout |
| `/reports/upload` | POST | Upload & analyze medical report |
| `/reports/{id}` | GET | Get report details |
| `/prescriptions/upload` | POST | Upload prescription |
| `/prescriptions/{id}/extract` | GET | Extract medicines |
| `/alerts` | GET | List health alerts |
| `/medicine-reminders` | GET | Get medicine reminders |
| `/appointments/doctors` | POST | Book doctor appointment |
| `/appointments/labs` | POST | Book lab test |
| `/share/{token}` | GET | Access secure shared report |
| `/chat` | POST | Chat with AI assistant |
| `/downloads/pdf/{report_id}` | GET | Download report as PDF |

---

## Security & Privacy

✅ **Encryption & Authentication**
- Passwords hashed with bcrypt
- JWT tokens with expiry for stateless auth
- HTTPS recommended in production

✅ **File Security**
- MIME type and extension validation
- Random filename generation
- Never served as public URLs
- Cleaned up after processing

✅ **API Security**
- API keys stored backend-only
- Frontend uses only `VITE_API_BASE_URL`
- Request validation with Pydantic
- SQLAlchemy ORM prevents SQL injection
- CORS policy enforced

✅ **Data Privacy**
- Report access restricted to owner
- Secure share links use random tokens + optional password
- Token expiry ensures time-limited access
- No personal data in logs

✅ **AI Safety**
- AI output rendered as text (no raw HTML)
- Medical disclaimer always shown
- Non-diagnostic language enforced

---

## Medical Disclaimer

⚠️ **Important:** The AI-generated explanations provided by this platform are **for informational support only** and **do not constitute medical diagnosis or advice**. 

- Always consult a qualified healthcare professional before making medical decisions
- Seek urgent medical care if symptoms are severe, sudden, or worsening
- This tool is a personal health assistant, not a replacement for professional medical care

---

## Environment Variables

### Backend (`.env`)
```env
DATABASE_URL=sqlite:///./app.db
GEMINI_API_KEY=your_gemini_key_here
GROQ_API_KEY=your_groq_key_here  # Optional
JWT_SECRET_KEY=your_secret_key_here
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

### Frontend (`.env`)
```env
VITE_API_BASE_URL=http://localhost:8000
```

---

## Development

### Running Tests (Backend)
```bash
cd backend
pytest
```

### Building Frontend for Production
```bash
cd frontend
npm run build
# Output: dist/
```

### Deployment
- **Backend:** Deploy with Gunicorn/Uvicorn to cloud (Heroku, Railway, Vercel, etc.)
- **Frontend:** Deploy dist folder to Netlify, Vercel, or any static host

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit changes: `git commit -m "feat: add my feature"`
4. Push to branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## License

This project is provided as-is for personal and educational use.

---

## Support & Contact

For issues, feature requests, or questions:
- Open an issue on GitHub
- Contact: [your-email@example.com]

---

**Built with ❤️ for personal health intelligence.**
