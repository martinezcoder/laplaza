# apps/api — LaPlaza (Ruby on Rails)

> ⚠️ **Placeholder.** This folder does not contain the Rails project yet.
> Scaffolding will happen in a later session (out of scope for the bootstrap).

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

When the project is initialized here, decisions to make include:

- Ruby/Rails version and API-only vs full mode (we need views for the backoffice).
- GraphQL gem (`graphql-ruby`).
- Database (planned default: **PostgreSQL**).
- Job runner for reminders (e.g. Sidekiq / Solid Queue).

The **product source of truth** lives in [`/docs`](../../docs).
