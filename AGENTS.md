# AGENTS.md — LaPlaza

Guide for agents (human and AI) working in this repository.

> ⛔ **No commits without explicit approval.** See [Approval before commits](#approval-before-commits).

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
  roadmap. Prioritizes and validates the "done" criteria. **Must explicitly approve every
  increment before it is committed** (see [Approval before commits](#approval-before-commits)).
- **Engineer / Architect:** owns and executes the _how_; owns the architecture and the
  code. Translates product into implementation and keeps `docs/architecture/` up to date.

Both keep `docs/` consistent with what is built.

> 🎭 Each role has a matching Cursor rule in [`.cursor/rules/`](./.cursor/rules)
> (`po.mdc`, `engineer.mdc`). They are **manually activated** — start a chat with
> `@po` or `@engineer` to tell the agent which role it is playing in that session.

### Who actually plays these roles

- **Both roles are played by separate AI agents**, not by a single person or a single
  agent wearing two hats. There is a **PO agent** (drives `docs/product/`, the roadmap,
  and repo setup such as the remote) and an **Engineer/Architect agent** (drives
  `docs/architecture/` and the code in `apps/`).
- **A human orchestrates both agents.** The human is the ultimate authority: they direct
  each agent, mediate between PO and Engineer/Architect when priorities conflict, and are
  the one who ultimately grants the approval required in
  [Approval before commits](#approval-before-commits) — whether given directly or relayed
  from the PO agent.
- More agents may join over time (e.g. one per surface: mobile, api, docs). Any new agent
  onboarding onto this repo should read this file first and follow the same rules: `docs/`
  is the source of truth, everything recorded is in English, and nothing is committed or
  pushed without explicit human/PO approval.

## Conventions

### Approval before commits

- **No commits (or pushes) without the PO's explicit, prior approval.** This applies to
  every increment of code or docs, no exceptions — including AI agents working in this
  repo.
- The workflow for any change is: implement/edit → **show the diff to the PO for
  review** → wait for explicit go-ahead ("commit it", "sí, commitea", etc.) → only then
  run `git commit` (and `git push`, if applicable).
- If it is unclear whether approval was given, **ask before committing** — do not assume.
- This rule overrides any default or habitual behavior of committing automatically after
  finishing a task.

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
- Foundation / bootstrap tickets may be engineer-facing ("as an engineer, so that…");
  they still need explicit user or developer value.
- A ticket is **ready** only if it meets the Definition of Ready below. Coarse tickets
  (one issue hiding several independent increments) must be split before implementation.

#### Definition of Ready

A ticket is ready only if **all** of the following are true:

1. **One increment, one PR.** If an engineer would naturally make a checklist of three or
   more distinct deliverables (environment, scaffold, tests, a feature, …), split into
   separate issues. Do not hide that work behind a long checklist in a single issue.
2. **Closable independently.** Merging it leaves the repo in a useful, documented state
   even if the next ticket never happens.
3. **Size S or M.** **L is a smell:** split unless the work is truly atomic. If an L is
   kept, the ticket must justify why it cannot be split.
4. **Outcome, not implementation.** Acceptance criteria describe the observable result.
   Tooling and layout choices (Compose services/ports/volumes, RSpec vs Minitest, Expo vs
   React Native CLI, gem selection) belong to the Engineer and are recorded in
   `docs/architecture/` when decided — not dictated in the ticket. Notes may list a
   likely tool as *"expected default, engineer confirms"*. Exceptions already decided by
   the human owner are encoded as outcomes and must not be reopened (currently: Docker
   Compose for local PostgreSQL for `apps/api`; Ruby **3.3.6**; Rails **8.1**).
5. **Explicit boundaries.** Dependencies, epic link, and a **Not in this ticket**
   section so work does not leak back into a mega-issue.

### Pull Requests

- **Mandatory:** if a PR resolves one or more GitHub Project issues, its description
  **must include `Closes #<issue_number>`**, one line per issue it closes.
- GitHub's closing keywords (`Closes`, `Fixes`, `Resolves`) are **case-insensitive**, but
  auto-close on merge only triggers when the PR targets the **default branch** and the
  issue lives in the **same repository**.

Example PR description:

```markdown
## Summary
- Add the `Event` GraphQL type and its resolver.

Closes #8
```

### Workflow

- `main` is the primary branch. Work happens on `type/short-description` branches.
- Keep **PRs small** and reviewable; the message explains the _why_, not just the _what_.
- Remember: **no commit happens without prior PO approval** (see
  [Approval before commits](#approval-before-commits)).
