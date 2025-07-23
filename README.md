# 🌾 Farmetrics Web Software

**Farmetrics** is a full-stack agricultural data monitoring platform built for **Admins** and **Supervisors** to manage and visualize field data submitted by Field Officers via a mobile app. It empowers Ghana’s agricultural sector with real-time geospatial insights, team coordination tools, and AI-ready data pipelines.

---
farmetrics-web/
├── public/                 # Static assets (images, favicon, APK)
│   └── farmetrics-app.apk
│   └── ...
├── src/
│   ├── app/                # Next.js App Router root
│   │   ├── (auth)/         # Grouped authentication routes
│   │   │   ├── admin-signup/
│   │   │   │   └── page.tsx
│   │   │   ├── admin-signin/
│   │   │   │   └── page.tsx
│   │   │   ├── supervisor-signup/
│   │   │   │   └── page.tsx
│   │   │   ├── supervisor-signin/
│   │   │   │   └── page.tsx
│   │   │   └── layout.tsx  # Auth-specific layout (e.g., minimalist)
│   │   ├── (dashboard)/    # Grouped dashboard routes with authentication guards
│   │   │   ├── admin-dashboard/
│   │   │   │   └── page.tsx
│   │   │   │   └── layout.tsx # Admin dashboard specific layout/sidebar
│   │   │   ├── supervisor-dashboard/
│   │   │   │   └── page.tsx
│   │   │   │   └── layout.tsx # Supervisor dashboard specific layout/sidebar
│   │   │   └── layout.tsx  # Common dashboard layout (e.g., for sidebar, header)
│   │   ├── page.tsx        # Landing page (/)
│   │   ├── about/
│   │   │   └── page.tsx
│   │   ├── contact/
│   │   │   └── page.tsx
│   │   ├── field-officers/
│   │   │   └── page.tsx
│   │   ├── supervisors/
│   │   │   └── page.tsx
│   │   └── layout.tsx      # Root layout for public pages
│   │   └── global.css      # Global styles
│   │   └── not-found.tsx   # Custom 404 page
│   │   └── api/            # API routes (for server-side data fetching/mutation if needed)
│   │       └── auth/
│   │           └── route.ts
│   │       └── farms/
│   │           └── route.ts
│   │       └── ...
│   ├── components/         # Reusable UI components
│   │   ├── ui/             # Generic UI components (buttons, input, modal)
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   └── Modal.tsx
│   │   ├── auth/           # Auth-specific components
│   │   │   ├── AuthForm.tsx
│   │   │   ├── UserRoleSelector.tsx
│   │   │   └── PasswordInput.tsx
│   │   ├── dashboard/      # Dashboard-specific shared components
│   │   │   ├── SummaryCard.tsx
│   │   │   ├── Sidebar.tsx
│   │   │   ├── Header.tsx
│   │   │   └── DataTable.tsx
│   │   ├── layout/         # Layout components
│   │   │   ├── PublicLayout.tsx
│   │   │   └── DashboardLayout.tsx
│   │   └── MapDisplay.tsx  # Leaflet map component
│   ├── lib/                # Utility functions, helpers, and configurations
│   │   ├── supabase/       # Supabase client initialization & API interactions
│   │   │   ├── server.ts   # Server-side Supabase client
│   │   │   └── client.ts   # Client-side Supabase client
│   │   │   └── auth.ts     # Auth-related Supabase functions
│   │   │   └── data.ts     # Data fetching/mutation functions
│   │   ├── constants.ts    # Global constants (regions, roles)
│   │   ├── utils.ts        # General utility functions
│   │   ├── validation.ts   # Zod schemas for form validation
│   │   └── hooks/          # Custom React hooks
│   │       ├── useAuth.ts
│   │       └── useForms.ts
│   ├── services/           # Business logic services (optional, for complex operations)
│   │   ├── userService.ts
│   │   ├── farmService.ts
│   │   └── ...
│   ├── types/              # TypeScript type definitions
│   │   ├── auth.d.ts
│   │   ├── farm.d.ts
│   │   ├── user.d.ts
│   │   └── global.d.ts
│   └── styles/             # Specific component styles (if not using Tailwind-in-JS)
│       └── components.module.css
├── .env.local              # Environment variables
├── next.config.js          # Next.js configuration
├── package.json
├── tsconfig.json           # TypeScript configuration
└── README.md


🧭 Table of Contents

- [🔍 Overview](#-overview)
- [🛠️ Tech Stack](#-tech-stack)
- [🚀 Getting Started](#-getting-started)
- [🔐 Supabase Setup](#-supabase-setup)
- [🌐 Routing Structure](#-routing-structure)
- [📊 Dashboard Modules](#-dashboard-modules)
- [📦 Supabase Tables](#-supabase-tables)
- [🛰️ Deployment Guide](#-deployment-guide)
- [🎨 Visual Identity](#-visual-identity)
- [📱 APK Download](#-apk-download)
- [🤝 Credits & Contact](#-credits--contact)

---

## 🔍 Overview

Farmetrics is a geospatially-enabled web platform with two main user roles:

- **Admin**: Oversees the national system, manages users/farms/visits/issues.
- **Supervisor**: Manages regional operations, field officers, and farm data approvals.

**Field Officers** use a mobile app to capture polygon data, images, and submit visit forms. The web platform is the control center.

---

## 🛠️ Tech Stack

| Layer | Tech |
|-------|------|
| Frontend | Next.js, Tailwind CSS |
| Backend | Supabase (Auth, Realtime DB, Edge Functions) |
| Mapping | Leaflet.js + OpenStreetMap |
| State | React Context / Zustand |
| UI Kit | Tailwind UI, Lucide Icons |
| Deployment | Vercel, Supabase Hosting |

---

## 🚀 Getting Started

### 1. Clone the Repo

```bash
git clone https://github.com/<Ainexus-dotcom/farmetrica.git
cd farmetrics-web
