# Run instructions (Windows PowerShell)

This project contains a Spring Boot backend and a React frontend. Use the steps below to run the full project locally on Windows.

Prerequisites
- Java 17+ JDK installed and JAVA_HOME set
- Node.js + npm installed (frontend)
- Git (optional)
- Maven installed OR Docker (see options below)

Quick checklist commands to verify:
```powershell
java -version
node -v
npm -v
mvn -v   # if installed
docker --version  # optional
```

Option A — Local Maven (recommended if you prefer running locally)
1. Install Maven (one of the methods below). Then verify with `mvn -v`.

Chocolatey (admin PowerShell):
```powershell
choco install maven -y
mvn -v
```

Scoop (user-level):
```powershell
iwr -useb get.scoop.sh | iex
scoop install maven
mvn -v
```

Manual installation:
- Download binary zip from https://maven.apache.org/download.cgi
- Extract to `C:\Program Files\Apache\maven\apache-maven-<version>`
- Add `MAVEN_HOME` or `M2_HOME` and add `%M2_HOME%\bin` to your PATH.
- Open a new PowerShell and run `mvn -v`.

2. Start the backend (from repo root):
```powershell
cd D:\D\coding\enhanced
mvn -DskipTests=false spring-boot:run
```
This runs the Spring Boot app using the configuration in `application.properties` (defaults to H2 database and Redis on localhost:6379).

3. Start the frontend (in a separate terminal):
```powershell
cd D:\D\coding\enhanced\frontend
npm install
npm start
```
Open http://localhost:3000 to view the UI. The frontend will call the backend at http://localhost:8080.

Option B — Docker Compose (recommended for an isolated environment)
1. Install Docker Desktop for Windows (https://www.docker.com/products/docker-desktop).
2. From repo root:
```powershell
cd D:\D\coding\enhanced
docker compose up --build
```
This builds and starts three services: app, postgres, redis. The app will be accessible at http://localhost:8080 (container maps 8080:8080).
- Frontend: you can either run the local dev server (`frontend/npm start`) or serve the built frontend from the Spring Boot static resources if you build it into the jar.

Notes & Troubleshooting
- If `mvn` is not recognized: ensure PATH points to Maven's `bin` and open a new shell.
- If backend fails with Redis connection errors and you do not want to run Redis, set `spring.cache.type=simple` in `src/main/resources/application.properties` and restart backend.
- If the frontend at 3000 can't reach backend at 8080 due to CORS, ensure backend is running and check browser console / network tab.
- To build an executable jar and run:
```powershell
cd D:\D\coding\enhanced
mvn -DskipTests=true package
java -jar target/RealTimeAutoComplete-1.1.0.jar
```

Want me to add Maven Wrapper?
- I can add Maven Wrapper files (`mvnw`, `mvnw.cmd`, `.mvn` directory) so you can run `./mvnw spring-boot:run` without installing Maven. Creating the wrapper normally requires running `mvn -N io.takari:maven:wrapper` on a machine with Maven; I can generate wrapper files content if you want to add them manually in this repo.

If you'd like, I can now:
- Produce the Maven Wrapper files for you to add (I can craft them but they are typically generated), or
- Walk you step-by-step through installing Maven via Chocolatey or Scoop now (I can provide commands), or
- Try running `mvn` here again if you install Maven on this environment.

