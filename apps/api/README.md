# apps/api — LaPlaza (Ruby on Rails)

The Rails application is **not generated yet**. This folder holds the Docker
development environment so the API can be generated and run later without
installing Ruby, Rails, or PostgreSQL on the host.

## Local development (Docker)

The host only needs Docker. Do not install Ruby, Rails, or PostgreSQL on the host.

From this directory (`apps/api`):

```sh
docker compose up --build
```

Detached:

```sh
docker compose up --build -d
```

Stop (keeps the Postgres data volume):

```sh
docker compose down
```

Stop and delete the Postgres data volume:

```sh
docker compose down -v
```

Optional overrides: copy `.env.example` to `.env`. Compose already has working defaults.

### Check that the environment is up

```sh
docker compose exec api ruby -v
docker compose exec api rails -v
docker compose exec api pg_isready -h postgres -U laplaza
```

Open a shell in the development container:

```sh
docker compose exec api bash
```

The container bind-mounts this directory at `/app`. The Rails app will be generated
here in a later increment.

## What will live here

The LaPlaza backend, built with **Ruby on Rails** exposing a **GraphQL API**
(plus the occasional REST endpoint where it adds value, e.g. magic-link callbacks or webhooks).

Main MVP responsibilities:

- Data model for events, locations, organizations, users, interests, saved events
  ("Me interesa") and reminders.
- GraphQL API consumed by the mobile app.
- **Minimal web backoffice** for **manually verified** organizations to publish events by hand.
- Scheduling of push reminders (1 day and 1 hour before).

## Pending scaffolding

The next increment generates the full Rails app (not API-only) from this Docker
environment.

The **product source of truth** lives in [`/docs`](../../docs).
