# DocMind — Document Q&A (RAG-Based)

A business-focused, Retrieval-Augmented Generation (RAG) web application that lets users upload documents (PDF, DOCX, TXT) and ask natural-language questions, receiving precise, cited answers grounded entirely in their own files.

![Status](https://img.shields.io/badge/status-active-success)
![License](https://img.shields.io/badge/license-MIT-blue)

### 🔗 [Live Demo](https://docmind6.netlify.app)

> 💡 To try the AI Q&A feature without API credits, sign up → **Settings → Demo Mode → ON**

---

## ✨ Features

- **Authentication** — email/password signup & login, plus Google Sign-In
- **Document upload** — drag-and-drop PDF, DOCX, TXT, HTML (up to 50MB)
- **Real text extraction** — PDF.js-powered parsing, page-aware chunking
- **Smart retrieval** — keyword + phrase-scored chunk ranking (BM25-style)
- **Grounded Q&A** — answers generated only from retrieved document context, with source citations
- **Full dashboard** — Documents, Q&A History, Collections, Members, Analytics, API & Integrations, Profile, Settings
- **Demo Mode** — generates realistic answers locally from real document content, with zero API cost — ideal for presentations and interviews
- **Single-file deployment** — the entire app is one self-contained `index.html`

---

## 🏗️ Architecture

```
Browser (index.html)
   │
   ├── PDF.js — client-side text extraction
   ├── Local chunking + BM25-style retrieval
   │
   └── Cloudflare Worker (proxy) ──▶ Anthropic Claude API
                                      (bypasses browser CORS restrictions)
```

- **Frontend:** Vanilla HTML/CSS/JS — no build step, no framework
- **AI:** Claude (Anthropic API), called via a lightweight Cloudflare Worker proxy
- **Auth & data:** Stored in browser `localStorage` (demo-grade; swap for a real backend in production)

---

## 🚀 Quick Start

### 1. Deploy the site
The entire app is a single `index.html` file.

**Option A — Netlify Drop (fastest)**
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag in `index.html`
3. Get a live URL instantly

**Option B — Any static host**
Upload `index.html` to GitHub Pages, Vercel, Cloudflare Pages, or any static file host.

### 2. Set up the AI proxy (Cloudflare Worker)
Browsers block direct calls to the Anthropic API (CORS), so a small proxy is required:

1. Create a free account at [dash.cloudflare.com](https://dash.cloudflare.com)
2. Go to **Workers & Pages → Create → Create Worker**
3. Replace the default code with the contents of `worker.js` (included in this repo)
4. Deploy — copy your Worker URL (e.g. `https://your-worker.username.workers.dev`)
5. In `index.html`, find the `fetch(...)` call inside `sendMsg()` and update the URL to your Worker's address

### 3. Add your Anthropic API key
1. Get a key from [console.anthropic.com](https://console.anthropic.com)
2. Open the deployed site → sign up → **Settings → Anthropic API Key**
3. Paste your key and save

### 4. Try it
- Upload a PDF or TXT document
- Wait for status to show **Ready**
- Ask a question — get a cited, grounded answer

---

## 🎤 Running without API credits (Demo Mode)

For presentations, interviews, or testing without billing:

1. Go to **Settings → Demo Mode**
2. Toggle it **ON**
3. Ask questions — answers are generated locally from real retrieved document content, no API calls or cost

---

## 📁 Project Structure

```
docmind-app/
├── index.html      # Complete application (HTML + CSS + JS)
├── worker.js        # Cloudflare Worker — secure Anthropic API proxy
└── README.md
```

---

## 🔒 Security Notes

- API keys are stored in `sessionStorage` (cleared when the browser tab closes) — never written to disk or sent to any third party
- The Cloudflare Worker only forwards requests to Anthropic — it does not log or store keys
- This is a demo-grade auth system (`localStorage`-based) — replace with a real authentication backend (e.g. Supabase, Firebase, Auth0) before production use with real users

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| PDF parsing | PDF.js |
| AI | Anthropic Claude API |
| Proxy | Cloudflare Workers |
| Auth (demo) | Browser `localStorage` |
| Hosting | Netlify / any static host |

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🙋 Use Cases

- Legal & compliance document review
- Financial report analysis
- HR policy and onboarding Q&A
- Research paper summarization
- Customer support knowledge bases
- Real estate contract review
