# Local setup with Docker Compose

## Start
    cd local-setup
    docker compose up --build -d
    docker compose ps            # wait until db, backend, frontend are "healthy"

Open http://localhost:3000 (frontend via nginx; /api/* is proxied to the backend).
API docs: http://localhost:8000/api/docs

## Use
- Add, complete and delete tasks in the UI.
- Health: `curl localhost:3000/api/health` and `curl localhost:8000/api/health/ready`
- Logs: `docker compose logs -f backend`

## Persistence test
    docker compose restart backend         # tasks survive
    docker compose down && docker compose up -d   # tasks survive (volume pgdata)

## SonarQube (optional)
    docker compose --profile sonar up -d   # http://localhost:9000 (admin / admin)

## Stop
    docker compose down        # keeps data
    docker compose down -v     # deletes the database volume too