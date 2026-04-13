# 🎯 Interview AI — AI-Powered Mock Interview Platform

> **"Ace your next interview with real experts"**
> Book 1:1 mock interviews with senior engineers from top companies. Get AI-powered feedback, role-specific questions, and the confidence to land your dream job.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-interviewaii--i.vercel.app-blue?style=for-the-badge&logo=vercel)](https://interviewaii-i.vercel.app/)
[![Next.js](https://img.shields.io/badge/Next.js-16.2.2-black?style=for-the-badge&logo=next.js)](https://nextjs.org/)
[![License](https://img.shields.io/badge/License-Private-red?style=for-the-badge)]()

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Database Setup](#database-setup)
- [How It Works](#how-it-works)
- [Deployment](#deployment)

---

## Overview

**Interview AI** (branded as **Prept**) is a full-stack SaaS platform that connects job seekers with experienced engineers for live mock interview sessions. The platform leverages AI to generate tailored interview questions in real time, provide post-session feedback reports, and manage a credit-based booking system — all within a polished, production-grade web app.

Over **2,400+ engineers** have used this platform to crack FAANG and top-tier company interviews at Amazon, Google, Meta, Microsoft, Netflix, Atlassian, and Uber.

---

## ✨ Features

### For Interviewees
- 🔍 **Browse Interviewers** by category — Frontend, Backend, System Design, Product Management
- 📅 **Slot-based Scheduling** — pick from available slots, confirm with one click
- 🤖 **AI Feedback Reports** — post-interview analysis powered by Google Gemini with actionable insights
- 📹 **Session Recordings** — access recordings to review your own performance
- 💬 **Persistent Chat** — message your interviewer before and after the call

### For Interviewers
- 🧠 **AI Question Generator** — live co-pilot generating role-specific questions on demand (System Design, Behavioural, DSA)
- 🗓️ **Set Your Own Availability** — manage session slots on your schedule
- 💰 **Credit Earnings** — earn credits per session with withdrawal requests via dashboard

### Platform-wide
- 💳 **Credit System** — subscribe for monthly credits; unused credits roll over
- 📹 **HD Video Calls** — powered by Stream with screen sharing, recording, and playback
- 🔒 **Security by Arcjet** — bot protection, rate limiting, and abuse prevention on every API route
- 📧 **Transactional Emails** — React Email + Resend for beautiful email notifications

---

## 🛠️ Tech Stack

| Category | Technology |
|---|---|
| **Framework** | Next.js 16.2.2 (App Router) |
| **Language** | JavaScript (97.7%), CSS (2.1%), TypeScript (0.2%) |
| **Authentication** | Clerk (`@clerk/nextjs`) |
| **Database ORM** | Prisma 7 with PostgreSQL (`@prisma/adapter-pg`) |
| **AI / LLM** | Google Gemini (`@google/generative-ai`) |
| **Video Calls** | Stream Video React SDK (`@stream-io/video-react-sdk`) |
| **Chat** | Stream Chat React (`stream-chat-react`) |
| **Email** | Resend + React Email |
| **Security** | Arcjet (`@arcjet/next`) |
| **UI Components** | shadcn/ui, Radix UI, Lucide React |
| **Styling** | Tailwind CSS v4 |
| **Animations** | Motion (Framer Motion) |
| **Syntax Highlighting** | Shiki |
| **Date Utilities** | date-fns |
| **Notifications** | Sonner (toast) |
| **Deployment** | Vercel |
| **Dev Tunnel** | ngrok (for local webhook testing) |

---

## 📁 Project Structure

```
Interview-AI/
├── app/                    # Next.js App Router — pages & API routes
├── actions/                # Server Actions (Next.js server-side logic)
├── components/             # Reusable React components
├── emails/                 # React Email templates
├── hooks/                  # Custom React hooks
├── lib/                    # Utility functions and shared libraries
├── prisma/                 # Prisma schema and migrations
├── public/                 # Static assets (logos, brand SVGs)
├── AGENTS.md               # AI agent instructions
├── CLAUDE.md               # Claude Code configuration
├── components.json         # shadcn/ui configuration
├── next.config.mjs         # Next.js configuration
├── prisma.config.ts        # Prisma configuration
├── proxy.js                # Local dev proxy / ngrok setup
├── package.json
└── tailwind.config (via postcss.config.mjs)
```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** 18+
- **npm** / **yarn** / **pnpm**
- A **PostgreSQL** database (local or hosted, e.g. Neon, Supabase)
- Accounts for: [Clerk](https://clerk.dev), [Stream](https://getstream.io), [Resend](https://resend.com), [Arcjet](https://arcjet.com), [Google AI Studio](https://aistudio.google.com)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/prakashramav/Interview-AI.git
cd Interview-AI

# 2. Install dependencies
npm install
# Prisma client is auto-generated via postinstall hook

# 3. Set up environment variables (see below)
cp .env.example .env.local

# 4. Push the Prisma schema to your database
npx prisma db push

# 5. Start the development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 🔑 Environment Variables

Create a `.env.local` file in the root with the following variables:

```env
# Database
DATABASE_URL="postgresql://user:password@host:port/dbname"

# Clerk (Authentication)
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up

# Google Gemini (AI)
GOOGLE_GENERATIVE_AI_API_KEY=AIza...

# Stream (Video & Chat)
NEXT_PUBLIC_STREAM_API_KEY=...
STREAM_SECRET_KEY=...

# Resend (Email)
RESEND_API_KEY=re_...

# Arcjet (Security)
ARCJET_KEY=ajkey_...
```

---

## 🗄️ Database Setup

This project uses **Prisma** with a **PostgreSQL** adapter.

```bash
# Generate Prisma client (also runs automatically on npm install)
npx prisma generate

# Push schema changes to your database
npx prisma db push

# Open Prisma Studio (visual DB browser)
npx prisma studio
```

> The `postinstall` script in `package.json` automatically runs `prisma generate` on every `npm install`.

---

## ⚙️ How It Works

### Interviewee Flow
1. **Sign up / Sign in** via Clerk authentication
2. **Browse interviewers** filtered by specialisation
3. **Book a session** by selecting an available time slot — uses the credit system
4. **Join the video call** at session time via Stream-powered HD video
5. **Chat** before/after the session through the persistent Stream Chat interface
6. **Receive AI feedback** — Gemini analyses the session and produces a detailed report

### Interviewer Flow
1. **Onboard** and set up your profile with expertise and rates
2. **Configure availability** — set open time slots for booking
3. **Join sessions** and use the **AI Question Generator** co-pilot to get tailored questions live
4. **Earn credits** per completed session; request withdrawals from the dashboard

### Security
Every API route is protected by **Arcjet** — providing bot detection, rate limiting, and abuse prevention without extra infrastructure.

---

## 📦 Scripts

| Script | Description |
|---|---|
| `npm run dev` | Start development server |
| `npm run build` | Production build |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npx prisma generate` | Regenerate Prisma client |
| `npx prisma db push` | Sync schema to database |
| `npx prisma studio` | Open visual DB browser |

---

## 🌐 Deployment

This project is deployed on **Vercel**.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/prakashramav/Interview-AI)

### Steps
1. Push your repository to GitHub
2. Import the project on [vercel.com](https://vercel.com)
3. Add all environment variables in the Vercel project settings
4. Vercel auto-detects Next.js and handles builds automatically

> **Note:** Make sure your PostgreSQL database is accessible from Vercel's deployment region (e.g., use Neon or Supabase with connection pooling enabled).

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m 'Add my feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## 📄 License

This project is private. All rights reserved © [prakashramav](https://github.com/prakashramav).

---

> Made with ❤️ by [RoadsideCoder](https://interviewaii-i.vercel.app/)
