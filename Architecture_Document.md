# Architecture Document

## Architecture Type
**Monolith** (simpler to build and deploy for MVP)

## Technology Stack
- **Frontend**: React
- **Backend**: Node.js + Express
- **Database**: PostgreSQL
- **Authentication**: JWT (JSON Web Tokens)
- **Hosting**: Vercel (frontend) + Render (backend)

## Components
- **Web App** — user interface (search, track, apply)
- **API Server** — handles requests, business logic
- **Database** — stores users, jobs, applications
- **Auth Service** — login, signup, token verification

## Authentication Flow
1. User submits email/password
2. Server verifies and returns JWT token
3. Token stored in localStorage
4. Token sent with every API request
5. Server verifies token before responding

## Data Flow
1. User searches for internships
2. Frontend sends request → API Server
3. API Server queries → Database
4. Database returns results → API Server
5. API Server sends response → Frontend
6. Frontend displays results to user

## Diagram (Text-based)
