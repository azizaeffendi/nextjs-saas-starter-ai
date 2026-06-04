<div align="center">

# ⚡ Next.js SaaS Starter + AI

**Production-ready SaaS boilerplate dengan AI integration — dari zero ke production dalam 1 hari**

[![Next.js](https://img.shields.io/badge/Next.js-15-black?style=for-the-badge&logo=next.js)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?style=for-the-badge&logo=typescript)](https://typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3-38bdf8?style=for-the-badge&logo=tailwind-css)](https://tailwindcss.com)
[![Supabase](https://img.shields.io/badge/Supabase-green?style=for-the-badge&logo=supabase)](https://supabase.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-412991?style=for-the-badge&logo=openai)](https://openai.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

<br/>

> **Jangan build infrastruktur dari nol. Boilerplate ini sudah include auth, billing, AI, dashboard, dan semua yang Anda butuhkan. Fokus ke produk, bukan plumbing.**

```
┌────────────────────────────────────────────────────────────────┐
│                    SAAS STARTER STACK                          │
├────────────────────────┬───────────────────────────────────────┤
│  Frontend              │  Backend / Infra                       │
│  ─────────────────     │  ────────────────                      │
│  Next.js 15 (App Dir)  │  Supabase (DB + Auth + Storage)       │
│  TypeScript            │  OpenAI GPT-4 / Claude                │
│  Tailwind CSS          │  Stripe (Billing)                     │
│  shadcn/ui             │  Resend (Email)                       │
│  Framer Motion         │  Vercel (Deployment)                  │
│  React Query           │  Upstash Redis (Rate limiting)        │
└────────────────────────┴───────────────────────────────────────┘
```

[🚀 Demo](#-demo) · [⚡ Quick Start](#-quick-start) · [📁 Struktur](#-struktur-proyek) · [🔧 Features](#-fitur-lengkap)

</div>

---

## ✨ Fitur Lengkap

### 🔐 Authentication & Authorization
- Email/password login dengan Supabase Auth
- Google OAuth, GitHub OAuth
- Magic link (passwordless)
- Role-based access control (admin, user, guest)
- Protected routes + middleware
- Session management

### 💳 Billing & Subscriptions (Stripe)
- Free, Pro, dan Enterprise tiers
- Monthly & Annual billing dengan diskon
- Checkout flow yang seamless
- Customer portal (manage subscription sendiri)
- Webhook handling (payment success, cancellation, upgrade)
- Usage-based billing support

### 🤖 AI Features
- OpenAI GPT-4 integration dengan streaming response
- Rate limiting per user tier (free: 10 req/day, pro: unlimited)
- Prompt templates yang bisa dikustomisasi
- AI usage tracking & analytics
- Token cost monitoring

### 📊 Dashboard & Analytics
- Admin dashboard dengan real-time metrics
- User management (ban, upgrade, delete)
- Revenue analytics (MRR, churn, LTV)
- AI usage analytics
- Google Analytics / Mixpanel integration

### 📧 Email System
- Transactional emails via Resend
- Welcome email sequence
- Password reset
- Invoice/receipt emails
- Email template dengan React Email

### 🎨 UI Components
- shadcn/ui component library
- Dark/Light mode toggle
- Responsive design (mobile-first)
- Loading skeletons
- Toast notifications
- Modal & drawer system

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- Supabase account (free)
- Stripe account (test mode)
- OpenAI API key

### 1. Clone & Install

```bash
git clone https://github.com/azizaeffendi/nextjs-saas-starter-ai.git my-saas
cd my-saas
npm install
```

### 2. Setup Environment

```bash
cp .env.example .env.local
```

Isi nilai di `.env.local`:
```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key

# Stripe
STRIPE_SECRET_KEY=sk_test_...
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...

# OpenAI
OPENAI_API_KEY=sk-...

# Resend (email)
RESEND_API_KEY=re_...

# App
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### 3. Setup Database

```bash
# Install Supabase CLI
npm install -g supabase

# Init dan jalankan migrations
supabase init
supabase db push
```

### 4. Jalankan

```bash
npm run dev
```

Buka `http://localhost:3000` — SaaS Anda sudah berjalan! 🎉

---

## 📁 Struktur Proyek

```
nextjs-saas-starter-ai/
├── app/                          # Next.js App Router
│   ├── (auth)/                   # Auth pages (login, register, reset)
│   ├── (dashboard)/              # Protected dashboard
│   │   ├── dashboard/            # Main dashboard
│   │   ├── ai/                   # AI features
│   │   ├── settings/             # User settings
│   │   └── billing/              # Subscription management
│   ├── (marketing)/              # Public pages
│   │   ├── page.tsx              # Landing page
│   │   ├── pricing/              # Pricing page
│   │   └── blog/                 # Blog
│   └── api/                      # API routes
│       ├── auth/                 # Auth callbacks
│       ├── stripe/               # Stripe webhooks
│       └── ai/                   # AI endpoints
├── components/
│   ├── ui/                       # shadcn/ui components
│   ├── dashboard/                # Dashboard-specific components
│   ├── marketing/                # Landing page components
│   └── shared/                   # Shared components
├── lib/
│   ├── supabase/                 # Supabase client & helpers
│   ├── stripe/                   # Stripe helpers
│   ├── openai/                   # OpenAI integration
│   └── utils/                    # Utility functions
├── supabase/
│   └── migrations/               # Database migrations
├── emails/                       # React Email templates
├── public/                       # Static assets
├── .env.example                  # Environment variables template
└── README.md
```

---

## 🎨 Kustomisasi

### Ganti Branding
Edit `lib/config.ts`:
```typescript
export const siteConfig = {
  name: "Nama SaaS Anda",
  description: "Deskripsi produk",
  url: "https://yourapp.com",
  logo: "/logo.svg",
  primaryColor: "#your-brand-color"
}
```

### Tambah AI Feature
```typescript
// app/api/ai/generate/route.ts
import { openai } from '@/lib/openai'
import { checkRateLimit } from '@/lib/rate-limit'

export async function POST(req: Request) {
  const user = await getUser()
  await checkRateLimit(user.id, user.plan)

  const { prompt } = await req.json()

  const stream = await openai.chat.completions.create({
    model: 'gpt-4-turbo-preview',
    messages: [{ role: 'user', content: prompt }],
    stream: true
  })

  return new StreamingTextResponse(stream)
}
```

### Tambah Pricing Tier
Edit `lib/stripe/plans.ts`:
```typescript
export const plans = [
  { id: 'free', name: 'Free', price: 0, features: [...] },
  { id: 'pro', name: 'Pro', price: 297000, features: [...] },  // Rp 297k/bulan
  { id: 'enterprise', name: 'Enterprise', price: 'custom', features: [...] }
]
```

---

## 🚢 Deployment (Vercel — 2 Menit)

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel

# Set environment variables di Vercel dashboard
# atau via CLI:
vercel env add OPENAI_API_KEY
vercel env add STRIPE_SECRET_KEY
# ... dst
```

---

## 📊 Tech Stack Detail

| Layer | Technology | Alasan |
|-------|-----------|--------|
| Framework | Next.js 15 | App Router, RSC, Streaming |
| Language | TypeScript | Type safety, developer experience |
| Styling | Tailwind + shadcn/ui | Rapid UI development |
| Database | Supabase (PostgreSQL) | Auth + DB + Storage in one |
| Billing | Stripe | Most reliable, great DX |
| AI | OpenAI GPT-4 | Best performance |
| Email | Resend + React Email | Modern email DX |
| Deployment | Vercel | Optimal untuk Next.js |
| Cache/Rate limit | Upstash Redis | Serverless-compatible |

---

## 📜 Lisensi

MIT © [azizaeffendi](https://github.com/azizaeffendi)

---

<div align="center">

**Muhammad Aziz A Effendi**
*Full-Stack Developer · AI Marketing Engineer · Indonesia*

[![GitHub](https://img.shields.io/badge/GitHub-@azizaeffendi-181717?style=flat-square&logo=github)](https://github.com/azizaeffendi)

Berikan ⭐ dan fork jika berguna untuk project Anda!

</div>