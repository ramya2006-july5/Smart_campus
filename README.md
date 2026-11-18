# SMART CAMPUS – AI-Powered College Management & Placement Intelligence System

A full-stack college management and AI-powered placement preparation platform built with React, TypeScript, Tailwind CSS, Express.js, Drizzle ORM, PostgreSQL (Cloud SQL), Firebase Authentication, and the Google Gemini API (`@google/genai`).

> **Database Note**: The backend uses **Cloud SQL (PostgreSQL)** via `drizzle-orm` and `pg`.

---

## Core Features

1. **Three-Role Authentication & RBAC (`admin`, `placement_officer`, `student`)**
   - Registration, login, bcrypt password hashing, JWT + Firebase Google Sign-In, role-guarded API endpoints, profile management, and password updates.
   - Quick demo access buttons on the login screen for all three roles.
2. **Role-Specific Dashboards**
   - **Admin & Placement Officer Dashboard**: Dynamic database metrics (registered students, faculty members, partner companies, active drives, eligible students, placed students, average LPA), Recharts department & drive charts, and recent campus activities.
   - **Student Dashboard**: Academic snapshot, transparent placement readiness score, upcoming drives with deterministic eligibility status, daily study tasks, and announcements.
3. **Student Management CRUD**
   - Add, edit, delete, search, and filter students by department and academic year, including CGPA, arrears, technical skills, resume links, and placement status.
4. **AI Placement Intelligence Suite**
   - **Company & Placement Drive Management**: Manage companies, job roles, CTC packages, min CGPA, max arrears, allowed departments, required skills, selection rounds, and deadlines.
   - **Deterministic Eligibility Checker**: Pure backend rules compare student academic profiles against drive criteria (never delegated to AI).
   - **AI Company Preparation Analyzer**: Generates round-wise roadmaps, DSA/Java/Core CS focus topics, and personalized skill-gap guidance per drive.
   - **Personalized Learning Roadmap**: Generates daily or weekly task schedules across Java, OOP, DSA, DBMS, SQL, OS, CN, SE, Aptitude, Reasoning, Verbal, and Communication with progress tracking and editable goals.
   - **AI Aptitude & Technical Assessments**: Timed MCQs across 10 aptitude topics + Java/DSA/Core CS MCQs and coding problems with AI code evaluation and score persistence.
   - **AI Mock Interview Studio**: Multi-turn company/role/category interviews (`Technical`, `Java`, `DSA`, `HR`, `Project Explanation`, `Communication`) with structured feedback scorecards.
   - **Performance & Readiness Analyzer**: Transparent weighted score (`Aptitude 25% + Technical 30% + Mock Interview 25% + Roadmap 20%`), topic accuracy bar charts, and score trend graphs.
   - **AI Placement Career Assistant**: Interactive placement chatbot for Java, DSA, Aptitude, Core CS, and Resume advice.
5. **Campus Services**
   - **Lost & Found Hub**: Report lost/found items with photos, search/filter, and claim tracking.
   - **Skill Swap Network**: Post teach/learn skill listings and exchange collaboration requests.
   - **Announcements & Notifications**: Targeted campus alerts (`placement`, `exam`, `event`, `deadline`, `general`) with real-time unread counts.

---

## Demo Credentials

- **Administrator**: `admin@smartcampus.edu` / `Admin@123`
- **Placement Officer**: `placement@smartcampus.edu` / `Officer@123`
- **Student (CS)**: `aarav.sharma@smartcampus.edu` / `Student@123`
- **Student (DS)**: `priya.patel@smartcampus.edu` / `Student@123`

---

## Local Setup & Running in VS Code

1. **Install dependencies**:
   ```bash
   npm install
   ```
2. **Configure environment variables** (`.env` based on `.env.example`):
   - `GEMINI_API_KEY`: Your Google Gemini API key (used exclusively on the server in `src/services/ai.ts`).
   - `JWT_SECRET`: Secret string for signing local session JWT tokens.
   - `SQL_HOST`, `SQL_PORT`, `SQL_USER`, `SQL_PASSWORD`, `SQL_DATABASE`: Cloud SQL PostgreSQL connection credentials.
3. **Push schema to PostgreSQL**:
   ```bash
   npx drizzle-kit push --config=src/db/drizzle.config.ts
   ```
   *(Or apply `database/schema.sql` directly.)*
4. **Run the development server** (starts Express API + Vite frontend on port `3000`):
   ```bash
   npm run dev
   ```
5. **Production build & start**:
   ```bash
   npm run build
   npm start
   ```

---

## Key API Endpoints

- **Auth & Profile**: `POST /api/auth/register`, `POST /api/auth/login`, `POST /api/auth/firebase-sync`, `GET /api/profile`, `PUT /api/profile`, `PUT /api/profile/password`
- **Dashboard & Students**: `GET /api/dashboard`, `GET /api/students`, `POST /api/students`, `PUT /api/students/:id`, `DELETE /api/students/:id`
- **Placement Drives & Eligibility**: `GET/POST/PUT /api/companies`, `GET/POST/PUT/DELETE /api/placement-drives`, `GET /api/placement-drives/:id/eligibility`, `POST /api/placement-drives/:id/apply`, `PATCH /api/applications/:id`
- **AI Placement Prep**: `POST /api/ai/company-prep`, `GET /api/roadmaps`, `POST /api/roadmaps/generate`, `PATCH /api/roadmaps/tasks/:id`, `PUT /api/roadmaps/:id/goals`
- **Assessments & Analytics**: `GET /api/aptitude/questions`, `POST /api/aptitude/generate`, `GET /api/technical/questions`, `POST /api/technical/generate`, `POST /api/technical/evaluate-code`, `POST /api/assessments/submit`, `GET /api/performance/analytics`
- **Mock Interviews & Chatbot**: `GET/POST /api/mock-interviews`, `POST /api/mock-interviews/:id/respond`, `POST /api/mock-interviews/:id/complete`, `POST /api/ai/chat`
- **Campus Hub**: `/api/lost-found`, `/api/skills`, `/api/skill-requests`, `/api/announcements`, `/api/notifications`
