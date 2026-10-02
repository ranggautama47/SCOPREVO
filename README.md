
<div align="center">

<img src="frontend/public/asset/logo.png" alt="SCOPREVO" width="120" />

# SCOPREVO

**Kecerdasan Buatan (AI) untuk Manajemen Scope & Revisi pada Proyek Freelance**

Ubah feedback klien yang berantakan — chat WhatsApp, thread email — menjadi checklist revisi yang terstruktur dan terklasifikasi sesuai scope.

**🌐 Language / Bahasa:** **🇮🇩 Indonesia** · [🇬🇧 English](./README.en.md)

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

## 🎯 Masalah

Freelancer sering kehilangan uang karena **scope creep** (pekerjaan membengkak di luar kesepakatan). Feedback klien datang dalam bentuk chat WhatsApp atau thread email yang berantakan — setiap pesan terdengar mendesak, tidak ada yang diklasifikasikan, dan saat Anda menyadari separuh permintaan tersebut berada di luar scope, Anda sudah mengerjakannya secara gratis.

PM tool generik (Trello, Notion, Jira) hanya menyimpan kekacauan tersebut. Mereka tidak memberi tahu Anda **permintaan mana yang sebenarnya masuk dalam scope**.

## 💡 Solusi

SCOPREVO bertindak sebagai **penjaga scope**. Paste feedback mentah dari klien → AI memecahnya menjadi checklist revisi terstruktur di mana **setiap item diklasifikasikan sebagai `IN_SCOPE`, `OUT_OF_SCOPE`, atau `NEEDS_REVIEW`** — masing-masing dilengkapi dengan deskripsi masalah yang jelas, rekomendasi, dan alasan yang masuk akal. Klien melakukan konfirmasi melalui magic link, dan kuota revisi dilacak secara transparan.

## ✨ Fitur Utama

| Fitur | Deskripsi |
|---|---|
| **🤖 Ekstraksi Feedback AI** | Paste thread WhatsApp/email mentah — AI memecahnya menjadi item terstruktur. Setiap item diklasifikasikan `IN_SCOPE` / `OUT_OF_SCOPE` / `NEEDS_REVIEW` dengan masalah, rekomendasi, dan alasan. Divalidasi menggunakan skema Zod. |
| **📄 Parsing Dokumen Scope** | Upload dokumen scope proyek (PDF / DOCX) — diparsing di sisi server dengan `pdf-parse` dan `mammoth` untuk mendasari keputusan AI pada perjanjian yang sebenarnya. |
| **🎯 Pelacakan Kuota Revisi** | Kuota revisi per proyek (mis. terpakai 2 dari 3) dengan progres visual — scope creep menjadi titik data, bukan lagi bahan perdebatan. |
| **🔗 Portal Klien Magic-Link** | Klien mengonfirmasi atau menyanggah revisi melalui link portal ber-token — tidak memerlukan akun atau login di sisi mereka. |
| **📁 Manajemen Proyek** | Ringkasan dashboard, CRUD proyek, riwayat batch revisi per proyek, dan pengaturan — semuanya di satu tempat. |
| **📴 Ketahanan Offline-First** | Penyimpanan lokal IndexedDB + SWR (stale-while-revalidate) + deteksi status jaringan — aplikasi tetap berjalan saat koneksi terputus. |
| **🌐 Bilingual (EN / ID)** | i18n penuh dengan pilihan bahasa Inggris dan Indonesia. |
| **🔐 Backend yang Mengutamakan Keamanan** | Helmet, autentikasi JWT, hashing bcryptjs, pembatasan akses (`rate-limiter-flexible`), dan validasi request Zod di setiap rute. |
| **⚙️ Kunci AI BYOK** | Pengguna membawa kunci API provider LLM mereka sendiri; server melacak penggunaan AI per akun. |

## 📸 Tangkapan Layar

| Dashboard | Proyek |
|---|---|
| ![Dashboard](docs/screenshots/dashboard.png) | ![Projects](docs/screenshots/projects.png) |

| Riwayat Revisi | Pengaturan |
|---|---|
| ![History](docs/screenshots/history.png) | ![Settings](docs/screenshots/settings.png) |

## 🛠 Tech Stack

**Frontend** — Vue 3 · Vite · TypeScript (strict) · Tailwind CSS · Pinia · Vue Router · i18n (EN/ID) · IndexedDB (`idb`) · Storybook

**Backend** — Express.js · TypeScript (strict) · Zod · JWT + bcryptjs · PostgreSQL (Supabase) · Redis (Upstash, `ioredis`) · Nodemailer · WebSocket (`ws`) · Parsing PDF/DOCX (`pdf-parse`, `mammoth`)

**Infrastruktur** — Tencent EdgeOne Makers (deployment) · Supabase (database) · Upstash (Redis)

## 🚀 Memulai

### Prasyarat

- Node.js 18+
- Database PostgreSQL (atau proyek Supabase)
- Instance Redis (atau Upstash)
- Kunci API LLM (BYOK — bring your own key)

### 1. Clone repo

```bash
git clone [https://github.com/ranggautama47/scoprevo.git](https://github.com/ranggautama47/scoprevo.git)
cd scoprevo

```

### 2. Backend

```bash
cd backend
cp .env.example .env        # isi dengan kredensial Anda
npm install
npm run dev                 # berjalan di http://localhost:3000

```

Variabel environment utama (lihat `backend/.env.example` untuk daftar lengkapnya): `DATABASE_URL`, `REDIS_URL`, `JWT_SECRET`, `RESEND_API_KEY` (atau SMTP), dan kunci provider LLM.

### 3. Frontend

```bash
cd frontend
npm install
npm run dev                 # berjalan di http://localhost:5173

```

## 🧪 Pengujian

```bash
cd backend
npm test                    # seluruh test suite backend (node run-tests.js)

```

Test suite ini mencakup keamanan auth, alur email, siklus hidup proyek, dan ketahanan Redis. Skenario E2E berada di dalam folder `tests/`.

## 📁 Struktur Proyek

```text
├── frontend/          # Vue 3 SPA (views, stores, i18n, resilience layer)
├── backend/           # Express API (controllers, services, repositories, migrations)
│   └── src/tests/     # backend test suites
├── docs/              # architecture, phases, database, UML, design system
└── tests/             # script pengujian E2E

```

Lihat [docs/PROJECT_STRUCTURE.md](https://www.google.com/search?q=docs/PROJECT_STRUCTURE.md) untuk rincian lengkapnya.

## 📚 Dokumentasi

| Dokumen | Konten |
| --- | --- |
| [PHASES.md](https://www.google.com/search?q=docs/architecture/PHASES.md) | Fase pengerjaan & roadmap implementasi |
| [DATABASE.md](https://www.google.com/search?q=docs/ai%2520context/DATABASE.md) | Skema Database & ERD |
| [UML.md](https://www.google.com/search?q=docs/ai%2520context/UML.md) | Diagram UML |
| [DESIGN_SYSTEM_BRUTALIST.md](https://www.google.com/search?q=docs/architecture/DESIGN_SYSTEM_BRUTALIST.md) | Sistem desain Brutalist |
| [KNOWN_ISSUES.md](https://www.google.com/search?q=docs/KNOWN_ISSUES.md) | Masalah umum & batasan |

## ☁️ Deployment

Dideploy pada **Tencent EdgeOne Makers** → [scoprevo.edgeone.dev](https://scoprevo.edgeone.dev)

## 🤝 Kenapa SCOPREVO dan bukan PM tool generik?

PM tool generik menyimpan tugas — mereka tidak mengklasifikasikannya berdasarkan scope yang telah ditandatangani. Seluruh model data SCOPREVO berpusat pada dokumen scope dan kuota revisi, sehingga kalimat "ini tidak ada dalam kesepakatan" berhenti menjadi bahan negosiasi dan mulai menjadi output sistem.

## 👤 Author

**Rangga Utama**

[![GitHub](https://img.shields.io/badge/GitHub-ranggautama47-181717?logo=github)](https://github.com/ranggautama47)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Rangga%20Utama-0A66C2?logo=linkedin)](https://www.linkedin.com/in/rangga-utama)

## 📄 Lisensi

Proyek ini dilisensikan di bawah [MIT License](LICENSE).
