# InternFit v3 — Powered by ChintuAI 🤖

A complete redesign of your internship platform with **real AI**, **live job listings**, **beautiful reports**, and **persistent conversation memory**.

---

## What's new in v3

| Feature | v2 | v3 |
|---|---|---|
| AI name | Fitty | **ChintuAI** |
| Chat UI | Small corner popup | Full-screen panel with history |
| AI engine | Claude Haiku | **Claude Sonnet** (much smarter) |
| ATS analysis | Rule-based only | **AI-powered deep analysis** |
| Job listings | Static samples | **Live from Remotive API** |
| Career paths | Generic message | **Visual career timelines** |
| Reports | Boring bars | **Animated, beautiful, specific** |
| Data storage | Basic localStorage | **Full session persistence** |
| Voice input | ❌ | **✅ Built-in (Chrome/Edge)** |
| Conversation memory | Single session | **Multiple saved conversations** |

---

## Quick Start

### Option A — No backend (Built-in mode)
Just open `index.html` in a browser. You get:
- ✅ Resume analysis (rule-based scorer)
- ✅ Live job listings (Remotive API)
- ✅ Career path visualizations
- ✅ Roadmap and tracker
- ✅ Basic ChintuAI (built-in responses)

### Option B — Full AI mode (Recommended)
Deploy the Cloudflare Worker to unlock deep AI analysis and smart conversations.

---

## Deploying ChintuAI (Cloudflare Worker)

### Step 1: Create a Cloudflare Worker
1. Go to [dash.cloudflare.com](https://dash.cloudflare.com)
2. Click **Workers & Pages** → **Create Application** → **Create Worker**
3. Paste the contents of `worker.js`
4. Click **Deploy**

### Step 2: Add your API key
1. In the Worker dashboard, go to **Settings** → **Variables and Secrets**
2. Add a **Secret** named `ANTHROPIC_API_KEY` with your key from [console.anthropic.com](https://console.anthropic.com)
3. Optional: Add `MODEL` variable = `claude-sonnet-4-6` (default)
4. Optional: Add `ALLOWED_ORIGIN` = your GitHub Pages URL for security

### Step 3: Connect in the app
1. Open `index.html`
2. In the **Check your resume** section, paste your Worker URL (e.g. `https://chintuai.your-username.workers.dev`)
3. Click **Connect**
4. You'll see "✓ Connected to ChintuAI"

---

## Hosting on GitHub Pages

1. Create a new GitHub repo
2. Upload `index.html` (and optionally `.nojekyll`)
3. Go to **Settings** → **Pages** → Source: **main branch**
4. Your site will be live at `https://username.github.io/repo-name`

---

## ChintuAI can answer questions like:

- "Why is my ATS score low?"
- "Which internship should I apply to?"
- "Create a 6-week study plan for me"
- "Help me prepare for my interview at Zoho"
- "Write a cover letter for the ML intern role"
- "Explain React hooks like I'm a beginner"
- "What skills am I missing for a data science role?"
- "Improve this bullet: worked on bug fixes"
- "What should I focus on this week?"
- "Can you remember what we discussed about my resume?"

---

## Architecture

```
User Browser
  ↓
index.html (frontend)
  ├── Local ATS engine (always works)
  ├── Remotive API (live jobs)
  ├── localStorage (resume, history, tracker)
  └── ChintuAI Worker (optional, recommended)
         ↓
    Cloudflare Worker
         ↓
    Anthropic Claude API
         ↓
    Streaming response
```

---

## Worker endpoints

| Method | Path | What it does |
|---|---|---|
| GET | `/health` | Check connection status |
| GET | `/jobs?field=web` | Proxy live job listings |
| POST | `/analyze` | AI-powered ATS analysis |
| POST | `/career` | Personalized career advice |
| POST | `/` | Main ChintuAI chat |

---

## Environment variables

| Name | Required | Default | Description |
|---|---|---|---|
| `ANTHROPIC_API_KEY` | ✅ Yes | — | Your Anthropic API key |
| `MODEL` | No | `claude-sonnet-4-6` | Claude model to use |
| `ALLOWED_ORIGIN` | No | `*` | Restrict CORS to your domain |

---

## Data privacy

- Your resume text is analyzed **locally in the browser** by the built-in scorer
- When ChintuAI is connected, your resume summary and chat messages go to **your own Cloudflare Worker** — not to us
- Conversations are stored in **your browser's localStorage** only
- No accounts, no tracking, no data collected by InternFit

---

## Troubleshooting

**"AI server did not respond"**
→ Check your Worker URL. Test it at `https://your-worker.workers.dev/health`

**"ANTHROPIC_API_KEY is not set"**  
→ Add the secret in Cloudflare Worker settings → Variables and Secrets

**Jobs not loading**
→ Remotive API may be temporarily unavailable. Curated sample listings will show instead.

**Voice not working**
→ Voice input requires Chrome or Edge. Make sure microphone permission is granted.

**Resume not auto-loading**
→ Browser might have cleared localStorage. Paste your resume again and it will be remembered.
