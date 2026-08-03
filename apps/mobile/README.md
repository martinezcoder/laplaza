# apps/mobile — LaPlaza (React Native)

> ⚠️ **Placeholder.** This folder does not contain the React Native project yet.
> Scaffolding will happen in a later session (out of scope for the bootstrap).

## What will live here

The LaPlaza mobile app (iOS + Android), built with **React Native**.

Main MVP responsibilities:

- Wall of events for one location, ordered by date (from today into the future).
- **Account-free** browsing (zero friction).
- Filtering by the user's interests.
- Login only when tapping **"Me interesa"** (Google, Sign in with Apple, email magic link).
- Push reminders (1 day before and 1 hour before the event), announced in the event
  detail with a support text such as **"Te avisaremos 1 día y 1 hora antes"**.

### App language

- User-facing copy is in **Spanish** (the pilot is a Spanish town), built **i18n-ready**
  so other languages can be added later. Strings live in localization files with `es`
  as the default locale — never hardcoded.

## Pending scaffolding

When the project is initialized here, decisions to make include:

- Expo vs React Native CLI.
- GraphQL client (e.g. Apollo Client or urql).
- Navigation (e.g. React Navigation).
- i18n library (e.g. i18next / react-intl).

The **product source of truth** lives in [`/docs`](../../docs).
