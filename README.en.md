<div align="center">

<img src="frontend/public/asset/logo.png" alt="SCOPREVO" width="120" />

# SCOPREVO

**AI-powered Scope & Revision Intelligence for freelance projects**

Turn scattered client feedback — WhatsApp chats, email threads — into structured, scope-classified revision checklists.

**🌐 Language / Bahasa:** **🇬🇧 English** · [🇮🇩 Indonesia](./README.md)

[![Live Demo](https://img.shields.io/badge/Live%20Demo-scoprevo.edgeone.dev-0B0B0B?style=for-the-badge&labelColor=CCFF00&color=0B0B0B)](https://scoprevo.edgeone.dev)
[![License: MIT](https://img.shields.io/badge/License-MIT-CCFF00?style=for-the-badge&labelColor=0B0B0B)](LICENSE)
[![Status](https://img.shields.io/badge/status-live-CCFF00?style=for-the-badge&labelColor=0B0B0B)](https://scoprevo.edgeone.dev)

![Vue 3](https://img.shields.io/badge/Vue%203-35495E?logo=vuedotjs&logoColor=4FC08D)
![TypeScript](https://img.shields.io/badge/TypeScript-strict-3178C6?logo=typescript&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?logo=express&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?logo=redis&logoColor=white)

</div>

---

## 🎯 The Problem

Freelancers lose money to **scope creep**. Client feedback arrives as messy WhatsApp or email threads — every message sounds urgent, nothing is classified, and by the time you realize half the requests are out of scope, you've already done the work for free.

Generic PM tools (Trello, Notion, Jira) just store the chaos. They don't tell you **which request is actually in scope**.

## 💡 The Solution

SCOPREVO acts as a **scope guardian**. Paste raw client feedback → the AI decomposes it into a structured revision checklist where **every item is classified as `IN_SCOPE`, `OUT_OF_SCOPE`, or `NEEDS_REVIEW`** — each with a clear issue description, a recommendation, and a reasoned justification. Clients confirm via a magic link, and revision quotas are tracked transparently.

## ✨ Key Features

| Feature | Description |
|---|---|
| **🤖 AI Feedback Extraction** | Paste a raw WhatsApp/email thread — AI decomposes it into structured items, each classified `IN_SCOPE` / `OUT_OF_SCOPE` / `NEEDS_REVIEW` with issue, recommendation, and justification. Validated with Zod schemas. |
| **📄 Scope Document Parsing** | Upload project scope documents (PDF / DOCX) — parsed server-side with `pdf-parse` and `mammoth` to ground AI decisions in the actual agreement. |
| **🎯 Revision Quota Tracking** | Per-project revision quota (e.g. 2 of 3 used) with visual progress — scope creep becomes a data point, not an argument. |
| **🔗 Magic-Link Client Portal** | Clients confirm or dispute revisions through a tokenized portal link — no account or login required on their side. |
| **📁 Project Management** | Dashboard overview, project CRUD, per-project revision batch history, and settings — all in one place. |
| **📴 Offline-First Resilience** | IndexedDB local storage + SWR (stale-while-revalidate) + network state detection — the app keeps working when connectivity drops. |
| **🌐 Bilingual (EN / ID)** | Full i18n with English and Indonesian locales. |
| **🔐 Security-First Backend** | Helmet, JWT auth, bcryptjs hashing, rate limiting (`rate-limiter-flexible`), and Zod request validation on every route. |
| **⚙️ BYOK AI Keys** | Users bring their own LLM provider keys; server tracks AI usage per account. |

## 📸 Screenshots

| Dashboard | Projects |
|---|---|
| ![Dashboard](docs/screenshots/dashboard.png) | ![Projects](docs/screenshots/projects.png) |

| Revision History | Settings |
|---|---|
| ![History](docs/screenshots/history.png) | ![Settings](docs/screenshots/settings.png) |

## 🛠 Tech Stack

**Frontend** — Vue 3 · Vite · TypeScript (strict) · Tailwind CSS · Pinia · Vue Router · i18n (EN/ID) · IndexedDB (`idb`) · Storybook

**Backend** — Express.js · TypeScript (strict) · Zod · JWT + bcryptjs · PostgreSQL (Supabase) · Redis (Upstash, `ioredis`) · Nodemailer · WebSocket (`ws`) · PDF/DOCX parsing (`pdf-parse`, `mammoth`)

**Infrastructure** — Tencent EdgeOne Makers (deployment) · Supabase (database) · Upstash (Redis)

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- PostgreSQL database (or Supabase project)
- Redis instance (or Upstash)
- LLM API key (BYOK — bring your own key)

### 1. Clone the repo

```bash
git clone https://github.com/ranggautama47/scoprevo.git
cd scoprevo
```

### 2. Backend

```bash
cd backend
cp .env.example .env        # fill in your credentials
npm install
npm run dev                 # starts on http://localhost:3000
```

Key environment variables (see `backend/.env.example` for the full list): `DATABASE_URL`, `REDIS_URL`, `JWT_SECRET`, `RESEND_API_KEY` (or SMTP), and LLM provider keys.

### 3. Frontend

```bash
cd frontend
npm install
npm run dev                 # starts on http://localhost:5173
```

## 🧪 Testing

```bash
cd backend
npm test                    # full backend test suite (node run-tests.js)
```

The test suite covers auth security, email flows, project lifecycle, and Redis resilience. E2E scenarios are in `tests/`.

## 📁 Project Structure

```
├── frontend/          # Vue 3 SPA (views, stores, i18n, resilience layer)
├── backend/           # Express API (controllers, services, repositories, migrations)
│   └── src/tests/     # backend test suites
├── docs/              # architecture, phases, database, UML, design system
└── tests/             # E2E test scripts
```

See [docs/PROJECT_STRUCTURE.md](docs/PROJECT_STRUCTURE.md) for the full breakdown.

## 📚 Documentation

| Doc | Content |
|---|---|
| [PHASES.md](docs/architecture/PHASES.md) | Build phases & implementation roadmap |
| [DATABASE.md](docs/ai%20context/DATABASE.md) | Database schema & ERD |
| [UML.md](docs/ai%20context/UML.md) | UML diagrams |
| [DESIGN_SYSTEM_BRUTALIST.md](docs/architecture/DESIGN_SYSTEM_BRUTALIST.md) | Brutalist design system |
| [KNOWN_ISSUES.md](docs/KNOWN_ISSUES.md) | Known issues & limitations |

## ☁️ Deployment

Deployed on **Tencent EdgeOne Makers** → [scoprevo.edgeone.dev](https://scoprevo.edgeone.dev)

## 🤝 Why SCOPREVO and not a generic PM tool?

Generic PM tools store tasks — they don't classify them against a signed scope. SCOPREVO's entire data model revolves around the scope document and the revision quota, so "this wasn't agreed" stops being a negotiation and starts being a system output.

## 👤 Author

**Rangga Utama**

[![GitHub](https://img.shields.io/badge/GitHub-ranggautama47-181717?logo=github)](https://github.com/ranggautama47)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Rangga%20Utama-0A66C2?logo=linkedin)](https://www.linkedin.com/in/rangga-utama)

## 📄 License

This project is licensed under the [MIT License](LICENSE).
