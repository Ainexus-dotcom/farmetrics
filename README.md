**Farmetrics Software - Production Ready PRD**

Document Purpose

This document serves as a Production Ready Product Requirements Document (PRD) for the Farmetrics Web Software. It captures all functional and visual aspects of the Admin and Supervisor dashboards, the landing page, authentication system, and supporting components. All specifications are tailored for full-stack AI-powered development, with Supabase as the database (shared with the mobile app, which collects field data).


1. Overview
1.1 Product Name
Farmetrics

1.2 Description
Farmetrics is a web platform enabling Admin and Supervisor roles to manage and monitor agricultural field data collected by field officers via a mobile app. The system integrates mapping, data approval workflows, field visit progress tracking, and geospatial farm data visualization.

1.3 User Roles
Admin: Manages system-wide users, assigns tasks, reviews field data, exports reports.

Supervisor: Oversees field officers in assigned regions, approves data, and handles issues.

Field Officer: (Indirectly managed) collects data through the Farmetrics mobile app.

1.4 Tech Stack
Frontend: Next.js (React-based)

Database: Supabase (shared with mobile app)

Authentication: Supabase Auth, custom routing

GIS: Leaflet.js for polygon display

2. Routing and URL Structure
Public Pages:
Page

URL

Description

Home

/

Landing page with intro to Farmetrics + cards to access portals

Supervisors Info

/supervisors

Information about supervisors' responsibilities

Field Officers

/field-officers

Field officer roles and APK download button

About

/about

About Farmetrics

Contact

/contact

Contact form or info page

Authentication Routes:
Page

URL

Admin Signup

/admin-signup

Admin Signin

/admin-signin

Supervisor Signup

/supervisor-signup

Supervisor Signin

/supervisor-signin

Dashboard Routes:
Dashboard

URL

Admin Dashboard

/admin-dashboard

Supervisor Dashboard

/supervisor-dashboard

Avoid paths like /auth/admin/signin. Keep it clean and flat.

3. Page-by-Page Breakdown
3.1 Landing Page (/)
Purpose:
To serve as the main entry point for the Farmetrics platform. The homepage must communicate the core value of the system (agricultural data monitoring), offer clear navigation, and direct users to the correct role-based portal (Admin or Supervisor).

Header:
Logo (top left)

Navigation Links: Home, Supervisors, Field Officers, About, Contact

Optional: Toggle for light/dark mode

Hero Section:
Main Heading: "Agricultural Data Monitoring"

Subtext: "Empowering Ghanaian farmers with data-driven insights and management tools."

Purpose: Clearly state the platform's mission and who it serves (farmers, supervisors, admin)

Portal Cards Section:
Two interactive cards:

Admin Portal Card

Icon (shield or lock)

Title: "Admin Portal"

Description: "Manage users, monitor farm operations, and analyze agricultural data."

Link: /admin-signin

Supervisor Portal Card

Icon (group/team)

Title: "Supervisor Portal"

Description: "Coordinate field teams, manage regional operations, and track farm activities."

Link: /supervisor-signin

Footer:
Year and copyright

Company name: "Farmetrics. All rights reserved."

Footer Links:

Privacy

Terms

Data Protection

Social Icons (bottom right):

Twitter

LinkedIn

Purpose: Provide legal context and professional contact points for transparency

3.2 **Supervisors Page (/supervisors**)
Describes the role of a supervisor in Ghana's agricultural system

Lists responsibilities: approving data, managing regional teams, resolving issues

Includes visuals or icons to enhance clarity

CTA Buttons: [Sign Up] /supervisor-signup, [Sign In] /supervisor-signin

3.3 Field Officers Page (/field-officers)
Short explanation of the role of field officers

Clarify they use the mobile app for:

Visiting farms

Submitting polygon data

Collecting EXIF-tagged images

Download APK Button prominently visible

Optional QR Code to install the app

3.4 Admin Sign Up (/admin-signup) & Sign In (/admin-signin)
Admin Sign Up Form Fields:

Full Name

Email

Password (with confirmation)

Sign In Form:

Email

Password

Validates input before submission

On success: Redirect to /admin-dashboard

No regional data required (Admins are national/system-wide)

3.5 Supervisor Sign Up (/supervisor-signup) & Sign In (/supervisor-signin)
Supervisor Sign Up Form Fields:

Full Name

Phone Number

Email

Password (with confirmation)

Region (dropdown of Ghana's regions)

District (filtered by region)

Location (filtered by district)

Sign In Form:

Email

Password

On success: Redirect to /supervisor-dashboard

4. Admin Dashboard (/admin-dashboard)
4.1 Overview
Summary cards:

Total Farmers

Total Farms

Active Field Officers

Farm Visits Completed

Progress bar: % of farms visited (filterable by region)

Activity Feed: Latest logins, submissions, updates

4.2 User Management
Field Officers Tab

List, filter, search

Approve new accounts

Assign farms to officers

View officer performance stats

Supervisors Tab

View and add supervisors

Assign to regions

Edit or deactivate

4.3 Farm Management
Farm Table View

Farm ID, Farmer Name, District, Region, Crop Type

Visit Count, Last Visit Date

Click to expand:

Farmer details

Map view of polygon farm area

Coordinates (from EXIF)

Visit history timeline

Approval Queue for new farm submissions

Filters: Region, District, Crop, Assigned Officer

Export CSV/XLSX

4.4 Farmer Management
Full list of farmers

Associated farms

Contact info

Edit option

4.5 Visit Reports
Chart: Visits per field officer (weekly)

Table: Farm Name, Officer, Visit #, Timestamp

Click for visit details:

Officer notes

Images with EXIF

Map polygon display

Filter by: Region, Officer, Date range

4.6 Issue Management
Table view of issues reported

Actions:

Mark resolved

Assign to another officer

Transfer officer

History tracking per issue

4.7 Supervisor Transfers
View transfer requests from supervisors

Approve/reject with comment field

4.8 Settings
Edit admin profile

Define default region labels

Set visit thresholds, reminders

Backup/export database

5. Supervisor Dashboard (/supervisor-dashboard)
5.1 Overview
Region-specific metrics

Officer status breakdown

Incomplete visits tracker

5.2 Field Officer Management
List of officers assigned to this region

Performance %

Assign new farms (select from list or map)

Officer status (active/inactive/idle)

5.3 Farm & Farmer Data
Region's farms view

Approval queue

Highlight:

Unvisited farms ("sleeping")

Visit status per farm (progress bar)

Map polygon with data overlay

Export options

5.4 Issues Panel
View reported issues by officers

Add notes, assign, or escalate

Status (new, in review, resolved)

5.5 Messaging
Internal chat:

One-to-one

Group chat per region

Attach images or notes

5.6 Profile
Update profile details

View region assignment

6. Supabase Integration Notes
Mobile app shares the same Supabase database.

Supabase tables to include:

users (roles: admin, supervisor, officer)

farms

farmers

visits

issues

polygons

images (with EXIF fields)

transfers

Authentication via Supabase Auth

7. Deployment Considerations
Base URL must follow flat structure:

/admin-signup not /auth/admin/signup

Set environment variables for Supabase keys

Use environment detection for staging vs production

Add favicon and PWA manifest for future mobile integration

8. Visual Identity
Colors: Green (success), Dark Blue/Navy (background), Light Gray/White (text)

Fonts: Sans-serif (Poppins or Inter)

Icons: FontAwesome or Lucide

Maps: Mapbox (polygons) or Leaflet with OpenStreetMap

9. README.md Instruction Summary
The README of this repository MUST include:

Intro: What is Farmetrics?

Tech stack

How to run the project (dev & prod)

How to structure Supabase tables (with types)

Route list as above

Supabase auth setup

Deployment guide

Link to APK (field officers)

Credits / Contact