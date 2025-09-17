# RealTimeAutoComplete (Enhanced)

Enhanced version (v1.1.0) with:
- Time-decayed + recency-boosted ranking
- Fuzzy fallback (BK-tree)
- N-gram fallback
- Redis caching using Spring Cache abstraction
- Optional Postgres configuration and Docker Compose (app + postgres + redis)
- React frontend (in /frontend) with keyboard navigation & highlighting
- More unit tests & GitHub Actions CI workflow

Run locally (quick):
- `mvn spring-boot:run` (uses H2 by default)
- Open `http://localhost:8080/` for demo frontend

Run with Docker Compose (Postgres + Redis):
- `docker compose up --build`

See README inside project for more details.
