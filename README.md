# 🔮 Oracle's Decree — DeepFake Detector

> An AI-powered deepfake detection platform for images, videos, and audio — built with React + Flask.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![React](https://img.shields.io/badge/react-18-61DAFB?logo=react)
![HuggingFace](https://img.shields.io/badge/models-HuggingFace-orange)

---

## 📸 Overview

**Oracle's Decree** is a full-stack deepfake detection application that analyzes images, videos, and audio files for signs of AI manipulation. It uses a dual-model HuggingFace ensemble for visual media, librosa signal analysis for audio, and Google Gemini to generate a forensic summary.

---

## ✨ Features

| Feature | Details |
|---|---|
| 🖼️ **Image Detection** | Dual HuggingFace model ensemble (`dima806` + `prithivMLmods`) |
| 🎥 **Video Detection** | FFmpeg frame extraction + per-frame ensemble scoring with center-weighting |
| 🎵 **Audio Detection** | Librosa MFCC variance + spectral flatness analysis |
| 🤖 **Forensic Summary** | Google Gemini generates a 3-sentence AI forensic report |
| 📡 **Live Progress** | Real-time SSE streaming progress bar during analysis |
| 📊 **Dashboard** | Scan history, stats, and recent results |
| 🌐 **Live Shield** | Webcam-based real-time deepfake detection |

---

## 🧱 Tech Stack

### Frontend
- **React 18** + **TypeScript**
- **Vite** dev server with proxy to Flask
- **Lucide React** icons
- Vanilla CSS with glassmorphism/cyberpunk design system

### Backend
- **Flask** (Python 3.10+)
- **HuggingFace Inference API** — image/video classification
- **Librosa** — audio signal analysis
- **Google Gemini API** — forensic summary generation
- **FFmpeg** — video frame extraction

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- Python 3.10+
- FFmpeg installed and accessible in PATH
- HuggingFace API token
- Google Gemini API key

---

### 1. Clone the repository

```bash
git clone https://github.com/ankit-sharma-cyber/DeepFake-Detector.git
cd DeepFake-Detector
```

---

### 2. Backend Setup

```bash
cd backend

# Create and activate a virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
copy .env.example .env
```

Edit `backend/.env` and fill in your API keys:

```env
HUGGINGFACE_API_TOKEN=hf_your_token_here
GEMINI_API_KEY=your_gemini_key_here
```

Start the Flask server:

```bash
python app.py
# Server runs at http://localhost:5000
```

---

### 3. Frontend Setup

```bash
# From the project root
npm install
npm run dev
# App runs at http://localhost:5173
```

---

## 🔑 Environment Variables

| Variable | Required | Description |
|---|---|---|
| `HUGGINGFACE_API_TOKEN` | ✅ Yes | HuggingFace token for image/video models |
| `GEMINI_API_KEY` | ✅ Yes | Google Gemini key for forensic summaries |
| `FLASK_DEBUG` | No | Set `true` for debug mode |
| `CONFIDENCE_THRESHOLD` | No | Detection threshold (default: `0.85`) |
| `AMBIGUITY_MARGIN` | No | Margin for UNKNOWN verdict (default: `0`) |
| `MAX_CONTENT_LENGTH` | No | Max upload size in bytes (default: 100 MB) |

Get your keys here:
- 🤗 **HuggingFace**: [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)
- 🔮 **Gemini**: [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)

---

## 🧠 Detection Pipeline

```
Upload File
     │
     ├─ Image ──► HF Model A (dima806)  ┐
     │            HF Model B (prithiv)  ├─► Ensemble Average ──► Verdict
     │                                  ┘
     ├─ Video ──► FFmpeg Frame Extract ──► Per-frame Ensemble ──► Weighted Avg ──► Verdict
     │
     └─ Audio ──► Librosa MFCC Variance + Spectral Flatness ──► Threshold Rules ──► Verdict
                                                                        │
                                                               Gemini Forensic Summary
```

---

## 📁 Project Structure

```
DeepFake-Detector/
├── backend/
│   ├── app.py                  # Flask app & API routes
│   ├── requirements.txt
│   ├── .env.example
│   ├── services/
│   │   ├── image_detector.py   # HF ensemble for images
│   │   ├── video_detector.py   # FFmpeg + HF ensemble for videos
│   │   ├── audio_detector.py   # Librosa audio analysis
│   │   ├── gemini_analyzer.py  # Gemini forensic summary
│   │   └── scan_store.py       # Scan history & stats
│   └── utils/
│       └── file_utils.py
├── src/
│   ├── components/
│   │   ├── views/
│   │   │   ├── AnalysisView.tsx   # Main scan UI + SSE progress
│   │   │   ├── DashboardView.tsx
│   │   │   └── SettingsView.tsx
│   │   ├── landing/               # Homepage components
│   │   └── LiveDetector.tsx       # Webcam live detection
│   ├── App.tsx
│   └── main.tsx
├── vite.config.ts
└── package.json
```

---

## 📡 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/health` | Server health & model info |
| `POST` | `/api/scan` | Scan a file (synchronous) |
| `POST` | `/api/scan/stream` | Scan with SSE progress stream |
| `POST` | `/api/scan/url` | Scan a file from URL |
| `GET` | `/api/scans/recent` | Recent scan history |
| `GET` | `/api/stats` | Detection statistics |
| `GET/PUT` | `/api/settings` | App settings |
| `GET` | `/api/models` | List available models |

---

## 🛡️ Supported Formats

| Type | Formats |
|---|---|
| Image | JPG, JPEG, PNG, WEBP |
| Video | MP4, AVI, MOV, MKV |
| Audio | WAV, MP3, FLAC |

---

## 📜 License

MIT © [ankit-sharma-cyber](https://github.com/ankit-sharma-cyber)
