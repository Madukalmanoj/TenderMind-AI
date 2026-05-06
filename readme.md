
  
  
  





## 🏛️ TenderMind AI


AI-Powered Government Tender Evaluation Platform


Turning 3-day manual evaluations into 38-minute traceable verdicts


---


## 🏆 Hackathon

| | |
|---|---|
| **Event** | AI for Bharat 2 — HackerEarth |
| **Theme** | 3: AI-Based Tender Evaluation and Eligibility Analysis for Government Procurement by CRPF |
| **Stage** | ✅ Shortlisted for Prototype Round |
| **Team** | Trust_the_Process |
| **Live Demo** | https://tender-mind-ai--kakashisparta1.replit.app |




  
  
  
  




---

## 🎯 The Problem

Every Monday morning, a CRPF procurement officer sits down with a 60-page tender document, ten bidder submissions totalling 800 pages, and a deadline on Friday.

By Wednesday, two colleagues have marked the same bidder as both eligible and ineligible — neither is wrong, they just read different pages. By Thursday, nobody can remember which document proved which criterion. On Friday the report goes out. Two months later, a rejected bidder files a legal challenge, and nobody can reconstruct the paper trail.

**This is not a rare failure. This is how government procurement evaluation works across India today.**

---

## ✅ The Solution

TenderMind AI is an end-to-end explainable procurement intelligence platform:

- 📄 **Upload a tender** → AI extracts all eligibility criteria in 90 seconds
- 👮 **Officer approves** the criteria checklist before any evaluation starts
- 📦 **Upload bidder packages** → AI evaluates each bidder against every criterion
- 🔍 **Compliance checks** → debarment registry, conflict of interest, shell companies
- ⚖️ **Confidence gating** → auto-commit (≥85%), soft review (65–84%), hard review (<65%)
- 📊 **Review dashboard** → every verdict traceable to source page + bounding box
- 📑 **Signed audit report** → cryptographically signed PDF, legally defensible

**Result:** 38 minutes instead of 3 days. Every verdict traceable. Every rejection defensible.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      TenderMind AI                          │
├──────────────────────┬──────────────────────────────────────┤
│   Frontend           │   Backend                           │
│   React + Vite 7     │   Express 5 + TypeScript            │
│   Tailwind CSS v4    │   Drizzle ORM + PostgreSQL          │
│   React Query        │   Zod v4 validation                 │
├──────────────────────┴──────────────────────────────────────┤
│                    AI / LLM Layer                           │
│  Claude Sonnet (Anthropic) · Llama 3.1 70B (Groq)         │
│  Gemini Flash (Google) · Auto-fallback router              │
├─────────────────────────────────────────────────────────────┤
│              Procurement Intelligence Pipeline              │
│  OCR → Criteria Extraction → Debarment Check →            │
│  Bidder Evaluation → Confidence Gating → Audit Report     │
└─────────────────────────────────────────────────────────────┘
```

---

## ⚡ Key Features

| Feature | Description |
|---|---|
| 🧠 **AI Criteria Extraction** | Parses tender PDFs and extracts structured eligibility rules with source references |
| 🔒 **Officer Approval Gate** | No evaluation starts until officer verifies extracted criteria |
| 📋 **Debarment Check** | Cross-checks bidder GST/PAN against CPPP debarred vendor registry |
| ⚠️ **Conflict of Interest** | Flags bidder directors matching evaluation committee members |
| 🏢 **JV/Consortium Handling** | Aggregates eligibility across joint venture partners correctly |
| 📎 **Corrigendum Detection** | Diffs amended tenders and re-flags changed criteria for re-approval |
| 🎯 **Confidence Gating** | Three-tier system — never auto-rejects uncertain cases |
| 🔍 **Bounding Box Evidence** | Every verdict links to exact page + region in source document |
| 🚨 **Criteria Anomaly Detection** | Flags suspiciously narrow criteria (anti-corruption layer) |
| 📊 **Bid Price Check** | Flags abnormally low L1 bids before contract award |
| 📱 **Mobile PWA** | Offline review + sync — works in low-connectivity field environments |
| 📑 **Signed Audit Report** | SHA-256 signed PDF — legally defensible paper trail |

---

## 🤖 AI Stack

| Provider | Model | Usage | Free Tier |
|---|---|---|---|
| **Anthropic** | Claude Sonnet | Criteria extraction, reasoning | API key |
| **Groq** | Llama 3.1 70B | Fast inference, entity extraction | 14,400 req/day |
| **Google** | Gemini Flash | Long document analysis | 1,500 req/day |
| **OpenRouter** | Llama 3.1 8B | Fallback | Free tier |

The LLM router tries providers in order and falls back automatically on rate limits.

---

## 🗂️ Project Structure

```
TenderMind-AI/
├── artifacts/
│   ├── api-server/        # Express 5 REST API
│   ├── tendermind/        # React + Vite frontend
│   └── mockup-sandbox/    # UI component sandbox
├── packages/
│   ├── db/                # Drizzle ORM schema + migrations
│   └── api-spec/          # OpenAPI spec + Orval codegen
├── .env.example           # Environment variable template
└── pnpm-workspace.yaml
```

---

## 🚀 Quick Start

### Prerequisites
- Node.js v24+ → https://nodejs.org
- pnpm → `npm install -g pnpm`
- PostgreSQL (local or Docker)

### Environment Variables

```env
PORT=3000
BASE_PATH=/
NODE_ENV=development
SESSION_SECRET=           # node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
DATABASE_URL=postgresql://postgres:password@localhost:5432/tendermind
ANTHROPIC_API_KEY=        # https://console.anthropic.com
GROQ_API_KEY=             # https://console.groq.com  (free)
GEMINI_API_KEY=           # https://aistudio.google.com  (free)
OPENROUTER_API_KEY=       # https://openrouter.ai  (free tier)
```

### Linux / Mac

```bash
git clone https://github.com/madukalmanoj/TenderMind-AI
cd TenderMind-AI
pnpm install
cp .env.example .env
# fill in .env with your keys
pnpm --filter @workspace/db run push
# Terminal 1
pnpm --filter @workspace/api-server run build && pnpm --filter @workspace/api-server run start
# Terminal 2
pnpm --filter @workspace/tendermind run dev
# Open http://localhost:3000
```

### Windows (PowerShell)

```powershell
git clone https://github.com/madukalmanoj/TenderMind-AI
cd TenderMind-AI
pnpm install --ignore-scripts

# Windows native binaries (required)
pnpm add @rollup/rollup-win32-x64-msvc -w --ignore-scripts
pnpm add lightningcss-win32-x64-msvc -w --ignore-scripts
pnpm add @tailwindcss/oxide-win32-x64-msvc -w --ignore-scripts
pnpm add @esbuild/win32-x64@0.27.3 -w --ignore-scripts

# Set env vars
$env:PORT="3000"
$env:BASE_PATH="/"
$env:NODE_ENV="development"
$env:SESSION_SECRET="your-32-char-random-string"
$env:DATABASE_URL="postgresql://postgres:password@localhost:5432/tendermind"
$env:ANTHROPIC_API_KEY="your-key"
$env:GROQ_API_KEY="your-key"
$env:GEMINI_API_KEY="your-key"

# Push DB schema
pnpm --filter @workspace/db run push

# Terminal 1 — API
pnpm --filter @workspace/api-server run build
pnpm --filter @workspace/api-server run start

# Terminal 2 — Frontend
pnpm --filter @workspace/tendermind run dev

# Open http://localhost:3000
```

---

## 🔑 Key Commands

```bash
pnpm run typecheck                              # typecheck all packages
pnpm run build                                  # build all packages
pnpm --filter @workspace/api-spec run codegen  # regenerate API hooks from OpenAPI spec
pnpm --filter @workspace/db run push           # push DB schema (dev only)
pnpm --filter @workspace/api-server run dev    # run API server in dev mode
pnpm --filter @workspace/tendermind run dev    # run frontend in dev mode
```

---

## 🎬 Demo Walkthrough

1. Upload the sample CRPF tender PDF (included in `/demo-data`)
2. Watch criteria extracted in 90 seconds — approve the checklist
3. Upload 3 bidder packages — watch verdicts populate in real time
4. See debarment flag trigger on Bidder 3
5. Click any verdict — source PDF renders with highlighted evidence region
6. Download the signed audit report

---

