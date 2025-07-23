// README.md

# 🌾 Farmetrics Web Platform

Farmetrics is a full-stack agricultural data management system designed for Admins and Supervisors to manage farms, monitor field officer activity, visualize GPS-tagged data, and support Ghanaian farmers with data-driven insights.

---

## 🚀 Tech Stack

- **Frontend**: Next.js + Tailwind CSS
- **Backend**: Supabase (Database, Auth, Storage)
- **GIS**: Leaflet.js for polygon and map data

---

## 📁 Project Structure

```
farmetrics-web/
├── components/
│   ├── Navbar.tsx
│   ├── Footer.tsx
│   ├── DashboardCard.tsx
│   ├── MapPolygonViewer.tsx
│   ├── Auth/
│   │   ├── SigninForm.tsx
│   │   └── SignupForm.tsx
├── pages/
│   ├── index.tsx
│   ├── supervisors.tsx
│   ├── field-officers.tsx
│   ├── about.tsx
│   ├── contact.tsx
│   ├── admin-signup.tsx
│   ├── admin-signin.tsx
│   ├── supervisor-signup.tsx
│   ├── supervisor-signin.tsx
│   ├── admin-dashboard/
│   │   └── index.tsx
│   ├── supervisor-dashboard/
│   │   └── index.tsx
├── lib/
│   └── supabaseClient.ts
├── public/
│   └── logo.svg, icons
├── styles/
│   └── globals.css
├── .env.local
└── README.md
```

---

## 🔐 Supabase Auth Setup

- Roles: `admin`, `supervisor`, `officer`
- Auth logic inside `lib/supabaseClient.ts`

```ts
import { createClient } from '@supabase/supabase-js'
export const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
)
```

---

## 🌍 Leaflet Map Integration

```tsx
<MapContainer center={[6.0072, -0.1921]} zoom={13}>
  <TileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png" />
  <Polygon positions={polygonCoords} />
</MapContainer>
```

---

## 🧾 Supabase Tables Schema

- `users`: id, role, name, email, phone, region, district
- `farms`: id, farmer_id, region, district, polygon (geojson)
- `farmers`: id, name, phone
- `visits`: id, farm_id, officer_id, date, notes
- `images`: id, farm_id, url, exif_json, lat, lng
- `issues`: id, description, farm_id, status
- `transfers`: id, from_region, to_region, supervisor_id, status

---

## 🌐 Routes

### Public Pages

| Path | Description |
|------|-------------|
| `/` | Landing page |
| `/supervisors` | Supervisor role info |
| `/field-officers` | Mobile app info |
| `/about` | About Farmetrics |
| `/contact` | Contact form/info |

### Auth Pages

| Path | Role |
|------|------|
| `/admin-signup` | Admin |
| `/admin-signin` | Admin |
| `/supervisor-signup` | Supervisor |
| `/supervisor-signin` | Supervisor |

### Dashboards

| Path | Role |
|------|------|
| `/admin-dashboard` | Admin |
| `/supervisor-dashboard` | Supervisor |

---

## 🛠 Run Locally

```bash
npm install
npm run dev
```

---

## 🚢 Deployment

Recommended: **Vercel**

```bash
vercel --prod
```

---

## 📱 APK (Field Officers)

**[Download APK here](https://your-download-link.com)**

---

## 🤝 Credits

Built by the Farmetrics team. All rights reserved.

Contact: [admin@farmetrics.com](mailto:admin@farmetrics.com)

---

