# AGENTS.md — LaPlaza

Guide for agents (human and AI) working in this repository.

## Project description

**LaPlaza** is a mobile app that centralizes the events (sports, cultural, music, etc.)
of a location, so people can find out what is happening in their town or neighborhood.
Today this information is scattered across Facebook and Instagram.

We start **with a small town in Spain** as the pilot location.

## 📌 Source of truth

> **The product source of truth is the [`docs/`](./docs) folder.**
>
> Read `docs/` before implementing anything. If code and documentation conflict, `docs/`
> wins (and a change is opened to reconcile them). Any relevant product or architecture
> decision must be reflected there.

Key documents:

- [`docs/product/vision.md`](./docs/product/vision.md) — problem, user, and value proposition.
- [`docs/product/mvp-scope.md`](./docs/product/mvp-scope.md) — MVP scope and what is out.
- [`docs/architecture/overview.md`](./docs/architecture/overview.md) — monorepo architecture.
- [`docs/architecture/data-model.md`](./docs/architecture/data-model.md) — data model.
- [`docs/roadmap.md`](./docs/roadmap.md) — phases and milestones.

## Target stack

- **Mobile frontend:** React Native (iOS + Android).
- **Backend:** Ruby on Rails with a **GraphQL API** (occasional REST where it adds value).
- **Structure:** monorepo.

> Note: the stack is **documented but not yet installed**. `apps/mobile` and `apps/api`
> are placeholders pending scaffolding.

## Monorepo structure

```text
laplaza/
├── AGENTS.md            # This guide
├── .gitignore
├── apps/
│   ├── mobile/          # React Native app (placeholder)
│   └── api/             # Rails + GraphQL backend (placeholder)
└── docs/                # 📌 Product source of truth
    ├── product/
    │   ├── vision.md
    │   └── mvp-scope.md
    ├── architecture/
    │   ├── overview.md
    │   └── data-model.md
    └── roadmap.md
```

## Roles

There are **two roles** working on LaPlaza:

- **Product Owner (PO):** owns the _what_ and the _why_; owns `docs/product/` and the
  roadmap. Prioritizes and validates the "done" criteria.
- **Engineer:** owns and executes the _how_; owns the architecture and the code.
  Translates product into implementation and keeps `docs/architecture/` up to date.

Both keep `docs/` consistent with what is built.

## Conventions

### Language

- **Everything recorded is written in English.** Even though the team speaks Spanish,
  all persisted artifacts — **documentation, requirement tickets, issues, PRs, commit
  messages, code, branches, and comments** — must be in **English**.
- **Spoken/chat communication** between the PO and the engineer can be in Spanish; only
  what gets **written down** must be in English.
- **User-facing app copy** is in **Spanish** (the pilot is a Spanish town), built to be
  **i18n-ready** so other languages can be added later. UI strings live in
  localization files, never hardcoded, with Spanish (`es`) as the default locale.

### Commits

- [Conventional Commits](https://www.conventionalcommits.org/):
  `type(scope): summary`, e.g.:
  - `feat(api): add Event GraphQL type`
  - `fix(mobile): correct wall date ordering`
  - `docs: refine mvp scope`
- Common types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `build`, `ci`.
- Suggested scopes: `mobile`, `api`, `docs`, `repo`.

### Requirement tickets

- Written in **English**, product-driven, and traceable back to `docs/`.
- Each ticket states the user value, acceptance criteria ("done" checklist), and links to
  the relevant doc section.

### Workflow

- `main` is the primary branch. Work happens on `type/short-description` branches.
- Keep **PRs small** and reviewable; the message explains the _why_, not just the _what_.
