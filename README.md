# autocomplete-search-engine-
A backend-focused project that implements a real-time autocomplete engine using advanced data structures in Java. The system is built with Spring Boot and showcases how to design efficient text suggestion services similar to those in search engines.
# RealTime Autocomplete

A small full-stack project demonstrating a fast live autocomplete service with a React frontend and a Spring Boot backend.

Features
- Live autocomplete suggestions (Trie + BK-tree + n-gram fallbacks)
- Add/select terms with frequency
- "Show All Terms" modal with pagination
- Responsive, accessible UI with keyboard navigation
- Simple H2-based seeding for development and optional Docker-compose setup (Postgres + Redis)

Quick demo
- Start the backend
- Start the frontend
- Open http://localhost:3000 and start typing in the search box to see suggestions in real time

Getting started (Windows PowerShell)

Prerequisites
- Java 17+ (JDK) and `JAVA_HOME` set
- Node.js and npm
- Maven (or use Docker)

Option A — Run locally with Maven
1. From the repo root, start the backend:
```powershell
cd D:\D\coding\enhanced
mvn -DskipTests=false spring-boot:run
```
2. In a separate terminal, start the frontend:
```powershell
cd D:\D\coding\enhanced\frontend
npm install
npm start
```
3. Open http://localhost:3000

Option B — Docker Compose (isolated)
1. Install Docker Desktop for Windows
2. From repo root:
```powershell
cd D:\D\coding\enhanced
docker compose up --build
```
This starts services for the app, postgres, and redis. The app will be available on http://localhost:8080. You can run the frontend dev server or serve the built frontend from the Spring Boot static resources.

Database seeding
- Development seed data is in `src/main/resources/data.sql`. The app's `DatabaseSeeder` inserts seed rows only when the repository is empty (repo.count()==0).
- If the database already has rows and you want to reseed, either clear the DB or update `DatabaseSeeder` to force insertion.

API Endpoints (selected)
- GET /api/suggest?prefix=abc&k=8 — returns top suggestions for the prefix.
- GET /api/terms?page=0&size=100 — paginated list of terms (backend returns { items, total, page, size }).
- POST /api/term — add a new term (JSON body: { term, frequency }).
- POST /api/select — record selection of a term (body: { term }).

Troubleshooting
- If backend fails to start because port 8080 is in use, stop the process using that port or change the server port in `application.properties`.
- If you don't want Redis while developing, set `spring.cache.type=simple` in `src/main/resources/application.properties`.
- If CORS prevents the frontend from reaching the backend, ensure the backend is running and check console/network tab.

Development notes
- Frontend is a Create React App in `frontend/`.
- Backend is a Spring Boot app with JPA repositories; the indexing components (Trie, BKTree, n-gram) are constructed after application startup so seeding happens first.

Contact
- Project author: Jay Gurav
- Email: jayashgurav12345@gmail.com
- GitHub: https://github.com/jay-gurav
- Twitter/X: https://x.com/jayash_gurav

License
- No license file included. Add an open-source license if you plan to publish the repository.
