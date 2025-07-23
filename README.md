# Farmetrics Web Application

**Farmetrics** is a full-stack agricultural data monitoring platform built for **Admins** and **Supervisors** to manage and visualize field data submitted by Field Officers via a mobile app. It empowers Ghana’s agricultural sector with real-time geospatial insights, team coordination tools, and AI-ready data pipelines.


### Admin Dashboard
- **User Management**: Manage field officers and supervisors
- **Farm Management**: View and manage farm data with map visualization
- **Visit Reports**: Track farm visit progress and completion
- **Media Library**: View photos with EXIF data from field visits
- **Activity Log**: Monitor system activities and user actions
- **Issue Management**: Handle reported issues from field operations

### Supervisor Dashboard
- **Regional Overview**: Monitor assigned region operations
- **Field Officer Management**: Manage and assign field officers
- **Farm Monitoring**: Track farm visits and data approval
- **Issue Resolution**: Handle regional issues and escalations

## Tech Stack

- **Frontend**: Next.js 14 (React)
- **Database**: Supabase
- **Authentication**: Supabase Auth
- **Styling**: Tailwind CSS
- **Maps**: Leaflet.js for polygon visualization
- **Icons**: Lucide React

## Getting Started

### Prerequisites

- Node.js 18+ installed
- Supabase account and project set up

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd farmetrics-web
```

2. Install dependencies:
```bash
npm install
```

3. Create environment file:
```bash
cp .env.local.example .env.local
```

4. Configure environment variables in `.env.local`:
```
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

5. Run the development server:
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the application.

## Database Schema

### Required Supabase Tables

```sql
-- Users table
CREATE TABLE users (
  id UUID REFERENCES auth.users ON DELETE CASCADE PRIMARY KEY,
  email TEXT UNIQUE NOT NULL,
  full_name TEXT,
  phone TEXT,
  role TEXT CHECK (role IN ('admin', 'supervisor', 'field_officer')),
  region TEXT,
  district TEXT,
  location TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Farms table
CREATE TABLE farms (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  name TEXT NOT NULL,
  farmer_id UUID REFERENCES farmers(id),
  location_coordinates POINT,
  polygon_data JSONB,
  region TEXT,
  district TEXT,
  crop_type TEXT,
  assigned_officer_id UUID REFERENCES users(id),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Farmers table
CREATE TABLE farmers (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  name TEXT NOT NULL,
  phone TEXT,
  email TEXT,
  address TEXT,
  region TEXT,
  district TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Visits table
CREATE TABLE visits (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  farm_id UUID REFERENCES farms(id),
  officer_id UUID REFERENCES users(id),
  visit_date TIMESTAMP WITH TIME ZONE,
  status TEXT CHECK (status IN ('pending', 'completed', 'approved')),
  notes TEXT,
  images JSONB,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Issues table
CREATE TABLE issues (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  farm_id UUID REFERENCES farms(id),
  reporter_id UUID REFERENCES users(id),
  title TEXT NOT NULL,
  description TEXT,
  status TEXT CHECK (status IN ('open', 'in_progress', 'resolved')),
  priority TEXT CHECK (priority IN ('low', 'medium', 'high')),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  resolved_at TIMESTAMP WITH TIME ZONE
);
```

## Project Structure

```
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
│   └── styles/             # Specific component styles (if not using Tailwind/CSS-in-JS)
│       └── components.module.css
├── .env.local              # Environment variables
├── next.config.js          # Next.js configuration
├── package.json
├── tsconfig.json           # TypeScript configuration
└── README.md

```

## Deployment

### Build for Production

```bash
npm run build
npm start
```

### Environment Variables for Production

Ensure the following environment variables are set in your production environment:

- `NEXT_PUBLIC_SUPABASE_URL`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY`

## Authentication Flow

1. **Public Routes**: Landing page, about, contact, auth pages
2. **Protected Routes**: Dashboard pages require authentication
3. **Role-based Access**: Admin and supervisor roles have different dashboard access
4. **Automatic Redirects**: Users are redirected to appropriate dashboards based on their role

## API Integration

The application integrates with Supabase for:
- User authentication and management
- Real-time data synchronization
- File storage for farm images
- Row-level security for data access control

## Mobile App Integration

This web application shares the same Supabase database with the Farmetrics mobile app used by field officers for:
- Farm data collection
- GPS coordinate capture
- Image upload with EXIF data
- Offline data synchronization

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## Support

For technical support or questions about the Farmetrics platform, please contact the development team.

## License

This project is proprietary software developed for agricultural data management in Ghana.
```
