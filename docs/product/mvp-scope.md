# MVP scope — LaPlaza

Single pilot location: **a small town in Spain** (kept unnamed in this documentation).

MVP goal: validate that people **discover and decide to attend** local events from a
chronological wall, with the least possible friction.

## In scope

### 1. Events wall

- Shows the events of **one location**, ordered by date **from today into the future**.
- **Filterable by the user's interests** (categories).
- Browsable **without an account** (zero friction).

**Done when:**

- [ ] A visitor without an account sees the pilot location's wall ordered by ascending date.
- [ ] Past events do not appear on the wall.
- [ ] The user can filter by one or more interest categories and the wall updates.
- [ ] Each event shows at least: title, date/time, location, category, and organization.

### 2. Event detail + "Me interesa"

- Event detail screen.
- **"Me interesa"** button.
- Support text next to the button: **"Te avisaremos 1 día y 1 hora antes"**.

**Done when:**

- [ ] The event detail opens from the wall.
- [ ] Tapping "Me interesa" **requires login** (see section 3) if not logged in yet.
- [ ] After login, the "Me interesa" mark is recorded and the button reflects the state.
- [ ] The user can undo "Me interesa".
- [ ] The event detail shows the support text **"Te avisaremos 1 día y 1 hora antes"**
      near the "Me interesa" button.

### 3. Login (only when tapping "Me interesa")

- No login to browse; it is **only** requested when tapping "Me interesa".
- Providers: **Google**, **Sign in with Apple**, and **email magic link**.
- **No** Facebook/Instagram login.

**Done when:**

- [ ] Login only appears when triggering "Me interesa" (or another action needing an account).
- [ ] The three providers work (Google, Apple, email magic link).
- [ ] After authenticating, the original action ("Me interesa") continues without repeating steps.

### 4. Push reminders

- When confirming "Me interesa", push reminders are scheduled **1 day before** and **1 hour before**.

**Done when:**

- [ ] Marking "Me interesa" schedules two reminders (D-1 and H-1).
- [ ] Canceling "Me interesa" cancels the pending reminders.
- [ ] Device notification permissions are handled.

### 5. User interests

- The user can pick their event categories to filter the wall.

**Done when:**

- [ ] A catalog of categories (interests) exists.
- [ ] The user can select/deselect interests.
- [ ] The wall filter respects the chosen interests.

### 6. Minimal web backoffice

- Minimal web app to **publish events by hand**.
- Only **manually verified organizations** can publish.

**Done when:**

- [ ] A verified organization can create/edit/unpublish its events.
- [ ] A **non**-verified organization cannot publish.
- [ ] Organization verification is done manually (internal process).
- [ ] Published events appear on their location's wall.

## Out of scope (explicit)

Mentioned in the [roadmap](../roadmap.md) but **not** designed in detail now:

- ❌ **Bots/scraping** of social media + AI to ingest events (discarded for now).
- ❌ **Payments and subscriptions** (ticket sales, fees, etc.).
- ❌ **Advertising** on the wall.
- ❌ **Multi-location**: the MVP covers the pilot location only.
- ❌ **Neighborhood filtering**: not exposed in the MVP.
  ⚠️ **But the data model must be prepared** to support it in the future for large cities
  (see [`../architecture/data-model.md`](../architecture/data-model.md)).
- ❌ **Facebook/Instagram** login.
- ❌ Event creation **by end users** (only verified organizations).
- ❌ Social features (comments, chat, following other users).

## Assumptions and default decisions

- A single active location (the pilot location); a location picker is not needed yet, but
  the model supports it.
- App language: **Spanish** for the MVP, **i18n-ready** for future languages.
- Reference time zone: **Europe/Madrid**.
- "Past event" = one whose end date/time (or start, if there is no end) is before now.
