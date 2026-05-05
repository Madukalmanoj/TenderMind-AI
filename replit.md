# TenderMind AI 🏛️

> AI-powered government tender evaluation platform — built for the **AI for Bharat Hackathon**, Theme 3: AI-Based Tender Evaluation and Eligibility Analysis for Government Procurement by CRPF.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Replit-blue)](https://tender-mind-ai--kakashisparta1.replit.app)
[![Theme](https://img.shields.io/badge/Theme-3%20CRPF%20Procurement-navy)](https://www.hackerearth.com/challenges/hackathon/ai-for-bharat-2/)

---

## What It Does

TenderMind AI automates the evaluation of government procurement tenders. A procurement officer uploads a tender document and bidder submissions — the AI extracts eligibility criteria, evaluates each bidder, flags compliance issues (debarment, conflict of interest), and generates a legally defensible audit report with full human oversight.

**The problem it solves:** Manual tender evaluation takes 2–3 days, produces inconsistent results, and leaves no audit trail. TenderMind AI does it in ~38 minutes with every verdict traceable to a source document and page.

---

## Live Demo

🔗 **[https://tender-mind-ai--kakashisparta1.replit.app]**

---

## Tech Stack

| Layer | Technology |
|---|---|
| Monorepo | pnpm workspaces |
| Runtime | Node.js v24 |
| Language | TypeScript 5.9 |
| API | Express 5 |
| Database | PostgreSQL + Drizzle ORM |
| Validation | Zod v4 + drizzle-zod |
| Frontend | React + Vite 7 + Tailwind CSS v4 |
| AI / LLM | Groq (Llama 3.1 70B) + Gemini Flash |
| Build | esbuild (CJS bundle) |

---

## Project Structure

```
TenderMind-AI/
├── artifacts/
│   ├── api-server/       # Express 5 backend
│   ├── tendermind/       # React + Vite frontend
│   └── mockup-sandbox/   # UI component sandbox
├── packages/
│   ├── db/               # Drizzle ORM schema + migrations
│   └── api-spec/         # OpenAPI spec + codegen
└── pnpm-workspace.yaml
```

---

## Prerequisites

- Node.js v24+ → https://nodejs.org
- pnpm → `npm install -g pnpm`
- PostgreSQL running locally (or Docker)

---

## Environment Variables

Create a `.env` file in the root (see `.env.example`):

```env
PORT=3000
BASE_PATH=/
NODE_ENV=development
SESSION_SECRET=generate-with-node-e-crypto-randomBytes-32-toString-hex
DATABASE_URL=postgresql://postgres:password@localhost:5432/tendermind
GROQ_API_KEY=        # free at console.groq.com
GEMINI_API_KEY=      # free at aistudio.google.com
```

Generate SESSION_SECRET:
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

---

## Running Locally

### Linux / Mac

```bash
# 1. Clone
git clone https://github.com/YOUR_USERNAME/TenderMind-AI
cd TenderMind-AI

# 2. Install
pnpm install

# 3. Copy and fill env vars
cp .env.example .env

# 4. Push database schema
pnpm --filter @workspace/db run push

# 5. Terminal 1 — API server
pnpm --filter @workspace/api-server run build
pnpm --filter @workspace/api-server run start

# 6. Terminal 2 — Frontend
pnpm --filter @workspace/tendermind run dev

# 7. Open http://localhost:3000
```

### Windows (PowerShell)

```powershell
# 1. Clone and install
git clone https://github.com/YOUR_USERNAME/TenderMind-AI
cd TenderMind-AI
pnpm install --ignore-scripts

# 2. Add Windows native binaries
pnpm add @rollup/rollup-win32-x64-msvc -w --ignore-scripts
pnpm add lightningcss-win32-x64-msvc -w --ignore-scripts
pnpm add @tailwindcss/oxide-win32-x64-msvc -w --ignore-scripts
pnpm add @esbuild/win32-x64@0.27.3 -w --ignore-scripts

# 3. Set environment variables
$env:PORT="3000"
$env:BASE_PATH="/"
$env:NODE_ENV="development"
$env:SESSION_SECRET="any-random-32-char-string"
$env:DATABASE_URL="postgresql://postgres:password@localhost:5432/tendermind"
$env:GROQ_API_KEY="your-groq-key"
$env:GEMINI_API_KEY="your-gemini-key"

# 4. Push database schema
pnpm --filter @workspace/db run push

# 5. Terminal 1 — API server
pnpm --filter @workspace/api-server run build
pnpm --filter @workspace/api-server run start

# 6. Terminal 2 — Frontend (with env vars set)
pnpm --filter @workspace/tendermind run dev

# 7. Open http://localhost:3000
```

---

## Key Commands

```bash
pnpm run typecheck                          # full typecheck across all packages
pnpm run build                              # typecheck + build all packages
pnpm --filter @workspace/api-spec run codegen   # regenerate API hooks from OpenAPI spec
pnpm --filter @workspace/db run push        # push DB schema changes (dev only)
pnpm --filter @workspace/api-server run dev # run API server locally
```

---

## Free API Keys

| Service | Free Tier | Link |
|---|---|---|
| Groq (Llama 3.1 70B) | 14,400 req/day | https://console.groq.com |
| Google Gemini Flash | 1,500 req/day | https://aistudio.google.com |

---

## Hackathon

- **Event:** AI for Bharat 2
- **Theme:** 3 — AI-Based Tender Evaluation and Eligibility Analysis for Government Procurement by CRPF
- **Team:** madukalmanoj_e400
