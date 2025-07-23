# 🌾 Farmetrics Web Software

**Farmetrics** is a full-stack agricultural data monitoring platform built for **Admins** and **Supervisors** to manage and visualize field data submitted by Field Officers via a mobile app. It empowers Ghana’s agricultural sector with real-time geospatial insights, team coordination tools, and AI-ready data pipelines.

---

## 🧭 Table of Contents

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
git clone https://github.com/Ainexus-dotcom/farmetrics-web.git
cd farmetrics-web
